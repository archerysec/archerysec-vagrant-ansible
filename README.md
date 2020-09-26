# Ansible Vagrant profile ArcherySec

Vagrant and VirtualBox can be used to quickly build or rebuild virtual servers.

This example installs Ansible's ArcherySec Project on a Ubuntu VM, so you can test and run ArcherySec.

## Prerequisite

- VirtualBox
- Vagrant
- Ansible

## Getting Started

```bash
git clone https://github.com/archerysec/archerysec-vagrant-ansible.git
cd archerysec-vagrant-ansible
vagrant up 
```

After that is configured, you could visit http://archerysec.local/ in a browser, and you'll see the ArcherySec login page. Log in with the default credentials:

- Username: admin
- Password: test@123A