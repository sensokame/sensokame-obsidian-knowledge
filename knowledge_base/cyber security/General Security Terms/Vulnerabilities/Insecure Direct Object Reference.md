# Insecure Direct Object Refernece
This is part of the [[Broken Access Control]] Vulnerabilities for web apps

an IDOR vulnerability can occur if too much trust has been placed on that input data. In other words, the web application does not validate whether the user has permission to access the requested object.
This can also be related to [[Local file inclusion somehow]] meaning that the server does not validate the request data and just returns the requested data
This vulnerability is easily spotted when there is a number in the request header (specially if this number is sequential and could increment for each item)
> example: https://store.tryhackme.thm/customers/user?id=16
> this means that we can try other numbers and access other user data if this vulnerability exists

