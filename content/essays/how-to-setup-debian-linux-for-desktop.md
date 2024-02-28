---
date: '2024-02-24T02:50:20-06:00'
title: 'How to Setup Debian Linux for Desktop'
draft: true
tags: [linux, operating systems]
description: "A guide to install and setup Debian Linux on the desktop."
---

# debian
How I set up Debian 12 "Bookworm" on desktop.

This sets up bash aliases, adds self to sudoers group, and updates and upgrades apt packages.
```bash
# create ~/.bash_aliases and add some aliases
touch ~/.bash_aliases
export VISUAL=vim # set the default text editor
export EDITOR=vim; # set the default text editor
alias vim=nvim # set vim alias to neovim
alias vi=nvim # set vi alias to neovim

# set an alias to update apt packages and flatpaks
alias update-system="sudo apt-get update -y && sudo apt-get upgrade -y; flatpak update; sudo apt-get dist-upgrade; sudo apt autoremove -y;"

su # switch to root user
# add self to sudoers group
sudo usermod -a -G sudo bran

# upsudo date and upgrade apt packages
sudo apt-get update -y && sudo apt-get upgrade -y

# reboot the system
sudo reboot
```

This is how I installed nvidia drivers. [Here is the Debian documentation](https://wiki.debian.org/NvidiaGraphicsDrivers).
```bash
# add the contrib, non-free, and non-free-firmware components to /etc/apt/sources.list
sudo vim /etc/apt/sources.list

# update the list of available packages
sudo apt-get update

# install the nvidia driver and the required firmware
sudo apt-get install nvidia-driver firmware-misc-nonfree

# reboot the system
sudo reboot
```

This is how to setup GRUB to locate Windows installed on another drive.
```bash
# edit the grub configuration and un-comment the line with GRUB_DISABLE_OS_PROBER=false
sudo vim /etc/default/grub

# allow grub to discover other OS's installed
sudo os-prober 

# update the grub configuration
sudo update-grub
```

This is how I set up flatpaks. [Here are the commands to set up flatpak on Debian](https://flatpak.org/setup/Debian).
```bash
# install flatpak
sudo apt-get install flatpak

# something for KDE Plasma
apt install plasma-discover-backend-flatpak

# add flathub repository
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo 

# reboot the system
sudo reboot
```

Browse through the [KDE Plasma themes "store"](https://store.kde.org) to find themes. I have not learned to "rice" or create my own themes yet.  


Install pyenv to manage different versions of Python. Here is [the dependencies required to install python and pyenv](https://github.com/pyenv/pyenv/wiki#suggested-build-environment).
```bash
# install python build dependencies
sudo apt update; sudo apt install build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# run the automatic installer
curl https://pyenv.run | bash

# add commands to ~/.bashrc (interactive shells)
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

# add commands to ~/.profile (login shells)
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc

# source ~/.bashrc for the commands to take effect within the current session
source ~/.bashrc

# update pyenv installation list
pyenv install --update

# install the latest version of python as of the time of this writing
pyenv install 3.12.1

# set the global version of python
# this reads and writes ~/.python-version to determine which version of python to use
pyenv global 3.12.1

# set the local version of python
# this reads and writes the ./.python-version to determinw which version of python to use within the current directory
# the value of ./.python-version takes precedence over the gloabl version that is set
pyenv local 3.12.1

# set the shell version of python
# this sets PYENV_VERSION environment variable for the shell
# this will be temporary and work for the current session because the value is not persisted
pyenv shell 3.12.1
```

Install nvm to manage different version of NodeJS.
```bash
# download and run the install script
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# add commands to configure nvm
# will be placed in ~/.bashrc or ~/.profile
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```
Configure neovim. Will add config file later. Here is just a basic config.
```bash
# make directory to store config
mkdir ~/.config/nvim/init.vim

# add minimal config settings
echo "set nu" >> ~/.config/nvim/init.vim
echo "set hlsearch" >> ~/.config/nvim/init.vim
echo "set tabstop=4" >> ~/.config/nvim/init.vim
echo "set shiftwidth=4" >> ~/.config/nvim/init.vim
echo "syntax on" >> ~/.config/nvim/init.vim