# Brute Force
Brute forcing is the process of trying to guess the correct input (usually password).
there are many variations of this techniques, but usually it involves automating the guessing process with a generated input.
depending on the input size, Brute Forcing can take too long and can be impossible to perform (12 character complex password would take a month to brute force with current computational power), so normal Brute Forcing is not always applicable, so instead, people would usually use some variation of brute forcing, consisting of trying, not EVERY, but a collection of possible entries, this is called a Dictionary attack, where you have a list of possible answers that you try instead of trying every possible answer.
in most cases a well prepared dictionary can save you weeks of brute forcing.
The way of creating a Rainbow list (the list of input) can be different from one attack to the next.
some of the ways of choosing the rainbow list
## Using [[data dumps]] 
people think alike
many people use the same passwords, either different people use the same password, or the same person uses the same password on different websites.
>**NOTE:** If a person's credentials are compromised, there is a big chance that those credentials are used in other platforms, so it could be useful to try the password of that person, or even different variations of it, there are tools to make rainbow lists with variations of a word or phrase.
>**NOTE:** if your credentials are compromised, make sure to change them, change your credentials regularly either way, pick different credentials for different platforms (a password manager can help with this), use two factor authentication, use complex passwords, do not save your password in your browser as browsers can be hacked

many pre prepared rainbow lists are already available on the internet, with [[kali linux]] already coming with many lists pre installed. so those can be a good starting point.

## [[OSINT]]
In order to easily remember passwords, people have a tendency to use personal information in their passwords (names, dates, favourite things.) and so, collecting information on the target using [[OSINT]] helps with creating custom made rainbow lists with variations of the information provided
>**NOTE:** there are already tools that help with this process, some tools you can input the personal information of a target, and it will randomize a list of possible passwords that you can use as a rainbow list

## found exploits
When a system is compromised, there is a chance that credentials are reused across the network, so it's good to create a list of the compromised credentials in a network and try it in other machines/services in the network as well. 
>**NOTE:** sometimes developers would leave credentials lying around in different files, git history, log files, databases, comments, random files; so it's important to be aware of how and where to fish for information.