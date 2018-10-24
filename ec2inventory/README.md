# Dynamic Inventory from AWS EC2 Using ec2.py
ec2.py is a contributed script that can directly output JSON and YAML formatted lists of your AWS resources, ready to become a dynamic inventory for your Anisble system.

## Steps for using ec2.py:
1. Install pip to allow easy installation of the [Boto python package](https://github.com/boto/boto) (which implements AWS communication for Python)
````
apt-get update
apt-get install curl
curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
python get-pip.py
pip --version
````
2. Then install Boto
````
pip install boto
````
3. Now you're ready to use ec2.py, so go ahead and grab it:
````
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
AKIAI5EJJ4EUWHFZEUYQ
uFu1iU3A4bXaWGvoAylMBbvqqPGdjGfEx4r+j03U
5. Set the AKID & SV as environment variables OR set them in ec2.ini file. Environment variable override, so be cautious.
````
export AWS_ACCESS_KEY_ID='AKIAI5EJJ4EUWHFZEUYQ'
export AWS_SECRET_ACCESS_KEY='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'
````
6. Get the ec2.py script and make it executable
````
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py
chmod +x ec2.py
````
7. Get the sample ec2.ini file
````
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini
````
8. Edit the ec2.ini to make appropriate changes
   1. Uncomment and properly set comma delimited list of regions
   2. Comment regions_exclude
   3. Uncomment rds = false (unless you want to include RDS instances and have set appropriate permissions for you IAM user)
   4. Uncomment ElastiCache = false (again, unless you need them and have set permissions appropriately)
9. Try running the script
````
./ec2.py --list
````
