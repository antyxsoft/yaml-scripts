# Install 3CX (ANSIBLE)
This guide describes how to deploy a 3CXv20 install in remote VM.

## Requirements
- A clean debian 12 VM with a static IP.
- Passed root ssh keys.
- Ansible 2.16.3


## Installing 3CX PBX.
1. Run the role. `ansible-playbook 3cx-install.yaml`
2. When the role is complete, you can access the web-ui via `<ip-of-vm>:5015/?v=2`
3. Have fun doing calls!
