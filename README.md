
An Ansible Playbook to deploy rathole, caddy, and fail2ban to a remote server and a rathole client with a WireGuard connection to replace CloudFlare Tunnels.



## Get started
```bash
    git clone https://github.com/cWatto/gateway
    cd gateway
    # Copy client.toml config
    cp ./rathole-client/tasks/
```
- Rename `server.toml.example` to `server.toml` and `client.toml.example` to `server.toml` in the `rathole-[client/server]/tasks/files/` respectively
- Modify both files to your needs, see [rathole](https://github.com/rapiz1/rathole/tree/main) for more info.
- Copy the SSH key of computer you are deploying from to the `authorized_keys` file of the remote server, [guide here](https://www.ssh.com/academy/ssh/copy-id).
- Modify `inventory.ini` to point to your server/client IP
- Done!



```bash 
ansible-playbook playbook.yml -i inventory.ini all
```

```bash 
ansible-playbook playbook.yml -i inventory.ini -l client --tag "copy-config"
```
