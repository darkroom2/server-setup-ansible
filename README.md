# server-setup-ansible

Ansible Playbook for the initial setup of the remote server.

Each installed/deployed project is defined as a role in `roles/` directory.

## Requirements

- Ansible 7.6.x on control node
- ssh access to target nodes
- sudo access on target nodes
- python3 on target nodes

## Usage

1. Define target nodes (hosts) in `inventory.ini` file.
2. Change `hosts` variable in `playbook.yml` file to match your target nodes.
3. Adjust `roles` variable in `playbook.yml` file to match your roles.
4. Run `ansible-playbook playbook.yml --ask-become-pass` to run the playbook.

## Debugging

Run `ansible-playbook -i localhost, -c local playbook.yml --ask-become-pass` to run the playbook locally.

## Example

Requirements:

- 4x CPU, 8GB RAM, 2x 128GB SSD

Steps:

1. Install Ubuntu Server 22.04 LTS with default settings (adjust the LVM on a single disk to use whole free space).
2. Extend the LVM to use the whole second disk space:
    ```shell
    sudo pvcreate /dev/sdb
    sudo vgextend ubuntu-vg /dev/sdb
    sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
    sudo resize2fs /dev/ubuntu-vg/ubuntu-lv
    sudo reboot
    ```
3. Update the system and reboot:
    ```shell
    sudo apt update && sudo apt full-upgrade && sudo apt autoremove && sudo apt autoclean
    sudo update-grub
    sudo reboot
    ```
4. Run the playbook on the control node:
    ```shell
    ansible-playbook playbook.yml --ask-become-pass
    ```

## TODO

- make role for updating system
- make role for extending LVM
- make role for installing zsh
