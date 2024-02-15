# Lab3-1_Segmentation1

### Windows Desktop/Server Setup

Add user through powershell

`New-LocalUser -Name "username"`

Then enter the password when prompted

Add user to Administrators group

`Add-LocalGroupMember -Group "Administrators" -Member "username"`

Setting the hostname was not supported through powershell, but we can use a graphical, `Win`+`R`  or right click on the windows logo and select *Run* and enter `systempropertiescomputername`. 

### Configuring RIP on Vyos

On system1 (facing the WAN):

`set protocols rip interface [interface]`

`set protocols rip network [address]/[mask]`

On system2 (inside network):

`set protocols rip interface [interface]`

`set protocols rip network '[address]/[mask]'`

### Configuring network using netplan

System: Ubuntu server

Configuration file location: `/etc/netplan/00-installer-config.yaml`

Could be named something different, but same folder and extention.

Configuration file:

<img title="" src="file:///C:/Users/ben/AppData/Roaming/marktext/images/2024-02-14-19-02-28-image.png" alt="" width="432">
