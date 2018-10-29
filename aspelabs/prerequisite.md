# Prerequisite: Creating and Connecting to an Ansible Test Environment
- Your lab environment starts as a standard Ubuntu 16.04 LTS Linux virtual machine deployed in the Amazon Web Services (AWS) or Azure public cloud. Since Ansible is all about managing multiple nodes (hosts) and requires a controller to do this job, one virtual machine wouldn't normally be enough. So, we're going to use a script to set up a series of Docker containers  running on our virtual machine. (Your instructor will talk about Docker in more detail later.) Once those containers are running, we can use one as our Ansible controller, and several others as nodes under management. Follow these steps to get started:

1. Connect to the virtual machine using SSH. Use your terminal if your workstation is a Linux machine, a Mac, or a version of Windows new enough to have an SSH client available in PowerShell. If your workstation is an older Windows machine, you will need an application such as PuTTY to connect. If you need PuTTY, download it now. Your instructor will provide you with the fully qualified domain name and credentials needed to connect. Replace ## with your instructor-provided user number. **Remember, Linux is case-sensitive almost everywhere, so be careful to preserve upper and lower case characters in all these exercises.**
```
ssh username@FQDN
```
2. Once connected to the virtual machine via SSH we will need to setup our environment. To do so, we'll start by elevating our privileges temporarily and using the apt-get package manager (standard for Debian-based Linux distributions) to make sure the latest available version of the git version control system is installed. These steps can take some time, so be patient. Type the following into the terminal:
```
sudo apt-get update
sudo apt-get install git
```
3. After we're sure we have the atest version of git installed, use the following command to obtain the setup script and other environment files from the github cloud source code repository system.
```
git clone https://github.com/mattdavis0351/AnsibleBootCamp.git
```
4. Navigate into the directory structure of the cloned environment files.
```
cd AnsibleBootCamp/Ansible_class
```
5. Next you will need to execute setup.sh with elevated privileges to start the environment. Type the following. These steps can take some time, so be patient.
```
sudo ./setup.sh
```
6. The output of the above command should look something like this, but **please note that your CONTAINER ID values will be different**:
```
CONTAINER ID     IMAGE                                   COMMAND
fda1cabd099b     ansibleclass_ansiblecontroller          "/run.sh"
42649f76698a     ansibleclass_centos7                    "/bin/sh -c 'service..."
ad457c3eea8a     ansibleclass_ubuntu                     "/run.sh"
736a9b3ff4c4     ansibleclass_centos7                    "/bin/sh -c 'service..."
8f234e1ab32e     ansibleclass_ubuntu                     "/run.sh"
```
7. Once all our containners are running, we'll want to know the docker network IP addresses of the nodes we intend to have under management. These are IP addresses that the machines participating in the docker-compose overlay network will use to communicate with one another. To retrieve the IP addresses, we can use the `docker inspect` command. The command returns a lot of information about containers so we'll pipe it's output to `grep` so we can filter for just the IP Addresses.
   1. First let's get the container ID and IP addresses of your ubuntu nodes. `docker inspect` wants enough of a container ID or name to have a unique ID, and using ID is less typing. Find the container IDs of the ansibleclass_ubuntu containers (in the CONTAINER ID column of the script output). Make a note of the first few characters of the container ID (enough to ensure a unique value). If you've got a printed copy of this manual, use the table below, otherwise open a notepad or text editor document on your local machine and record the values in a similar fashion.
   2. Now use those first few characters of the ansibleclass_ubuntu CONTAINER IDs (enough to ensure a unique value) to get those machine's IP addresses. **Remember that case matters for 'IPAddress', and that YOUR values for the CONTAINER IDs of your ansibleclass_ubuntu containers probably won't be 'ad' and '8f' - substitute your own values.**
   ```
   sudo docker inspect ad 8f | grep IPAddress
   ```
   3. Make note of the two IP addresses for your ubuntu machines. We'll be calling these machines ubuntu1 and ubuntu2 in most of our exercises. If you've got a printed copy of this manual, use the table below.
   4. Now use the same process with the centos nodes by using docker inspect against BOTH of your ansibleclass_centos7 containers. **Remember that case matters for 'IPAddress', and that YOUR values for the CONTAINER IDs of your ansibleclass_centos7 containers probably won't be '42' and '73' - substitute your own values.**
   ```
   sudo docker inspect 42 73 | grep IPAddress
   ```
   5. Make note of the two IP addresses for your centos machines. We'll be calling these machines centos1 and centos2 in most of our exercises. If you've got a printed copy of this manual, use the table below.
   
   
   |Machine Name                   |Unique start of container ID|IP address of the container|
   |-------------------------------|----------------------------|---------------------------|
   |ansibleclass_ansiblecontroller |                            |not needed for our purposes|
   |ansibleclass_ubuntu (ubuntu1)  |                            |                           |
   |ansibleclass_ubuntu (ubuntu2)  |                            |                           |
   |ansibleclass_centos7 (centos1) |                            |                           |
   |ansibleclass_centos7 (centos2) |                            |                           |

8. Now that we have the IP addresses of our ubuntu and centos machines, we can connect to our controller and manage those nodes. To connect to the controller, we'll ask docker to connect our current SSH session into a bash shell that we start in the ansibleclass_ansiblecontroller container. Once connected we will conduct the remainder of these labs from that environment.
   1. Find the container ID of the ansibleclass_ansiblecontroller from the setup script output. Again, we only need as many characters as a required for the ID to be unique among our running containers. Make note of the value.
   2. Issue the following command to ask docker to execute the /bin/bash command on our controller machine and create an interactive terminal connection between our VM and that container. **Remember that YOUR value for the CONTAINER ID of your ansibleclass_ansiblecontroller containers probably won't be 'fd' - substitute your own value.**
   ```
   sudo docker exec -it fd /bin/bash
   ```
   3. If your prompt has changed to something like the following example (the container ID after root@ will very likely be different), then you know you have successfully attached to the Ansible control container.
   ```
   root@fda1cabd099b:
   ```

- Reminder: The above steps do not have anything to do with Ansible and are strictly for connecting to our lab environment for this course! Your actual work environment might require different connection steps prior to using Ansible.

From: ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide - ©2018 Techtown Training
