# Development Tasks / Releasing #

Releasing the software consists of compiling StateMod into an executable and packaging into an installer that can be distributed.
The StateMod executable may be further packaged with StateMod datasets and StateMod GUI,
although this documentation does not currently describe those steps.

This documentation contains the following sections:

* [Build and Release Checklist](#build-and-release-checklist)
* [Creating StateMod Installer](#creating-statemod-installer)
* [Releasing StateMod](#releasing-statemod)

---------------------

## Build Checklist ##

Currently there is not a need for StateMod to be built in a continuous integration process because the development team is small.
Consequently the build process is done by the software developers responsible for StateMod testing and release.

The full build process checklist is as follows:

1.  As of version 17.0.0, the software version has 3 parts such as 17.0.0 (parts are **not** padded with extra zeros, as was done previously).
    The version should be incremented accordingly as public releases are made
    based on [Semantic versioning](https://semver.org/).
    If necessary, add a fourth part such as `.dev1`, `.dev2`, etc. to indicate development versions that
    are not intended for public use.
2.  Issues in the GitHub repository should be coordinated to decide when a public versioned release should occur.
    Normally a release will be made to fix bugs only and/or to introduce one or more new features.
3.  Recompile the program for release in `src/main/fortran` folder:  `make statemod_release`
4.  Run tests to confirm program accuracy. See the [Testing](testing.md) documentation.
5.  Update the documentation, in particular user documentation and release notes.  See the [Documenting](documenting.md) documentation.
6.  Create the installer. The [Creating StateMod Installer](#creating-statemod-installer)
    section below discusses the installer in more detail.
7.  Publish the new version.  The compiled executable can be distributed.  See the [Releasing StateMod](#releasing-statemod) section below.

## Creating StateMod Installer ##

StateMod software executables are packaged into a zip file by running the following `make` target in the
`src/main/fortran` folder:

```
make installer
```

This runs the `build-util/copy-to-co-dnr-gcp.bash` script,
which creates the zip file, optionally uploads to the OpenCDSS Google Cloud Platform bucket/website,
and optionally creates an updated
[StateMod index page](https://opencdss.state.co.us/statemod/).

## Releasing StateMod ##

The previous section describes how to create and upload a zip file installer for the StateMod executables.
The executables can be packaged into other products as described in the
[Deployed Environment / Overview](../deployed-env/overview.md) documentation.
