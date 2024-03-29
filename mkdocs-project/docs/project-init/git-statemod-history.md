# Initial Project Setup / Git StateMod History #

StateMod code was at version 15.00.01 when the OpenCDSS GitHub repository was initialized.
A recent history of versions was saved in the GitHub repository in order to archive several versions
and work out issues in the development environment.
The focus on the repository initialization was source code, makefile, and compiling on Windows and Linux with `gfortran`.
Documentation and test files will be saved in the repository as additional time is spent reviewing and cleaning up files.

Legacy StateMod code versions utilize a Lahey 95 compiler.
Compiling uses a makefile approach where the executable file depends on object files and object files depend on source files.
Because the StateMod code files are not organized in libraries, the makefile can be relatively straightforward
and simply needs to compile each source file into an object file, and link the object file into the final executable.
Migration of legacy snapshots of StateMod consists of the steps described in this page.
The process was repeated for the following StateMod versions in order to bracket recent work done by Jim Brannon (version 14.01.01)
and Ray Bennett (through versions 15.00.01).  The following list also indicates whether an executable is archived that
can be used for testing.

* 13.00.03 (`Statem/Forwell/for13_0003` folder, `StateMod13_0003` executable)
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder, `StateMod14_0204` executable)
* 14.02.06 (`Statem/Forwell/for14_0206` folder, no executable archived)
* 14.02.07 (`Statem/Forwell/for14_0207` folder, `StateMod14_0207`, executable)
* 14.02.08 (`Statem/Forwell/for14_0208` folder, `StateMod14_0208`, executable)
* 14.02.09 (`Statem/Forwell/for14_0209` folder, `StateMod14_0209`, executable)
* 14.02.11 (`Statem/Forwell/for14_0211` folder, `StateMod14_0211`, executable)
* 14.02.14 (`Statem/Forwell/for14_0214` folder, `StateMod14_0214`, executable)
* 14.02.22 (`Statem/Forwell/For14_0222` folder, `StateMod14_0222`, no executable archived)
* 14.02.23 (`Statem/Forwell/for14_0223` folder, `StateMod14_0223`, executable)
* 14.02.24 (`Statem/Forwell/for14_0224` folder, `StateMod14_0224`, executable)
* 15.00.00 (`Statem/Forwell/for15_0000` folder, `StateMod15_0000`, executable)
* 15.00.01 (`Statem/Forwell` folder, `StateMod15_0001` executable)

The following sections are included in this documentation and describe steps repeated for each code snapshot:

