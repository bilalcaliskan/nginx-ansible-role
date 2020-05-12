## Nginx Ansible Role

[![Build Status](https://travis-ci.org/bilalcaliskan/nginx-ansible-role.svg?branch=master)](https://travis-ci.org/bilalcaliskan/nginx-ansible-role)

Installs and configures Nginx on Centos/RHEL 7/8 servers.

## Requirements

No special requirements; note that this role requires root access, so either run it in a
playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: all
      become: true
      roles:
        - role: bilalcaliskan.nginx

## Role Variables

Example parameters are listed below. See defaults/main.yml for all:

    version: 1.17.9
    worker_processes: auto
    worker_connections: 4096
    worker_rlimit_nofile: 10240
    enable_ramfs: true
    ramfs_dir: /var/lib/nginx
    ramfs_size: 2G

## Dependencies

None

## Additional Vserver Configuration

You can provide additional Nginx vserver configurations if you like. To do that;
*Override the parameters inside `vars/main.yml`:
    vservers:
      - name: ${name_of_vserver}
        file: ${path_of_custom_file}
        port: ${port_of_vserver}/tcp

## Example Playbook

    - hosts: all
      become: true
      vars_files:
        - vars/main.yml
      roles:
        - role: bilalcaliskan.nginx

*Override the parameters you need to change inside `vars/main.yml`*:

    version: 1.17.9
    worker_processes: auto
    worker_connections: 4096
    worker_rlimit_nofile: 10240
    enable_ramfs: true
    ramfs_dir: /var/lib/nginx
    ramfs_size: 2G

## Playbook for uninstall

    - hosts: all
      become: true
      roles:
        - { role: bilalcaliskan.nginx }

*Inside `vars/main.yml`*:

    install_nginx: false

## License

MIT / BSD
