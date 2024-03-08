# OSQuery

### Installation (Linux)

[Instructions for Different Distros](https://osquery.io/downloads/official/5.11.0)

1. `export OSQUERY_KEY=1484120AC4E9F8A1A577AEEE97A80C63C9D8B80B`

2. `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys $OSQUERY_KEY`

3. `sudo add-apt-repository 'deb [arch=amd64] https://pkg.osquery.io/deb deb main'`
   
   ![](https://lh7-us.googleusercontent.com/x-yDr19SQHBKoYhjRenGGm62_P2rN2N4Z5puquOUXgmFLwET7JwTgdJONsw-HmRoYcbG7ZP4nvvefHHXuveorRmG7pFEa4OKAKDl1m3UQvzN4nt_JjV5GqxjNq02wx0_oA5bZsW15vEAwJJIESZVgA)

4. `sudo apt-get update`

5. `sudo apt-get install osquery`

6. `sudo systemctl start osqueryd`

7. `sudo systemctl enable osqueryd`

8. `To start a standalone osquery use: osqueryi. This does not need an osquery server or service. All the table implementations are included`

9. `Once in the osqueryi interactive shell, you can explore system tables using SQL-like queries. For example: SELECT * FROM osquery_info;`
   
   ![](https://lh7-us.googleusercontent.com/fEv6qa3nUmPBINXEKbObE1edImui_-OBtFBsnMh6aFSNcyzMgPdgMDnDb-jiUnMS6lXjOramlzLdNO0sksUZh4rZqJ3rTo1yte8sizQEN220tvfo1rGb6JjiHfc6cpcxMb4Y7FJVfMLiHnDs21zPzQ)
   
   ![](https://lh7-us.googleusercontent.com/2W5Mdnv8fZytD7HkVKDtUUZhygMIJz41JMj_kqZHzBsGrE7CNTksazDaDiW92ZpmI85zc9PXtuuVBgnkgNg7yck2KB4ehX82joyJUBbkid8MBKwAhgVEIFu2GgZ-ofYyyeuB-XXus5AMca7822qnYw)
   
   ![](https://lh7-us.googleusercontent.com/GJPb62yyIGWgyJT6BUWNsN6griJjDvpkRm1_B8bo1NXvVYuIs1gR2pVH_Wq_9ANfxFB2pqlYcjjMyLExI-TZAdywXNyxHFAsk_CoZa1Hg-1pyGOcsy_hLoXKOxVqSG8rwCnf1auhZMjFUJr7TquOWg)

10. `Configuration files for osquery are usually found in /etc/osquery/`
    
    1. Create the file `/etc/osquery/osquery.conf`
    
    2. Config File:
       
       ```Config
       {
           {
               "options": {
                     "config_plugin": "filesystem",
                 "logger_plugin": "filesystem",
                 "utc": "true"
               },
               "schedule": {
                     "system_info": {
                 "query": "SELECT hostname, cpu_brand, physical_memory FROM system_info;",
                 "interval": 60
             },
           "processes_binding_to_ports": {
             "query": "SELECT DISTINCT process.name, listening.port, listening.address, process.pid FROM processes AS process JOIN listening_ports AS listening ON process.pid = listening.pid;",
             "interval": 60
             }
         }
       }
       ```
       
       `osquery.conf`

11. Set up Wazuh
    
    1. Once the config file is defined, Wazuh should be logging.
    
    2. Log into Wazuh web console
    
    3. Go to Settings->Modules
       
       1. Enable Osquery module under Threat Detection and Response
       
       ![](https://lh7-us.googleusercontent.com/oAM_ILh7sWC22X2nJ8tK5do5jJeGGG_nZ5HnLmEjLuoa8x8y7cdZNMt5dAKcqLr0xO6Of3RqxPdnCRF5cZC_7IHTEzP5Uc2bPvMMzVc-yJViBg6x4LFQGA7b2pVKR0BFIccBgVMxfF8m5AT7IeY84g)
    
    4. Go to Management->Groups
       
       1. Edit `agent.conf` 

```
<agent_config>
    <wodle name="osquery">
        <disabled>no</disabled>
        <run_daemon>yes</run_daemon>
        <bin_path>/usr/bin</bin_path>
        <log_path>/var/log/osquery/osquery.results.log</log_path>
        <config_path>/etc/osquery/osquery.conf</config_path>
        <add_lables>no</add_labels>
    </wodle>
</agent_config>
```

`agent.conf` 

![](https://lh7-us.googleusercontent.com/gL-klHlK0S0ctppBpB2JN5hugrxtO0kDEFBccp7KgUcYbd6vdN4dkV27tdthwoy7OwHp_Ap2O_a7FiEyjvje6TS-QcHGLSELIEJ3CBtYI0CrsQbJ4Zl1O2pZCI9Vtc6TYX3g7PR-fnPITThZWfkLuw)

![](https://lh7-us.googleusercontent.com/rzxf936-xNLJQXdv4lsRzrDB95qZskQbQpsf8kuVPZbFSBETHHyDJao3ijccWP21fExofoPOZkIElL4aKZoQ23NXvyRhziF__4Sn4KQVsbTTChyCVzbR6lvP35IYlwnvavOP-VEV4so2BG7PDPKgrQ)



### Installation (Windows via Chocolatey)

[Supported Versions](https://chocolatey.org/packages/osquery/)

1. `choco install osquery`
   
   1. This installs the binaries, example packs, example configuration, and an OpenSSL certificate bundle to `C:\Program Files\osquery`

2. To install a Windows SYSTEM-level service, use `choco install osquery --params='/InstallService'`

### Running OSQuery

On all playforms, the command `osqueryi` will launch the interactive shell.

Linux Service:

`sudo systemctl start osqueryd`

`sudo systemctl enable osqueryd`

Windows Service:

`Start-Service osqueryd` - Powershell

`sc.exe start osqueryd` - CMD

### Overview of OSQuery

OSQuery is an operating system instrumentation framework for Windows, macOS, and Linux. The tools make low-level operating system analytics and monitoring both performant and intuitive. It turns your operating system into a high-performance relational database, making it easier to gather information about your systems, monitor security-related events, and perform investigations. With OSQuery, SQL tables represent abstract concepts such as running processes, loaded kernel modules, open network connections, browser plugins, hardware events or file hashes. OSQuerycomes with an interactive shell (`osqueryi`) that allows users to run ad-hoc queries and explore the system's information in real-time. Use cases include security monitoring, compliance checking, and incident response.

### Pros and Cons

##### Pros

- Versatility: OSQuery is highly versatile, allowing the user to query a wide range of information about Linux systems. This flexibility makes it valuable for various use cases, including security monitoring, compliance checking, and system troubleshooting.

- Unified Interface: With its SQL-like interface, OSQuery provides a unified way to access and query diverse system information. This makes it more accessible for security professionals who may not have extensive experience with complex scripting or command-line tools.

- Real-time Monitoring: OSQuery supports real-time monitoring, enabling you to continuously monitor system activities and respond to potential security threats promptly.

- Cross-Platform Compatibility: OSQuery is not limited to Linux; it supports multiple operating systems, including macOS and Windows. This cross-platform compatibility is beneficial for organizations with mixed environments.

- Community Support: OSQuery has an active community that contributes to its development and shares queries and plugins. This community support enhances the tool's functionality and keeps it up-to-date with the latest security requirements.

##### Cons

- Resource Consumption: OSQuery can be resource-intensive, especially when running complex queries or monitoring a large number of systems simultaneously.

- Learning Curve: While the SQL-like interface is user-friendly, there is still a learning curve for users who are not familiar with SQL or database concepts

- Limited Built-in Queries: While OSQuery has a broad range of capabilities, some users may find that it lacks certain built-in queries for specific use cases. Users may need to create custom queries or rely on community-contributed queries to address these gaps.

- Security Risks: As with any software, OSQuery may introduce security risks if not properly configured and monitored. It's essential to follow best practices for securing OSQuery deployments to prevent unauthorized access or misuse.

- Integration Challenges: Integrating OSQuery into existing security workflows and tools may pose challenges. Ensuring seamless integration with other security solutions can require additional effort.
