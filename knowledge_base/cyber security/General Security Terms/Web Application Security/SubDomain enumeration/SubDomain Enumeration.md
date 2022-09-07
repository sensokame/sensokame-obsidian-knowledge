# Subdomain enumeration
this is the process of finding valid subdomains for a [[domain]], this is done to expand the attack service and try to discover more potential points of vulnerability.
usually a [[domain]] will lead back to an IP address via the [[DNS]] protocol, and sometimes multiple subdomains lead back to the same domain, usually leading to the same IP address just on different ports.
finding different subdomains usually means finding different open ports and possibly vulnerable apps to the same server.

Usually, subdomain enumeration is done through one of these ways:
- Brute Force
- [[OSINT]]
- [[Virtual Host]]

## OSINT
some of the OSINT ways of enumerating subdomains include:
- [[SSL TLS Certificates]]
- [[OSINT Search Engines]] or [[Google Hacking or dorking]]
- Tools, such as [[sublist3r]]
## Brute Forcing
This is straight forward approach, basically, we try as many subdomain combinations as possible and see which ones bite, this is usually done through tools that perform dictionary or brute force attacks on the system and gets the subdomains with a positive response, some of the tools used include
- [[sublist3r]]
- [[SubBrute]]
- [[DnsRecon]]
## Virtual Hosts
Some subdomains aren't hosted in public DNS records, some of these include development versions or administration portals. instead, the [[DNS]] records are kept in a private [[DNS]] server, or recorded on the local machine in the /etc/hosts [[Linux]] file or c:/windows/system32/drivers/etc/hosts ([[Windows]])

this means that [[DNS]] will not work with our subdomains, but we can grab the IP address from the domain, and using tools to map the subdomains to that IP Address, usually with brute forcing methods.

This can be done with tools such as [[ffuf]]