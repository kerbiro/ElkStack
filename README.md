# ElkStack
Elk stack repository used for deploying elk server with web servers. 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

ElkStack/Diagram/RedTeam_ElkStack_NetworkDiagram

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - firstplaybook.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml
  - hosts
  - filebeat-config.yml
  - metricbeat-config

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessable, in addition to restricting DoS attacks to the network.
- Load balancers ensure that there is a reduced chance for a denial of service attack and keep the servers up and running more reliably.
- A jumpbox gives the added benifit of having one point of entry into your server giving less points of entry into your servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
- Filebeat monitors your log files and forwards them to your ELK server so that they are complied in a centralized location.
- Metricbeat records the metrics and staticstics of your system and will send them to your ELK server so that all the information is in a centralized location.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| Web-3    | Server   | 10.0.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ELK machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 

Machines within the network can only be accessed by Jump Box.
- Jumpbox is able to access the Elk Machine through ssh at ip address 13.68249.88

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | Personal IP             |
| Web-1    | yes                 | Jumpbox IP, Personal IP |
| Web-2    | yes                 | Jumpbox IP, Personal IP |
| Web-3    | yes                 | Jumpbox IP, Personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- If this setup is used on multiple machines you can have the set up autamaticly run saving time and resources. 

The playbook implements the following tasks:
- Install docker.io
- Install Python3
- Increase virtual memory
- install sebp/elk:761

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Elckstack/Diagram/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- Web-3 10.0.0.7

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will collect all the logs from the systems in the cluster and will send the to the ELK server so that you can monitor what the logs from a central location.
- Metricbeat will send the metrics of your computer to the ELK server. It will show data like CPU usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk file to /etc/ansible.
- Update the host file to include the private IP addresses of the target websever to the host file
- Run the playbook, and navigate to the ELK server to check that the installation worked as expected.

- install-elk.yml is the playbook and you will put that in /etc/ansible
- you will update the ansible.cfg file and add the private IP addresses under the webservers tag or create your own tag with the addresses. once you do this you will specify in the yml file what tag you want the playbook to run on.
- 13.68.253.247:5601/app/kibana
