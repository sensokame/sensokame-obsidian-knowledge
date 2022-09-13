# Cookie Tampering
Basically, cookies are what tells websites who you are, cookies keep persistence in web applications during a session and even, depending on the duration of the cookie, for weeks to come;
cookies can also present a metric for the web application, and the web server to know who you are, a cookie would act like a unique identifier to your customer profile on the server.
However, sometimes cookies can be vulnerable to tampering, allowing attackers to execute all kinds of malicious activities in the server.
there are many ways of tampering cookies, but it either includes changing a pre-existing cookie to include some additional malicious information, or copying parts (or the entirety) from someone else's cookie (cookie stealing would allow hackers to impersonate a victim)
## Getting Started 
Tampering with cookies often requires understanding how a cookie is formed, so it might be useful to try and reverse engineer a cookie
### Clear Text
sometimes a cookie is is in clear text, that way, we can just understand what we need to change in it to tamper with the server, for example; an attacker can change the ``customer_id`` field to gain access to a different customer data.
### hashing
Sometimes a cookie is a text in a non readable format, however, this would usually mean that it's merely hashed to hide the clear text behind it, in that case, the attacker could just decode the cookie, change the values as if handling clear text, encode the cookie again and send it to the server.
### [[Brute Force]]
Sometimes a cookie is incredibly incomprehensible, in that case, an attacker can try and brute force different cookie combinations until they get a working cookie 
### Cookie Stealing
Cookies are client side assets, this means that even though they might be created on the server, they are stored in the client's machine, so, if an attacker compromises a client's cookie, they might be able to gain access to the server while pretending to be that client.