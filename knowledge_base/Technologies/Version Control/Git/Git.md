# Git
Git is a powerful open source version control tool, arguably the most famous and most used one
> **NOTE:** [GitHub Page](https://github.com/git/git) (Note that the Github is a publish only repo, contributions can be done elsewhere)
>**NOTE:** git has a collection of  commands, each with its own parameters and arguments, a normal git command execution is as follows `git subcommand args` a more comprehensive list of commands can be found in the [git page](https://git-scm.com/docs/git)

## Getting started with git
Usually the starting point with git is to clone or create a new git repository.
>**NOTE:** A Git repository is basically a folder with a .git folder, this .git folder is read by git application to execute the git workflow commands
>**NOTE:** It is unwise to manually change items in .git folder, but there may come a time where you need to do so (example case: lock files refusing to be deleted)

### Creating a git repository
To create a git repository we need to init the repository with git
>git init . 

the command `git init` takes as input the folder where to init the git repo in with the most common case being the current directory `.`
usually after initing the git repo we need to set one or multiple remotes, we can see this later in this document.

### Cloning a git repository
The second most common git command is the clone command, for this we need a remote
>git clone remote_url

the command `git clone` takes as input the remote url from where to clone the git repo
this will clone the remote repo into the current directory, additional parameters can be set like the output path, this can be done with the `-C` parameter followed with a path
>**NOTE:** git clone will always create a new folder with the repo name in the output path

> **NOTE:** git usually works with the saved default credentials; when cloning, to specify a different username, can be done using `git clone https://username@git_remote`

### Setting up remotes
Usually, when first cloning a git repo, a remote by the name ``origin`` is created, we can add other remotes or modify the existing remotes using the ``remote`` command of git

The most basic remote command is 
>`git remote add name url`

where we add the name of the new remote and the url