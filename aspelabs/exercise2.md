# Exercise 2: Post Installation Tasks
- By default, Ansible manages machines using the SSH protocol. Since SSH has not yet been configured in our environment we need to take a few minutes to create the keys for our user and get them copied over to our target machines. These commands are not Ansible specific, however without them our labs will not work.
- You work environment may use a different method of ensuring keys are on the hosts machines. You are not wrong for doing it your way, this is just ONE of the many ways to distribute the necessary keys. What will nearly always be true, however, is that Ansible uses SSH, so ensuring that good key management is in place is essential to adopting the tool.
1. To generate a set of keys, use the following command. **You will be prompted for a passphrase. In our environment LEAVE IT BLANK and just press ENTER.** In your actual production environment this is not a safe, nor recommended, practice! However, if you do not leave it blank here, you will need to type that passphrase every time we run anything using Ansible... for each host that task is run against, which will slow us down considerably.
```
ssh-keygen
```
2. Once you have the key generated, we now need to copy it to all the nodes we intend to manage in our environment so that we can connect to them using SSH. To do so, we will need the IP Addresses of our target machines, which we gathered in an earlier exercise. Refer to your notes for those IP addresses. we will run the ssh-copy-id command once for each of our target nodes. You will be prompted to enter the password for the root account. That password is **pass** (all lowercase - this was defined in our docker setup script). **Remember to use the IP addresses of YOUR ubuntu and centos nodes.**
```
ssh-copy-id [ubuntu1 IP address]
ssh-copy-id [ubuntu2 IP address]
ssh-copy-id [centos1 IP address]
ssh-copy-id [centos2 IP address]
```

From: ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide ©2018 Techtown Training
