# Ansible_Notes

`https://stackoverflow.com/questions/58105841/cannot-run-ansible-on-rhel-7-paramiko-is-not-installed`

-----

`/etc/ansible/ansible.cfg`

-   Default Control Node config

`/etc/ansible/hosts`

-   Default Managed Node List

`ansible all --list-hosts`

-   List All Hosts.

`ansible webservers --list-hosts`

-   List only hosts in the WebServers Group.

`ansible all -m ping`

-   Ping all hosts.

`ansible-doc -l`

-   List Available Modules.

`http://docs.ansible.com/ansible/latest/modules_by_category.html`

-   Lists Modules.
