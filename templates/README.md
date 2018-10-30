- Often we'll want to copy a large text-based file (say a configuration file) to hosts but with changes made at runtime. To do this, we can use the Ansible ```template``` module. The template module uses Jinja2 replacement techniques to allow us to store our text-based files in their native format (no worrying about escaping common characters, etc.) while also defining places where variables should be innserted or code should be run at run-time.
- In our example, we will demonstrate how to do variable replacement, how to execute code during that variable replacement process, and how to access groups defined in our inventories as lists.
- The example contemplates a fairly common scenario. One (or more) nodes is intended to act as a load balancer. The load balancer needs to know which nodes under management should have traffic directed toward them. To do this, we will use the ```template``` module to pull from a template for the load balancer's config file. In the template we will loop over the declared webserver group as an array and add a server line for each item in the array. We'll also insert a port number from a variable to show how this might also be set as a separate variable. The resulting output file will be copied by the template module to it's correct home on the load balancer(s).
1. Install the git version control system onto your Ansible controller (if you haven't already).
```
apt-get update && apt-get install git -y
```
1. Change directories to the the root user's home directory, then clone the tutorials to that directory (if you haven't already). Then change directories to templates tutorial.
```
cd ~
git clone https://github.com/papaludwig/ansible-tutorials.git
```
2. Edit the sample inventory file. Notice you will need to substitute your own IP address values, and pay special attention to the vars declared for the loadbalancers group.
```
vim production
```
4. Now edit the file "haproxy.cfg.j2" in the templates directory. 
```
vim templates/haproxy.cfg.j2
```
5. Notice the ```{{ }}``` and ```{% %}``` notation at several places in the file. We are usung the Jinja2 python templating language to allow us to do inline variable replacement and code execution to alter the output file. Your instructor can explain exactly what's going on in the template file.
6. Now edit the playbook file product-playbook.yml. This is where we call the template module in a task for the loadbalancer play.
```
vim product-playbook.yml
```
