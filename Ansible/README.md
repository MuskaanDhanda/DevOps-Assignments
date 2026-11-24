# Ansible: Apache Web Server Setup

Installs and starts Apache on a group of web servers and deploys a web page, using an Ansible playbook run from a control node.

Based on the October 2026 batch course material.

## Files

| File | Purpose |
|------|---------|
| [ansible.cfg](ansible.cfg) | Ansible settings: inventory path, `ubuntu` remote user, host key checking off, sudo privilege escalation, 5 parallel forks |
| [hosts](hosts) | Inventory with `webservers` and `dbservers` groups |
| [playbook.yaml](playbook.yaml) | Installs Apache, starts and enables the service, copies `index.html` to the web root |

## How to run

1. On the control node, copy `ansible.cfg` and `hosts` to `/etc/ansible/`.
2. In `hosts`, replace `10.1.1.1` with your web server's private IP and point `ansible_ssh_private_key_file` to your `.pem` key.
3. Put the page you want to serve at `/etc/ansible/index.html`.
4. Check connectivity, then run the playbook:

```bash
ansible all -m ping
ansible-playbook playbook.yaml
```

5. Open `http://<web-server-public-ip>` in a browser to see the page.
