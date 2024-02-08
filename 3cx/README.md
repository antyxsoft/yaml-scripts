# Install 3CX (ANSIBLE)

## Requirements
- A clean debian 10 VM with a static IP
- Passed root ssh keys
- Ansible 2.16
- Have a managable DNS server and configure split DNS to ensure that your 3CX FQDN resolves to the 3CX host machine's IP on your LAN ans from the internet to your public IP. [How to create FQDN using split DNS](https://www.3cx.com/docs/creating-fqdn-split-dns/)
- When installing on premise, you must have a proper firewall on which you are able to configure the ports correctly for VoIP to pass. [Firewall & Router Configuration Guide](https://www.3cx.com/docs/manual/firewall-router-configuration/)

## Install Ansible in Debian (WSL)
1. Install pipx
> apt install pipx
2. Install ansible 2.16
> pipx install ansible==1.16.3

## Create a Debian VM in virtual box
1. Download the [debian 10 ISO](https://cdimage.debian.org/cdimage/archive/10.13.0/amd64/iso-cd/debian-10.13.0-amd64-netinst.iso)
2. Attach the network adapter to **"Bridged Adapter"** and select the physical network card on the machine.
3. Run the VM and install the Debian Distro.
4. Add your ssh pubkey in the root.
5. Run `ip a` to check the ip of the machine.

## Running the Ansible roles
1. Download the [git repo]()
2. Inside the `hosts` file add the ip of the VM
3. Run `ansible-plabook 3cx-install.yaml`
4. Login the VM and run `apt install 3cxpbx -y`
5. Wait for the install. When done accept the licence and select the 1st option.
6. In a browser access the web-ui via `<ip-of-vm>:5015/?v=2`

---

### Improvements
**No need to run the debian installer.**
Find a way to spawn a VM without the need to manualy configure the distro. qcow images?

**Setting a static ip before install.**
Can oVirt set the private ip if the vm before install?
Else i can do it with ansible.

**Is there a way to install the 3cxpbx package without the need to accept the licence?**
The window is created using `dialog` is there a way to automaticaly accept?
After accepting the licence:
1. it updates the certificates (/etc/ca-certificates/update.d...)
2. Runs hooks in /etc/ca-certificates/update.d...
3. Shows the welcome message with 2 options. Run the tool using the web browser or from the CLI
4. When selecting Option 1 it gives this output:
> Setting up nginx
> Prossesing triggers for systemd
> Prossesing triggers for man-db
> Prossesing triggers for libc-bin