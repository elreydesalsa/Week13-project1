# Week13-project1
UNCC Week 13
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](https://github.com/elreydesalsa/Week13-project1/blob/main/Diagrams/Copy%20of%20EduardoDiaz.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

  -- The ansible-playbooks [elk.yml](https://github.com/elreydesalsa/Week13-project1/blob/main/Ansible/install-elk.yml) and the [filebeat-playbook.yml](https://github.com/elreydesalsa/Week13-project1/blob/main/Ansible/filebeat-playbook.yml) are needed to create and implement the Elk-Server.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology
 
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load Balancer will maintain availability of data security in regards to the CIA Triad.  The advantage of a jump box is a secure conection for administrators to update a single system and administrative tasks. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
Filebeat watches for log files/locations and collects log events
Metricbeat will record metric and statistical data from OS and from services running.

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Ansible  | 10.0.0.4   | Linux            |
| Web1     | DVWA     | 10.0.0.5   | Linux            |
| Web2.1   | DVWA     | 10.0.0.6   | Linux            |
| Web 3    | DVWA     | 10.0.0.7   | Linux            |
| Elk      | VM       | 10.1.0.4   | Linux
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-(Personal IP Address

Machines within the network can only be accessed by SSH.
Within the network you can ssh from outside the newtwork PRIVATE Personal IP Address.
A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |   Yes               | Any machine, SSS     |
| Web 1    |    no               | 10.0.0.4             |
| Web 2.1  |    no               | 10.0.0.4             |
| Web 3    |    no               | 10.0.0.4             |
| Elk      |    no               | 10.0.0.4 Personal IP |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- You are able with ease to use Playbooks to configure multiple Machines through the use of a single command after initial config.

The playbook implements the following tasks:
- Creates a New VM.
- Downloads and Configures the ELK-docker Container. Create Ansible-playbook (elk.yml) that will configure Elk server to accept following ports 5601,9200,5044
- Lauch and attach container and veryify container is up and running by SSH into the container from JumpBox.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- [10.0.0.4, 10.0.0.5, 10.0.0.6, 10.0.0.7]

We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
- File beat monitors log files, collects log events and forwards them to Elasticsearch or Logstash.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.yml and metricbeat.yml file to /etc/ansible.
- Update the configuration files to include the Private IP of the ELK-Server.
- Run the playbook, and navigate to elk-server to check that the installation worked as expected.


- _Which file is the playbook? Where do you copy it?_
- The playbook is filebeat-playbook.yml and was copied to the /etc/ansibel/hosts/ directory
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ 
     File to update Ansible is filebeat.yml this is a Configuration file. We need to configure .yml file to have designated Ip address from the Private Ip Address of the Elk Server.
- _Which URL do you navigate to in order to check that the ELK server is running? 
  http://[10.1.0.4]:5601/app/kibana
*specific commands the user will need to run to download the playbook, update the files, etc._
ssh RedAdmin@JumpBox(PrivateIP)
sudo docker container list -a (locate your ansible container)
sudo docker start container (name of the container)
sudo docker attach container (name of the container)
cd /etc/ansible/
ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server
cd /etc/ansible/roles/
ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat)
open a new web browser (Elk-Server PublicIP:5601) This will bring up the Kibana Web Portal
