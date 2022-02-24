# Nginx Ansible Role

[![CI](https://github.com/bilalcaliskan/nginx-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/nginx-ansible-role/actions?query=workflow%3ACI)
[![GitHub tag](https://img.shields.io/github/tag/bilalcaliskan/nginx-ansible-role.svg)](https://GitHub.com/bilalcaliskan/nginx-ansible-role/tags/)

Installs and configures Nginx on Redhat/Debian based hosts.

## Requirements

This role requires minimum Ansible version 2.4 and maximum Ansible version 2.9. You can install suggested version with pip:
```
$ pip install "ansible==2.9.16"
```

Also note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook.

## Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role can ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to start and enable `firewalld` service, please modify below variable as true while running playbook:
> ```yaml
> firewalld_enabled: true
> ```

**Additional vserver configuration**
You can provide additional Nginx vserver configurations if you like. To do that;

_invoke the role with role vars:_
```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.nginx
      vars:
        vservers:
          - name: ${name_of_vserver}
            file: ${path_of_custom_file}
            port: ${port_of_vserver}/tcp
```

## Dependencies

None

## Examples
### Inventory
```
[nginx]
nginxnode01.example.com
nginxnode02.example.com
nginxnode03.example.com
```

### Installation
```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.nginx
      vars:
        version: 1.17.9
        worker_processes: auto
        worker_connections: 4096
        worker_rlimit_nofile: 10240
        enable_ramfs: true
        ramfs_dir: /var/lib/nginx
        ramfs_size: 2G
```

### Uninstallation
```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.nginx
      vars:
        install_nginx: false
```

## Development
This project requires below tools while developing:
- [Ansible 2.4 or higher](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [pre-commit](https://pre-commit.com/)
- [ansible-lint](https://ansible-lint.readthedocs.io/en/latest/installing.html#using-pip-or-pipx) - required by [pre-commit](https://pre-commit.com/)
- [Bash shell](https://www.gnu.org/software/bash/) - required by [pre-commit](https://pre-commit.com/)

## License
Apache License 2.0
