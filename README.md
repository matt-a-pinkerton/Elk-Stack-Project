# Elk-Project
Creation of an elk stack on cloud network

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Diagram/diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.


- Elk Playbook to install and configure the ELK server.
- Filebeat Playbook to install Filebeat on the target machines.
- Metricbeat Playbook to install Metricbeat on the target machines.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and system Metrics.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| DVWA 1   |Web Server| 10.0.0.5   | Linux            |
| DVWA 2   |Web Server| 10.0.0.6   | Linux            |
| ELK      |Monitoring| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 
- 64.85.252.52

Machines within the network can only be accessed by others on that network.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 64.85.252.52         |
| DVWA 1   | No                  | 10.0.0.1-.254        |
| DVWA 2   | No                  | 10.0.0.1-.254        |
| ELK      | No                  | 10.0.0.1-.254        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- This drastically reduces the potential for human error and simplifies the process of configuring potentially thousands of machines identically all at once.

The playbook implements the following tasks:
- install Docker.io
- install Python3-pip
- install Docker – the docker python pip module
- adjusts the virtual memory in size
- adjusts the virtual memory on restart
- then start and run docker with specific open ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.



https://github.com/wolf266/Elk-Project/blob/main/Images/ELk.jpg

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name     | IP Address |
|----------|------------|
| DVWA 1   | 10.0.0.5   |
| DVWA 2   | 10.0.0.6   |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: sends and centralizes log data by monitoring log files or locations specified, collecting log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat: takes the metrics and statistics that it collects from the OS and services and sends them to the output that specified, such as Elasticsearch or Logstash

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to the Ansible control node.
- Update the playbook file to include proper IP address.
- Run the playbook and navigate to the servers to check that the installation worked as expected.

TODO: Answer the following questions:
- Which file is the playbook? Where do you copy it?

The files with an extension of .yml are playbook files and are located in /etc/ansible

- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?


To specify what servers have Filebeat or Elk installed, you must modify the hosts file with in the directory /etc/ansible/files

- Which URL do you navigate to in order to check that the ELK server is running?

You can either navigate to the public IP address of your ELK server and add :5601 at the end to see if it pops up.  Otherwise, you can run the command curl http://(Elk_Server_Private_IP):5601 to see if it responds with and HTML response.

- Provide the specific commands the user will need to run to download the playbook, update the files, etc.

cd /etc/ansible

mkdir files

git clone https://github.com/wolf266/Elk-Project

cp ELK-Project/playbooks/* .

cp ELK-Projects/files/* ./files

cd /etc/ansible

vi hosts

	[webservers]

	10.0.0.5 ansible_python_interpreter=/usr/bin/python3

	10.0.0.6 ansible_python_interpreter=/usr/bin/python3

	[elk]

	10.1.0.4 ansible_python_interpreter=/usr/bin/python3

:wq

ansible-playbook ELK.yml

ansible-playbook Filebeat.yml

ansible-playbook Metricbeat.yml

Once complete either run “curl http://10.1.0.4:5601” or enter the public IP address of the elk server followed by “:5601” into a browser to verify success.
