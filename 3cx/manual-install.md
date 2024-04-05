# 3CX installation in a clean Debian 10 VM

## Requirements
- A clean debian 10 VM with a static IP
- Passed root ssh keys
- Have a managable DNS server and configure split DNS to ensure that your 3CX FQDN resolves to the 3CX host machine's IP on your LAN ans from the internet to your public IP. [How to create FQDN using split DNS](https://www.3cx.com/docs/creating-fqdn-split-dns/)
- When installing on premise, you must have a proper firewall on which you are able to configure the ports correctly for VoIP to pass. [Firewall & Router Configuration Guide](https://www.3cx.com/docs/manual/firewall-router-configuration/)

## Installation
***After installing, updating and upgrading the Debian VM***

1. Install gnupg: `apt install gnupg`

2. Get the 3CX public key and add it to your keyring.

		wget -O- http://downloads-global.3cx.com/downloads/3cxpbx/public.key | apt-key add -

3. Add the 3CX repo.

		echo "deb http://downloads-global.3cx.com/downloads/debian buster main" | tee /etc/apt/sources.list.d/3cxpbc.list

4. Update the repositories: `apt update`
5. Install required tools for 3CX install.

		apt install net-tools dphys-swapfile htop mtr screen curl dnsutils -y

6. Now the system is ready to install 3CX! `apt install 3cxpbx -y`
