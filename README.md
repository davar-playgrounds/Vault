## Overview

- In this demonstration, a Vault server is created using Vagrant, with Consul as the backend
- Provisioning is achieved using Ansible roles for both Vault and Consul

### Setup

1. Install Hashicorp Vagrant and in the selected project directory run
```
vagrant init
```

Replace the vagrant file with the one from this repo, and include all other files.

2. Setup Vault access

Setup your hosts file
```
echo "<vault_IP_Address> vault_server" >> /etc/hosts
```
The vault IP address is defined in dev_vault/json/vconfig.json

Create the following environment variable
```
export VAULT_ADDR='http://<vault_server>:8200'
```

### Running Vault

1. Vagrant automates the whole process therefore we simply run
```
vagrant up
```

### Setup Vault

1. Initialize Vault

Initialize Vault with the following command
```
vault operator init -key-shares=5 -key-threshold=3
```

You can store the root token as an Environment variable
```
export VAULT_ROOT_TOKEN_ID="xxxxxxxxxxxxxxxx"
```

Remember to take note of all keys

2. Unseal the vault

Using the keys obtained from the init phase, unseal the vault using the command:
```
vault operator unseal
```

3. Authenticate

Login to vault using
```
vault login “root_token_here”
```



#### License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
