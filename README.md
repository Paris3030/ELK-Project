# ELK-Project
Unit 13 - Elk Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.


![ELK Network Diagram](https://user-images.githubusercontent.com/94578361/161435928-3902bf12-8c4f-444b-8c64-db8701279f51.PNG)



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.

 

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.  Load balancers help ensure environment availabiity through distribution of incoming data to web servers.  Jump boxes allow for more easy administration of multiple systems and provide an additional layer between the outside and internal assets.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
 -Filbeats watch for log directories or specific log files.
 -Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server.
![Filebeat-Configuration](Configuration-Files/filebeat-configuration.yml)
![Metricbeat-Configuration](Configuration-Files/metricbeat-configuration.yml)


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function | IP Address   | Operating System |
|----------  |----------|------------  |------------------|
| Jump Box   | Gateway  | 10.0.0.5     | Linux (Ubuntu)   |
| Web-1      | Server   | 10.0.0.7     | Linux (Ubuntu)   |
| Web-2      | Server   | 10.0.0.8     | Linux (Ubuntu)   |
| ELK-Server | Log Serv | 10.1.0.4     | Linux (Ubuntu)   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbopx machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by the Jump Box.  The Elk machine can have access from personal IP address through port 5601.


A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------|----------------------|
| Jump Box      |       Yes           |    52.184.100.221    |
| Web-1         |       No            |    10.0.0.5          |
| Web-2         |       No            |    10.0.0.5          |
| Elk-Server    |       No            |    Personal          |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because multiple servers are deloyed 
easily and quickly without physcially touching each server.

The playbook implements the following tasks:
- Installs docker.io, pip3, and the docker python module
- Increases the virtual memory
- Uses sysctl module
- Downloads and launches a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/94578361/161397103-92f0a0cb-8c9c-47b0-9b43-31ef7eee8628.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1    10.0.0.7
- Web-2    10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.  It is a lightweight shipper for forwarding and centralizing log data.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.   Also, Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server.
 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
- Update the configuration file to include the private IP of the ELK-server to the ElasticSearch and Kibana Sections of the configuration file.
- Run the playbook, and navigate to "https (ELK server public IP):5601/app/kibana" to check that the installation worked as expected.
- Which file is the playbook?
   - elk-playbook.yml - used to install ELK server
   - filebeat-playbook.yml - used to install and configure filebeat on ELK server and DVWA servers.
   - metricbeat-playbook.yml - used to install and configure metricbeat on ELK server and DVWA servers.    
- Where do you copy it?  /etc/ansible/
- Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts.cfg 
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?  You will specify which machine  to install by updating the host files with web/elk servers IP addresses and selecting which group to run on in ansible.
- Which URL do you navigate to in order to check that the ELK server is running?  http://(elk-server public IP):5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
The specific commands to download the playbook and update the files
