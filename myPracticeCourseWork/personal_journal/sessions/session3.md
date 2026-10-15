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
 
## Summary of learning
*What did you learn through these exercises*