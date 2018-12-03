# Development Tasks / Releasing #

Releasing the software consists of compiling StateMod into an executable and packaging into an installer that can be distributed.

**Need to coordinate with WWG on how StateMod should be released.
Also need to evaluate whether to release from the Git Project page, GCP website and/or CDSS website.**

This documentation contains the following sections:

* [Build Checklist](#build-checklist)
* [Creating StateMod Installer](#creating-statemod-installer)
* [Releasing StateMod](#releasing-statemod)

---------------------

## Build Checklist ##

Currently there is not a need for StateMod to be built in a continuous integration process because the development team is small.
Consequently the build process is done by the software developers responsible for StateMod testing and release.

The full build process checklist is as follows:

1. The software version currently has 3 parts such as 15.00.14.
The version should be incremented accordingly as public releases are made.
2. Issues in the GitHub repository should be coordinated to decide when a public versioned release should occur.
3. Recompile the program:
	1. Run `make clean`.
	2. Run `make statemod`.
4. Run tests to confirm program accuracy.
5. Update the documentation, in particular user documentation and release notes.
6. Create the installer.  Currently there is no installer for the model executable and the StateMod GUI software is not packaged with the current executable.
The [Creating StateMod Installer](#creating-statemod-installer)
section below discusses the installer in more detail.
7. Publish the new version.  The compiled executable can be distributed.  See the [Releasing StateMod](#releasing-statemod) section below.

## Creating StateMod Installer ##

StateMod is not currently distributed as an installer.
The executable program that is created from the `gfortran` compiler build process will by default have
a name `statemod-gfortran-32bit.exe`.
This file should renamed with the version, for example `statemod-15.01.23-gfortran-32bit.exe` for distribution.

## Releasing StateMod ##

As indicated above, there is currently no installer. Therefore the executable can be distributed without additional packaging.
To do so, run the `build-util/copy-to-co-dnr-gcp.sh` script from Git Bash.
This will copy the latest compiled executable to the State's Google Cloud Platform storage location,
for the detected and latest version.  Run the script with `-h` to see usage.

