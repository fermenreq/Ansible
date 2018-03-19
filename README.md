
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

