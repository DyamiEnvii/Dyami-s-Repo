# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![diagram](Diagram/Diagram.png.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the **yaml** file may be used to install only certain pieces of it, such as Filebeat.

  [elkalicious](Ansible/elkalicious.yml)
  
  [pentest](Ansible/pentest.yml)
  
  [ansible-cfg](Ansible/ansbile-cfg.yml)
  
  [hosts](Ansible/hosts.yml)
  
  [Filebeat-playbook](Ansible/filebeat-playbook.yml)
 
  [filebeat-config](Ansible/filebeat-config.yml)
  
  [metricbeat-palybook](Ansible/metricbeat-playbook.yml)
  
  [metricbeat-config](Ansible/MetricbeatConfig.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessable, in addition to restricting non-authorized to the network.
 What aspect of security do load balancers protect? Load balancers can protect you against a Ddos attack due to its ability to split the work between two different servers, allowing one to go down and the system will still be running due to the load balancer now turning all the task back on to only one server instead of both.  What is the advantage of a jump box? The advantage of a jumpbox is that you have only one location that can be used to access multiple location this also allows for very good protection for all other locations you may have

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system matrix.
 What does Filebeat watch for? Filebeat is watching for a specific logs and specific set of files you have set.
 What does Metricbeat record? Metricbeat is recording the statics of the files and or logs you have specified for it look. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| RedWeb1  | Dvwa/WS  | 10.0.0.6   | Linux            |
| Redweb2  | Dvwa/WS  | 10.0.0.7   | Linux            |
| Elk-1    | Elk      | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
<enter personal public ip address> in order to connect to the machine you will want to set a rule allowing for your own personal public ip address to pass through the firewall

Machines within the network can only be accessed by RedTeam1(Jump Box).
Which machine did you allow to access your ELK VM? What was its IP address? We access the elk vm from the container were we have our ansible-playbooks. For myself this would the first sudo docker container list -a that I would run and grab the tender_liskov and start the machine then attach myself in order to SSH into the ELK machine.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.1.0.4             |
| Redweb1  | No                  |                      |
| Redweb2  | No                  |                      |
| Elk1     | No                  |                      |
  
### Elk Configuration

- Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? Main advantage would be being able to copy a master copy of the playbook and copying into the container that you want to run it off of. Making it easy for updating the file if need be and makes the tedious changes easy.

- The playbook implements the following tasks:
- The playbook will first install docker.io on to all webservers that have been underlined in the hosts file. after that it will follow and install the rest python3-pip, and - docker module.
- The second task in our playbook will run a systemctl command to insure that the memory that is being used is within a stated amount
- The third task that is being used in our playbook is installing and elk container with certain ports open allowing for us to get into it after succesful download the playbook
  will run its final task
- The final task will be used as a systemd command to ensure that the service that has been installed and configured is up and running with no issues.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](Images/Dockerps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
RedWeb1 - 10.0.0.6
RedWeb2 - 10.0.0.7
  
We have installed the following Beats on these machines:
We installed filebeat in our second playbook, after successfully running Filebeat-playbook we ran a metricbeat-playbook. Running both of these succesfully allowed us to grab the required logs.
These Beats allow us to collect the following information from each machine:
Filebat is collecting the system log information and storing that information into a designated location, and will be readable using kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible-playbook file to the designated container.
- Update the host file to include all webservers that you are requesting as well as uncommenting [webservers] and adding underneath your webservers ip addresses you will be adding a [elk] and the elks IP address. Next to all IP addresses you need to include ansible_python_interpreter=/usr/bin/python3.
- Run the playbook, and navigate to Kibana<also the public ip address of the elk server:port address that you opened((5601))> to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- Which file is the playbook? Where do you copy it? the playbook to set up elk is elkalicious.yml and you copy this file into the /etc/ansible/directory
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- Which URL do you navigate to in order to check that the ELK server is running? In order to check and see if you elk server is up and running you will want to connect to the public ip address of the elk machine in a browser with the open port. so your url should read http://13.77.219.27:5601/app/kibana#/home <this is my url for my machine yours will be different>.

####  Step by Step from Downloading Docker to Setting up a Playbook
  In order to run this set of dockers you will want to run the commands as follows(this is of course with you having already set up a azure VM;
  sudo apt update
  
  sudo apt install docker.io
  
  systemctl status docker ( run this command to ensure that your docker.io was installed and running)
  
  After installation your process is not running please run sudo systemctl status docker to start your process
  
  sudo docker pull cyberxsecurity/ansible ( this will pull the container((you must know the container/image name exactly)) and download the container for you to acces)
  
  sudo docker run -ti cyberxsecurity/ansible:latest bash ( please only run this once if you run it more than once you will have one or more container)
  
  sudo docker container list -a ( this will show all available containers that you have after running ((run -ti)) this will also give you the name of the container for you to     start
  
  sudo docker start <name of your container> (for instance mine is tender_liskov) this will start your container and make it available to attach too.
  
  sudo docker attach <name of your container> 
  
  sudo docker run -it cyberxsecurity/ansible /bin/bash (this will set up a host and config file within your container allowing you to set up the files how you want) 
  
  once you have done that you will want to locate the files. 
  
  cd /etc/ansible once you have moved into the directory /etc/ and moved into ansible you will want to run a ls to confirm your files are there.
  
  once you have done this you will be able to adjust the playbook files here. This will allow you to overwrite your playbooks, update your config files into include new           webservers, or even new elk servers. 
  
  The first file we should look at is the hosts file. In here you will want to remove the # next to [webservers] and underneath a couple of lines that are already added there     you will want to add the IP addresses that you want for your webservers for example mine being 10.0.0.6. Once you have added that you will want to hit tab and add the           following line next to it. ansible_python_interpreter=/usr/bin/python3 this will allow for your python-pip3 that you installed in your playbooks to work with out an issue.
  
  After we are done with the our changes to the hosts file we are going to save and exit and go into our configure file for ansible.
  
  Once we are in the ansbile.cfg file, we are going to page down to the remote_user section of this file and change the remote_user= sysadmin to the username that you used to     set up your VM. This will also be commented. You will want to uncomment the line after changing the username to your username.
  
  Now that we have set up both of our hosts and configure files we are now going to create a play book.
  
  Once we have started our contianer and we are at a screen that looks like root@5e4b8f36e048:~# you will want to move into /etc/ansible.
  
  When you are in here you are more than welcome to create a playboook, for this exercise we are creating a DVWA(Damn Vulnerable Website App) so this playbook will be for         that.
  
  Our first step will be nano pentest.yml this will create the playbook.
  
  The top of your playbook should read something like this
  
  ![image](Images/Pentest1.PNG)
  
  This is declaring what you want the playbook to do. So we are Configuring a Web Virtual Machine using Docker
  
  Our host for this is going to be webservers hence why we uncommented and added the IP addresses
  
  Last but not least we have become true. Allowing for this entire playbook to come true
  
  ![image](Images/DockerUpdate.PNG)
  
  This segment is saying we want docker.io to install force it to go through if we do not have it, update the chace yes, name of the process we want and the sate of the           process.
  
  In the next segment we are installing pip3 which is pulling from a index of python libary that is unable to be carried with python when we install python.
  
   ![image](Images/pip3.PNG)
  
  The next step should speak for its self :)
  
   ![image](Images/DockerModule.PNG)
  
  The next step in the playbook is going to start the webserver and open the desired ports you want. this is also where you want to include the most important piece in all of     the ansible-playbook in my opinion. That would be the restart_policy: always. If you do not include this, you will have to always restart the playbook in order for the           webserver to start up instead of starting up when you start up your machine.
  
   ![image](Images/DVWA.PNG)
  
  The final step in a playbook is making sure that the service is up and running. The first line in this is the name of the service we are running. The second line is the         command we are running. the third is the name of service we are running. and the fourth is what we want to do with the service, do we want it enabled or disbaled.
  
   ![image](Images/service.PNG)
  
  Now that we have completed that we are going to run this command; ansible-playbook pentest.yml
  
  You should get this read(mine is a bit differnt and says OK yours should say changed) the only reason its differnt is because I have ran this before.
  
   ![image](Images/Output.PNG)
  
  If you would like to test that the webserver is up an running you can ssh into your PRIVATE Ip address of your webserver. using ssh <username you designated>@<private ip address>
  
  Congrats you have successfully set up a webserver, playbook, configure file, and a host file.
