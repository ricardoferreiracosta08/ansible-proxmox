# ansible-proxmox

**About:** this repo is a forked and you can run it to manage instances on Proxmox Cluster:

- create VM instance from the storage that stores the iso file
- create Container LXC from the template downloaded previously
- run task "install package" on container LXC created

On Proxmox, to list sotarege content

```bash
pvesm list STORAGE-NAME
```

# Step-by-step

1 - Clone this repository

2 - On Proxmox, create role Admin for new user

```bash
pveum useradd ansible@pve -comment "Ansible user"
pveum passwd ansible@pve
pveum aclmod / -user ansible@pve -role PVEAdmin (ROLE ADMIN)
```

3 - On Ansible Server, install the requirements to Proxmox API, create role proxmox and send files for there

```bash
pip3 install proxmoxer
pip3 instlal requests
```

```bash
mkdir -p /etc/ansible/roles/proxmox
cp -r roles/proxmox/* /etc/ansible/roles/proxmox
```

4 - The end, adjust your inventory and run the playbook

```bash
ansible-playbook -i inventory play.yml
```

In other hand, to run task "install package" on container created:

1 - Create new role

```bash
cp -r roles/dhcp/* /etc/ansible/roles/bind_dhcp
```

2 - Add IP container on Inventory file and run playbook

```bash
echo -e "[container]\n172.18.60.140" >> inventory
ansible-playbook -i inventory play.yml
``` 

# NOTES

- Change the vars on defaults/main.yml according to your environment 
- Dont forget to change the var {{ proxmox_type }} to either container or kvm
- My changes are present on branch main
