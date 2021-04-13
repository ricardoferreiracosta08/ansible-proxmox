# ansible-proxmox

**About:** this repo is a forked and you can run on Proxmox Cluster:

- create VM instance from the storage that stores the iso file
- create Container LXC from the template downloaded previously

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
cp -r handlers/ tasks/ defaults/ /etc/ansible/roles/proxmox/
```

4 - The end, adjust your inventory and run the playbook

```bash
ansible-playbook -i inventory play.yml
```

# NOTES

- Change the vars on defaults/main.yml according to your environment 
- dont forget to change the var {{ proxmox_type }} to either container or kvm
