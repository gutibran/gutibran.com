---
date: '2024-02-27T23:32:48-06:00'
title: 'How to Use Nginx'
draft: true
tags: [nginx]
description: "A simple guide for using NGINX to host websites and web applications."
---

# NGINX
## Installation
Install NGINX. The configuration file will be located in */etc/nginx*.
```bash
sudo apt install nginx
```

## How to create a site
Create a directory to store the website. Websites are conventionally stored in */var/www/*. I store my websites in */home/username/* so I use symbolic links in */var/www* that point to those websites. I do this because it makes it easier to work (regards Linux users & permissions, have not learned about that yet) with especially for CI/CD with GitHub Actions. So in this essay I will show you how to do that. I have no idea if this is following best practices, conventions, etc. If it is wrong feel free to contact me so I can update this.

In this example website is our main website and subwebsite is our sub website that is associated with out sub-domain.
```bash
# move to the home directory
cd ~

# create directories to hold websites
mkdir websites
mkdir ~/websites/website.com
mkdir ~/websites/subwebsite.website.com

# create symbolic links in /var/www/ to point to our websites
ln -s /home/websites/website /var/www/website.com
ln -s /home/websites/subwebsite /var/www/subwebsite.com

# create a index.html files within respective website directories
touch ./website/index.html
touch ./subwebsite/index.html

# add some text to the HTML files within respective website directories
echo "website index page" >> ./website/index.html
echo "subwebsite index page" >> ./subwebsite/index.html
```

## How to configure NGINX to serve a site
The configuration files for NGINX are in */etc/nginx/*.
```bash
cd /etc/nginx/sites-available

# create sub
touch subwebsite
```

Paste this NGINX site configuration and paste it into */etc/nginx/sites-available/subwebsite*.
```nginx
server {
    listen 80;
    server_name subwebsite.website.com;
    root /var/www/subwebsite.website.com;
    index index.html;
    location / {
        try_files $uri $uri/ = 404;
    }
}
```

Paste this NGINX site configuration and paste it into */etc/nginx/sites-available/website*.
```nginx
server {
    listen 80;
    server_name website.com;
    root /var/www/website.com;
    index index.html;
    location / {
        try_files $uri $uri/ = 404;
    }
}
```

Create symbolic links to enable the sites.
Create symbolic link from */etc/nginx/sites-available/website* to */etc/nginx/sites-enabled/website*. 

Create symbolic link from */etc/nginx/sites-available/subwebsite* to */etc/nginx/sites-enabled/subwebsite*. 
```bash
ln -s /etc/nginx/sites-available/website /etc/nginx/sites-enabled/website
ln -s /etc/nginx/sites-available/subwebsite /etc/nginx/sites-enabled/subwebsite
```

Enable the NGINX service (starts on boot) and start the NGINX service.
```bash
# test to see if the nginx config is proper
sudo nginx -t

sudo systemctl enable nginx
sudo systemctl start nginx
```

## How to setup sub-domains

### Create CNAME records
1. log into domain registrar
2. edit the DNS records for owned domain name.
3. add CNAME record

- set the the type to ALIAS - CNAME
- set the host to be what you want the subdomain to be
- set the answer to be you domain name
- set the TTL to be 600
- leave the priority blank

### Edit NGINX configuration to handle the sub-domain
```bash
# coming soon
```

## How to set up HTTPS

## How to configure UFW (uncomplicated firewalls)

# Resources