
# Gateway
An Ansible Playbook to deploy [rathole](https://github.com/rapiz1/rathole), [Caddy](https://caddyserver.com/), and [fail2ban](https://github.com/fail2ban/fail2ban) to a remote server exposed to the internet and a client with Wireguard on the local network, designed to replace CloudFlare Tunnels.

Expose services hosted locally via the external server IP, securly VPN into your local network with the included Wireguard server.

## Currently Implemented
- [x] Client
    - [x] Install and configure rathole 
    - [x] Install and configure Wireguard
    - [x] Apply config changes on subsequent deploys
    - [ ] Flags to force re-install, do updates, etc
    - [ ] Provide backup functionality and copy the backup to the controller
    - [ ] Specify rathole version for client-side installation
- [x] Server
    - [x] Install and configure rathole
    - [ ] Install and configure Caddy
    - [ ] Install and configure fail2ban
    - [ ] Apply config changes on subequent deploys (rathole supported)
    - [ ] Flags to force re-install, do updates, etc
    - [ ] Specify rathole version for server-side installation

## Get started
```bash
    sudo apt-get install ansible-core
    git clone https://github.com/cWatto/gateway
    cd gateway

    # Make a live copy from the example config files
    cp rathole/files/client.toml.example rathole/files/client.toml
    cp rathole/files/server.toml.example rathole/files/server.toml
    cp wireguard/files/wireguard.conf.example wireguard/files/wireguard.conf
```

### Inventory.ini
Modify the inventory.ini to point to your `client` and `server`, ensure that the remote devices have a copy of your ssh keys stored in `authorized_keys`, more info [here](https://www.ssh.com/academy/ssh/copy-id).
### Rathole
Modify `client.toml` and `server.toml` in the rathole/files directory as required. See [rathole](https://github.com/rapiz1/rathole/tree/main) documentation for more info

### Wireguard
> [!TIP]
> If you're not sure what changes you need to make to `wireguard.conf`, you can install PiVPN [manually](https://docs.pivpn.io/install/) via the GUI and copy the resulting file from `/etc/pivpn/wireguard/setupVars.conf` to `wireguard.conf` then run the playbook, Ansible will skip the install as it's already installed but will use the file in future deployments.

Modify `wireguard.conf` in the wireguard/files directory as required. See [PiVPN](https://docs.pivpn.io/guides/user-data/) documetation for more info.
**Note**: gateway only supports Wireguard installation **currently**. You can comment out the `wireguard` play in `playbook.yml` and install it manually if you require OpenVPN. 



### Commands
Deploy
```bash 
ansible-playbook playbook.yml -i inventory.ini all
```

Deploy only Client or Server

```bash 
ansible-playbook playbook.yml -i inventory.ini -l client 
# or 
ansible-playbook playbook.yml -i inventory.ini -l server 
```

You're done! Now just setup any services, and a WireGuard profile via PiVPN on the client, and setup on your device.

## Customization
Modify `playbook.yml` to remove certain features or add your own!

### Example
Disable WireGuard and add custom functionality
```diff
  - hosts: client
    become: true
    roles:
      - common
      - rathole
+     # - wireguard
+     - mycustomrole
```