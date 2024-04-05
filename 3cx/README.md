# Install 3CX (ANSIBLE)
This guide describes how to use the roles on Windows Subsystem for Linux (WSL) for remote installs and locally on a Debian 10 vm.

## Requirements
- A clean debian 10 VM with a static IP
- Passed root ssh keys
- Ansible 2.16.3
- (requirements for ansible)
 
## Installing on remote VM using Debian ([WSL](https://learn.microsoft.com/en-us/windows/wsl/install)).
1. Install [pipx](https://github.com/pypa/pipx): `apt install pipx -y`
2. Install ansible 2.16.3: `pipx install ansible==1.16.3`
3. Download the [git repo](https://github.com/antyxsoft/yaml-scripts/tree/main).
4. Navigate to `yaml-scripts/3cx`.
5. Run `ansible-plabook 3cx-install.yaml` 
6. Once the role is finished running login to the can remote host and you can install [3cxpbx](https://www.3cx.com/pbx/hosted/) with `apt install 3cxpbx -y` or the [3cxsbc](https://www.3cx.com/docs/3cx-tunnel-session-border-controller/#h.cpwvn0i4qyw8) with `apt install 3cxsbc -y`

## Installing locally on Debian 10.
1. Update the repositories: `apt update`.
2. Install pip: `apt install python3-pip`.
3. Install ansible with pip: `python3 -m pip install ansible-core`.
4. Download the [git repo](https://github.com/antyxsoft/yaml-scripts/tree/main).
5. Navigate to `yaml-scripts/3cx`.
6. Run `ansible-plabook 3cx-install.yaml --connection=local`.
7. Once the role is finished running you can choose to install [3cxpbx](https://www.3cx.com/pbx/hosted/) `apt install 3cxpbx -y` or the [3cxsbc](https://www.3cx.com/docs/3cx-tunnel-session-border-controller/#h.cpwvn0i4qyw8) `apt install 3cxsbc -y`.

## Installing 3CX PBX.
1. After the role is complete run: `apt install 3cxpbx -y`
2. Wait for the install. When done accept the licence and select the 1st option.
3. In a browser access the web-ui via `<ip-of-vm>:5015/?v=2`

## Creating a Debian VM in virtual box
If you want to try the roles on a local VM using the Debian (WSL) method you'll need to have the local VM be on the same network with the host. This can be done by following these steps:

1. Download the [debian 10 ISO](https://cdimage.debian.org/cdimage/archive/10.13.0/amd64/iso-cd/debian-10.13.0-amd64-netinst.iso).
2. Attach the network adapter to **"Bridged Adapter"** and select the physical network card on the machine.
3. Run the VM and install the Debian Distro.
4. Add your ssh pubkey in the root.
5. Run `ip a` to check the ip of the machine.

---

### Improvements
**Is there a way to install the 3cxpbx package without the need to accept the licence?**

The window is created using `dialog` is there a way to automaticaly accept?

After accepting the licence:
1. it updates the certificates (/etc/ca-certificates/update.d...)
2. Runs hooks in /etc/ca-certificates/update.d...
3. Shows the welcome message with 2 options. Run the tool using the web browser or from the CLI
4. When selecting Option 1 it gives this output:

		Setting up nginx
		Prossesing triggers for systemd
		Prossesing triggers for man-db
		Prossesing triggers for libc-bin
