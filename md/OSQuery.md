# OSQuery

### Installation (Linux)

[Instructions for Different Distros](https://osquery.io/downloads/official/5.11.0)

1. `sudo apt-get update`

2. `sudo apt-get install osquery`

3. `sudo systemctl start osqueryd`

4. `sudo systemctl enable osqueryd`

5. `To start a standalone osquery use: osqueryi. This does not need an osquery server or service. All the table implementations are included`

6. `Once in the osqueryi interactive shell, you can explore system tables using SQL-like queries. For example: SELECT * FROM osquery_info;`

7. `Configuration files for osquery are usually found in /etc/osquery/`

Screenshots TBD



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
