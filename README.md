# pxe-boot-provsion
Use Ansible provision pxe boot service

## Purpose
This repository is dedicated to provisioning PXE boot and Nginx server. It includes DHCP, TFTP, and Nginx server, and it can provision OS settings using YAML configuration.

## How to use
Prerequsite:
1. Install Ansible, NFS.
1. Clone this repository.
3. Prepare ISO and bootloader file then place them on the NFS server. Ensure folder sturcture follows the exmaple provided in documentation. 
[How to download files](https://hackmd.io/@LJlHdtK5RuqEvb56diBuvw/ryMiKYXUlx).

exmaple:

```
├── iso
│   └── ubuntu-22.04.5-live-server-amd64.iso
└── tftp
    ├── bios
    │   ├── initrd
    │   ├── ldlinux.c32
    │   ├── libcom32.c32
    │   ├── libutil.c32
    │   ├── menu.c32
    │   ├── pxelinux.0
    │   ├── vesamenu.c32
    │   └── vmlinuz
    └── efi
        ├── bootx64.efi
        ├── grubx64.efi
        ├── initrd
        └── vmlinuz
```
## How to Deploy
1. Run the following command to copy your SSH key to the target host:
`ssh-copy-id <host-user>@<host-ip>`
1. Modify the inventory file to set the [pxe-server] host's IP address and user.
Set the parameters for cloud-init, host MAC address, host type, etc., in roles/nginx/vars/main.yaml.
1. Set the parameters for DHCP, TFTP, and NFS mount information in roles/inventory/vars/main.yaml.
1. Run the Ansible playbook to provision the PXE boot setup:
`ansible-playbook -i inventory provision.yaml`
