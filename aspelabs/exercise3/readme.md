Exercise 3: Building an Inventory
 Ansible makes configuration management a breeze for us, however it has no idea what machines to configure unless we give it somewhere to look for those machines. Being agentless, it relies on us telling the control machine what our actual targets are.
ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide
©2018 Techtown Training
                             
 Let’s look at an ad‐hoc command in ansible. For this we will pick one of our IP Addresses that isn’t our Ansible control machine. The first ad‐hoc command we will look at uses the ping module. Refer to the screenshot below.
 Line 2 is comprised of multiple parts that each play a key role in this ad‐hoc command. First ansible calls the Ansible program installed on our control machine. The ‐m specifies that we are going to use a module, in this case the module used is ping. The ping module requires an argument to function properly, in the above example that argument is the IP Address of the node we wish to ping.
 While using Ansible in ad‐hoc mode completes our task as desired, the module only ran against one target machine. In our environments we always have an array of targets to complete tasks against. Ansible handles these targets in it’s inventory file. The inventory is located, by default, in the path below.
 Note that the actual file is named hosts, do not confuse this with the hosts file that is used to map IP Addresses to host names on a network. Each operating system has a hosts file, and this is largely confusing to new Ansible users. The hosts file in this directory is Ansibles inventory file.
 Let’s take a few minutes to build out the inventory file we are going to use for the time being in this lab. On your control machine navigate to the location of the Ansible hosts file and use vim to open it for editing.
 Line 2 is what sets our working directory to the desired location
 Line 4 uses vim, a terminal‐based text editor, to make changes to our hosts file.
ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide
©2018 Techtown Training
                                              
 When the hosts file is opened for editing you will notice it is prefilled with examples in comment form for the host file. Take a minute to read through what is there. Once you are done you can either remove all the current contents of the hosts file, or just navigate to a new line at the bottom of the document.
 Adding the target machines in our environment to the inventory is done in a simple manner. No programming language is necessary, making this an ideal tool for just about anyone in your organization.
 To form a new group inside of the inventory file square brackets, [ ], are used with a desired group name in between them. First, let’s make two groups that separate our Ubuntu machines from our Centos7 machines.
 Keep in mind that the IP Addresses you have for your target machines might be different from what you see in the example above. Make sure you place the IP Addresses that your target machines are using into the proper group.
 Line 2 uses the square brackets to declare a group named deb. This is name was assigned by us and could have been anything we wanted it to be, deb makes sense for our Ubuntu machines, since that’s what the distribution is based on.
 Lines 3‐4 place one IP Address per line, in this case it is the IP Addresses of our Ubuntu machines.
 Line 6 creates a second group named rpm which will contain the IP Addresses of our Centos7 targets. Again, this could be named anything, so use care when naming groups, the more they make sense the easier managing them in the future will be.
 Lines 7‐8 add our Centos7 machines to the rpm group. Double check to be sure you added the IP Addresses of the Centos7 machines currently running in your environment, as they might be different from what you see in the example above.
ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide
©2018 Techtown Training
                                   
 Now that we have two separate groups we can practice using Ansible in ad‐hoc mode, and better orchestrating where those modules are being directed. Let’s use the ping module again, but this time we will specify a group instead of a single IP Address.
 You should now see output that shows the result of the module running against the entire group. This is just a small example of how configuration management can be leveraged, there are more to come as this course continues.
 Ansible contains a built‐in group. The name of this group is all. This group allows us to run a module, or playbook, which will be covered later, against every host, except localhost, in the inventory file. Let’s try this same module using all instead of one of our newly created groups.
 There should now be output for every host in your inventory file.
 Now that we have seen the most basic way to use an inventory file, use vim to create two new groups dbservers and webservers. Once both groups are made add one Ubuntu machine and one Centos7 machine to each group. We will use these two groups as this lab continues, so please be sure to ask for help if you are stuck.
                              ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide
©2018 Techtown Training

                                        Take note that now we have a situation where our target machines are members of multiple groups. This is not uncommon for an Ansible inventory file. It is important to understand that if a target is a part of multiple groups, that target will get its variables from all the groups it is a part of.
 The Ansible inventory is also capable of holding behavioral inventory parameters for each host. In this next section we will use the variables to give our target machines actual names, which will allow us to work with them easily. Understand that although this will look like a DNS entry, it is nothing more than a user defined alias for a given target machine.
 We will look at variables in greater detail later in this workshop. For now, let’s add the example below to our playbook just so we can get an introduction to the flexibility of the inventory file.
           ANSIBLE CONFIGURATION MANAGEMENT Student Lab Guide
©2018 Techtown Training

                 
