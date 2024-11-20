# Ansible Role: Create VM with QEMU-KVM (libvirt)

This Ansible role automates the process of creating a virtual machine (VM) using QEMU-KVM and libvirt. It installs the necessary virtualization packages, manages storage pools and volumes, and spins up a new VM on the specified KVM host.

## Requirements
----------------

- Ansible 2.9+
- The community.libvirt and community.general collections (can be installed with ansible-galaxy):
```ansible-galaxy collection install community.libvirt community.general```
- A host with QEMU-KVM and libvirt installed. The host should also have SSH access and be listed in the inventory file.
- Libvirt running on the KVM host with network configuration ready (e.g., default network for VMs).

## Role Variables
----------------

Variables can be configured in defaults/main.yml or passed during runtime. Here are the important ones:

| Variable	| Description	Default Value |
| vm_name	| The name of the virtual machine	myvm | 
| vm_memory	| Amount of memory (in MB) for the VM	2048 |
| vm_vcpus	| Number of virtual CPUs for the VM	2 |
| vm_disk_size	| Disk size for the VM in GB	10G | 
| iso_path	| Path to the ISO file for VM installation	/var/lib/libvirt/boot/ubuntu.iso |

## Dependencies
----------------

This role depends on the following Ansible collections:

- community.libvirt for interacting with libvirt.
- community.general for additional utilities.

## Example Playbook
----------------

### Setup the Inventory
Define your KVM host in an inventory file. Here's an example inventory file:

```
[libvirt_hosts]
kvm_host ansible_host=192.168.122.1 ansible_user=root ansible_python_interpreter=/usr/bin/python3
```

### Define the Playbook
Create a playbook that includes the role. Here's an example playbook.yml:

```
---
- hosts: libvirt_hosts
  become: true
  roles:
    - create_vm
```

### Run the Playbook
Run the Ansible playbook to create and start the virtual machine:

```
ansible-playbook -i inventory playbook.yml
```

## License
-------

This project is licensed under the MIT License.

## Author Information
------------------
