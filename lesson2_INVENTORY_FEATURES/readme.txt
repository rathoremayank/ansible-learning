stduser@ansible-controller:~/ansible-learning/lesson2_INVENTORY_FEATURES$ ansible datacenter -i inventory -m ping -v
Using /etc/ansible/ansible.cfg as config file
/home/stduser/ansible-learning/lesson2_INVENTORY_FEATURES/inventory did not meet host_list requirements, check plugin documentation if this is unexpected
/home/stduser/ansible-learning/lesson2_INVENTORY_FEATURES/inventory did not meet script requirements, check plugin documentation if this is unexpected
web1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
db1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
