# Development Environment / Linux Commands #

This documentation provides a summary of useful Linux commands that are used during StateMod development.
Using a command line interface is necessary because the StateMod `gfortran` development
environment uses MinGW Linux environment.

* [Introduction](#introduction)
* [Shell Scripts](#shell-scripts)
* [Linux Command Summary](#linux-command-summary)

--------------------

## Introduction ##

The StateMod development environment uses MinGW, which provides a Linux environment within Windows desktop.
The MinGW environment is provided as a command line terminal window that displays a prompt
and responds to typed commands.
Documentation for each command is available on the internet.
Links are provided in the following documentation and additional documentation can be searched for.

## Shell Scripts ##

In addition to commands, the StateMod development environment makes use of shell scripts for `bash` and `sh` command "shells".
These scripts typically have extension `.bash` and `.sh` to avoid confusion with other Windows files,
but the file extension is not required by Linux.

Programs to run are located by checking the `PATH` environment variable.
This concept is similar on Windows and Linux.
To display the `PATH`, type:

```
echo $PATH
```

If a program or shell script to be run is not found in the `PATH`,
it can be run by typing the path to the file.
If the file is in the current folder, run with `./scriptname`
because the current folder (`.`) is not typically added to the `PATH` for security reasons.

## Linux Command Summary ##

The following table lists common commands that are used during development.
Linux provides many commands to perform common tasks.
Commands often can operate on more than one file, specified as multiple file separated by spaces or use `*` as wildcard in names.
Click on the command name for additional documentation.

| **Command** | **Description** |
| -- | -- |
| [`cat`](https://man7.org/linux/man-pages/man1/cat.1p.html) | Print the contents of a file, for example: `cat filenme` |
| [`cd`](https://man7.org/linux/man-pages/man1/cd.1p.html) | Change directory (folder), for example:<ul><li>`cd` - change to user's home folder</li><li>`cd folder` - change to the specified folder</li><li>`cd ..` - change to the parent folder of the current folder</li><li>`cd ../..` - change up two folder levels</li></ul> |
| [`cygpath`](https://cygwin.com/cygwin-ug-net/cygpath.html) | Convert between Linux and Windows file paths, for example:<ul><li>`cygpath -w ~` - print the Windows location of Linux user's home folder</li><li>`cygpath -w /some/path` - print the Windows location of a Linux folder</li></ul> |
| [`ls`](https://man7.org/linux/man-pages/man1/ls.1.html) | List files, for example:<ul><li>`ls -l` - long listing</li><li>`ls -la` - list all files including hidden files (hidden files have name that start with a period), long output</li><li>`ls folder/path` - list the contents of a folder given its path</li></ul> |
| [`mkdir`](https://man7.org/linux/man-pages/man1/mkdir.1.html) | Make a new directory (folder), for example: `mkdir newfolder` |
| [`pwd`](https://man7.org/linux/man-pages/man1/pwd.1.html) | Print the present working directory (folder).  Although the prompt often shows the directory, it may only show part of the full path. |
| [`rm`](https://man7.org/linux/man-pages/man1/rm.1.html) | Remove one or more files, for example: `rm *.log` |
| [`rmdir`](https://man7.org/linux/man-pages/man1/rmdir.1.html) | Remove one or more directories (folders), for example: `rmdir folder` |
| `which` | Find where a program exists on the system by searching the `PATH` environment variable, for example:  `which gfortran` |
