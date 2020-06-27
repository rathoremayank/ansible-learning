stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ tree
.
├── group_vars
│   ├── all
│   ├── db
│   └── webservers
├── host_vars
│   └── web1
└── inventory_prod

2 directories, 5 files
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ cat ~/.ssh/known_hosts 
|1|9153YQTmGizdUnCsIvgqMmJMdQs=|W8LPEIl4m7hLC98bQyHvgfmNrNk= ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJg8mtxICrpTO5UD5G4oqeYxRADH/1SHYbq9PFhBomrJI4jiJXxpGE6vj8MzY/62/kZF/95/rW6MxpNAh0wvatw=
|1|p8olPNHclyrHl7GxCls82q0GVw0=|Vd4PAnwpSKN6tszlT34EObHUpqI= ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBHmDax1t6tlJYQFPzgYxAGAY3oZAt5q+9YkwX/NwUgEUioyKrCCiuij+jLpPsaobMq1iPdriQnOHsagFBH/ZaoM=
|1|D4+qCFi0pAgAQ6ZM2u87SXAekFE=|atOqTIcppmP4T2zJPc5QpTfqi2Q= ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBHmDax1t6tlJYQFPzgYxAGAY3oZAt5q+9YkwX/NwUgEUioyKrCCiuij+jLpPsaobMq1iPdriQnOHsagFBH/ZaoM=
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ vi ~/.ssh/known_hosts 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ ansible web1 -i inventory_prod -m ping 
web1 | FAILED! => {
    "msg": "Using a SSH password instead of a key is not possible because Host Key checking is enabled and sshpass does not support this.  Please add this host's fingerprint to your known_hosts file to manage this host."
}
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 



--------------------------------------------------------------------------------------------------
OVERRIDING DEFAULT CONFIGURATION WITH ./ansible.cfg FILE


stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ vi ansible.cfg
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ cat ~/.ssh/known_hosts 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ ansible web1 -i inventory_prod -m ping
web1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ cat ~/.ssh/known_hosts 
|1|42vebLilTU0Okd32bgNDhs85+TY=|O5hqkw0KftgpXbej02051+8l0E8= ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBHmDax1t6tlJYQFPzgYxAGAY3oZAt5q+9YkwX/NwUgEUioyKrCCiuij+jLpPsaobMq1iPdriQnOHsagFBH/ZaoM=
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$









-------------------------------------------------------------------------------------------------
OVERRIDING ./ansible.cfg WITH ENV VARS


stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ vi ~/.ssh/known_hosts 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ cat ~/.ssh/known_hosts 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ export ANSIBLE_HOST_KEY_CHECKING=True
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ echo $ANSIBLE_HOST_KEY_CHECKING
True
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ cat ansible.cfg 
[defaults]
host_key_checking=False
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ ansible web1 -i inventory_prod -m ping 
web1 | FAILED! => {
    "msg": "Using a SSH password instead of a key is not possible because Host Key checking is enabled and sshpass does not support this.  Please add this host's fingerprint to your known_hosts file to manage this host."
}
stduser@ansible-controller:~/ansible-learning/lesson4_ANSIBLE_CONFIGURATION/production$ 

