## ELK Stack Deployment 
#### The following files in this repository were used to configure the network depicted below
 
![alt text](https://github.com/ellakatherinee/super-duper-guacamole/blob/main/Diagrams/ELK-1.png "Azure Diagram")

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml files may be used to install only certain pieces of it, such as: **ELK, Filebeat, and Metricbeat**

[Ansible](https://github.com/ellakatherinee/super-duper-guacamole/tree/main/Ansible)

This document contains the following details:
* Description of the Topology
* Access Policies
* ELK Configuration: 
  1. Beats in Use  
  2. Machines Being Monitored
* How to Use the Ansible Build

### Description of the Topology 
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
 * Load Balancers allow for an extra layer of security protection for web servers by shifting tasks and resources for optimal use. DDos attacks are reduced by traffic that is being distributed  
  * The Jump Box is only acessible via port 22. It is a great tool used by an administrator to perform tasks on the network. 
  
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system metrics. ELK is great for those who are visual learners,it allows for whomever to easily understand the basic mechanics of what log data looks like  
  * Filebeat monitors log data in specified locations. It collects log events, and forwards them to Elastisearch or Logstash for indexing. 
  * Metricbeat monitors the system metrics of your network, and forwards the data to Elastisearch 

The configuration details of each machine may be found below: 
| Name | Function | IP Address | Operating System |
|:------:|:---------:|:----------:|:----------------:|
|Jump-Box| Gateway | ? | Linux | 
|Web 1| Server |10.0.0.8|Linux|
|Web 2| Server |10.0.0.9|Linux|
|Web 3| Server |10.0.0.10|Linux|
|ELK-Server1|Log Server|10.1.0.4|Linux| 


### Access Polices 
The machines within the internal network are not exposed to the public 

Only the Jump Box can accept connections from the internet via port 22/SSH. Access to this machine is allowed from a designated IP address that has been given permission within the network security group. If you're happening to work from more than one IP address (like myself) then you need to adjust your security rules for what IP addresses are allowed. 

Machines within the network can only be accessed by each other. The user can only access the Web Servers and ELK Server only through the Jump Box by connecting to them via port 22/SSH. The data that is collected from the Web Servers gets sent to the ELK server for indexing. 

A summary of the access policies in place can be found in the table below.
| Name | Publicly Acessible | Allowed IP Address |
|:------:|:---------:|:----------:|
|Jump-Box| Yes |? | 
|Web 1| No |? |
|Web 2| No |?|
|Web 3| No |?|
|ELK-Server1|No|?| 

### ELK Configuration 
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it greatly reduces the chance of human error over the course of potentially configuring thousands of machines.

The playbook implements the following tasks:
* Install docker on all network machines so they will be able to recieve and install containers 
* Installing ansible on the Jump Box allows for the distribution of containers on the other web servers 
* Ansible playbooks are used to install the Elk stack container on the Elk server and "Beats" containers on the web servers 

The following screenshot displays the result of running `docker ps` after successfully configuring the [ELK](https://github.com/ellakatherinee/super-duper-guacamole/blob/main/Ansible/install-elk.yml) instance.
 
![alt text](https://github.com/ellakatherinee/super-duper-guacamole/blob/main/Diagrams/Docker-ELK.jpeg "Docker")

### Target Machine & Beats
ELK server monitors the following machines: 
* Web 1: 10.0.0.8
* Web 2: 10.0.0.9
* Web 3: 10.0.0.10

Filebeat/Metricbeat are on the following machines:
* Web 1: 10.0.0.8
* Web 2: 10.0.0.9
* Web 3: 10.0.0.10

These Beats allow us to collect the following information from each machine:

**Filebeat** : Monitors log data in specified locations. It collects log events, and changes to the system 

**Metricbeat** : Monitors the system metrics of your network such as CPU/RAM statistics, collects data on SSH login attempts, and failed sudo escalations

### Using Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned. 

SSH into the control node and follow the steps below:

* Copy the .yml files to `/etc/ansible` directory 
* Update the hosts  file to be as follows. This will assign the VM servers to their server groups for the Ansible Playbooks 

```
     [webservers]
       10.0.0.5
       10.0.0.6
       10.0.0.7
     [elkservers]
       10.1.0.4
```
* To configure ELK, Filebeat,and Metricbeat run the following commands:
```
cd /etc/ansible
ansible-playbook elk-playbook.yml
ansible-playbook filebeat-playbook.yml
ansible-playbook metricbeat-playbook.yml 
````
* Lastly, if configured correctly navigate to: `curl http://10.0.0.8:5601` this is Kibana's web address. 
  
