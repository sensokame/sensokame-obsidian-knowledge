# File Inclusion
One of the ways that a server creates dynamic content, is by loading different files based on parameters that clients provide, (language, id, etc)
sometimes these parameters are not properly validated, which means that an attacker can trick the server into including files that it's not supposed to include, this include
- Local File Inclusion
- Remote file Inclusion
- Directory traversal
## Getting started with file inclusion
The first step would be to detect where a file inclusion is possible. this means to inspect the request parameters and see which ones are doing file calls, and then trying to change the files being requested to see if we can include files that we're not supposed to.
File inclusion vulnerability usually happens in poorly written code that doesn't not sanitize the input before executing it (doesn't check for permission before including the file)
File inclusion is incredibly dangerous, as it can lead to dangerous exploits such as [[data dumps]] or [[RCE]]
## Path Traversal
The attacker exploits this vulnerability by manipulating and abusing the web application's URL to locate and access files or directories stored outside the application's root directory.
usually this vulnerability is not caused by the programming language, but rather by the developer not not validating the input provided by the users.
this attack is also called the ``dot-dot-slash`` because it involves adding ``../`` elements to the file inclusion parameter in order to access folders outside the application root directory.
when this is applicable, attackers would usually attempt to access specific files that contain information they need (passwords, logs, etc); for this it is essential to have an understanding of [[Operating System]] and the different services and files that they contain to know which files are targeted.
## Local File Inclusion
LFI attacks against web applications are often due to a developers' lack of security awareness. With PHP, using functions such as include, require, ``include_once``, and ``require_once``
t's worth noting LFI vulnerabilities also occur when using other languages such as ASP, JSP, or even in Node.js apps. LFI exploits follow the same concepts as path traversal.
>**NOTE:** the difference between LFI and path traversal, is that path traversal is a read only, while LFI can give [[RCE]] exploits to attacker

for LFI, the attacker also needs a basic understanding of how [[Operating System]] stores the different files they might need access to
## Remote file Inclusion
Remote is basically the same thing as local file inclusion, but with the added caveat that the attacker can include remote files to the server. this means that the attacker can upload his own malicious files which can enable [[RCE]] or similar issues, RFI's usually lead to 
- [[RCE]] (Remote code execution)
- Sensitive Information Disclosure
- [[XSS]] (Criss site scripting)
- [[DoS]] denial of service
RFI is usually caused by misconfiguration that allows the server to include remote files. for example setting ``allow_url_fopen`` option needs to be ``on`` which can be really dangerous.

## By passing the filter
Sometimes developers will try to get around this vulnerability by doing some validation, but sometimes this validation is not enough, so it could be good to try some of these tricks
### NullBytes
Sometimes developers would try to append an extension to the input to force it to only read certain types of files, appending a null byte at the end of the parameter, means that the validator might stop reading after the null byte and ignore the rest of the parameter.
>**NOTE:** this vulnerability may not work on later patched versions, so check the version of the technology to see if this trick might work on not (example, null byte was patched in PHP 5.3.4)

### Forcing fuzzed parameter after client side sanitization
Sometimes, developers would perform some client side input validation before passing the parameter to the server (this might include Uri encoding the input or removing certain special character);
so it might be useful to force the desired payload with other means, direct input injection with requests instead of the website UI for example.
### Understanding sanitization
sometimes developers would try to sanitize input by doing certain workarounds, for example filtering specific file names or specific special words; there are some ways of getting around this.
- accessing specific files: ``/etc/passwd`` becomes ``/etc/passwd/.``
- injecting special characters twice (this is effective if the sanitizer only runs once): ``../`` becomes ``....//`` which will be sanitized back to what it was
- including needed data in the payload: sometimes the validator needs a specific condition, for example starting with a directory name, in that case, we need to include the directory in our payload
## File Inclusion defense
Check [[General Tips for defending against vulnerabilities]] for more information from a blue team member perspective.