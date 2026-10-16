[Personal Learning Record](../../personal_journal/personal_journal.md) | [Session Notes](../sessions/README.md) 

# Session 3

## Topics covered
*What topics were covered in this session*
* dnsmasq
* dhcp
* vagrant networking
* configuration of dnsmasq with ansible


## Personal Notes and research following this session
*Which class sessions and personal research refers to technology in this proposal. Link to examples.*

* The notes on [Session 3 Notes](../../../sessions/session3/vagrant-examples/example3-1/README.md) were very helpful in later steps of the lab.
* I also kept going back to [session 1 Notes](../../../sessions/session1/docs/sessionNotes.md) to help me avoid the virtualbox and ubuntu version mismatches.
* Notes on [Dnsmasq official page](https://dnsmasq.org/docs/setup.html) were also very helpful in understanding how to configure dnsmasq.
* Got help understanding vagrant networking from [Vagrant Networking](https://developer.hashicorp.com/vagrant/docs/providers/virtualbox/networking).


## Exercises and results
*What exercises did you complete. What results. Screen shots and notes*

Because I want to challenge myself, I was doing this lab on windows and mac, and I was using virtualbox on windows and vmware on mac. I would like to say the ride hasn't been smooth but we are getting there and I am learning a lot about vagrant and how to troubleshoot issues with it.

### Windows using virtualbox

Tried to spin up all the vms, I tried to recreate everything we did in class on my mac which was using a different provider (vmware) and it was working fine, on my windows laptop using virtualbox. For some reason on every vm when it got to `Unpacking GuestAdditions` section it would hang or not make any progress no matter how long I waited. 

The workaround I found was to ctrl + c from the process and then find the process using the command

```cmd
tasklist | findstr ruby
or
tasklist | findstr vagrant

```
Then I would kill the process using the command

```cmd
taskkill /IM ruby /F
```

After that I would `vagrant ssh` into the vm that was stuck and run `sudo apt-get update && sudo apt-get upgrade` which would install all the packages. Then I would exit, and shutdown the **all the vms** and run the command.

> I later on found out that I didn't need to shut down any vms, just run

```cmd
vagrant up --provision
```

And it would try to run the scripts from the vagrant file again.

Yeah this gave me a lot of headaches, but I learned a lot about how vagrant works and how to troubleshoot issues with it.

There was one more wierd issue I had, which was no matter which vm I would ssh into, it would always say `vagrant@vagrant:~$` and not the name of the vm I was ssh into.

### VMware networking issue (ubuntu_1 / ubuntu_2 got no IP)

- On my Mac (VMware provider) `ubuntu_1` and `ubuntu_2` never received a DHCP lease from dnsmasq on the controller.
- Checked the VM config files: `grep -H 'ethernet1' .vagrant/machines/*/vmware_desktop/*/*.vmx`
- Found the controller and `ubuntu_bind` on `vmnet2`, but the clients on `vmnet3`, so they were on different networks and the DHCP broadcasts never reached dnsmasq.
- Cause: the Vagrantfile gives the clients `ip: "0.0.0.0"`, and the `virtualbox__intnet` option is ignored by VMware. Vagrant chose the vmnet from the IP's subnet.
- Fix: changed the client IPs to `192.168.100.50` and `.51` (same subnet as the controller), then reloaded them with `vagrant reload ubuntu_1 ubuntu_2 --provision`. The netplan provisioner still switches eth1 to DHCP, so the leases came from dnsmasq.
- Also fixed a duplicate MAC in `hosts.ini`: the controller had `...A2` (same as ubuntu-1) instead of `...A1`.
 
## Summary of learning
*What did you learn through these exercises*
## Summary of learning
*What did you learn through these exercises*

- **Providers behave differently.** Running the same lab on Windows (VirtualBox) and Mac (VMware) showed that a Vagrantfile is provider-specific. Options like `virtualbox__intnet` are silently ignored by VMware, so the same code built a different network.
- **DHCP only works inside one Layer 2 network.** When `ubuntu_1` and `ubuntu_2` got no lease, the first thing to check was which virtual switch each NIC was on. Reading the `.vmx` files showed the clients on `vmnet3` and the controller on `vmnet2`, which explained why the broadcasts never reached dnsmasq.
- **A static IP in Vagrant also decides which network a NIC joins.** Giving the clients `ip: "0.0.0.0"` put them on the wrong VMware network. Using addresses in the controller's subnet (`.50` and `.51`) fixed it, and since these differ from the reservations, it also proved the leases came from dnsmasq and not from Vagrant.
- **Small config errors break automation.** A duplicate MAC in `hosts.ini` produced conflicting DHCP reservations, so I learned to check the rendered `reservations.conf` and not just trust the template.
- **Troubleshooting Vagrant.** I learned to recover from a stuck `Unpacking GuestAdditions` step by killing the process, installing updates inside the VM with `vagrant ssh`, and re-running the provisioners with `vagrant up --provision` instead of restarting every machine.
- **Reproducibility depends on more than code.** The hypervisor, operating system and box version all affect whether an environment builds the same way, so a real deployment should pin versions and test on every supported platform.
- **Testing on two platforms was worth it.** It was slower and more frustrating, but each failure taught me something about how Vagrant, networking and DHCP actually work.