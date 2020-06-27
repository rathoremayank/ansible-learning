stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES$ tree
.
├── production
│   ├── group_vars
│   │   ├── all
│   │   ├── db
│   │   └── webservers
│   ├── host_vars
│   │   └── web1
│   ├── inventory_prod
│   └── readme.txt
└── test
    ├── group_vars
    │   ├── all
    │   └── db
    ├── host_vars
    │   └── web1
    └── inventory_test

6 directories, 10 files

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------



stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345"
 [WARNING]: The input password appears not to have been hashed. The 'password' argument must be
encrypted for this module to work properly.

web1 | FAILED! => {
    "changed": false,
    "msg": "useradd: Permission denied.\nuseradd: cannot lock /etc/passwd; try again later.\n",
    "name": "all_username",
    "rc": 1
}
stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" -v
Using /etc/ansible/ansible.cfg as config file
/home/stduser/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production/inventory_prod did not meet host_list requirements, check plugin documentation if this is unexpected
/home/stduser/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production/inventory_prod did not meet script requirements, check plugin documentation if this is unexpected
 [WARNING]: The input password appears not to have been hashed. The 'password' argument must be
encrypted for this module to work properly.

web1 | FAILED! => {
    "changed": false,
    "msg": "useradd: Permission denied.\nuseradd: cannot lock /etc/passwd; try again later.\n",
    "name": "all_username",
    "rc": 1
}
stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --sude
Usage: ansible <host-pattern> [options]

ansible: error: no such option: --sude
stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --sudo
[DEPRECATION WARNING]: The sudo command line option has been deprecated in favor of the "become" 
command line arguments. This feature will be removed in version 2.9. Deprecation warnings can be 
disabled by setting deprecation_warnings=False in ansible.cfg.
web1 | FAILED! => {
    "changed": false,
    "module_stderr": "Shared connection to 10.128.0.5 closed.\r\n",
    "module_stdout": "sudo: a password is required\r\n",
    "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error",
    "rc": 1
}

stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --sudo 
[DEPRECATION WARNING]: The sudo command line option has been deprecated in favor of the "become" command line arguments. This feature will be removed in version 2.9. Deprecation warnings can be 
disabled by setting deprecation_warnings=False in ansible.cfg.
web1 | FAILED! => {
    "changed": false,
    "module_stderr": "Shared connection to 10.128.0.5 closed.\r\n",
    "module_stdout": "sudo: a password is required\r\n",
    "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error",
    "rc": 1
}
stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --sudo -k
[DEPRECATION WARNING]: The sudo command line option has been deprecated in favor of the "become" command line arguments. This feature will be removed in version 2.9. Deprecation warnings can be 
disabled by setting deprecation_warnings=False in ansible.cfg.
stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible websSSH password: 
web1 | FAILED! => {
    "changed": false,
    "module_stderr": "Shared connection to 10.128.0.5 closed.\r\n",
    "module_stdout": "sudo: a password is required\r\n",
    "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error",
    "rc": 1
}
stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --sudo 
[DEPRECATION WARNING]: The sudo command line option has been deprecated in favor of the "become" command line arguments. This feature will be removed in version 2.9. Deprecation warnings can be 
disabled by setting deprecation_warnings=False in ansible.cfg.
 [WARNING]: The input password appears not to have been hashed. The 'password' argument must be encrypted for this module to work properly.

web1 | CHANGED => {
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1004,
    "home": "/home/all_username",
    "name": "all_username",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "",
    "state": "present",
    "system": false,
    "uid": 1003
}



-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

"--sudo" should be replaced by "--become"



stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --become
 [WARNING]: The input password appears not to have been hashed. The 'password' argument must be encrypted for this module to work properly.

web1 | SUCCESS => {
    "append": false,
    "changed": false,
    "comment": "",
    "group": 1004,
    "home": "/home/all_username",
    "move_home": false,
    "name": "all_username",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "",
    "state": "present",
    "uid": 1003
}


THIS IS A SUCCESS |  ANSIBLE CREATED A NEW USER IN 10.128.0.5 WITH THE USERNAME all_username
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------





















NOW WE HAVE PROVIDED A NEW USERNAME IN A FILE IN THE GROUP DIRECTORY [group_vars/webserver]

THIS IS THE OUTPUT: 

stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --become
 [WARNING]: The input password appears not to have been hashed. The 'password' argument must be
encrypted for this module to work properly.

web1 | CHANGED => {
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1005,
    "home": "/home/group_user",
    "name": "group_user",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "",
    "state": "present",
    "system": false,
    "uid": 1004
}

IT PICKED UP THE NEW USERNAME || ACCORDING TO THE PRECEDENCE RULES
----------------------------------------------------------------------------------

















NOW WE HAVE PROVIDED A NEW USERNAME IN A FILE IN THE HOST DIRECTORY [host_vars/web1]

THIS IS THE OUTPUT:




stduser@ansible-controller:~/ansible-learning/lesson3_ANSIBLE_DIRECTORIES/production$ ansible webservers -i inventory_prod -m user -a "name={{username}} password=12345" --become
 [WARNING]: The input password appears not to have been hashed. The 'password' argument must be
encrypted for this module to work properly.

web1 | CHANGED => {
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1006,
    "home": "/home/web1_user",
    "name": "web1_user",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "",
    "state": "present",
    "system": false,
    "uid": 1005
}

IT PICKED UP THE NEW USERNAME AGAIN | ACCORDING TO THE PRECEDENCE RULES 

----------------------------------------------------------------------------------



