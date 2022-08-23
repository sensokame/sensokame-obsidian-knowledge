# Security Operations
A company would usually have a security operations center who are responsible for monitoring the security of the company.
This team would take care of:
- Find Vulnerabilities on the network
- Detect unautharized activity
- Discover policy violations
- Detect intrusions
- Support with incident response

## Data sources
As talked about briefly in the overview, there are multiple sources for data for the security operations center, from these we cite:
- server logs: there are many servers on the network, including mail, web, domain controller, etc
- [[dns]] activity: this can tell us which domain names is the internal system trying to communicate with
- [[firewall]] logs: firewall logs can tell us about which applications/packets attempted to get through
- [[dhcp]] logs: dhcp logs can tell us about the devices that joined the network.

>**NOTE:** server logs include all kinds of data, with the most important ones being successful and failed login atteempts
>**NOTE:** there could be more data sources such as the event viewer or the system logs, it's up to the security center to identify these data sources

## SOC Services
SOC services include reactive and proactive services

### Reactive SOC Services
These services refer to tasks after detecting an intrusion or malicious events. some of the examples of reactive services are:
- Monitor Security posture: this includes monitoring the system for security alers and responding to them
- Vulnerability management: this refers to finding vulnerabilies in the system and patching them.
- [[Malware Analysis]]: the SOC will analyze the malware found
- Intrusion detection: this is usually done using an [Intrusion detection system] (IDS) which alerts the SOC team about intrusions
- Reporting: it is essential to report incidents so that the company can learn from them.

### Proactive services
These are the services done prior of an intrusion, as precautions, some of the examples of proactive services include:
- [[Network Security monitoring]] (nsm)
- [[Thread hunting]]
- [[Threat Intelligence]]
