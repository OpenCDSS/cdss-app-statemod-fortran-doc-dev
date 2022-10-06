# Development Tasks / FAQ for MinGW #

The MinGW environment is intended as a self-contained developer environment for C, Fortran, and other languages.
It is not intended as an operational environment (Cygwin is recommended for that).
MinGW is installed with a number of Unix/Linux system tools to facilitate development work, referred to as MSYS.

Answers to the following questions are provided in this documentation:

* [How do I access MSYS/MinGW programs from the Windows Command Shell?](#how-do-i-access-msysmingw-programs-from-the-windows-command-shell)

------------

## How do I access MSYS/MinGW programs from the Windows Command Shell? ##

Previous versions of MinGW required configuring a Windows command shell.
However, the latest MSYS/MinGW environment ([see Development Environment/Machine](../dev-env/machine.md))
provides command shells in the ***Start / MSYS2*** menu.
Software that is installed using these command shells and MSYS2 installation commands will
be available in the shell windows without additional configuration.

Other Windows programs are also available if in the `PATH`.
