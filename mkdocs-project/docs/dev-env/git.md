# Development Environment / Git #

Git software and GitHub cloud-hosted repositories are used for version control.
CDSS software developers are expected to follow Git best practices that have been established for CDSS software development.

Git software must be installed and configured on the computer in order to use Git for version control.
The [Eclipse IDE](eclipse.md), which is an option for interactive development, provides Git integration;
however, Git command line tools can also be used independent of Eclipse.
The Git tools described below are recommended, although developers may use other Git client software if they have preferences.
Many of the examples in this documentation use command line Git (Git Bash) for clarity and consistency.

Git integration with other tools such as text editors is not currently documented but may be added in the future.

Refer to the [CDSS / Learn Git](http://opencdss.state.co.us/cdss-learn-git/)
documentation for information about installing, configuring, and using Git software within the CDSS environment.

Currently, for StateMod development on Windows,
it is recommended to install Git for Windows and use a Git Bash window to run Git commands.
It is possible to install Git within the MSys2 MinGW environment but the process has not been tested or documented.
Because both Git for Windows and MSYS2 use MinGW, the command line environments are consistent
for file permissions, text file end of line, etc.
Using Git Bash requires changing to the `/c/Users/someuser/...` folders to run Git commands on StateMod files
rather than `/home/someuser`, for example.
