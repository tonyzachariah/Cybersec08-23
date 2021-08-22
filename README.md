## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/tonyzachariah/Cybersec08-23/blob/main/Diagrams/Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - [install-elk.yml](https://github.com/tonyzachariah/Cybersec08-23/blob/main/Ansible/install-elk.yml.txt)
  - [filebeat-playbook.yml](https://github.com/tonyzachariah/Cybersec08-23/blob/main/Ansible/filebeat-playbook.yml.txt)
  - [metricbeat-playbook.yml](https://github.com/tonyzachariah/Cybersec08-23/blob/main/Ansible/metricbeat-playbook.yml.txt)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable and available, in addition to restricting access to the network. 
- Load balancers protect the availability aspect of security. Load balancers have their own public IP addresses that is accessed by the internet. Load balancers distribute traffic across multiple servers. They also have a health probe function that makes sure all the servers behind the balancer are functioning to send traffic to them. 
- A jump box is essentially identical to a gateway router. A jump box allows administrators to maintain a secure environment by fanning in through a single node. A jump box sits in front of other machines not exposed to the public internet. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat watches log files or locations we specify. Filebeat collects log events and forwards the data to Elasticsearch or Logstash for indexing. 
- Metricbeat records machine metrics. Metrics include stats such as CPU usage and uptime. It allows administrators to easily collect information about machines in the network. 

The configuration details of each machine may be found below.

|   Name   |  Function  |  IP Address  | Operating System |
|----------|------------|--------------|------------------|
| Jump Box | Gateway    | 20.55.23.183 | Linux            |
| Web 1    | Web Server | 10.0.0.5     | Linux            |
| Web 2    | Web Server | 10.0.0.6     | Linux            |
| ELK      | Log Server | 52.165.88.86 | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

 Only the Jump box provisioner machine and ELK stack can accept connections from the Internet. Access to these machines is only allowed from the following IP address:
- 173.56.251.160. We have access to the ELK GUI (Kibana) by TCP port 5601. 

Machines within the network can only be accessed by the Ansible container within the jump box provisioner.
- The jump box can have access to the ELK VM. The elk server can also be accessed from my personal IP address to TCP port 5601. My personal IP address is 173.56.251.160.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump Box      | Yes                 | 173.56.251.160       |
| Load Balancer | Yes                 | Any                  |
| Web 1         | No                  | 10.0.0.4             |
| Web 2         | No                  | 10.0.0.4             |
| ELK           | Yes                 | 173.56.251.160       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because installs can be consistant efficeint. Administrators dont need to spend too much time doing the same tasks 
over again when they can focus their time and energy on more important taksks. 

The playbook implements the following tasks:
- Increases virtual memory
- Install docker.io, pip3 using the apt module
- Install docker python module using the pip module
- downloads and launches the docker container for the ELK server
- Enables docker service using systemd module

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![dockerps](https://github.com/tonyzachariah/Cybersec08-23/blob/main/Diagrams/docker_ps_output.png.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

 | Machine | IP address |
 |---------|------------|
 |  Web 1  |  10.0.0.5  |
 |  Web 2  |  10.0.0.6  |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat watches log files or locations we specify. Filebeat collects log events and forwards the data to Elasticsearch or Logstash for indexing. An example of a filebeat is syslog. we can use syslog input to read events over TCP or UDP.
- Metricbeat records machine metrics. Metrics include stats such as CPU usage and uptime. It allows administrators to easily collect information about machines in the network.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the hosts file to include the IP addresses of the ELK server (10.1.0.4 ansible_python_interpreter=/usr/bin/python3).
- Run the playbook, and navigate to http://52.165.88.86:5601/app/kibana to check that the installation worked as expected.

