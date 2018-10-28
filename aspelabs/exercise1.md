##Exercise 1: Installing Ansible##
- These instructions will show you how to install the Ansible controller on a Debian-based Linux distribution (like Ubuntu 16.04 LTS - our controller container's distribution). Refer to the documentation from Ansible if your operating system is not Debian based.

1. First we'll ask the apt-get package manager to reload it's cache of available packages. It is important to run this so that subsequent package insall get the most current version of the specified packages.
```
apt-get update
```
2. Next we'll ask apt-get to install the latest verion of the "software-properties-common" package, which defines a number of common dependencies which we'll need. in order to add a new repository and run install scripts.
```
apt-get install software-properties-common
```
3. Now we'll add the Ansible repository to our sources list so that we can easily manage the Ansible package.
```
apt-add-repository ppa:ansible/ansible
```
4. Anytime a repository is added or removed from the sources list another update needs to be run against the package managers cache. Now that we have added the Ansible repositories, our package manager still does not know about any of the Ansible packages since it only has a list of what is available based on the last cache update. So, we'll ask apt-get to reload it's cache of available packages again.
```
apt-get update
```
5. Finally, this command uses the package manager to reach out and install Ansible on our control machine.
```
apt-get install ansible
```

From: ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide ©2018 Techtown Training
