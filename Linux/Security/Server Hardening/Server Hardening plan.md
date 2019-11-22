# Server Hardening Plan

### Index
- [Overview](#overview)
#### Steps to Take
- [Create a New User](#create-new-user)
- [Setup Key Based Logon](#setup-key-based-logon)
- [Edit The Ssh Config File](#edit-the-ssh-config-file)
  - [Disable Root Logon](#disable-root-logon)
  - [Change SSH Port](#)
  - Limit SSH to certain Users
  - Limit Authentication Attempts
  - Set SSH Idle Timeout
  - Disable Empty Passwords
  - Disable Rhosts
  - Disable Host Based Authentication
  - Disable Password Based Logon
- Enable and Configure UFW
- Enable and Configure GeoIP
- Enable and Configure Fail2Ban
  <br><br>
##### Overview
<br>
##### Create New User
Create another user and add them to the Sudo Group  
`sudo adduser "Username"`  
`sudo usermod -aG sudo "Username"`  
Check you can login via ssh with this new user

##### Setup Key Based Logon
Create a new key pair on your local machine  
`sudo ssh-keygen`  
![ssh keygen image](./resources/ssh_keygen.png)  
Copy the key to the server  
`ssh-copy-id -i "keyname" user@hostname`  
Test you can logon using the new key

##### Edit The Ssh Config File
Open /etc/ssh/sshd_config and change the configuration within  
`sudo nano /etc/ssh/sshd_config`

Change the following lines
###### Disable root login
`PermitRootlogon no`
###### Change SSH Port
`Port ####`
###### Limit SSH access to certain users
`AllowUsers user1 user2`
###### Limit Authentication Attempts
`MaxAuthTries #` ( Recommended is less than 5)
###### Set SSH Idle Timeout
`ClientAliveInterval ###` (Seconds)
###### Disable Empty Passwords
`PermitEmptyPasswords no`
###### Disable RHosts
`IgnoreRhosts yes`
###### Disable Host Based Authentication
`HostBaseedAuthentication no`

<br>
##### Setup Email Alerts for logon
Install 'mailx' package  
`sudo apt install mailx`  
Open the .bashrc file  
`sudo nano -w /root/.bashrc`  
Add this to the end of the file
<pre>echo 'ALERT - Root Shell Access (ServerName) on:' `date` `who` | mail -s
"Alert: Root Access from `who | cut -d'(' -f2 | cut -d')' -f1`" your@email.com </pre>

Enable and Configure UFW
Enable and Configure GeoIP
#### Enable and Configure Fail2Ban
Install Fail2ban
`sudo apt install fail2ban`
Enable Fail2ban
`systemctl start fail2ban && systemctl enable fail2ban`
Edit the config file 
`nano /etc/fail2ban/jail.local`