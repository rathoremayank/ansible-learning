ansible webservers -i inventory -m ping -vv
ansible 2.7.7
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/stduser/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.7.3 (default, Dec 20 2019, 18:57:59) [GCC 8.3.0]
Using /etc/ansible/ansible.cfg as config file
/home/stduser/ansible-learning/lesson2_INVENTORY_FEATURES/inventory did not meet host_list requirements, check plugin documentation if this is unexpected
/home/stduser/ansible-learning/lesson2_INVENTORY_FEATURES/inventory did not meet script requirements, check plugin documentation if this is unexpected
META: ran handlers
web1 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
META: ran handlers
META: ran handlers
