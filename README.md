# Project-13

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_ELK_deployment.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat.

- _TODO: Enter the playbook file._

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
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
The load balancer has an offloading function that protects the server stack from Denial of Service (DoS and DDoS) attacks and also keeps service available in event that one or two of the VM's are unreachable for any reason.
Using the jump box as a provisioner allows us to hide the vulnerable machines with no public IP address and by using ansible and ssh functionality to manage all VM effectively and efficiently at the same time.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log and system files.
- _TODO: What does Filebeat watch for?_
Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- _TODO: What does Metricbeat record?_
Metricbeat collects metrics from the operating system and from services running on the server.  In this deployment we are looking at Docker metrics Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function   | IP Address | Operating System |
|----------------------|------------|------------|------------------|
| Jump-Box-Provisioner | Gateway    | 10.0.0.7   | Linux            |
| ELK-Server           | Monitoring | 10.1.0.4   | Linux            |
| Web-1                | DVWA       | 10.0.0.4   | Linux            |
| Web-2                | DVWA       | 10.0.0.5   | Linux            |
| Web-3                | DVWA       | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-my public IP address

Machines within the network can only be accessed by SSH from the Jump Box VM.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
- The ELK-Server is accessible using the Jump-Box_Provisioner via SSH from its private IP 10.0.0.7:22

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Address     |
|----------------------|---------------------|------------------------|
| Jump-Box-Provisioner | Yes/SSH             | My public IP address   |
| ELK-Server           | Yes/HTTP            | My public IP address   |
| Web-1                | No                  | 10.0.0.7               |
| Web-2                | No                  | 10.0.0.7               |
| Web-3                | No                  | 10.0.0.7               |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
Ansible allows us to automate the configuration of all attached devices simultaneously using playbooks.
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker
- Install pip3
- Install docker python module
- Download and launch docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- Virtual Machines Web-1, Web-2 and Web-3
- 10.0.0.4
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
Metricbeat collects metrics from the operating system and from services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the playbook file to /etc/ansible/.
- Update the hosts file to include each client VM private IP addresses
    - 10.0.0.4 ansible_python_interpreter=/usr/bin/python3
    - 10.0.0.5 ansible_python_interpreter=/usr/bin/python3
    - 10.0.0.6 ansible_python_interpreter=/usr/bin/python3
    - [elk]
    - 10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- Run the playbook, and navigate to localhost/setup.php on a client to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
To run the playbook for Filebeat use the command: ansible-playbook filebeat-playbook.yml from /etc/ansible/
To run the playbook for Metricbeat use the command: ansible-playbook metricbeat-playbook.yml from /etc/ansible/
