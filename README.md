
# Decription

This is a brief guide in order to install and deploy: Apache & Postgresql using Ansible


# Project folder:

```
├── postgresql_playbook.yml
├── roles
│   └── createdb
│       ├── handlers
│       │   └── main.yml
│       └── tasks
│           └── main.yml
│   └── createApache
│       ├── handlers
│       │   └── main.yml
│       └── tasks
│           └── main.yml
└── vars
    └── main.yml
```
# Mandatory Installations 

```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

# Understanding Basic Terminology

1. **Hosts**

Ansible contains information about the hosts and groups of hosts to be managed in the hosts file. This is also called an inventory file. We just finished with Inventory File.


2. **Playbook**

Ansible playbooks help the management of a remote computer in a scripted way.A group of systems can be configured by passing scripts to those systems, using ansible. These scripts are called playbooks. They are written in YAML format.

Each playbook contains one or more roles that provision one or more hosts by executing tasks.


3. **Roles**

In our case, we are provisioning a db server, in other cases, it would be db server, mail server, web server, so on and so forth. To manage all these different type of servers, it will become difficult to put the contents in a single file. For this purpose, we can have multiple directories, for multiple purpose(roles).

Roles, are abstractable, and one can inherit from the other. For instance, the web and mail server needs to install basic packages like build-essential, ntp, and supervisor. A common role can be created, and the web & mail server can execute the common tasks, present in the common role

# How it works


Set up Ansible host file. In this case Im working on localhost. 

```
root@osboxes:/home/osboxes/Desktop/Proyectos/STAMP/Ansible# cd /etc/ansible/
root@osboxes:/etc/ansible# ls
ansible.cfg  hosts  playbook.yml  roles
root@osboxes:/etc/ansible# cat hosts 
# This is the default ansible 'hosts' file.
#
# It should live in /etc/ansible/hosts
#
#   - Comments begin with the '#' character
#   - Blank lines are ignored
#   - Groups of hosts are delimited by [header] elements
#   - You can enter hostnames or ip addresses
#   - A hostname/ip can be a member of multiple groups

# Ex 1: Ungrouped hosts, specify before any group headers.

## green.example.com
## blue.example.com
## 192.168.100.1
## 192.168.100.10

# Ex 2: A collection of hosts belonging to the 'webservers' group

[webservers]
## alpha.example.org
## beta.example.org
## 192.168.1.100
## 192.168.1.110
**127.0.0.1**

# If you have multiple hosts following a pattern you can specify
# them like this:

## www[001:006].example.com

# Ex 3: A collection of database servers in the 'dbservers' group

## [dbservers]
## 
## db01.intranet.mydomain.net
## db02.intranet.mydomain.net
## 10.25.1.56
## 10.25.1.57

# Here's another example of host ranges, this time there are no
# leading 0s:

## db-[99:101]-node.example.com


```

Run ansible: 

```
root@osboxes:/Ansible# ansible-playbook ansible.yml

```

# Output

PLAY [Deploy an App using Ansible] ********************************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************************************
ok: [127.0.0.1]

TASK [createdb : Install PostgreSQL] ******************************************************************************************************************
ok: [127.0.0.1] => (item=[u'postgresql', u'postgresql-contrib', u'libpq-dev', u'python-psycopg2'])

TASK [createdb : Create user and gran access to database] *********************************************************************************************
ok: [127.0.0.1]

TASK [createdb : Start the PostgreSQL service] ********************************************************************************************************
ok: [127.0.0.1]

TASK [createdb : Import data into the database (using psql to pull in data from /..)] *****************************************************************
changed: [127.0.0.1]

TASK [createdb : Ensure database is created] **********************************************************************************************************
ok: [127.0.0.1]

TASK [createdb : Ensure user has access to the database] **********************************************************************************************
ok: [127.0.0.1]

TASK [createdb : Ensure user does not have unnecessary privileges] ************************************************************************************
ok: [127.0.0.1]

TASK [createApache : install apache2] *****************************************************************************************************************
ok: [127.0.0.1]

TASK [createApache : enabled mod_rewrite] *************************************************************************************************************
ok: [127.0.0.1]

PLAY RECAP ********************************************************************************************************************************************
127.0.0.1                  : ok=10   changed=1    unreachable=0    failed=0   
