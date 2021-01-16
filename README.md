## Nginx Ansible Role

[![CI](https://github.com/bilalcaliskan/nginx-ansible-role/workflows/CI/badge.svg?event=push)](https://github.com/bilalcaliskan/nginx-ansible-role/actions?query=workflow%3ACI)

Installs and configures Nginx on RedHat/CentOS servers(7 and 8).

### Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: true`, or invoke the role in your playbook like:

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.nginx
```

### Role Variables
See the default values in [defaults/main.yml](defaults/main.yml). You can overwrite them in [vars/main.yml](vars/main.yml) if neccessary or you can set them while running playbook.

> Please note that this role will ensure that `firewalld` systemd service on your servers are started and enabled by default. If you want to stop and disable `firewalld` service, please modify below variable as false when running playbook:  
> ```yaml  
> firewalld_enabled: false

### Dependencies

None

### Additional Vserver Configuration

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

### Example Inventory File
```
[nginx]
nginxnode01.example.com
nginxnode02.example.com
nginxnode03.example.com
```

### Example Playbook File For Installation

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

You can also override default variables inside [vars/main.yml](vars/main.yml)*:
```yaml
version: 1.17.9
```

### Example Playbook File For `Ununinstallation`

```yaml
- hosts: all
  become: true
  roles:
    - role: bilalcaliskan.nginx
      vars:
        install_nginx: false
```

### License

MIT / BSD
