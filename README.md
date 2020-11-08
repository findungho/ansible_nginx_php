### Author: Dung Ho
### Email: fin.dungho@gmail.com
### Phone number: +358 449865555


## Overview
_This is a simple automative tasks that is using 'ansible' to install the webservices and run a simple php webpage._

## General
- The automative ansible includes 2 ubuntu node, inventory, 3 roles and variables.
- The ubuntu nodes address can re-define in '/inv/hosts'.
- Roles:
    + nginx_install: Install nginx packages, modify nginx configuration and copy the website templates to the target hosts.
    + php_install: Install php packages to the target hosts.
    + webservices_uninstall: Uninstall nginx and php packages, also remove the website templates. 
- Folder structure:
```
├── ansible.cfg
├── group_vars
│   ├── testservers.yml
│   └── webservers.yml
├── inv
│   └── hosts
├── README.md
├── roles
│   ├── nginx_install
│   │   ├── files
│   │   │   ├── index.php
│   │   │   └── info.php
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   │   └── nginx.conf.j2
│   │   └── vars
│   │       └── main.yml
│   ├── php_install
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   └── main.yml
│   │   └── vars
│   │       └── main.yml
│   └── webservices_uninstall
│       ├── tasks
│       │   └── main.yml
│       └── vars
│           └── main.yml
├── test.yml
├── webservices_install.yml
└── webservices_uninstall.yml
```

## Requirements
- The controller and the target hosts are running on Ubuntu.
- 'openssh' is installed on the controller and the target hosts.

## How to use
1. Re-define the target hosts IP addresses:
        `~/inv/hosts`
2. Testing all hosts are reachable:
        `ansible all -m ping`
3. Run the playbook to install webservice packages:
        `ansible-playbook webservices_install.yml`
4. Tesing the target hosts are work probperly:
- Navigate on the controller browser to see the landing page:
        `http://{{target_hosts_ip}}`
- Navigate on the controller browser to see PHP info:
        `http://{{target_hosts_ip/info.php}}`
5. Unsintall the webservice packages:
        `ansible-playbook webservices_uninstall.yml`