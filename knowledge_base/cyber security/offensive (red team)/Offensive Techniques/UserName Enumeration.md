# Username Enumeration
This is the process of identifying when a server sends back a specific response when we give it an existing username (easiest way is through the signup page), then we use a combination of [[Brute Force]] and guessing to figure out the correct usernames based on this response.
some excellent tools for this include
- [[ffuf]]
- [[Burp Suite]]
Consider automating the username enumeration process, by the end of this, you could have a list of the valid usernames, that can narrow down the future steps of getting the rest of the authentication (passwords)
> **NOTE:** As with most brute force like processes, this process can take a really long time, so it might be useful to do it as part of multi tasking as it runs in the background while you do something else.