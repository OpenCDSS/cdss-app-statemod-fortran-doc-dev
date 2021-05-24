# Development Tasks / Compiling #

StateMod code is compiled using a "makefile", which defines rules for detecting when a file needs to be recompiled,
based on code dependencies.
The code can be compiled from command line or from the Eclipse IDE.
The Eclipse IDE provides benefits during development but it may be necessary or useful to compile on the command line,
for example, if automating the build process.

This documentation contains the following sections:

* [Compile StateMod on Command Line with `gfortran` Compiler](#compile-statemod-on-command-line-with-gfortran-compiler)
* [Compile StateMod on Command Line with Lahey Compiler](#compile-statemod-on-command-line-with-lahey-compiler)
* [Compile StateMod in Eclipse](#compile-statemod-in-eclipse)

----------------------

## Compile StateMod on Command Line with `gfortran` Compiler##

Compiling on the command line uses the `make` command and `makefile`.

### ![Linux](../images/linux-32.png) Linux ###

Compiling on Linux is similar to Windows.  Use the `make` command targets.

### ![Windows](../images/windows-32.ico) Windows - MinGW ###

StateMod can be compiled on the command line using a ***Start / MSYS2 64bit*** command shell.
Select ***Start / MSYS2 64bit / MYSYS2 MinGW 32-bit*** or ***Start / MSYS2 64bit / MYSYS2 MinGW 64-bit*** command shell that
is appropriate for the executable to be created.

If the standard folder structure is used:

```
> cd            (to change to user's home folder)
> cd cdss-dev/StateMod/git-repos/cdss-app-statemod-fortran/src/main/fortran
> make veryclean
> make statemod
```

The executable `statemod-<version>-gfortran-win-32bit.exe` or
`statemod-<version>-gfortran-win-64bit.exe`
is created in the same folder and can copied to a location that is
convenient to run with model dataset.

### ![Windows](../images/windows-32.ico) Windows - MinGW (Old Environment) ###

**These instructions are for the initial environment.  A newer environment consistent with previous section should be used instead.**

To compile StateMod on the command line it is first necessary to configure the environment to run the compiler.
Open a Windows command prompt window and change to the folder where the setup script exists.
Then run the `build-util/mingw/setup-mingw-env.bat` batch file to configure the MinGW environment (note that setting up the environment in the window only needs
to be done once after the window is opened).

```
> C:
> cd \Users\user\cdss-dev\StateMod\git-repos\cdss-app-statemod-fortran\build-util\mingw
> setup-mingw-env.bat
```

Then change to the code location and run the makefile:

```
> C:
> cd \Users\user\cdss-dev\StateMod\git-repos\cdss-app-statemod-fortran\src\main\fortran
> make clean
> make statemod
```

The executable `statemod-gfortran-32bit.exe` is created in the same folder and can be run with model input,
typically in a test folder separate from the code folder.

## Compile StateMod on Command Line with Lahey Compiler ##

The ability to compile StateMod with the Lahey compiler that has previously been used
has been retained to facilitate contributions by existing developers
and to allow comparison of Lahey and `gfortran` versions of the StateMod executable program.

First open a Windows command prompt window.
It is assumed that the Lahey compiler environment is configured and that the compiler software
is found in the `PATH` (not covered in this documentation).

Then change to the code location and run the `AM` batch file:

```
> C:
> cd \Users\user\cdss-dev\StateMod\git-repos\cdss-app-statemod-fortran\src\main\fortran
> AM
```

The executable `statemod.exe` is created in the same folder and can be run with model input,
typically in a test folder separate from the code folder.
***TODO smalers 2017-11-30 need to output as `statemod-lahey-32bit.exe`.***

Note that the legacy StateMod Lahey `AM.bat` file has been updated to ignore
`gfortran`-specific source file.  See the following for more information about compiling with Lahey:

* [Lahey Fortran 95 Automake](http://www.lahey.com/docs/lfenthelp/F95UGMUAUTOMAKE.htm)

## Compile StateMod in Eclipse ##

***Note that although the StateMod project is configured to work with Eclipse,
the initial focus is command-line compilation.
This documentation has not been updated to reflect latest MSYS2/MinGW environment.***

### ![Linux](../images/linux-32.png) Linux ###

This section will be completed when resources are available for Linux development and testing.

### ![Windows](../images/windows-32.ico) Windows - MinGW ###

To compile StateMod in Eclipse, start Eclipse with the run script `run-eclipse-statemod-mingw.bat` as shown below.
This script automatically runs the MinGW setup script described in the previous section,
which will configure the compiler environment if necessary.


```
> C:
> cd \Users\user\cdss-dev\StateMod\git-repos\cdss-app-statemod-fortran\build-util\eclipse
> run-eclipse-statemod-mingw.bat
```

Then right-click in the ***Project Explorer*** area and select ***Make / Targets***.  Then select ***Build...***.  Then select a target and press the ***Build*** button.

Review the output in the ***Console*** area to see if any errors occurred.
