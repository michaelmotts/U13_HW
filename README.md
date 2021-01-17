## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/michaelmotts/U13_HW/blob/main/U12_Cloud-Security_HW.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/michaelmotts/U13_HW/tree/main/ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting  to the network.
- A load balancer is used to provide redundancy of the web servers in case of a failure, increased traffic, or DDOS attacks.  This will increase availability ot customers and prevent a complete outage if one machine fails or is compromised.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.
- Filebeat logs changes to the system files and logs of all the machines it is set up to monitor.
- Metricbeat logs changes in system metircs (CPU usage, RAM usage, Etc.) on all of the machines it is set up to monitor.

The configuration details of each machine may be found below.

| Name                 | Function         | IP Address | Operating System |
|----------------------|------------------|------------|------------------|
| Jump_Box_Provisioner | Gateway          | 10.0.0.4   | Linux            |
| Web-1                | DVWA Webserver   | 10.0.0.5   | Linux            |
| Web-2                | DVWA Webserver   | 10.0.0.6   | Linux            |
| Web-3                | DVWA Webserver   | 10.0.0.7   | Linux            |
| ELK-VM               | ELK Stack        | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump_Box_Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 73.82.25.88

Machines within the network can only be accessed by Jump_Box_Provisioner 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name                  | Publicly Accessible | Allowed IP Addresses                      |
|-----------------------|---------------------|-------------------------------------------|
| Jump_Box_ Provisioner | Yes                 | 73.82.25.88, 10.0.0.5 - 10.0.0.7 10.1.0.4 |
| Web-1                 | No                  | 10.0.0.4 - 10.0.0.7, 10.1.0.4             |
| Web-2                 | No                  | 10.0.0.4 - 10.0.0.7, 10.1.0.4             |
| Web-3                 | No                  | 10.0.0.4 - 10.0.0.7, 10.1.0.4             |
| ELK-VM                | Yes                 | 73.82.25.88, 10.0.0.4 - 10.0.0.7          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- Install docker.io, python3, and docker module
- Increase virtual memory using sysctl command
- Download and launch the elk container 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/michaelmotts/U13_HW/blob/main/ELK-Docker-ps.JPG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5
10.0.0.6
10.0.0.7

We have installed the following Beats on these machines:
-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat dectects changes to the filesystem on these machines including system logs and Apache logs.
- Metricbeat detects changes in system metrics (CPU usage, RAM usage, Etc.)  It is used to detect high levels of CPU usage indicating a Dos attack and failed logins or privilage escalations.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk-playbook.yml file to /etc/ansible directory in the ansible docker.
- Update the hosts file to include a new group named "[elk]" followed by the internal ip address of the elk vm you created.
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.
