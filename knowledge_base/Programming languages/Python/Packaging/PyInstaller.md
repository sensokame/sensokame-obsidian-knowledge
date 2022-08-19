# PyInstaller
PyInstaller is a python library that can be used to create python packages, the packages can extend from normal python package to an executable.

## Tricks with PyInstaller
>**NOTE:** when using --one-file tag to create executables, PyInstaller would bundle all the dependencies and a lot of files which can lead to big size files


- to reduce the file size, we can use [UPX](https://github.com/upx/upx) tool which can be specified with PyInstaller command line using the tag --upx-dir
- another trick to reduce file size, is to use virtual environment which may reduce the number of libraries being bundled with the executable