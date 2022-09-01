# Linux
Linux is a family of open-source [[Unix]]-like operating systems based on the Linux kernel, an operating system kernel first released on September 17, 1991, by Linus Torvalds.
Linux is arguable the most famous open source operating system, with many different distributions created from it, each distribution has something to offer, and depending on your use case, you can chose the distribution that works for you.
It is also easy enough to create your own distribution or to customize the one you have.
## Working with Linux
Linux presents a power house of an operating system with its incredible power of customization, on average, Linux is less user friendly than other operating systems, but offers more control to the user. 
as a developer, most of the work to be done in linux is done via a [[terminal]], there exists some GUI applications for linux, but the [[terminal]] remains the go to choice for most linux based applications.
> Check working with [[Linux Terminal]] for more information on the different commands and syntax

## The Different Linux distributions
as said before, depending on your use case, you can chose the Linux distribution that works for you, here I can mention some of the most famous ones.
### Debian
Debian, also known as Debian GNU/Linux, is a Linux distribution composed of free and open-source software, developed by the community-supported Debian Project. Debian is the father of many other Linux based operating systems. mainly Ubuntu
### Ubuntu
Arguably the most famous Linux distro, Ubuntu is known for its lovely User interface and Great user experience, could be the best beginner friendly Linux distro.
Ubuntu receives regular updates making it even more accessible to more and more people
### Kali
The ``hacking`` operating system, Kali is a Debian based operating system that comes preinstalled with a plethora of tools dedicated towards [[Penetration Tester]](ing), it could be very helpful to get a grasp on how some of these [[Security tools]] work, specially for people who are interested in a career in [[cyber security]] 

## shell and command
as most operating systems, Linux has its own shell and command language called [[bash]], this language lets users get even more powerful control over the operating system, bash is the best language for coding shell scripts that use command-line interface utilities, the most used bash feature is the piping feature which is passing the output of one command to the next. in theory, bash can execute up to 100 code lines.

check the [[bash]] page for what we can do with a Linux bash

## Scripting With Linux
creating scripts can allow the user to automate complex or repetitive processes, the best and easiest way for this is to set the first line of the script to the interpreter of your choice.
this is called a [Shebang](https://bash.cyberciti.biz/guide/Shebang), the most usual value would be `#!/bin/bash`, which means that /bin/bash interpreter will be used when executing this file.
after setting the Shebang, we finish the script, and then to be able to run it directly, we need to set it as executable using the `chmod` linux command
> Example: `chmod +x script.sh`

