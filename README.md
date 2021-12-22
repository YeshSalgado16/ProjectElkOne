### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

~/ProjectElk1/ProjectElkOne/Diagrams/AzureVirtualNetworkDiagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

Enter the playbook file.FileBeat-Playbook.txt

~/ProjectElk1/ProjectElkOne/AnsibleScripts/Filebeat-Playbook.yml

This document contains the following details:

1. Description of the Topology
2. Access Policies
3. ELK Configuration
   - Beats in Use 
   - Machines Being Monitored
4. How to Use the Ansible Build
5. Commands of the playbook


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly interactive and responsive, in addition to restricting access to the network. What aspect of security do load balancers protect? What is the advantage of a jump box?

- The aspect of security that load balancers protect against are the denial of service attacks, also known as (DDoS) attacks. The load balancer analyzes the incoming traffic and it decides which server the traffic will be sent to. While this happens it ensures that not one server will become overloaded with traffic due to the load balancer balancing out evenly among the servers that are connected. The load balancers also check to make sure the machines are running properly to ensure when the traffic is sent that there will be no issues. The advantage of a Jump Box is, it is a secure machine that can be used to connect to other servers, as well as untrusted environments. This is an advantage because it can be used in the sense that an administrator would not be running the same machines they use that they normally perform high risk activities, therefore decreasing the risk of being compromised. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Log and system traffic.
What does Filebeat watch for?

- Filebeat monitors for change in log files and when those changes occurred. It also collects log events and organizes the log files. 
What does Metricbeat record? 

- Metricbeat records the metrics and statistics and prints them to the output that is specified. It also helps monitor the servers.  

The configuration details of each machine may be found below.



| Name       | Function    | IP Address | Operating System |
|------------|-------------|------------|------------------|
| Jump Box   | Gateway     | 10.0.0.4   | Linux            |
| Web-1      | Web Server  | 10.0.0.5   | Linux            |
| Web-2      | Web Server  | 10.0.0.6   | Linux            |
| Elk-Server | Web Server  | 10.1.0.4   | Linux            |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

 - 70.93.14.131

Machines within the network can only be accessed by the Jump Box virtual machine.

- The Jump Box VM is the machine that has access to the Elk VM. The IP of the Jump Box is 10.0.0.4


A summary of the access policies in place can be found in the table below.


| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | No                  | 70.93.14.131         |
| Web-1      | No                  | 10.0.0.4             |
| Web-2      | No                  | 10.0.0.4             |
| Elk-Server | No                  | 10.0.0.4             |




### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- The main advantage of automating configuration with ansible is, it allows the IT admins to spend less/no time on daily tasks and it allows them to spend more time on more important tasks. 

The playbook implements the following tasks:

1. The first step is to install docker.io on the Elk VM. 
2. Then python is also installed on the Elk VM.
3. Since Elk will need to require more memory, the next step is to increase the memory to 262144.
4. Download, install and launch the docker elk container. 


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

~/ProjectElk1/ProjectElkOne/Images/Docker.ps.png 

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- Web-1: 10.0.0.5
- Web-2: 10.0.0.6

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat monitors log files and collects information about the system file and forwards them to Elasticsearch or Logstash. In the case of this project to see the output of Filebeat, we would connect to Kibana to check the logs for any changes. 

- Metricbeat shows the statistics of the processes being run on the system. This is memory, CPU usage, Network IO, Disk IO as well as the file system. To view the data you would then need to navigate to Kibana to view the metrics. 


### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the filebeat-config.yml file to /etc/ansible/files/filebeat-config.yml.
- Update the filebeat-config.yml file to include host ‘10.1.0.4:9200’ provided with the username ‘elastic’ and password ‘changeme’ as well as navigating to find the area where you need to setup.Kibana host ‘10.1.0.4:5601’
- Run the playbook, and navigate to Kibana to check the data to check that the installation worked as expected.

Which file is the playbook? Where do you copy it?

- FilebeatPlaybook.yml 
- Copied to /etc/ansible/FilebeatPlaybook.yml 

Which file do you update to make Ansible run the playbook on a specific machine?

- You would need to update the FilebeatPlaybook.yml file. 

How do I specify which machine to install the ELK server on versus which to install Filebeat on?

- This would need to be specified in the hosts files. The private IPs needed would need to be added in order to allow a connection. The ones that were added were the Web-1 and Web-2 private IPs as well as the ElkServer private IP. In the hosts file at the top it needs to be specified whether it will be installed to the Elk Server or the Web Server. In this case we installed it to the Elk server therefore included the private IP of the Elk Server to the config file. 
- [elk] 10.1.0.4 ansible_python_interpreter=/usr/bin/python3

Which URL do you navigate to in order to check that the ELK server is running?

- http://[Public.VM.IP]:5601/app/kibana

### Commands to Use the Playbook

1. Nano ansible.cfg
2. Add the ElkServer VM IP (10.1.0.4) as well as ansible_python_interpreter=/usr/bin/python3 to the 3. hosts file. 
4. Save and exit file
5. Navigate to where Elkserver.yml /etc/ansible
6. Run ansible-playbook Elkserver.yml
