# Initial Project Setup / GitHub Git Repository #

The initial StateMod code for OpenCDSS is a history of versions maintained by Ray Bennett spanning versions
13.00.03 to 15.00.01.  This sequence brackets changes made by Jim Brannon to enable support for gfortran and Linux.
Jim's changes were implemented in parallel by Ray Bennett but recent changes by Jim may need to be incorporated.
The approach taken for OpenCDSS is to implement a folder structure similar to StateCU.
A new Open Water Foundation repository was created because the OpenCDSS GitHub account was not available at that time.
The OWF repository was later transferred to the OpenCDSS organizational account (November/December, 2018).

This documentation contains the following sections:

* [Prerequisites](#prerequisites)
* [Create a New StateMod Repository on GitHub](#create-a-new-statemod-repository-on-github)
* [Clone Empty GitHub StateMod Repository](#clone-empty-github-statemod-repository)
* [Next Steps](#next-steps)

---------------

## Prerequisites ##

This step requires that the Git software was previously installed as per [Development Environment / Git](../dev-env/git.md) documentation.

## Create a New StateMod Repository on GitHub ##

The private repository [cdss-app-statemod-fortran](https://github.com/OpenWaterFoundation/cdss-app-statemod-fortran) was created using the
GitHub website within the Open Water Foundation organization account.  This established an empty "remote" repository.
Note that accessing this repository now will forward to the OpenCDSS GitHub account.

## Clone Empty GitHub StateMod Repository ##

Git Bash was used to create a local clone of the empty repository.

```sh
$ cd ~/cdss-dev/StateMod/git-repos
$ git clone https://github.com/OpenWaterFoundation/cdss-app-statemod-fortran.git
```

This copies the existing repository to the local computer with repository name `cdss-app-statemod-fortran`.

## Next Steps ##

The next step is to initialize Eclipse workspace and project to receive source files.
This ensures that Eclipse can be used if desired.