* [Create a Working Copy of a Version](#create-a-working-copy-of-a-version) - copy original source files to allow cleanup
* [Rename Files to Lowercase and remove CTRL-Z](#rename-files-to-lowercase-and-remove-ctrl-z) - needed to simplify comparison and for consistency
* [Cleanup End of Line Issues](#cleanup-end-of-line-issues) - ensure consistent line endings in working files
* [Compare File Lists](#compare-file-lists) - confirm that files are not left out or included by accident
* [Copy Source files to Clean Folder](#copy-source-files-to-clean-folder) - make clean copy of only needed files
* [Compare Code with Previous Version](#compare-code-with-previous-version) - make sure there are no major busts in the migration
* [Copy Files to Git Working Files](#copy-files-to-git-working-files) - copy files to the development environment
* [Confirm Compile using Makefile](#confirm-compile-using-makefile) - confirm that an executable can be created
* [Run Automated Tests](#run-automated-tests) - test the executable to confirm functionality
* [Commit Reviewed Code to Repository](#commit-reviewed-code-to-repository) - save the version in the repository

----

## Create a Working Copy of a Version ##

The StateMod files provided by Ray Bennett exist in folders with names similar to `Statem/Forwell/for13_0003`,
which corresponds to version 13.00.03.
The folder was copied to a working folder in Git Bash using the following command, which retains file modification dates:

```sh
cp -rp for13_0003 for13_0003_work
```

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + only source files, AUTOMAKE, and executable
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + only source files, AUTOMAKE, and executable
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + only source files, no AUTOMAKE, and executable
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + only source files, no AUTOMAKE, executable
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + only source files, AUTOMAKE, and executable
* 15.00.01 (`Statem/Forwell` folder)
    + focus on source files and AUTOMAKE

## Rename Files to Lowercase and remove CTRL-Z ##

The 14.01.01 version that was previously saved in GitHub introduced the convention of using all lowercase filenames for source files.
The legacy code used mixed convention of Pascal case (e.g., `AccDiv.for`) some uppercase filenames (e.g., `RETURN.for`),
and some lowercase (e.g., `adjcase.for`).
The convention of all lowercase filenames was adopted for the OpenCDSS repository to promote consistency in the data load and allow direct comparison of files.
The `build-util/git-init/rename-lowercase-for.sh` script was run in a snapshot working folder to rename the files.
The script also removes Ctrl-Z characters from the end of the file, if the character is found in a file.
CTRL-Z characters were used in older MS-DOS files to indicate end of file but are no longer needed and
if allowed to remain cause differences to be shown when comparing files.

Renaming the `common.inc` file, which specifies all of the common block array sizes,
is not an issue.  A review of all `include` statements indicates that the following is used throughout the code,
compatible with the lowercase name:

```txt
     include `common.inc`
```

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + 251 `*.for` files
    + `common.inc`
    + many files had Ctrl-Z character
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + 253 `*.for` files
    + `common.inc`
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + 253 `*.for` files
    + `common.inc`
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + 253 `*.for` files
    + `common.inc`
* 15.00.01 (`Statem/Forwell` folder)
    + 253 `*.for` files
    + `common.inc`

## Cleanup End of Line Issues ##

A common issue is that file end of line characters are problematic due to different standards for different operating systems
Windows uses CR+LF and Linux uses LF.
The script `build-util/git-init/count-lineend.sh` was run to count line endings for Windows (`CRLF`) and Linux (`LF`).
Inconsistencies were addressed so that each file has consistent end of line character within the file
and that all source files in the folder have consistent end of line characters.
Because Git Bash was used as the shell for Git operations and other manipulation tasks,

The main issues are to avoid different end of line within the same file, and to ensure that the repository always uses
consistent end of line representation.  The repository issue is addressed by using a `.gitattribues` file with `* text=auto`.
Consistency of line endings within files was reviewed and fixed as noted below.
If line endings in a file are consistent, then software tools like editors should keep the same line endings when
new content is added.
The following image illustrates the Eclipse setting that is used to ensure that
new files will have the line ending for the native operating system (*** Window / Preferences / General / Workspace ***).
The setting is generally defaulted for the current operating system and should not need to be changed.
Once a file is created, the editor detects the newline and will continue to use.

![Eclipse newline preferences](git-statemod-history-images/eclipse-newline-preference.png)

To minimize end of line issues in the repository, issues were detected using the script described above and 
then line end characters were adjusted to be consistent.
The original StateMod files use Windows-style CRLF line ending, although this will have changed if a
GitHub bash script modified the file (for example `tr` used to remove CTRL-Z characters).
The most important issue is that the line endings in each file need to be consistent within the file
so that editing tools can properly detect the pattern and retain consistency of line endings in the file.

Most of the files were converted to lowercase filename or had CTRL-Z removed in a shell script in Git Bash
and therefore were rewritten with `LF` line endings.
The remaining files appear to have `CRLF` endings and no end of line for the last line.
It does not appear possible to add a newline at the end of the last line when `LF` or `CRLF` is used
(vim -b and notepad++ don't do it).  Therefore use the solution in the following post, first by running `dos2unix` on the file in question:

[Stack Overflow one-liner to add end of line](https://unix.stackexchange.com/questions/31947/how-to-add-a-newline-to-the-end-of-a-file)

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `calldat.for`
        - `chkrivrf.for`
        - `chkver.for`
        - `common.inc`
        - `dayrate.for`
        - `directby.for`
        - `divalt.for`
        - `getrig.for`
        - `outgvc.for`
        - `powresp.for`
        - `rtnmax.for`
        - `splatte.for`
        - `takout.for`
    + `LF` files where end of line on last line was manually added to last line in file:
        - `comment.for`
        - `divrplp2.for`
        - `geteomx.for`
        - `getopr.for`
        - `getplnr.for`
        - `getplnw.for`
        - `getrch.for`
        - `oprinout.for`
        - `outrch.for`
        - `setcarl.for`
        - `setloss.for`
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed
* 15.00.01 (`Statem/Forwell` folder)
    + `CRLF` files where `dos2unix` was run and end of line on last line was manually added to last line in file:
        - `common.inc`
    + most files use CRLF because only file rename was needed

## Compare File Lists ##

The top-level `AUTOMAKE.RSP` contain the list of `.OBJ` object files that are linked by the Lahey compiler to create the `statemod.exe` executable.
This file is not included in snapshot folders, which typically only contain a list of source files (Fortran and include files).

Version 14.01.01 included support for `gfortran` and Linux and used `makefile_linux` and `makefile_windows` to compile,
with the different versions used to accommodate the different path separator characters in `getpath.for` and `setpath.for` subroutines.
The makefiles contain a list of `.o` object files to create the `statemod.exe` executable.

The following file lists were compared using Git Bash `diff` to ensure consistency:

* lowercase filename list `automake-for-filelist.txt` generated from `AUTOMAKE.RSP`, created by the `automake-to-filelist.sh` script run in the main `Forwell` folder
* lowercase filename list `filelist-for.txt` generated from folder listing after running `rename-lowercase-for.sh` in a snapshot working folder
* lowercase filename list `makefile_windows-for-filelist.txt` generated from `makefile_windows`, created by the `makefile-to-filelist.sh` script run in the main `Forwell` folder

In particular, differences for the last file indicates that the `makefile_windows` is not correct for a specific version and will
need to be modified to compile the specific version.

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + most recent `makefile_windows` file list has gfortran and windows specific files but change to use legacy files
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
    + new files are `directwr.for`, `divimpr2.for`
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + no `AUTOMAKE.RSP` but folder listing is as before
    + therefore, use the same makefile as previous and adjust
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + no `AUTOMAKE.RSP` but folder listing is as before
    + therefore, use the same makefile as previous and adjust
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust
* 15.00.01 (`Statem/Forwell` folder)
    + file list from `AUTOMAKE.RSP` and folder listing match
    + therefore, use the same makefile as previous and adjust

## Copy Source files to Clean Folder ##

The files modified in previous steps were copied to a folder to prepare for the project, using a folder similar to `for13_0003_work2`,
where only the needed files are copied.

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + Keep Lahey compiler control files as a historical reference
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + No issues
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + No issues
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + No issues
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + No issues
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + No issues
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + No issues
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + No issues
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + No issues
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + No issues
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + Remove `AM.bat` and `AMTEMP.BAT`
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + No issues
* 15.00.01 (`Statem/Forwell` folder)
    + Copied `*.for`, `*.FOR`, `*.inc`, `AUTOMAKE.RSP`, `automake.fig`

## Compare Code with Previous Version ##

A simple cross-check was performed to confirm that changes from one version to another were reasonable.
This ensured that no major global change or migration oversight occurred.
The [Kdiff3 software](../dev-env/kdiff3.md) was used to compare the current version and previous version,
using the "work" folder contents.

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + No comparison since first version processed
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + Compared with 13.00.03, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 175 files the same, 82 different
    + Changes include array bounds changes from Jim Brannon (Ray must have coordinated changes with Jim)
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + Compared with 14.02.04, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 247 files the same, 10 different, changes appear to be focused
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + Compared with 14.02.06, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 251 files the same, 6 different, changes appear to be focused
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + Compared with 14.02.07, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 250 files the same, 7 different, changes appear to be focused
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + Compared with 14.02.08, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 251 files the same, 6 different, changes appear to be focused
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + Compared with 14.02.09, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 247 files the same, 10 different, changes appear to be focused
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + Compared with 14.02.11, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 251 files the same, 6 different, changes appear to be focused
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + Compared with 14.02.14, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 229 files the same, 28 different, changes appear to be focused
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + Compared with 14.02.22, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 250 files the same, 8 different, changes appear to be focused
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + Compared with 14.02.23, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 247 files the same, 8 different, changes appear to be focused
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + Compared with 14.02.24, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 234 files the same, 23 different, changes appear to be focused
* 15.00.01 (`Statem/Forwell` folder)
    + Compared with 15.00.00, converted all to Linux `LF` line endings with `dos2unix` to simplify comparison
    + 252 files the same, 5 different, changes appear to be focused

## Copy Files to Git Working Files ##

The source files (omitting unnecessary files) were copied from the above working folder (e.g., `for13_0204_work2`)
to the repository working files in `src/main/fortran` so that the following steps can be completed.
Prior to copying a branch was created, for example:

```sh
$ git branch 14.02.04-gfortran
$ git checkout 14.02.04-gfortran
```

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + Ray Bennett indicated that dayrate.for and daily.inc are not used but include in the repository initial snapshot
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + No issues copying
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + No issues copying
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + No issues copying
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + No issues copying
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + No issues copying
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + No issues copying
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + No issues copying
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + No issues copying
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + No issues copying
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + No issues copying
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + No issues copying
* 15.00.01 (`Statem/Forwell` folder)
    + No issues copying

## Confirm Compile using Makefile ##

The `makefile_windows` from the latest Jim Brannon `fixmorearraybounderrors` branch was used as the initial `makefile` for each version
loaded into GitHub.  The makefile was updated for each commit to adjust file lists noted in a previous step
and result in working compilation process.
The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + code did not compile due to syntax issues - need to jump to next version to incorporate `gfortran` changes
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + Add new files directwr.for and divimpr2.for to makefile
    + Code initially compiles but there are undefined references that were resolved:
        - `getcl_1 in `parse` - resolve by using `parse_gfortran.for` from Jim Brannon work and
          update the general `makefile` to handle
        - `date_` and `time_` in `dattim` - resolve by using `dattim_gfortran.for` from Jim Brannon work and
          update the general `makefile` to handle
    + Since the above is implemented, also enabled 
    + Also confirm makefile dependency list on `common.inc`
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + No new files
    + Compiled successfully with previous makefile
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + No new files
    + Compiled successfully with previous makefile
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + No new files
    + Compiled successfully with previous makefile
* 15.00.01 (`Statem/Forwell` folder)
    + No new files
    + Compiled successfully with previous makefile

## Run Automated Tests ##

The StateMod code archive contains significant example files (`ex1`, etc.), each of which theoretically should run and
produce expected results.  However, these examples were not in the past structured as formal automated tests.
Additionally, Wilson Water Group indicates that testing typically consists of running StateMod on a complete dataset
and looking for issues, such as a bust in the water balance report.

To facilitate automated testing in OpenCDSS requires a more rigorous and efficient approach.
Therefore, a separate repository `cdss-app-statemod-fortran-test` was created to manage automated tests.
A separate repository is used because the files are extensive and use different technologies to run (Python).

Additional Fortran unit tests may be added to test specific subroutines.

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + automated tests are not yet in place
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + automated tests are not yet in place
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + automated tests are not yet in place
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + automated tests are not yet in place
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + automated tests are not yet in place
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + automated tests are not yet in place
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + automated tests are not yet in place
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + automated tests are not yet in place
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + automated tests are not yet in place
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + automated tests are not yet in place
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + automated tests are not yet in place
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + automated tests are not yet in place
* 15.00.01 (`Statem/Forwell` folder)
    + automated tests are not yet in place

## Commit Reviewed Code to Repository ##

The code files were committed to the repository.
This generally followed the steps, assuming branch is `14.02.04-gfortran`:

1. Previous step created branch and checked it out.
2. Check files that have changed:  `git status` (note that it may show many files for some reason, line endings?)
3. Add all changes on the branch, for example:  `git add -A` (this will show only the subset of files that have really changed)
4. Commit all changes on the branch, for example:  `git commit`
5. Check out the master:  `git checkout master`
6. Merge the branch into the master:  `git merge --no-ff 14.02.04-gfortran`
7. Push the changes to GitHub:  `git push`

The following is noted:

* 13.00.03 (`Statem/Forwell/for13_0003` folder)
    + committed and tagged as `StateMod-13.00.01-initial`
* 14.00.01 (`Statem/Forwell/for14_0001` folder)
    + skipped because this is Jim Brannon's version, which needs to be compared and merged at end
* 14.02.04 (`Statem/Forwell/for14_0204` folder)
    + committed and tagged as `StateMod-14.02.04-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.06 (`Statem/Forwell/for14_0206` folder)
    + committed and tagged as `StateMod-14.02.06-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.07 (`Statem/Forwell/for14_0207` folder)
    + committed and tagged as `StateMod-14.02.07-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.08 (`Statem/Forwell/for14_0208` folder)
    + committed and tagged as `StateMod-14.02.08-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.09 (`Statem/Forwell/for14_0209` folder)
    + committed and tagged as `StateMod-14.02.09-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.11 (`Statem/Forwell/for14_0211` folder)
    + committed and tagged as `StateMod-14.02.11-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.14 (`Statem/Forwell/for14_0214` folder)
    + committed and tagged as `StateMod-14.02.14-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.22 (`Statem/Forwell/For14_0222` folder)
    + committed and tagged as `StateMod-14.02.22-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.23 (`Statem/Forwell/for14_0223` folder)
    + committed and tagged as `StateMod-14.02.23-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 14.02.24 (`Statem/Forwell/for14_0224` folder)
    + committed and tagged as `StateMod-14.02.24-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 15.00.00 (`Statem/Forwell/for15_0000` folder)
    + committed and tagged as `StateMod-15.00.00-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
* 15.00.01 (`Statem/Forwell` folder)
    + committed and tagged as `StateMod-15.00.01-untested`
    + spot check GitHub `statem.for` file history and looks reasonable
