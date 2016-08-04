## Ansible Tower 3.0.1 installation

This is a quickstart reference of the commands needed to install and configure Ansible Tower. 


### Installation

**NOTE** These steps are specific to CentOS/RHEL

Install EPEL repository

```yum install -y http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm```

Download Tower

```wget https://releases.ansible.com/awx/setup/ansible-tower-setup-latest.tar.gz```

Extract Tower

```tar zxvf ansible-tower-setup-latest.tar.gz```

Switch to Ansible Tower directory

```cd ansible-tower-setup*```

Edit inventory file 

```vi inventory```

Below is an example inventory file, make sure to update the password values. 

```yaml
[primary]
localhost ansible_connection=local

[secondary]

[database]

[all:vars]
admin_password='password'
redis_password='password'

pg_host=''
pg_port=''

pg_database='awx'
pg_username='awx'
pg_password='password'
```
Ansible requires ssh access to the hosts it will be managing.  

Generate an SSH key

```ssh-keygen```

Hit enter to accept defaults

Add ssh key to authorized_keys file

```cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys```

Setup permissions

```chmod 600 ~/.ssh/authorized_keys```

Now ssh to localhost and accept the fingerprint

```ssh localhost```


Now we are ready to run the setup script

```./setup.sh```

After setup has completed successfully you will get the following message:

> The setup process completed successfully.
> 
Setup log saved to /var/log/tower/setup-2016-08-04-13:15:37.log


###Quick Start Guide

Now it's time to log into Tower. 

Load the Public IP of your Tower IP in a browser and you should see the login page.  The credentials are username admin and password is whatever you set in inventory file.

After logging in you will be prompted to provide your license file.  This should have been emailed when you signed up for the trial. 

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/no-license.png)

Add Admin user to default organization 

Click Settings cog in top right corner and then click on Organizations. 

Click Users 

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/qs-organizations-click-to-expand-users-section.png)

Click Add User 

Select checkbox next to Admin and click Save. 

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/qs-organizations-create-user-form.png)

After saving, the organization’s user information becomes available for viewing and the new user you created appears on the list.

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/qs-organizations-new-user-added-to-organization.png)

To run the demo project you must sync it first. 

At the top of the main screen click Projects and then click the cloud by demo project

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/qs-demo-proj-sync.png)

Now that you've synced the demo project go ahead and launch it! 

Click Job Templates and then click the rocket icon next to Demo Project

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/qs-job-templates-home.png)

You will now see the status of the job with a live events log. 

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/qs-job-templates-demo-pending.png)

Wait a few minutes and the job should complete successfully. 

![](http://docs.ansible.com/ansible-tower/latest/html/quickstart/_images/qs-job-templates-demo-complete.png)


