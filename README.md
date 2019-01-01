# Binal

This repository contains a playbook for provisioning modern hosting environments
geared towards WordPress.

The following is handled out of the box:

* User setup
* SSH hardening
* Firewall setup

It will also install the following software:

* Nginx with HTTP/2
* PHP 7
* MariaDB
* Redis
* WP-CLI
* Fail2Ban
* Git

## Usage

Install ansible: `sudo apt install ansible`.

Configure your `hosts` file, then edit `provision.yml` to configure your default user,
hashed sudo password and local public key path. This will create a new user on the
provisioned servers that you can use to gain SSH access.

To generate hashed password you can read [this documentation][hashed].

Please run commands as non-root user!

### Ping and send test command:

```bash
ansible testing -m ping
ansible testing -a "free -m"
ansible testing -a "ls -lha /home"
ansible testing -a "ping -c3 1.1.1.1"
```

### Finally, run:

`ansible-playbook provision.yml`

### Fixing ssh problem

```bash
mkdir -p ~/.ssh ; chmod 700 $_
touch ~/.ssh/id_rsa.pub ; chmod 700 $_
touch ~/.ssh/id_rsa ; chmod 600 $_
```

### Passphrase protected key

```bash
eval "$(ssh-agent -s)" ; ssh-add ~/.ssh/id_rsa
```

[hashed]:http://docs.ansible.com/ansible/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module