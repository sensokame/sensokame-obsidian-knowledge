# nmap
The Network Mapper, is arguably the most famous network mapper out there.
nmap is used to discover hosts and services on a computer network by sending packets and analysing the responses. nmap provides a number of features for probing computer networks, including host discovery and service and operating system detection.
the reason why nmap is extremely popular can be contributed to many things, namely nmap has been around since 1997 and is still under active development until now, secondly, nmap is very efficient at what it does, is extremely customizable and  it comes with a powerful scripting capability that allows it to be extended to do more mapping and might even check for vulnerabilities or run exploits.
[GitHub read only mirror](https://github.com/nmap/nmap/)
[svn actual git repo](https://svn.nmap.org/nmap)
[nmap website](https://nmap.org/)
## Getting Started with nmap
nmap is extremely customizable and allows for a shit ton of different ways and scans to perform on target(s)
so the most basic nmap scan is just giving an IP address or domain name; 
this will make nmap perform the most default basic scan on that IP address
> nmap IP_ADDRESS/DOMAIN_NAME

this command will do the following steps
- in case a domain name is provided, do a [[DNS]] lookup to convert the hostname to an IP address (this step is skipped if an IP address is provided)
- Ping the host, with default [[ICMP]] echo request, and a [[TCP]] ACK packet to port 80, this step is to determine if the target is up or not, this step can be skipped by providing the optional argument ``-Pn``
- Covert the host back to the name using a reverse [[DNS]] query, reverse name may not be the same as the target specified on the command line, this can be skipped by providing the ``-n`` argument
- Launch a [[TCP]] port scan of the most popular 100 ports listed in ``nmap-services``, a SYN stealth scan is usually used, but in case of a non root user, connect scan is performed instead
- Print the results to the standard output  in normal human-readable format and exits, output formats and locations can be specified with additional arguments

the most basic scan will check if any port responds to the [[TCP]] request (accepts connection request or refuses connection by sending a negative response), if a port answers the request, it is marked as open/closed, based on the response, and is added to the output list. the SERVICE is then mapped to the default value for that part (for example; port 80 open is mapped to [[HTTP]] service) but this is just a speculation, it is not always the case, additional probing to detect the actual service running on the port is possible through some additional arguments, this would make the scan result more accurate, but will probably slow down the result.

Since nmap scans are usually done in batch (scanning a batch of ports/addresses), some [[IDS]] systems are capable of detecting when an nmap scan is being executed on their machines and can then block the incoming requests, to get around this, nmap gives some customization capabilities to try and be more stealthy. but still, using nmap without authorization could still be against the law and could get you into trouble (similar to any other active reconnaissance technique), since the attacker is directly attacking a system without permission. 
> for public IP addresses, sometimes a [[shodan]] search is better than an nmap scan, since [[shodan]] is still considered passive reconnaissance so technically, the attacker is not breaking the law by doing it. having said that, nmap is still the ubiquitous scanning tool to use to find ways of interfacing with a machine (specially one that isn't on the public internet; also [[shodan]] scans could be outdated).

## Common arguments
nmap has a plethora of arguments that can be specified to customize the scanning process