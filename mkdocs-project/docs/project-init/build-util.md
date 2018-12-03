# Initial Project Setup / Build Utility Scripts #

This documentation references a number of build utility scripts.
These scripts are saved in the repository to help developers be efficient,
assuming that they have set up the development environment as per this documentation.

This documentation includes the following sections:

* [Build Utility Script Location](#build-utility-script-location)
* [Script to Configure MinGW Environment - `setup-mingw-env`](#script-to-configure-mingw-environment-setup-mingw-env)
* [Script to Run Eclipse - `run-eclipse-statemod`](#script-to-run-eclipse-run-eclipse-statemod-mingw)

----------

## Build Utility Script Location ##

The build utilities are located in the `build-util` folder in the repository.

For ![Linux](../images/linux-32.png) Linux:  `~/cdss-dev/StateMod/git-repos/cdss-app-statemod-fortran/build-util`.

For ![Windows](../images/windows-32.ico) Windows:  `C:\Users\user\cdss-dev\StateMod\git-repos\cdss-app-statemod-fortran\build-util`.

For Windows the folder structure is similar to the following:

```txt
C:/Users/user/
  cdss-dev/
    StateMod/
      git-repos/
        cdss-app-statemod-fortran/
          build-util/
            eclipse/
              run-eclipse-statemod-mingw.bat
            mingw/
              setup-mingw-env.bat
```

## Script to Configure MinGW Environment - `setup-mingw-env` ##

### ![Windows](../images/windows-32.ico) Windows ###

Run this batch file to configure the MinGW environment so that compilers can be found in the command shell and in eclipse.
This batch file is called by other batch files that use the MinGW environment, such as `run-eclipse-statemod-mingw.bat`.

This batch file is described first in [Development Environment / Machine](../dev-env/machine/) and is located in `build-util/mingw`.

## Script to Run Eclipse - `run-eclipse-statemod-mingw` ##

### ![Windows](../images/windows-32.ico) Windows ###

Use this batch file to start Eclipse in the MinGW environment.
This batch file calls `setup-mingw-env` before calling Eclipse.

This batch file is described first in [Initial Project Setup / Eclipse Run Script](eclipse-run-script/) and is located in `build-util/eclipse`.
