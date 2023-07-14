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
