# Prerequisite: Connecting to Your Ansible Control Machine
- Your lab environment starts as a standard Ubuntu 16.04 LTS Linux virtual machine deployed in the Azure public cloud. Since Ansible is all about managing multiple nodes (hosts) and requires a controller to do this job, one virtual machine wouldn't normally be enough. So, we're going to use a script to set up a series of Docker containers running on our virtual machine. This means that we need to attach to our Ansible control container before we get started. To do this follow these steps.
1. Connect to the virtual machine using SSH. Use your terminal if your workstation is a Linux machine or a Mac. If your workstation is a Windows machine, you will need an application such as PuTTY to connect. If you need PuTTY download it now. Your instructor will provide you with the credentials needed to connect. Replace ## with your instructor-provided user number. -Remember, Linux is case-sensitive almost everywhere, so be careful to preserve upper and lower cases in all these eercises.-
```
ssh ansible@ansible0##.westus.cloudapp.azure.com
```
2. Once connected to virtual machine via SSH we will need to setup our environment. To do so, we'll start by elevating our privileges temporarily and using the apt-get package manager (standard for Debian-based Linux distributions) to make sure the latest available version of the git version control system is installed. These steps can take some time, so be patient. Type the following into the terminal:
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

- Next you will need to execute setup.sh to start the environment. Type the following.
- The output of the above command should look like the screen shot below.
- Using the CONTAINER ID of the image name ansibleclass_ansiblecontroller we will use the following command to attach to that container, from there we will conduct the remainder of these labs.
- Notice how we only needed the first three characters of the CONTAINER ID to attach to the desired container. If the first three characters are unique this works, if they weren’t unique we would need to include more characters.
- If your prompt has changed to the following example, then you know you have successfully attached to the Ansible control container. Note that your CONTAINER ID will mostly likely be different from what you see in the lab guide.
- Reminder: The above steps do not have anything to do with Ansible and are strictly for connecting to our lab environment for this course! Your actual work environment might require different connection steps prior to using Ansible.

From: ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide - ©2018 Techtown Training
