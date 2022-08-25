# Nox
_nox_ is a command-line tool that automates testing in multiple _Python_ environments.
[nox startup page](https://nox.thea.codes/en/stable/)
[nox GitHub page](https://github.com/wntrblm/nox)
## Installing Nox
Nox is simply installed via the python package manager, pip
`pip install --upgrade nox`
## Getting started with Nox
the way to get started with nox is to create a noxfile.py file in the package folder.
the noxfile defines sessions using the nox defined decorator `@nox.sessions`
simply decorate a the functions with this decorator, and pass as argument the session object, then you can use the session methods to execute desired commands

a simple example nox file
```python
import nox

@nox.session
def tests(session):
    session.install('pytest')
    session.run('pytest')

@nox.session
def lint(session):
    session.install('flake8')
    session.run('flake8', '--import-order-style', 'google')
```

This nox file defines two sessions, tests and lint, each session has two main phases
- the install phase which collects the python library names and installs them using ``pip install``
- the run phase which takes the input param as array of arguments and executes them
>**NOTE:** the first argument is the command to execute with the following arguments being that command argument.

After defining all the desired sessions. it is enough to run ``nox`` (if nox executable is found in the system path) and the sessions will be identified and ran sequentially.
>**NOTE:** to run only one session, we can run nox with the `-e` argument followed by the name of the session, example: `nox -e tests`

## Using nox
- nox can be used in addition to other [[DevOps]] tools to automate tasks such as running python tests, creating packages and so on.

- Note that, for for every session, nox will create a python [[virtualenv]] with the appropriate interpreter, install the dependencies and run the commands in order. this means that the session has a clean python environment and will not pack any additional dependencies.

- if one is not sure if nox is in the system path or not, just as any other python module, nox can be called from python using the `-m` argument, example ``python -m nox``
