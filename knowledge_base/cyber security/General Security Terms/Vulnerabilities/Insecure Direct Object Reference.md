# Insecure Direct Object Reference
This is part of the [[Broken Access Control]] Vulnerabilities for web apps

an IDOR vulnerability can occur if too much trust has been placed on that input data. In other words, the web application does not validate whether the user has permission to access the requested object.
>**NOTE:** this is related to improper permissions, since the server doesn't check if the attacker has permission or not before returning the data.

This can also be related to [[Local file inclusion somehow]] meaning that the server does not validate the request data and just returns the requested data
This vulnerability is easily spotted when there is a number in the request header (specially if this number is sequential and could increment for each item)
> example: https://store.tryhackme.thm/customers/user?id=16
> this means that we can try other numbers and access other user data if this vulnerability exists

So basically this vulnerability is a misconfigured value that the attacker can change in order to make the server spit out data that the attacker should not be able to gain access to.
## Getting started
The first step would be to identify an injectable Id that could be tampered with
### Clear Text
Sometimes the injectable id is in clear text and can be easily changed
### Encoded
Sometimes the injectable Id is encoded, and so the trick would be to decode the id, change the values, encode it again and send it to the server. a common encoding algorithm is base64
### Hashed
Sometimes the injectable Id is hashed, this is different since hashing is not a two way operation, so breaking a hashed ID can be a little more difficult, and so the trick would be to crack (see [[Cracking]] for more on this) the hashed id, change the values, hash it again and send it to the server.
### Unpredictable
Sometimes an injectable Id has a wile format, in this case, to detect the vulnerability, we can create two account and swap the values to see if one client can impersonate another.
after discovering the vulnerability, it could be worth it to try and [[Brute Force]] the Id
## Where to find this
the most direct approach to this is to check the website URL, but it's not always so straight forward, to find this vulnerability, it might be helpful to check more places
- website URL
- cookies
- JavaScript scripts
- web requests (a good way at this is to check the network tab in the developer tools in the browser and try to notice any weird traffic)
- API calls (special values found in web requests)