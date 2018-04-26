
# Install and deploy your APP using Ansible

![alt text](https://raw.githubusercontent.com/fermenreq/Ansible/master/stamp_ansible.png)


## 1. Project folder:

```
├── postgresql_playbook.yml
├── roles
│   └── createdb
│       ├── handlers
│       │   └── main.yml
│       └── tasks
│           └── main.yml
│   └── createApp
│       ├── handlers
│       │   └── main.yml
│       └── tasks
│           └── main.yml
└── vars
|    └── main.yml
│ 
└──myproject
├── manage.py
├── myapp

```

## 2. Mandatory Installations 

```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```

## 2.1 System Requirements
```
root@osboxes:/home/osboxes/Proyectos/OFION/yourbpm# uname -a
Linux osboxes 4.13.0-39-generic #44~16.04.1-Ubuntu SMP Thu Apr 5 16:43:10 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

root@osboxes:/home/osboxes/Proyectos/OFION/yourbpm# ansible --version
ansible 2.5.1
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.12 (default, Dec  4 2017, 14:50:18) [GCC 5.4.0 20160609]
  
mysql.db
```

## 3. Understanding Basic Terminology

**1. Hosts**

Ansible contains information about the hosts and groups of hosts to be managed in the hosts file. This is also called an inventory file. We just finished with Inventory File.


**2. Playbook**

Ansible playbooks help the management of a remote computer in a scripted way.A group of systems can be configured by passing scripts to those systems, using ansible. These scripts are called playbooks. They are written in YAML format.

Each playbook contains one or more roles that provision one or more hosts by executing tasks.


**3. Roles**

In our case, we are provisioning a db server, in other cases, it would be db server, mail server, web server, so on and so forth. To manage all these different type of servers, it will become difficult to put the contents in a single file. For this purpose, we can have multiple directories, for multiple purpose(roles).

Roles, are abstractable, and one can inherit from the other. For instance, the web and mail server needs to install basic packages like build-essential, ntp, and supervisor. A common role can be created, and the web & mail server can execute the common tasks, present in the common role

## 4. How it works


Edit the ansible/hosts file and enter the IP address of the server you are deploying to

```
root@osboxes:/home/osboxes/Desktop/Proyectos/STAMP/Ansible# cd /etc/ansible/
root@osboxes:/etc/ansible# ls
ansible.cfg  hosts  playbook.yml  roles
root@osboxes:/etc/ansible# cat hosts 
# This is the default ansible 'hosts' file.
.....
.....

# Ex 2: A collection of hosts belonging to the 'webservers' group

[webservers]
## alpha.example.org
## beta.example.org
## 192.168.1.100
## 192.168.1.110
127.0.0.1

```
**Run ansible:**

```
root@osboxes:/Ansible# ansible-playbook ansible.yml

```

## 5. Output

```
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
```

## Author:

Fernando Méndez Requena - fernando.mendez@atos.net
