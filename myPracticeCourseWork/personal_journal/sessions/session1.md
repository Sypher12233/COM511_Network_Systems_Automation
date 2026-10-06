[Personal Learning Record](../../personal_journal/personal_journal.md) | [Session Notes](../sessions/README.md) 

# Session 1

## Topics covered
* VMs: what they are and how they work
* Vagrant
* Ansible
* Generating git ssh and personal access token
* Hypervisors
* IaS or Infrastructure as a Service



## Personal Notes and research following this session
*Which class sessions and personal research refers to technology in this proposal. Link to examples.*

### Virtual Machines (VMs)
When we want to learn, test or troubleshoot operating systems, applications, new features etc we do not want to worry about damaging our operating system or accidental deletion of important system files. 

#### Solution
To help with that, we can use VMs, which are a safe and efficient way to have isolated environments where we can deploy almost any operating system we want and as many as we want as long as we have the resources to handle it.
We can use softwares like virtual box or vmware fusion which are freely available to manage our VMs. These VMs operate the same way as a bare metal operating system.
If we are low on storage and we need different operating systems, we can spin up one os and finish our task then delete or reset it and spin up another os.

#### Vagrant
First we will discuss the limitation of running VMs without Vagrant. There is a lot of manual configuration involved when setting up our VMs, we have assign disk space, network adapters, user accounts and permissions and many more settings. As we can assume it is prone to human error and in testing where we need a stable and reliable environment to run our apps, a single mistake or misconfiguration can introduce unnecessary problems in our project.

#### Solution
Vagrant is an open source solution where we put all our configuration for an os in a file called vagrantfile and let vagrant handle the rest. This was we can gaurantee that all our apps will the same configuration applied to them.
#### Source
https://youtu.be/czMCO1w-xQU
### GitHub Infrastructure Incident – 17 August 2026

I researched [GitHub's major outage on 17 August 2026](https://github.blog/news-insights/company-news/the-august-17-outage-and-the-work-ahead/?utm_source=chatgpt.com). The incident was caused by a critical infrastructure component failing to scale when traffic reached a new peak, affecting services including GitHub Actions, APIs, authentication, Issues and Pull Requests.

The incident highlighted the importance of scalability, monitoring, redundancy and automated recovery when designing infrastructure. This is relevant to the COM511 project because Sirius will need infrastructure that can automatically scale and be managed with minimal staff involvement.



## Exercises and results
After I did a bit of reading on the [Hashicorp documentation page](https://developer.hashicorp.com/tutorials/library?product=vagrant) I initialized a new Vagrant box or environment, I'm still a bit confused about the different between the two.
Then I compared the VagrantFile with the one from this weeks ubuntu vagrantfile and turns out they are exactly the same.
#### Conclusion
The first weeks boxes are vanilla boxes.

## Questions
1. What backups are in place incase GitHub has issues and your data is not recoverable like it happened at **July 26 2026** 
2. How and where to store sources, put them in one file and refer to it or under each topic

## Summary of learning
*What did you learn through these exercises*