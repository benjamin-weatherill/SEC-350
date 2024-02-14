## Lab 1.1 - Routing and DMZ

### Configuring rw01

Xubuntu system - IP 10.0.17.39  - Hostname rw01-benjamin

Configured IP via built-in GUI

![](https://i.imgur.com/menrTpY.png)

Added user with command: 

`sudo adduser ben`

and added it to the sudoers group with:

`sudo usermod -aG sudo ben`

### Configuring fw01

Firewall, vyOS - IPs WAN-10.0.17.139 DMZ-172.16.50.2 LAN-172.16.150.2 - Hostname fw01-benjamin

Configure hostname

Run the commands in sequence:

`configure`

`set system host-name fw01-benjamin`

`commit`

`save`

`exit`

The new hostname will be set

---

Configure Interfaces

`show interfaces`

-

`configure`

`set interfaces ethernet eth0 description DESC`

(Repeate for all inerfaces with DESC replaced my a description of the interface)

`commit`

`save`

`exit`

![](https://i.imgur.com/mHmrBUc.png)

---

Now the IP Addresses

`configure`

`set interfaces ethernet ethX address IPADDRESS/MASK`

(Repeating for all interfaces replacing as necessary)

`commit`

`save`

`exit`

![](https://i.imgur.com/ATTQnpZ.png)

---

Configure Default Gateway and DNS

`configure`

`set protocols static route 0.0.0.0/0 next-hop 10.0.17.2`

`set system name-server 10.0.17.2`

`commit`

`save`

`exit`

![](https://i.imgur.com/fK023qT.png)

### Configuring web01

CentOS 7 System, IP 172.16.50.3, Hostname web01-benjamin

Set Ip information and hostname with `sudo nmtui`

---

Must configure fw01 for NAT and DNS forwarding

On fw01:
`configure`

`set nat source rule 10 description "NAT FROM DMZ to WAN"`

`set nat source rule 10 outbound-interface eth0`

`set nat source rule 10 source address 172.16.50.0/29`

`set nat source rule 10 translation address masquerade`

`commit`

`save`

`exit`

--- 

DNS forwarding on fw01:

`configure`

`set service dns forwarding listen-address 172.16.50.2`

`set service dns forwarding allow-from 172.16.50.0/29`

`set service dns forwarding system`

`commit`

`save`

`exit`

### Configuring log01

Centos 7 System, IP 172.16.50.5, Hostname log01-benjamin

Created user, set ip information and hostname.

---

Configuring rsyslog services:

Status: `sudo systelctl status rsyslog`

Allow udp/tcp port 514 through the firewall:

`sudo firewall-cmd --perminant --add-port 514/tcp`

`sudo firewall-cmd --perminant --add-port 514/udp`

`sudo firewall-cmd --reload`

Check: `sudo firewall-cmd --list-all`

![](https://i.imgur.com/wYMpGKa.png)

---

Editing the /etc/rsyslog.conf file

`sudo vim /etc/rsyslog.conf`

Uncomment the 4 uncommented lines here:\

(You can either enter interact mode `i` or go to the beginning of the line and press `Delete`)

![](https://i.imgur.com/F94CtUf.png)

`ESC` -> `:wq`->`Enter` to save and quit

Now restart the rsyslog service:

`sudo systemctl restart rsyslog`

Check the ports are open and listening:

`netstat -tupan | grep 514`

![](https://i.imgur.com/2LWsfIF.png)

### Configuring httpd on web01

Allowing http and httos through firewall

`sudo firewall-cmd --permanent --add-service http`

`sudo firewall-cmd --permanent --add-service https`

`sudo firewall-cmd --reload`

To view:

`sudo firewall-cmd --list-all`

### Configuring static route on rw01

Through the gui configuration menu:

![](https://i.imgur.com/sWGghmR.png)

### Configuring rsyslog client on web01

Install rsyslog on web01:
`sudo yum install -y rsyslog`

Now enable and start it:

`sudo systemctl start rsyslog`

`sudo systemctl enable rsyslog`

Create a file /etc/rsyslog.d/sec350.conf and restart rsyslog

`sudo vi /etc/rsyslog.d/sec350.conf`

Use `i` to enter interact mode

Add the line `user.notice @172.16.50.5`

Save `ESC`->`:wq`->`Enter`

Restart rsyslog `sudo systemctl restart rsyslog`
