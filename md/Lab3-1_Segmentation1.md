# Lab3-1_Segmentation1

### WKS01 Setup

Add user through powershell

`New-LocalUser -Name "username"`

Then enter the password when prompted

Add user to Administrators group

`Add-LocalGroupMember -Group "Administrators" -Member "username"`

Setting the hostname was not supported through powershell, but we can use a graphical, `Win`+`R`  or right click on the windows logo and select *Run* and enter `systempropertiescomputername`. 
