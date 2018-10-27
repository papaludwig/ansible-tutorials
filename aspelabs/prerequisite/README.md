# Prerequisite: Connecting to Your Ansible Control Machine
- Your lab environment starts as a standard Ubuntu 16.04 LTS Linux virtual machine deployed in the Amazon Web Services (AWS) or Azure public cloud. Since Ansible is all about managing multiple nodes (hosts) and requires a controller to do this job, one virtual machine wouldn't normally be enough. So, we're going to use a script to set up a series of Docker containers  running on our virtual machine. Once those containers are running, we can use one as our Ansible controller, and several others as nodes under management. Follow these steps to get started:

1. Connect to the virtual machine using SSH. Use your terminal if your workstation is a Linux machine, a Mac, or a version of Windows new enough to have an SSH client available in PowerShell. If your workstation is an older Windows machine, you will need an application such as PuTTY to connect. If you need PuTTY, download it now. Your instructor will provide you with the credentials needed to connect. Replace ## with your instructor-provided user number. **Remember, Linux is case-sensitive almost everywhere, so be careful to preserve upper and lower case characters in all these exercises.**
```
ssh ansible@ansible0##.westus.cloudapp.azure.com
```
2. Once connected to the virtual machine via SSH we will need to setup our environment. To do so, we'll start by elevating our privileges temporarily and using the apt-get package manager (standard for Debian-based Linux distributions) to make sure the latest available version of the git version control system is installed. These steps can take some time, so be patient. Type the following into the terminal:
```
sudo apt-get update
sudo apt-get install git
```
3. After we're sure we have the atest version of git installed, use the following command to obtain the setup script and other environment files from the github cloud source code repository system.
```
git clone https://github.com/mattdavis0351/AnisbleBootCamp.git
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
7. Once all  our containners are running, we'll want to know their docker network IP addresses. These are IP addresses that the machines participating in the docker-compose overlay network will use to communicate with one another. To retrieve the IP addresses, we can use the `docker inspect` command. The command returns a lot of information about containers so we'll pipe it's output to `grep` so we can filter for just the IP Addresses.
   1. First let's get the IP address of your ansible controller. `docker inspect` wants enough of a container ID or name to have a unique ID, and using ID is less typing. Find the container ID of the ansibleclass_ansiblecontroller container (in the CONTAINER ID column of the script output).
   2. Now use the first few characters of the ansibleclass_ansiblecontroller CONTAINER ID (enough to ensure a unique value) to get that machine's IP addres. **Remember that case matters for 'IPAddress', and that YOUR value for CONTAINER ID of your ansibleclass_ansiblecontroller conttainer probably won't be 'fd' - substitute your own value.**
   ```
   sudo docker inspect fd | grep IPAddress
   ```
   3.  Make note of the IP address somewhere. If you've got a printed copy of this manual, there's a handy table below.
8. Using the CONTAINER ID of the image name ansibleclass_ansiblecontroller we will use the following command to attach to that container, from there we will conduct the remainder of these labs.
- Notice how we only needed the first three characters of the CONTAINER ID to attach to the desired container. If the first three characters are unique this works, if they weren’t unique we would need to include more characters.
- If your prompt has changed to the following example, then you know you have successfully attached to the Ansible control container. Note that your CONTAINER ID will mostly likely be different from what you see in the lab guide.
- Reminder: The above steps do not have anything to do with Ansible and are strictly for connecting to our lab environment for this course! Your actual work environment might require different connection steps prior to using Ansible.

From: ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide - ©2018 Techtown Training
