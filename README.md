# Ansible-IOS-Labs

Ansible Code Snippets for IOS

## Lab Description

These Ansible code snippets are meant as lab examples using Cisco based equipmet, and not **&  AND NOT** - for use in productions. 

[Watch this live stream setup](https://www.youtube.com/live/t3Zvs24ciQo)

## Installation

Requires Python 2.6 or higher, and Ansible
Installing Ansible on Ubuntu:
- Use as an example of how to install Ansible on Ubuntu 
- Reference Ansible Doc's for other installation methods: ```https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu```

```bash
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible
```

## Configuration

- Example ansible.conf file
- Use these configs as a starting point to help you troubleshoot
- Reference Ansible Doc's Network Troubleshooting for more info: ```https://docs.ansible.com/ansible/latest/network/user_guide/network_debug_troubleshooting.html#error-authentication-failed```

## Add these to your ssh_config file located ```~/etc/ansible/ansible.conf```:

```bash
# Error: “Authentication failed”
[paramiko_connection]
look_for_keys = False

# Error: “connecting to host <hostname> returned an error” or “Bad address”
[paramiko_connection]
host_key_auto_add = True

# Timeout issues
[persistent_connection]
connect_timeout = 60

# Command timeout
[persistent_connection]
command_timeout = 60
```

## Use this to help you troubleshoot ssh connections issues

- Common issue occurs with the Diffie–Hellman key exchange
- View the wiki: ```https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange```
- Also reference Cicso Community Security Doc's for more infomation on issue and how to resolve: ```https://community.cisco.com/t5/security-documents/guide-to-better-ssh-security/ta-p/3133344```

## Add these to your ssh_config file located ```~/etc/ssh/ssh_config```:

```bash
KexAlgorithms=curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc
```

## Example hosts file ```host.conf```:

```bash
192.168.1.1 ansible_connection=local ansible_user=admin ansible_password=cisco
192.168.1.2 ansible_connection=local ansible_user=admin ansible_password=cisco
192.168.1.3 ansible_connection=local ansible_user=admin ansible_password=cisco

[R1]
192.168.1.1

[R2]
192.168.1.2

[SW1]
192.168.1.3

[routers]
192.168.1.1
192.168.1.2

[switches]
192.168.1.3

[all]
192.168.1.1
192.168.1.2
192.168.1.3
```

## DevNet Sandbox

A great way to learn more, check out: [DevNet Sandbox](https://developer.cisco.com/site/sandbox/)
