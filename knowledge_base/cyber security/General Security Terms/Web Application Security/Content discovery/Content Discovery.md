# Content Discovery
Content discovery is the process of trying to find the content of a web application, this includes files, media, pictures, etc.

There are three main ways of discovering content on a website:
- manually
- automated
- [[OSINT]]

## Manual
There are multiple places to manually check a website to discover the content
The most famous way is to check the Robots.txt 
### Robots.txt
This file when present in the main domain of a website tells search engines which pages they are and aren't allowed to crawl. looking at this website we can find some "secret" folders and files that we can attempt to check.
### Favicon
Sometimes when frameworks are used to build a website, a favicon that is part of the installation gets leftover, and if the website developer doesn't replace this with a custom one, this can give us a clue on what framework is in use. 
[OWASP hosts a database of common framework icons that you can use to check against the targets favicon](https://wiki.owasp.org/index.php/OWASP_favicon_database). Once we know the framework stack, we can use external resources to discover more about it.
the way to check the OWASP  database is to curl the icon and md5sum it 
command example: `curl website/favicon/images/favicon.ico | md5sum`
this will output an md5 hash that we can search for in the OWASP database.
### Sitemap.xml
Some websites offer a sitemap.xml, which lists every file on the website the owner wishes to be listed. so while this will not probably give out "secret" content, it is till useful to get an idea about the more difficult parts of the website to navigate to. or in some lucky cases, it will hold some old folders that were unintentionally left there by mistake.
### HTTP Headers
Websites mostly operate using HTTP requests/Reponses systems. this communication usually involves HTTP headers that include various information about the sender and receiver.
some of these information can include the programming/scripting language, some software versions, or other information, so it might be useful to check the http header for possible information.
### Framework Stack
After finding out the framework stack of the website through other means, we can locate the framework website, from there we can learn more about the software and other information (possibly hidden folders files in the framework or how they handle their information)
## Automatic
Automated discovery is the process of using tools to discover content, this is usually done by bombarding the server with a ton of automated requests that test all possibilities, this is done using [[wordlists]] and automation tools
some of these tools include:
- [[ffuf]]
- [[dirb]]
- [[GoBuster]]
these tools will try to fuzz the url and return the positive responses from the server indicating a valid content.