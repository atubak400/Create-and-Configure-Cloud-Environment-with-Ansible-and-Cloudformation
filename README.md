# Create-and-Configure-Cloud-Environment-with-Ansible-and-Cloudformation

![Ansible](./img/0a.webp)

## What is Ansible

Ansible is an open-source automation tool that simplifies configuration management, application deployment, and task automation through agentless, declarative playbooks written in YAML.

## What is Cloudformation

AWS CloudFormation is a service that enables users to define and provision AWS infrastructure as code (IaC) using declarative templates, allowing for automated and repeatable provisioning of resources.

## Objective

We will be using Cloudformation and Ansible to create and configure our Cloud Environment.


# Project Steps
> Step 1: Create and Activate a virtual Environment and Install Ansible using the codes below:

```
python3 -m venv myenv
```

```
source myenv/bin/activate
```

```
sudo pip install ansible
```

![Ansible](./img/1.png)

> Step 2: Confirm Ansible installation using the code below

```
ansible --version
```

![Ansible](./img/2.png)

> Step 3: Create Key Pair on AWS Console

![Key Pair](./img/3.png) 

> Step 4: Upload Template file `setup-env.yml`

![template file](./img/5.png) 
![template file](./img/6.png) 

> Step 5: Checkout your template file infrastructure design

![template design](./img/4.png)

> Step 6: Specify Stack Details

![stack details](./img/7.png)
![stack details](./img/8.png)

> Step 7: Create Stack

![Create Stack](./img/9.png)
![Create Stack](./img/10.png)
![Create Stack](./img/11.png)
![Create Stack](./img/12.png)

> Step 8: Confirm ec2 instances creation

![instances creation](./img/13.png)

> Step 8: Confirm elastic IP creation

![instances creation](./img/14.png)


## What is Ansible Inventory File

![stack details](./img/16.png)
![stack details](./img/17.png)

> Step 9: Create an Ansible Inventory File using the code below:

```
code hosts-dev.txt
```

and paste the code below in the file

```
# hosts-dev

[webservers]
`Server_1 IP`
`Server_2 IP`

[loadbalancers]
`LoadBalancer IP`

[local]
control ansible_connection=local
```

![instances creation](./img/18.png)

> Step 10: Use Ansible to list all hosts defined in your inventory file `hosts-dev`

```
ansible -i hosts-dev --list-hosts all
```

![list all hosts](./img/19.png)


## What in is an Ansible Configuration File

An Ansible configuration file, often named ansible.cfg, allows users to centrally define default settings, such as the inventory file path and SSH configuration, for maintaining consistency across Ansible playbooks and projects.

> Step 11: Create an Ansible Configuration File in the Project home directory using the codes below:

```
code ansible.cfg
```

and paste the code below in the configuration file

```
# ansible.cfg

[defaults]
inventory = ./hosts-dev
```

![Create Ansible Configuration File](./img/20.png)

> Step 12: With this configuration file, you no longer need to specify the inventory file location to list your hosts(i.e servers):

```
ansible --list-hosts all
```

![list all hosts](./img/21.png)


> Step 13: We can target our WebServers and LoadBalancers seperately:

![list all hosts](./img/22.png)


> Step 14: We can create aliases for our IP addresses

```
# hosts-dev

[webservers]
app1 ansible_host=54.203.202.27
app2 ansible_host=34.210.41.204

[loadbalancers]
lb1 ansible_host=52.34.47.202

[local]
control ansible_connection=local

```
![list all hosts](./img/23.png)

> Step 14: We can list our hosts by their aliases

![list all hosts](./img/24.png)
