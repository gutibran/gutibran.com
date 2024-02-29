---
date: '2024-02-28T19:32:14-06:00'
title: 'Nginx Guide'
draft: true
tags: [nginx, web hosting]
description: "A simple guide for using NGINX."
---

# NGINX GUIDE
There is a peertube video going over this in a live example if you prefer to watch instead of read.

## How to serve a website

## How to setup sub-domains

## How to setup HTTPS
Install certbot.
```bash
sudo apt install certbot
```

After properly configuring sites to serve with NGINX. Run certbot to create HTTPS certificates for that site.
```bash
sudo certbot --nginx
```

## Create an unprivileged user
```bash
sudo adduser <username>
sudo usermod -a -G sudo <username>
sudo reboot now
```

## Setup automatic upgrades
This package will update and upgrade server software automatically.
```bash
sudo apt install unattended-upgrades -y
dpkg-reconfigure --priority=low unattended-upgrades
```

## How to setup SSH connection between two hosts
After configuring and or installing a Linux distribution on a server you need a way to remotely connect to it. This is done through ssh. You need to create a key-pair that consists of a public and private key. Then upload the public key to the server. Lastly secure the ssh configuration by only allowing users to log in if they have an authorized public key.

### Create a key-pair (public/private key) on client host
```bash
ssh-keygen -t rsa -b 4096
```

### Copy the public key on the client host to the server host
The <code>-i</code> is implicitly set to <code>~/.ssh/id_rsa.pub</code>. If you have your key-pair is stored elsewhere set this flag to that path. After running this command a prompt will appear for a password for the corresponding user you have provided. Also a prompt to fingerprint this remote host onto your client. Enter the password and enter yes.
```bash
ssh-copy-id -p <port-number> <username>@<ip-address>
```

### Map the IP address to an alias in the */etc/hosts* file
This is just for ease of use so you don't have to memorize or type the IP address of your server. It will get annoying after a while.
```bash
sudo echo "<ip-address> <alias-name>" >> /etc/hosts
```

### Login into the server
After uploading your public key to the server you should be able to login to the server without being prompted for the password. Test this out. Ensure this works properly before moving forward.
```bash
ssh <username>@<alias-name>
```

### Edit the ssh configuration file in /etc/ssh/sshd_config to harden ssh
To be clear this is not a complete hardening guide this is just basic hardening for ssh. I suggest opening up two sessions just in case you mess up on the configuration. One to test if you can properly log back in to the server after editing the configuration files. It is possible to lock yourself out your server which will cause you to repeat all these steps over from the beginning and reset and or re-install your server. Telling you this now because I have done this before and it is very frustrating. 

Remove the default file in */etc/sshd_config.d/50-cloud-init.conf* and create a new config in */etc/sshd_config.d/*. In this example I am going to name the configuration file *99-my-settings.conf*. You can name it whatever you like.

```bash
sudo vim /etc/ssh/sshd_config.d/99-my-settings.conf
```


Here are the configuration settings that I have included in */etc/ssh/sshd_config.d/99-my-settings.conf*.
- PermitRootLogin no
- PasswordAuthentication no
- AllowUsers \<username>
- ClientAliveInterval 300
- ClientAliveCountMax 2 
- Port \<some random number>
- IgnoreRhosts
- PermitEmptyPasswords no
- UseDNS no
- LogLevel VERBOSE
- AllowTCPForwarding no
- X11Forwarding no

After saving your configuration reload the sshd service with systemctl. You have properly configured ssh between two remote hosts.
```bash
sudo systemctl reload sshd
```

### Setup UFW (uncomplicated firewall)
Install *ufw*.
```bash
sudo apt install ufw
```

Setup ufw rules. Add rules for any port you want to expose to the internet. Protocols that we are using are ssh, http, https which correspond to the tcp ports 22, 80, and 443 respectively. If you set up ssh to use a different port other than the default use that number instead of 22 in the rules down below.
```bash
sudo ufw limit 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```

### Setup Fail2Ban
Install fail2ban.
```bash
sudo apt install fail2ban
```

Edit the configuration file in */etc/fail2ban/jail.local* to add configuration for ssh. Add these settings to throw attackers that brute-force ssh port into jail effectively banning that IP from the server.
```bash
[DEFAULT]
ignoreip = 127.0.0.1/8 ::1
bantime = 3600
findtime = 600
maxretry = 5

[sshd]
enabled = true
```

Enable the fail2ban service on boot, start the service, and check if the fail2ban service is running properly.
```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
sudo systemctl status fail2ban
```

## How to setup CI/CD with Github Actions, Rsync, and SSH

## Server configuration optimizations

# Resources