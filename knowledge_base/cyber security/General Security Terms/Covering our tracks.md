# Covering our tracks
This is a very important part of hacking, specially with grey or black hat hacking, usually systems keep extensive logs of what happens with the system. so unless one is being careful, it is easy to get discovered and/or get into legal trouble.
Depending on the level of anonymity one wants to keep, different actions must be taken.
## Getting Started
In case clean up after exploitation fails for some reason (failing to gain privileged escalation for example) it important to make it difficult to be found even through our online fingerprints. this can be done in a number of ways.
- using [[Proxy]] (usually proxy chaining is safer than a single proxy)
- using [[VPN]] (some private VPNs could disclose your identity if pressed by the authorities, so be careful which [[VPN]] to chose)
- using [[Tor]] (controlling the entry and exit nodes in TOR means that the person is capable of decrypting the data and finding out who you are)
- Not using services that track activities, such as social media or google services.
- Not disclosing personal information, such as real names, addresses, phone numbers, etc.
- using password manager with strong passwords.
## Post exploitation clean-up
Once [[Privilege escalation]] is attained, it is important to cover our tracks as we leave the system, just in case, we do this through the following
- deleting or altering log files (this includes the ability to know which applications have captured our activity, where those log files exist and how to alter them)
> **NOTE:** most systems nowadays are packed with an [[intrusion detection system]], so it is important to be able to recognize these systems and learn how to deal with them (either get around them or simply cover our tracks once we leave)

Sometimes, hackers would leave a backdoor once they gain access to a system in order to go back easier in the next time. this can make the hackers life much easier, but could endanger the hacker as the backdoor if detected can serve as a beacon to finding him.
>**NOTE:** an important part of a good exploitation automation tool is automatic self clean up. some tools like [[pwncat]] would attempt to do some sort of clean up after a session is performed
