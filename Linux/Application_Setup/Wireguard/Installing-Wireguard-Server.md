# Installing WireGuard
### Index
 - [Install Wire Guard](#install-wire-guard)
 - [Configure Wire Guard](#configure-wire-guard-server)
 - [Configure Firewall Rules](#configure-firewall-rules)
 - [Start Wire Guard](#start-wire-guard)
 - [Test Wire Guard](test-wire-guard)


### Install Wire Guard
Add the Wireguard repository to your sources list. Apt will then automatically update the package cache.  
`sudo add-apt-repository ppa:wireguard/wireguard`

Install Wireguard. The `wireguard` package will install all necessary dependencies.  
`sudo apt install wireguard`

DKMS will then build the Wireguard kernel module. If successful, you'll see the following output:
<pre>
wireguard:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.15.0-43-generic/updates/dkms/

depmod...................

DKMS: install completed.
Setting up wireguard (0.0.20181218-wg1~bionic) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ... </pre>  

### Configure Wire Guard Server
Generate a private and public key pair for the WireGuard server:
`umask 077`
`wg genkey | tee privatekey | wg pubkey > publickey`

This will save both the private and public keys to your home directory; they can be viewed with `cat privatekey` and `cat publickey` respectively.

Create the file `/etc/wireguard/wg0.conf` and add the contents indicated below. You'll need to enter your server's private key in the `PrivateKey` field, and its IP addresses in the `Address` field.

<pre>
[Interface]
PrivateKey = <Private Key>
Address = 203.0.113.5/24, fd86:ea04:1115::1/64
ListenPort = 51820
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE; ip6tables -A FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE; ip6tables -D FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
SaveConfig = true </pre>

 - **Address** defines the private IPv4 and IPv6 addresses for the WireGuard server. Each peer in the VPN network should have a unique value for this field.

- **ListenPort** specifies which port WireGuard will use for incoming connections.

- **PostUp** and **PostDown** defines steps to be run after the interface is turned on or off, respectively. In this case, `iptables` is used to set Linux IP masquerade rules to allow all the clients to share the server's IPv4 and IPv6 address. The rules will then be cleared once the tunnel is down.

- **SaveConfig** tells the configuration file to automatically update whenever a new peer is added while the service is running.


### Configure Firewall Rules
Allow SSH connections and WireGuard's VPN port:
`sudo ufw allow 22/tcp`
`sudo ufw allow 51820/udp`
`sudo ufw enable`  

Verify the settings:
`sudo ufw status verbose`

### Start Wire Guard
Start Wireguard:
`wg-quick up wg0`  

**wg-quick** is a convenient wrapper for many of the common functions in `wg`. you can turn off the wg0 interface with `wg-quick down wg0`

Enable the Wireguard service to automatically restart on boot:
`sudo systemctl enable wg-quick@wg0`

### Test Wire Guard
Check if the VPN tunnel is running with the following two commands:

*Command One*
`sudo wg show`
You should see a similar output:

<pre>
user@ubuntu:~$ sudo wg show
interface: wg0
  public key: vD2blmqeKsV0OU0GCsGk7NmVth/+FLhLD1xdMX5Yu0I=
  private key: (hidden)
  listening port: 51820
</pre>

*Command Two*
`ifconfig wg0`
Your output should resemble the following:
<pre>
wg0: flags=209<UP,POINTOPOINT,RUNNING,NOARP>  mtu 1420
        inet 203.0.113.5  netmask 255.255.255.0  destination 203.0.113.5
        inet6 fd86:ea04:1115::1  prefixlen 64  scopeid 0x0<global>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 1000  (UNSPEC)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
</pre>