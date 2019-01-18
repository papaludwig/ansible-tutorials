# Dynamic Inventory from AWS EC2 Using ec2.py
[ec2.py](https://github.com/ansible/ansible/blob/devel/contrib/inventory/ec2.py) is a contributed script that can directly output JSON formatted lists of your AWS resources, ready to become a dynamic inventory for your Anisble system since it supports being marked executable and supports the --list argument.

## Steps for using ec2.py:
1. Install the [pip](https://pip.pypa.io/en/stable/installing/) Python package manager to allow easy installation of the [Boto python package](https://github.com/boto/boto) (which implements AWS communication for Python)
````
cd ~
wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py
pip --version
````
2. Then install [Boto](https://github.com/boto/boto)
````
pip install boto
````
3. Now you're ready to use ec2.py, so go ahead and grab it. (You may want to have it live in /etc/ansible, or wherever your hosts file would normally be for the role you're working with)
````
cd /etc/ansible
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py
chmod +x ec2.py
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini
````
4. In a production environment, you'll want an AWS IAM user with read-only permissions for the services you intend to inventory
   1. Log into AWS
   2. Navigate to Services->IAM
   3. Navigate to Users->Create User
   4. Choose an appropriate user name like ec2reader or ec2py-user and set that as the User name.
   5. Check the Programmatic access checkbox, make sure password/console access is unchecked
   6. Click Next: Permissions
   7. Click Attach Existing policies directly
   8. Search for ec2R
   9. Check the AMazonEC2ReadOnlyAccess checkbox
   10. Click Next:Review
   11. Click to download .csv for later
   12. Copy/paste Access Key ID & Secret Key Value for now
5. Set the AKID & SV as environment variables (this step) OR set them in ec2.ini file (see step 6 below). Environment variable overrides, so be cautious.
````
export AWS_ACCESS_KEY_ID='AK123'
export AWS_SECRET_ACCESS_KEY='SAKV'
````
6. Edit the ec2.ini to make appropriate changes
   1. Uncomment and properly set comma delimited list of regions (to improve performance by skipping unused regions)
   2. Comment regions_exclude (not needed when explicitly setting regions)
   3. Uncomment rds = false (unless you want to include RDS instances and have set appropriate permissions for you IAM user)
   4. Uncomment ElastiCache = false (again, unless you need them and have set permissions appropriately)
   5. If not using environment variables (skipped step 5 above) uncomment and adjust Access Key ID and Secret Access Key Value
7. Try running the script
````
./ec2.py --list
````
### References:
1. https://docs.ansible.com/ansible/latest/user_guide/intro_dynamic_inventory.html#example-aws-ec2-external-inventory-script
2. https://github.com/boto/boto
3. https://pip.pypa.io/en/stable/installing/
