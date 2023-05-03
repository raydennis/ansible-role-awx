# Ansible role to install AWX on k3s

Taken heavily from https://computingforgeeks.com/install-and-configure-ansible-awx-on-centos/

## Example Inventory (at ./inv/hosts.ini)

```ini
[master]
master1

[master:vars]
ansible_user=root
```

## Example playbook

```yaml
---

- hosts: master
  become: yes
  roles:
    - role: ansible-role-awx/master

```

## Login

When this playbook is run, it will add an AWX web interface on <host>:30080

Navigate to: 
http://your-server-ip-address:30080

The login username is admin

Obtain admin user password by decoding the secret with the password value:

```bash
kubectl -n awx get secret awx-admin-password -o go-template='{{range $k,$v := .data}}{{printf "%s: " $k}}{{if not $v}}{{$v}}{{else}}{{$v | base64decode}}{{end}}{{"\n"}}{{end}}'
```
