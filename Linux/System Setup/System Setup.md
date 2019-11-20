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

#### Disk Paritioning

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

#### Setup SSH

#####  Edit SSH Config

##### Add SSH Pubkey