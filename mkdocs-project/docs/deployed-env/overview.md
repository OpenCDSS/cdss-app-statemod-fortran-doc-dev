# Deployed Environment / Overview #

This documentation discusses how StateMod should be deployed into an operational environment.
It is important to keep this target in sight as the end result of software development.
StateMod modelers that are not software developers will only be working in the deployed environment.

Software development occurs using a version-controlled copy of files that are different than the deployed environment.
Ssee [New Developer Setup](../dev-new/overview.md) documentation for how to set up a new developer environment).
Files from the developer environment can be installed to the deployed environment for local testing,

This documentation contains the following sections:

* [Packaging the StateMod Executable with StateMod Dataset](#packaging-the-statemod-executable-with-statemod-dataset)
* [Packaging the StateMod Executable with StateMod GUI](#packaging-the-statemod-executable-with-statemod-gui)
* [StateMod 32 and 64 Bit Executable Considerations](#statemod-32-and-64-bit-executable-considerations)

---------------

## Packaging the StateMod Executable with StateMod Dataset

Each StateMod dataset contains the `StateMod` folder for model input files.
Some CDSS datasets include the StateMod executable with input files to ensure that the correct version
of the software is used with the dataset.
This approach can avoid problems and is recommended for deployment.

As of StateMod 17.0.0, the executable is available on the
[OpenCDSS website](https://opencdss.state.co.us/statemod/) in a zip file.
A specific StateMod executable version can be packaged with a StateMod dataset by
copying the `statemod*.exe` executable file into the dataset `StateMod` folder.
The `statemod.cmd` file can also be packaged with a dataset to provide a general command
for command-line use and to call from the StateMod GUI and other programs.

## Packaging the StateMod Executable with StateMod GUI

**As of 2021-09-10, the StateMod GUI is not actively maintained, with the last update being version 07.01.00 from 2008.
The following information assumes that if StateMod GUI is update,
the information presented below may be useful.**

**As of StateMod 17.0.0, the executable is available on the
[OpenCDSS website](https://opencdss.state.co.us/statemod/) in a zip file.
The executable name contains the version to uniquely identify the software version.
The StateMod executable is also distributed with a general `statemod.cmd` file
that can be used to run the most recent executable, for example from the StateMod GUI.
The StateMod GUI can be updated to use the general `statemod.cmd` program
as the default and can also run the version in a dataset's `StateMod` folder
(if the executable is packaged with a dataset).**

The StateMod executable has been distributed with the StateMod GUI as the `StateMod.exe` file.
See the [CDSS StateMod](https://cdss.colorado.gov/software/statemod) web page.
For Windows, the software defaults to an installation folder: 

```
C:\CDSS\StateModGUI-07.01.00\bin\
    StateMod.exe          StateMod model executable.
    StateModGUI.exe       StateMod GUI launcher executable.
    other files           Other files are used by the GUI.
```

The StateMod GUI software can be updated to use the longer filename and `statemod.cmd`,
or the longer filename can be renamed to the generic name shown above
to use newer StateMod executable version with older StateMod GUI.

## StateMod 32 and 64 Bit Executable Considerations ##

**As of StateMod 17.0.0, the software is distributed as a 64-bit executable.
The following information is for historical purposes only and can be used to confirm whether an executable is 32-bit or 64-bit.**

The StateMod software is a Fortran program that is compiled to a 32-bit static executable using the `gfortran` compiler.
The 32-bit Windows executable will run on 64-bit Windows computers similar to other 32-bit software.
However, compiling and distributing the 64-bit executable is now the default for development and distribution.

See the following resources to understand whether a program has been compiled as a 32-bit or 64-bit executable:

* [10 Ways to Determine if Application is Compiled for 32-bit or 64-bit](https://www.raymond.cc/blog/determine-application-compiled-32-64-bit/)

Based on the above, a useful utility to examine executable properties is the [7zip](https://www.7-zip.org/download.html) software.
Once installed, 7Zip can be used to examine the `statemod.exe` file as follows (the following uses an "el" not "one" 7zip command).
The `CPU = x86` indicates 32-bit, corresponding to i386 computer chips.  A 64-bit executable has `CPU = x64`.

```text
> "C:\Program Files\7-Zip\7zexe" l statemod.exe

7-Zip [64] 16.04 : Copyright (c) 1999-2016 Igor Pavlov : 2016-10-04

Scanning the drive for archives:
1 file, 4587318 bytes (4480 KiB)

Listing archive: statemod.exe

--
Path = statemod.exe
Type = PE
Physical Size = 4587318
CPU = x86
Characteristics = Executable 32-bit NoRelocs NoLineNums
Created = 2017-01-01 03:14:44
Headers Size = 1024
Checksum = 4635747
Image Size = 596111360
Section Alignment = 4096
File Alignment = 512
Code Size = 2475520
Initialized Data Size = 3134976
Uninitialized Data Size = 591632896
Linker Version = 2.25
OS Version = 4.0
Image Version = 1.0
Subsystem Version = 4.0
Subsystem = Windows CUI
Stack Reserve = 2097152
Stack Commit = 4096
Heap Reserve = 1048576
Heap Commit = 4096
Image Base = 4194304

   Date      Time    Attr         Size   Compressed  Name
   ------------------- ----- ------------ ------------  ------------------------
   2017-01-01 03:14:44 .....      2475520      2475520  .text
   2017-01-01 03:14:44 .....         2560         2560  .data
   2017-01-01 03:14:44 .....       613888       613888  .rdata
   2017-01-01 03:14:44 .....        38912        38912  /4
   2017-01-01 03:14:44 .....            0            0  .bss
   2017-01-01 03:14:44 .....         3072         3072  .idata
   2017-01-01 03:14:44 .....          512          512  .CRT
   2017-01-01 03:14:44 .....          512          512  .tls
   2017-01-01 03:14:44 .....         2048         2048  /14
   2017-01-01 03:14:44 .....       765952       765952  /29
   2017-01-01 03:14:44 .....        16896        16896  /41
   2017-01-01 03:14:44 .....       522240       522240  /55
   2017-01-01 03:14:44 .....         1536         1536  /67
   2017-01-01 03:14:44 .....         1024         1024  /78
   2017-01-01 03:14:44 .....       141622       141622  COFF_SYMBOLS
   ------------------- ----- ------------ ------------  ------------------------
   2017-01-01 03:14:44            4586294      4586294  15 files
```

Another option is to use an editor that can edit a binary file. 
For example, use Windows `Notepad`, `Notepad++`, or Linux shell `vim -b` editors.
Search for the characters `PE` at the top of the file.

* If these characters are followed closely by `L`, then the executable is 32-bit.
* If these characters are followed closely by a `d`, then the executable is 64-bit.
