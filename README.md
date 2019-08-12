[![Build Status](https://travis-ci.org/bihealth/ansible-role-provision-proxmox.svg?branch=master)](https://travis-ci.org/bihealth/ansible-role-provision-proxmox)

# Provisioning of Proxmox Virtual Machines/Containers

This role allows for the easy provisioning of Proxmox guest hosts.

## Requirements

- Remote proxmox host
- API user setup on proxmox host
- Python packages as described in [module documentation](https://docs.ansible.com/ansible/latest/modules/proxmox_module.html)
    - `proxmoxer`
    - `requests`

## Role Variables

See `defaults/main.yml` for all role variables and their documentation.

## Dependencies

none

## Example Playbook

```yaml
- name: provision container on proxmox host
  hosts: example_hosts
  connection: local
  roles:
    - bihealth.provision-proxmox
  vars:
    proxmox_api_user: ansible@pve
    proxmox_api_password: "{{ lookup('passwordstore', 'example-proxmox/password_ansible@pve') }}"
    proxmox_vmid: "101"
    proxmox_type: container
    proxmox_host: proxmox.example.com
    proxmox_ostemplate: "local:vztmpl/centos-7-default_20171212_amd64.tar.xz"
    proxmox_memory: 32384
    proxmox_disk: "245"
    proxmox_cores: 8
    proxmox_cpus: 4
    proxmox_ip: "{{ lookup('dig', inventory_hostname) }}"
    proxmox_hostname: "{{ inventory_hostname }}"
    proxmox_nested_container: true
  tags:
    - create-container
```

## Open Issues

- Deployment of virtual machines.
- Testing.

## License

MIT

## Author Information

- Manuel Holtgrewe

Created with love at [Core Unit Bioinformatics (CUBI), Berlin Institute of Health (BIH)](https://www.cubi.bihealth.org).
