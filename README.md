# rathole-gateway-setup
An Ansible Playbook to deploy [rathole](https://github.com/rapiz1/rathole) easily for my usecase.
This repository is deriverd from [cWatto/gateway](https://github.com/cWatto/gateway). Thanks for great efforts!!

### Commands

Install depenencies
```
$ ansible-galaxy role install artis3n.tailscale
```

Deploy
```bash 
$ ansible-playbook playbook.yml -i inventory.ini --ask-become-pass --ask-vault-pass -e tailscale_authkey=<tailscale authkey>
```

Deploy only Client or Server

```bash 
$ ansible-playbook playbook.yml -i inventory.ini -l client --ask-become-pass --ask-vault-pass -e tailscale_authkey=<tailscale authkey>
# or 
$ ansible-playbook playbook.yml -i inventory.ini -l server --ask-become-pass --ask-vault-pass -e tailscale_authkey=<tailscale authkey>
```

Check inventory.ini
```bash
$ ansible-vault view inventory.ini
```

