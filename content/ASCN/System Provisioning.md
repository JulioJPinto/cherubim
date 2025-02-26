# Provisioning

**Provisioning** is the action of providing or supplying something for use (server provisioning, storage ...).

# Deployment

**Deployment** is the process of installing or upgrading an application/service into a server (installing or upgrading a web application for example).

# Problems with both provisioning and deployment

- The process is repetitive and boring after its first iteration;
- So, it is a great target for automation;
- It may spread across multiple and heterogeneous systems (with different hardware e.g);
-  Will probably have tweaks/updates overtime so it is a good idea to use _versioning_;
- Sometimes it is a time consuming task so it's probably best to let the machine do it and do something else during that time.

# Configuration Management

It is a way of handling systematic system changes while maintaining integrity throughout its life cycle.

# Recipes

A way of defining task automation via a set of directives expressed in a given language:

### Example

```bash
#!/bin/sh  
username=deployer  
apt-get -y update  
apt-get -y upgrade  
apt-get -y install vim-nox openntpd sudo whois aptitude  
useradd -G sudo -p "password" -s /bin/bash -m $username  
mkdir -p /home/$username/.ssh  
chmod 700 /home/$username/.ssh  
chown $username: /home/$username/.ssh  
echo "public_key" >> /home/$username/.ssh/authorized_keys  
chmod 600 /home/$username/.ssh/authorized_keys  
chown $username: /home/$username/.ssh/authorized_keys
```


# Ansible

_Ansible_ is an open-source tool used for configuration management application deployment, intra-service orchestration, and provisioning.

- Agentless recipe execution via _SSH_ or locally:
	- Target hosts are defined in the inventory.
	
- Recipes are expressed in _YAML_:
	- Recipes are created via modules and task directives;
	- Recipes are organized into roles and playbooks.
	
- Tasks only run if the target differes from the expected result(idempotency).

##  How Ansible Works

- Ansible is operated from a **Management Node**, where you write and execute your playbooks and commands;
- The list of hosts to be managed by Ansisble is specified in the **Inventory** file;
- Ansible connects to remote hosts using SSH and executes the set of tasks defined in a _playbook_.

![[Pasted image 20241201153224.png]]



