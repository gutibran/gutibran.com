---
date: '2024-03-04T02:34:43-06:00'
title: 'How to Use Nginx to Serve Websites'
draft: true
tags: [nginx, web hosting]
description: "A simple guide to learn how to serve websites and website applications on a Debian based Linux server with NGINX."
toc: true
---

# Pre-requisites
A Linux server needs to be set up, running, and be accessible over the internet. I have written a blog post going over how to setup a VPS (virtual private server) from an arbitrary cloud provider which can be read [here](/blog/how-to-setup-a-vps). There are many resources on the internet to learn how to do this. Additionally, an SSH connection between you and the VPS needs to be established. I also have a blog post going over how to setup SSH between two hosts (computers) which can be read [here](blog/how-set-up-ssh-between-two-hosts).

One or more domain names need to be purchased from a domain registrar. I have also written a blog post going over how to purchase domain names from an arbitrary domain registrar which can be read [here](/blog/how-to-purchase-a-domain-name).

# Installation
Install NGINX. The configuration files will be located in */etc/nginx/*.

```bash
sudo apt install nginx -y
```

# Configuring UFW
Port 80 and 443 need to be open to allow clients to request for your website.

If you do not already have ufw installed run this command.
```bash
sudo apt install ufw -y
```

Run these commands to expose port 80 and 443, block any incoming traffic to the server unless there is a UFW rule set for it, enable and start the UFW service.
```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```

# Storing website on the server filesystem
NGINX looks for websites in */var/www/*. Store your website source code here.

# Configuring NGINX to serve a site
Create a server configuration file in */etc/nginx/sites-available/*. It can be named anything.

```nginx
server {
    listen 80;
    server_name <domain-name>;
    root /var/www/<domain-name>;
    index index.html;
    location / {
        try_files $uri $uri/ = 404;
    }
}
```

Create a symbolic link of this file to */etc/nginx/sites-enabled/*.

```bash
ln -s /etc/nginx/sites-available/<domain-name> /etc/nginx/sites-enabled/<domain-name>
```

Allow NGINX to check the configuration for errors.
```bash
sudo nginx -t
```

Enable and start the NGINX service.
```bash
sudo systemctl enable nginx
sudo systemctl start nginx
```

Whenever change is made run this command instead. Reloads the NGINX service.
```bash
sudo systemctl reload nginx
```

# Configuring HTTPS

# Configuring sub-domains