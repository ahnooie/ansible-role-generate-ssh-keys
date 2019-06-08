Generate SSH Keys Ansible Role
=========

This Ansible role generates a unique public/private ssh keypair for each host (ssh client), and then copies the public key to an ssh server.  This allows for quickly setting up ssh access to 1 server from many hosts in Ansible's inventory.

This would be useful when setting up ssh access for restic or borgbackup where you would need to setup many ssh clients with access to ssh into one target server.

Requirements
------------

The SSH service should be enabled on server

Role Variables
--------------

Required:
```
generate_ssh_keys_target_server: (required)
```

Optional (default values)
```
generate_ssh_keys_server_user: "root" (user ssh client will be logging in as on server)
generate_ssh_keys_client_user: "root" (user to setup keys on ssh client)
generate_ssh_keys_key_type: "ed25519" (can also choose rsa)
generate_ssh_keys_key_bits: 4096 (ignored for ed25519, but will be used for rsa key type)
generate_ssh_keys_key_state: "present"
```


Dependencies
------------

None

Example Playbook
----------------

generate-ssh-keys.yml
```
---
- hosts: clients
  roles:
    - role: ahnooie.generate-ssh-keys
      vars:
        generate_ssh_keys_target_server: "backups.example.com"
```
inventory
```
[clients]
host1.example.com
host2.example.com
host3.example.com
...
```

License
-------

MIT

Author Information
------------------

Created by [Benjamin Bryan](https://b3n.org)
