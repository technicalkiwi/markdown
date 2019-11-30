# New System Setup Guide

### Index
 - [OS Install](##os-install)
   - [Insalling Ubuntu](#installing-ubuntu)
     - [Install Type](#install-type)
     - [Disk Partitioning](#disk-partitioning)
     - [Initial User Account](#initial-user-account)
- [Base System Setup](#base-system-setup)
 - [Update Local Repository](#update-local-repository)
 - [Update Installed Applications](#update-installed-appliacations)
 - [Install Base Applications](#install-base-applications)
- [Setup Applications](#application-setup)
  - [Setup Git](#setup-git)
  - [Setup SSH](#setup-ssh)
    - [Edit SSH config](#edit-ssh-config)
    - [Add SSH Pubkey](#add-ssh-pubkey)
 

 ## Os Install

### Installing Ubuntu
- Create Bootable USB drive.
- Insert into the target machine
- Begin the installation process

#### Select Install Type

#### Disk Partitioning

#### Initial User Account


## Base System Setup

#### Update local Repository
Run Command `sudo apt update` to update local repository

#### Update Installed Applications
Run Command `sudo apt update -y` to update all preintstalled applications

#### Install Base Applications
Install to basic application with `sudo apt install XXX` Where XXX is the package name

Basic Packages include  
 - Git
 - SSH
 - net-tools
 - curl
 - wget
 - neofetch

## Application Setup

#### Setup Git

Add Git Username
`git config --global user.name "User Name"`

Add Git Email Address
`git config --global user.email "your_email@example.com"`

Set Default Git Editor (Nano)
`git config --global core.editor "nano -w"`


#### Setup SSH

Set SSH to run at startup
`systemctl enable ssh`

Start SSH
`systemctl start ssh`

Check SSH is running
`systemctl status ssh`
![SSH Running](./resources/SSH_running.png)

#####  Edit SSH Config
We are just going to change the basics, for a more comprehensive guide look at [SSH Setup](/Linux/Application-Setup/SSH/Configuring_SSH.md)

Open the SSH config File
`nano /etc/ssh/sshd_config`

Find the Following lines and change them accordingly

Change the port number
`port xxxx`

Enable Pubkey Authentication
`PubkeyAuthentication yes`

Check Authorized Key Location
`AuthorizedKeysFile ~/.ssh/authorized_keys`

Disable Root login
`PermitRootlogon no` 

##### Add SSH Pubkey