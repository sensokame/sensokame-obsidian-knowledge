# RAT
Remote access trojans (RATs) are **malware designed to allow an attacker to remotely control an infected computer**. Once the RAT is running on a compromised system, the attacker can send commands to it and receive data back in response.
Usually the attacker finds a way to make the victim install the RAT on the machine since RATs need elevated [[privelages]], so RATs are usually combined with other techniques (such as [[Phishing]]) to make the victim execute them with elevated [[privelages]]

some of the well known remote control software out there had humble beginnings as RATs with team viewer being the most famous example. and in a way, a RAT is just a very quiet remote control software.

### Revenge RAT
Revenge RAT is a simple and freely available Remote Access Trojan that automatically gathers system information before allowing threat actors to remotely access system components such as webcams, microphones, and various other utilities

### RAT post exploitations
RATs are usually used in concurrence with [[Command and control]] centers, once a RAT gets access to a system, it phones back home and the machine gets added to the database of zombie machines that the attacker has access to.

### Detecting RATs 
RATs are usually built with promescuity in mind, a RAT once installed can be extremely difficult to find and get rid of. 
The best Techniques of getting rid of RATs in my opinion would be 
- to perform routine data wipes and system resets.
- avoid downloading and executing non trusted files.
- avoid malicious websites
- keeping the [[antivirus]] up to date
- routinly check which files run at startup to check if there is something you don't recognize (Autorun.exe could help in this) 

> but this is still not a sure way since RATs are very good at hiding so the best bet is to just perform regular data wipes (don't get too attached to your files)

in theory it is possible to detect a RAT by its network activity, since a RAT needs to phone back home, you can see when there is weird network activity (unkown ip addresses), but a well made RAT would be very difficult to detect in this way, since they can mask their activity or find ways around detection.

