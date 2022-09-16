# Defending Against Vulnerabilities
Well, File inclusion vulnerabilities can happen in any web service, so it is imperative to do the best to keep the system free from this vulnerability, some of the ways of doing this for a blue team member includes:
- keeping [[software]] up to date, this includes systems and services even web application frameworks, it could be important to follow the change log of the [[software]] that is being used on the machine to be aware of any security patches that might be critical. sometimes a developer might even need to downgrade the software they are using if the latest version has a security flaw.
- in production mode, it is necessary to remove logging that might give an insight to the attacker about the source code, for example, developers should disable [[PHP]] error logging because it reveals function names, paths and other sensitive information
- keeping a web application firewall [[WAF]] to mitigate web application attacks, for example blacklisting IP addresses that are sending malicious data
- Disable any features that are not needed (specially network related features)
>Example: disabling `allow_url_fopen` on and `allow_url_include` in PHP.

- disabling protocols and wrapper that are not needed
- always sanitise user input, implement proper input validation, sanitization is different depending on where the input is needed, for example when reading input that will be used as a filename from the server (language for example), it is important to make sure that the input cannot be exploited for [[File Inclusion]]
- Implementing white and black lists. sometimes a user is not allowed to input specific words (black list), for example script tags or special file names, other times a user is ONLY allowed to input specific words (white list) for example language name