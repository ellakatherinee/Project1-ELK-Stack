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
  * Filebeat monitors log data in specified locations. 
