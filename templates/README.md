- Often we'll want to copy a large text-based file (say a configuration file) to hosts but with changes made at runtime. To do this, we can use the Ansible ```template``` module. The template module uses Jinja2 replacement techniques to allow us to store our text-based files in their native format (no worrying about escaping common characters, etc.) while also defining places where variables should be innserted or code should be run at run-time.
- In our example, we will demonstrate how to do variable replacement, how to execute code during that variable replacement process, and how to access groups defined in our inventories as lists.
- The example contemplates a fairly common scenario. One (or more) nodes is intended to act as a load balancer. The load balancer needs to know which nodes under management should have traffic directed toward them. To do this, we will use the ```template``` module to pull from a template for the load balancer's config file. In the template we will loop over the declared webserver group as an array and add a server line for each item in the array. We'll also insert a port number from a variable to show how this might also be set as a separate variable. The resulting output file will be copied by the template module to it's correct home on the load balancer(s).
1. Change directories to the the root user's home directory, the create a templates directory there.
```
cd ~
mkdir templates
```
2. Make an new inventory file in the root user's home directory (not in the templates directory we just created) called "production".
```
vim production
```
3. Make the contents of your new inventory file like this: **Remember, use your own IP address values for your nodes.**
```
ubuntu1 ansible_host=172.18.0.6
ubuntu2 ansible_host=172.18.0.4
centos1 ansible_host=172.18.0.5
centos2 ansible_host=172.18.0.3

[webservers]
ubuntu2
centos2

[loadbalancers]
ubuntu1

[loadbalancers:vars]
public_traffic_port=80
internal_traffic_port=8080
```
4. Now create and edit the file "haproxy.cfg.j2" in the templates directory.
```
vim templates/haproxy.cfg.j2
```
