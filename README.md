## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- _TODO: They prevent ddos attacks, the advatage of having a jump box is it gives a user a secured single node that can be monitored 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and system metrics.
- _TODO: What does Filebeat watch for?_monitors the log files or locations that you specify
- _TODO: What does Metricbeat record?_It records metrics and statistics that it collects and ships them to the output that you specify

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| DVWA 1   |Web server| 10.0.0.7   | Linux            |
| DVWA 2   |Web server| 10.0.0.8   | Linux            |
| ELK      |Monitoring| 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: 168.61.22.211

Machines within the network can only be accessed by eachother.
- _TODO: the JumpBox, 168.61.22.211

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|           | Jump Box | Yes                 | 168.61.22.211        |
| ELK      | No                  | 10.0.0.7             |
| DVWA 1   | No                  | 10.0.0.8             |
  DVWA 1   | No                    10.0.0.9  

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_ It allows IT adminis to automate away the crap from their daily tasks.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
Install: docker.io
Install: python-pip
Install: docker
Command: sysctl -w vm.max_map_count=262144
Launch docker container: elk
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_10.0.0.7/10.0.0.8/10.0.0.9

We have installed the following Beats on these machines:
- _TODO: _Filebeat, Metricbeat, Packetbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._Filebeat: Filebeat monitors the log files or locations that you specify, we use it to watch logs.

Metricbeat: periodically collect metrics from the operating system and from services running on the server. we use it to detect unusual connection attempts or privlage escilation.

Packetbeat:is a real-time network packet analyzer that you can use with Elasticsearch to provide an application monitoring and performance analytics system. it puts a tracer on there network just incase

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbooks file to Anisble Control Node.
- Update the hosts file to include... the vm ip's
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_/etc/ansible/file/filebeat-configuration.yml

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_edit the /etc/ansible/host file to add webserver/elkserver ip addresses

- _Which URL do you navigate to in order to check that the ELK server is running? curl http://10.0.0.8:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
  cd /etc/ansible
$ ansible-playbook install_elk.yml elk
$ ansible-playbook install_filebeat.yml webservers
$ ansible-playbook install_metricbeat.yml webservers
