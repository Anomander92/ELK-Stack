## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Images/RedTeamNet.png]

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - ELK-Stack/Ansible/

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting access to the network.
This load balancer will ensure the accessibility of the machine and the JumpBox will ensure a security due to the limited access to our virtual network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Installing Filebeat to our machines allows us consistant logging, even if interruptted it will remember the last syncronization and forward the logs on next connection to our ELK stack
- Installing Metricbeat will allow our us to "get system-level CPU usage, memory, file system, disk IO, and network IO statistics, as well as top-like statistics for every process running on your systems."

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| JumpBox  | Gateway  | 10.0.0.4   | Ubuntu 20.04     |
| Web-1    | Server   | 10.0.0.5   | Ubuntu 20.04     |
| Web-2    | Server   | 10.0.0.6   | Ubuntu 20.04     |
| ELK-Stack| Server   | 10.1.0.4   | Ubuntu 20.04     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from our personal IP address (Local PC)

- Machines within the networks can only be accessed by Jumpbox  (10.0.0.4).


A summary of the access policies in place can be found in the table below.

| Name     | Public Web Access   | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBox  | Yes                 | Local PC IP / 22     |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Elk-Stack| Yes                 | Local PC IP / 5601   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because we can quickly configure future machines by modifying ansible host file.

The playbook implements the following tasks:
- Install Docker using apt package manager
- Install python3-pip using apt package manager
- Downloads and enables the ELK container, configuring our host machine with proper published ports, and memory map count(ensuring a common misconfiguration is fixed on install)

The following screenshot displays the result of running `sudo docker ps` on our Elk-Stack VM after successfully configuring the ELK instance.

/Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1/10.0.0.5 and Web-2/10.0.0.6

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- System file changes and logs.
- System metrics and docker container information

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook files to your Ansible playbook directory, endure you have the beat configuration files in the proper source directory for the play books, default is /etc/ansible/files/*.
- Update the host file at /etc/ansible/hosts to include our elk and webserver groups.
- Run the playbook using 'ansible-playbook playbookfile'. Then navigate to Kibana located at http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.

###Troubleshooting
- Check your host file is changed to include your network's private IP addresses, this was built in Azure and shows defaults.

- Ensure your firewalls are set correctly, this will have to include your load balancer, jumpbox and kibana access rules. START WITH LEAST ACCESS FIRST, YOU MAY MAKE YOUR NETWORK VULNERABLE.

- Be patient and use web searches to troubleshoot your specific issues, projects like this are the best way to learn. 
