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

To compile StateMod, open an ***MSYS2 64bit / MSYS2 MinGW 64-bit*** window,
which will automatically be configured for software development tools.

Then change to the code location and run the makefile,
replacing `user` with the appropriate user name:

```
> cd /C/Users/user/cdss-dev/StateMod/git-repos/cdss-app-statemod-fortran/src/main/fortran
> make veryclean
> make statemod
```

The executable with name similar to `statemod-17.0.2-gfortran-win-64bit.exe`
is created in the same folder and can be run with model input,
such as in a test folder separate from the code.
The version will match that in the `statem.for` file.

Use the `make help` command to list available `makefile` targets.
The following are the main targets that are useful during development:

**<p style="text-align: center;">
`make` Targets for StateMod
</p>**

| **`makefile` Target**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | **Description** |
| -- | -- |
| `clean` | Remove dynamically created files (but not final executable). |
| `help` | Print help. |
| `installer` | Create the StateMod software installer zip file and optionally upload to GCP. |
| `statemod` | Compile the StateMod executable, recompiling any `.o` if `.for` files are modified.  Same as `statemod_o3` to compile the optimized variant for testing.  **Use for normal development.**
| `statemod_check` | Compile the StateMod executable including all runtime checks. |
| `statemod_o3` | Compile the StateMod executable for optimization level 3 and limited runtime checks.  Use for production release and full testing. |
| `statemod_release` | Do clean compile on `check` and `o3` release variant and copy `o3` variant to plain name without `-o3` for release. **Use to prepare for software release.** |
| `veryclean` | Make the 'clean' target, and also remove the final executable. |
| `veryclean_check` | Needed by `statemod_release`. |
| `veryclean_o3` | Needed by `statemod_release`. |

A typical development session will involve repeating:

1. editing source code
2. `make statemod`
3. Copy the executable to `StateMod` folder of a dataset for testing.  See the [Testing](testing.md) documentation.

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
Note that the current `gfortran` convention is to use a more explicit filename
including the operating system, compiler, and version.

Note that the legacy StateMod Lahey `AM.bat` file has been updated to ignore
`gfortran`-specific source file.  See the following for more information about compiling with Lahey:

* [Lahey Fortran 95 Automake](https://www.lahey.com/docs/lfenthelp/F95UGMUAUTOMAKE.htm)

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
