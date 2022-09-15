# SSRF 
Server Side Request Forgery is a vulnerability that allows malicious users to cause the webserver to make an additional or edited http request to the source of the attacker's choosing; basically, the attackers forges a request that makes the server believe that the attacker has access to the resource while the attacker in fact doesn't have that access.
there are two types of SSRF
- Regular SSRF, where the data is returned to the attacker
- Blind SSRF, where there vulnerability happens, but there is no information returned to the attacker.
SSRF can result in:
- Access to unauthorised areas
- Access to customer/organisational data
- Ability to Scale to internal networks
- Reveal authentication token/credentials
## Getting Started
Getting started with SSRF is simple, it's important to identify an injectable field in which the attacker can trick the server into calling the wrong internal resources
this can be done usually by switching the request parameters to include different resources, specially when the arguments are either absolute or relative paths.
when the request has an absolute path, it's also possible to trick the server into accessing a different domain (the attackers domain) which can grab sensitive information and spit it back to the attacker.
>**NOTE:** If working with a blind SSRF where no output is reflected back to you, you'll need to use an external HTTP logging tool to monitor requests such as requestbin.com, your own HTTP server or Burp Suite's Collaborator client.

## Getting around defences
Sometimes, blue team would add some ways in order to try and get around this vulnerabilities, here are few ways how those work and how to get around them if possible
### Deny List
this is partially covered in the defensive tips for defending against vulnerabilities, but one of the ways blue team do this, is by providing a black list of IP addresses that the server would not access, for example ``localhost``, ``127.0.0.1``
this would prevent the server from passing internal requests that would spit out sensitive information.
attackers can bypass this by specifying alternatives such as ``0.0.0.0``, ``0000``, ``127.1``, ``127\*.\*.\*``, ``2130706433``, ``017700000001`` or any subdomains that would resolve to the local IP address ``127.0.0.1`` or ``127.0.0.1.nip.io``
>**NOTE:** in cloud environment, there is a special IP address `169.254.169.254` that usually contains metadata, which is sensitive information and should be handled with care. Attackers can still bypass this by registering a subdomain that points to this address.
### Allow list
this is the opposite of an allow list, this list specifies which IP addresses the server is allowed to access.
this can stop the server from accessing redirect URLs that would lead to the attacker website.
attackers can bypass this by creating subdomains on the   attacker's domain name that would satisfy the allow list rules. (this happens when the allow list is loosely made, for example only checking for the way the URL starts and not the entire URL)
### Open Redirect
sometimes, when specific URLs are denied access to the server, the attacker can bypass this by creating a redirect request that looks like it goes to an innocent URL but would then redirect to the attacker or a malicious URL.