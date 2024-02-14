# Lab2-2_SyslogOrganizationOnLog01

### Configuration file for log01

![](https://i.imgur.com/eSUuySK.png)

### Configuration file for web01

![](https://i.imgur.com/ztPzELA.png)

### Configuring fw01 to send logs to log01

##### Adding user

`set system login user <name> full-name "<string>"`

##### Changing password

`set system login user <name> authentication plaintest-password <password>`

##### Configuration

`set system syslog host 172.16.50.5 facility authpriv level info`

`commit`

`save`

`exit`
