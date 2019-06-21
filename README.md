# Docker Quick Install
Playbook ansible to setup Docker and Swarm into multiple machines.

## Prerequisites
You should have ansible installed to your machine.

Actually, the playbook works with theses linux distributions:
* Ubuntu
* Debian

Other distributions will be implemented later.

## Configuration
You should have to edit some files to run the playbook. The following wil explain what file change.

### Files

#### group_vars

You should edit the group_vars/all.yml:
* ansible_ssh_private_key_file: set you private key

Example:
```
ansible_ssh_private_key_file: "/home/aimen/.ssh/aimen_ec2.pem"
```

#### hosts
You should edit the hosts file:
* manager1: add the ansible_host and user (user into the machine)
* worker1: add the ansible_host and user

You must have only one manager1, others managers could be declared to the managers group.

You can declare what number of workers you want.

Example:
```
[manager-first]
manager1 ansible_host="18.223.125.142" ansible_user="ubuntu"

[managers]

[workers]
worker1 ansible_host="18.224.34.32" ansible_user="ubuntu"
worker2 ansible_host="3.17.157.194" ansible_user="ubuntu"

```

### Security

#### AWS
If you want to run this playbook to AWS, you should have theses opened ports :
* TCP 22
* TCP 2376
* TCP 2377
* UDP 4789
* TCP and UDP 7946

You can refer to the [introduction of Digital Ocean article](https://www.digitalocean.com/community/tutorials/how-to-configure-the-linux-firewall-for-docker-swarm-on-ubuntu-16-04).

## Usage
To run the playbook, you can follow this command:
```
ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts docker_setup.yml
```

