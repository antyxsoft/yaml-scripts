# Install 3CX (ANSIBLE)
This guide describes how to deploy a 3CXv20 install in remote VM.

## Requirements
- A clean debian 12 VM with a static IP.
- Passed root ssh keys.
- Ansible 2.16.3


## Installing 3CX PBX.
1. Create a `hosts` file where you list the hosts you want to change. [instructions](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups)
2. Run the role. `ansible-playbook 3cx-install.yaml`
3. When the role is complete, you can access the web-ui via `<ip-of-vm>:5015/?v=2`
4. Have fun doing calls!
