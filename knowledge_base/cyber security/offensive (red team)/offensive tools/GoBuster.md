# GoBuster
Gobuster is a tool used to brute-force:

-   URIs (directories and files) in web sites.
-   DNS subdomains (with wildcard support).
-   Virtual Host names on target web servers.
-   Open Amazon S3 buckets

Gobuster is under active development, source code can be found in [Gobuster github page]([OJ/gobuster: Directory/File, DNS and VHost busting tool written in Go (github.com)](https://github.com/OJ/gobuster)) 

>**NOTE:** Gobuster comes pre installed with kali linux

we can use gobuster to enumerate a website and check for any hidden pages or directories.

Basic command goes like 
``gobuster dir -u host -w wordlist``
We can use ``-x`` switch to specify file extension