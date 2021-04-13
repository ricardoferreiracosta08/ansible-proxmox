# ansible-proxmox

1 - Clone this repository
2 - On Proxmox, create role Admin for new user

pveum useradd ansible@pve -comment "Ansible user"
pveum passwd ansible@pve
pveum aclmod / -user ansible@pve -role PVEAdmin (ROLE ADMIN)

3 - 

