# ffuf
ffuf is a brute forcing Fast web fuzzer written in Go. ffuf can help brute force many web related requests.
ffuf stands for ``Fuzz Faster U Fool``
[GitHub Page](https://github.com/ffuf/ffuf) 
## Getting Started with ffuf
the simplest way to use fuzz is to provide a url, a wordlist and a fuzzing argument.
### common arguments
- ``-w`` specify the wordlist to use, you can follow the path with colon ``:`` and then followed by the fuzzed name (default is ``FUZZ``), can specify multiple wordlists for multiple fuzz names
- ``-u`` specify the url to fuzz could also include the keyword for the argument to fuzz
- ``-H`` the header, can specify multiple headers
- ``-X`` the HTTP method (get, post, etc)
- ``-d`` POST data, can specify multiple data
- ``-fs`` filter by response size
### common commands
usually the same task is accomplished with the same command and only changing the data or url or wordlists, so these are some of the most known ffuf commands.
>**NOTE:** check the [FFUF Tips and Tricks](https://github.com/tamimhasan404/FFUF-Tips-And-Tricks) for more information

#### SubDomaine fuzzing
> ffuf -c -w `wordlist_path` -u http://domaine_name -H "Host:`FUZZ`.domaine_name" 
> this command would sometime need the correct size to know if the operation was successful or not. 

> ffuf -c -w `wordlist_path` -u http://FUZZ.domain_name
> this may not work properly