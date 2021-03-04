# ELK-Stack-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![network_diagram.png](Images/network_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the roles file may be used to install only certain pieces of it, such as Filebeat.

![install-elk.yml](Ansible/install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network.
Load balancers help to ensure that each machine is not overloaded with requests at any one point, and often offers health probing to help maintain a well functioning pool. 
The purpose of the jump box is to offer a single gateway machine that will allow an administrator to access machines that are on the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system services.

The configuration details of each machine may be found below.

| Name                 | Function  | IP Address | Operating System |
|----------------------|-----------|------------|------------------|
| Jump-Box-Provisioner | Gateway   | 10.0.0.4   | Ubuntu 18.04-LTS |
| ELK-Server           | ELK Host  | 10.1.0.4   | Ubuntu 18.04-LTS |
| Web-1                | DVWA Host | 10.0.0.5   | Ubuntu 18.04-LTS |
| Web-2                | DVWA Host | 10.0.0.6   | Ubuntu 18.04-LTS |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
My local machine's IP


Machines within the network can only be accessed by SSH.
Only the Jump-Box-Provisioner was able to access the ELK-Network via SSH

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My Local Machine IP  |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it reduces the amount of legwork should I need to redeploy, as the scripts are already built.

The playbook implements the following tasks:
- Install docker via apt
- Install python3-pip via apt
- Install the docker python module via pip
- Use systemctl to ensure the proper ram threshold to run the stack effectively
- Download and launch the docker ELK container
- Use systemd to enable docker at boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5
10.0.0.6

We have installed the following Beats on these machines:
- FileBeat
- MetricBeat

These Beats allow us to collect the following information from each machine:
Filebeat collects log information and displays major changes and events. I would expect to see evidence of different sessions and activity from filebeat.
Metricbeat collects system metrics from the services running on the machine. I would ecpect to be able to be able to see things like CPU and RAM usage by different programs.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yml file to /etc/ansible/roles.
- Update the hosts file to include a new host group. Add your machine to the group.
- Run the playbook, and navigate to http://[your-IP]:5601/app/kibana to check that the installation worked as expected.
