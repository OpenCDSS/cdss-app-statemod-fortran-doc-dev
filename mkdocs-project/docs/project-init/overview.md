# Initial Project Setup / Overview #

**This documentation is for historical purposes only.  Refer to current documentation for active project information.**

The Initial Project Setup documentation is a record of how the project was set up the first time.
It is assumed that all software listed in the [Development Environment](../dev-env/overview.md) has been installed,
although the project initialization steps will list each setup step.

This documentation is a useful reference in case the project needs to be reinitialized or other similar projects need to be configured.
Sections of this documentation are also referenced by the [New Developer Setup](../dev-new/overview.md) documentation,
such as configuring the Eclipse workspace.

This documentation includes the following sections:

*   [Background on Code Versions](#background-on-code-versions) - recent code history
*   [Development Folder Structure](#development-folder-structure) - overview of the development files
*   [Eclipse File Location Overview](#eclipse-file-location-overview) - locations of various Eclipse files
*   [Project Initialization Steps](#project-initialization-steps) - steps to initialize the StateMod software project,
    done once and thereafter [New Developer](../dev-new/overview/) instructions apply

----------------

## Background on Code Versions ##

The StateMod code has been under development for over 20 years as part of [CDSS](https://www.colorado.gov/cdss).

Ray Bennett has been the primary StateMod developer, first as an employee of the Colorado Division of Water Resources (CO DWR),
and later as a contractor.
Ray has made changes to StateMod code using a file-based versioning protocol, and multiple versions were used to initialize the Git repository.
The latest code from Ray prior to initializing the Git repository was version 15.00.01.
Jim Brannon (GitHub @jimbrannon), as a State of Colorado employee, and at different times a contractor, contributed to StateMod,
in particular to implement changes necessary for `gfortran` compilation.

The StateMod 14.01.01 code was accessible in a private `statemod-project` GitHub repository under Jim Brannon's GitHub account,
with the last commits to the master branch around September, 2014.
Jim was an employee of CO DWR for part of this time.
Subsequent edits were saved in branch `fixmorearraybounderrors` but were not committed to the master branch.
This repository contains source code, Word documentation, and a few tests, and all source code files are
located in the folder `code/src`.
The repository also contains Eclipse/Photran project files and makefiles.
Significant changes include creating makefiles for Windows and Linux and making changes to
address compiler warnings about array bound issues.

Steve Malers of the Open Water Foundation (OWF)
compared Jim's repository code with the latest code provided by Ray Bennett, as of July, 2017.
Due to the disconnect between Jim Brannon's version (`gfortran` compiler with testing on Windows and Linux)
and Ray Bennett's versions (Lahey 95 compiler focusing on Windows), the approach for OpenCDSS was
to reinitialized a Git/GitHub repository using Ray Bennett's code and load Ray's incremental versions.
This approach retains Ray's historical code consistent with feedback from StateMod modelers,
who have been using StateMod executables compiled using Ray's code.
Rather than wholesale adopt Jim Brannon's 14.01.01 version at that time, Ray appears to have incorporated changes surgically,
with the result being that Ray's versions after 14.01.01 compiles on `gfortran`.

OWF established a more comprehensive StateMod repository and development environment,
in particular to establish a development environment that can support multiple developers.
Consequently, the code from Ray Bennett's versions and Jim Brannon' repository was migrated to the OWF repository named
`cdss-app-statemod-fortran`,
retaining Ray's code history from versions 13.00.01 through 15.00.01, in order to retain recent history as well as
bracketing the changes made by Jim Brannon.  This migration involved the following changes in order to provide consistency:

*   OWF adopted a file structure compatible with development environments for other languages
    and providing flexibility for expansion,
    including placing source code in a folder `src/main/fortran`.
    This allows the following:
    +   Add code for other languages if necessary, such a wrappers to call from other languages.
    +   Add folders for utility programs outside of `src/main`.
    +   Add other files in a `resources` folder, if appropriate.
*   All source files were renamed to lowercase to ensure consistency and proper handling across platforms.
    Ray's code used inconsistent filenames, some mixed case, some all uppercase, and some lowercase.
    This worked OK on Windows, which tends to ignore case, but is problematic with new developer tools.
    The lowercase filename approach had been adopted by Jim Brannon but Ray had not incorporated.
    Ray concurred that this approach was OK to move forward.
    OWF used lowercase names for all versions loaded into Git (13.00.01 through 15.00.01) in order to simplify version comparisons.
*   A general `makefile` was created based on Jim Brannon's work, but with OWF enhancements to be more robust and
    work with Windows and Linux.  It is expected that additional changes will be needed because OWF did
    not initially test the Linux compile.
*   Several files are handled specifically due to windows/linux, or Lahey/gfortran requirements:
    +   `dattim_gfortran.for` - date/time code
    +   `getpath_linux.for` - handle file paths
    +   `parse_gfortran.for` - parse command line
    +   `putpath_linux.for` - handle file paths
*   Files were checked for line ending issues and were updated accordingly, with the goal being to ensure that
    line endings were consistent throughout each file.
    For example, some older files used `CTRL-Z` characters to indicate end of file, but this practice is no longer needed.
    This minimized differences between versions.
*   Each version that was loaded was compiled and run to ensure a valid executable, but was not executed on full datasets,
    pending more detailed testing on the final 15.00.01 version.
    Only the 13.00.01 version failed to compile with `gfortran`,
    consistent with the fact that version 14.01.01 was the first to include `gfortran` support.

The code organization was restructured as per the folder structure discussed in the
following section and additional content was added, including this developer documentation.
The goal is to allow a new developer to clone the repository and get up and running as quickly as possible,
while also avoiding user-specific files in the repository, which would cause ongoing conflicts in file content.

## Development Folder Structure ##

This documentation assumes that files are configured according to the following folder structure.
It is recommended that StateMod developers follow this folder structure closely because if they do not,
the documentation will be less helpful and troubleshooting will require additional resources.
There does not seem to be a clear folder structure standard for Fortran projects and consequently the following
builds upon [Maven Java Standard Directory Layout](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html).

The Linux development environment relies on compilers being installed on the operating system (whereas Windows development environment
relies on additional layer of MinGW or Cygwin).
The following folder structure is similar to the Windows version other than different conventions for Linux user's file locations.

```text
/c/users/user/                               Git Bash user files (same as Windows location).
/home/user/                                  Linux user files.
C:\Users\user\                               Windows user files (same as Git Bash location).
  cdss-dev/                                  CDSS software development.
    StateMod/                                CDSS StateMod software project.
      eclipse-workspace/                     Eclipse workspace to organize Eclipse projects (not in Git repository).
      git-repos/                             Git repositories that comprise StateMod.
--------------- below here folder names must match exactly --------------------------
        cdss-app-statemod-fortran/           StateMod Git main program repository.
          .git/                              Git local repository - DO NOT TOUCH DIRECTLY.
          .gitattributes                     Git repository properties.
          .gitignore                         Git repository global ignore list.
          .project/                          Eclipse project settings.
          .setttings/                        Eclipse project settings.
          build-util/                        Useful scripts for development/build environment.
          doc-dev-doxygen-project/           Auto-generated software code documentation, using Doxygen.
          resources/                         Additional resources.
          src/                               StateMod source code, main and tests.
            main/                            StateMod program code.
              fortran/                       StateMod Fortran code.
                *.for                        Fortran source files.
                *.inc                        Fortran include files (common blocks).
                makefile                     Used with make program to compile software.
            test/                            StateMod unit tests, possibly for future.
              fortran/
                *.for
        cdss-app-statemod-fortran-doc-dev/   Developer documenation.
        cdss-app-statemod-fortran-doc-user/  User documenation.
        cdss-app-statemod-fortran-test/      StateMod automated tests.
```

## Eclipse File Location Overview ##

The following summarizes Eclipse files, which are used if Eclipse/Photran software are used (optional).
These files are not stored in the repository because they are software files or
dynamically change for each developer.
The following folders are consistent with the above folder structure.

```
/c/users/user/                           Git Bash user files (same as Windows location).
/home/user/                              Linux user files.
C:\Users\user\                           Windows user files (same as Git Bash location).
  cdss-dev/                              CDSS software development.
    StateMod/                            CDSS StateMod software project.
      eclipse-workspace/                 Eclipse workspace to organize Eclipse projects (see above).
        .metadata/                       Eclipse workspace files (updated for each developer).
          .plugins/                      Eclipse files for each software plugin.

  .eclipse/                              Eclipse files in user files.

C:\Program Files\Eclipse\                Eclipse software installation folder.
  eclipse-parallel-mars-64/              Software files, as per installation instructions.
```

## Project Initialization Steps ##

The following are the project initialization steps in the recommended order,
although some steps were actually implemented in slightly different order for practical reasons such as
scripts to run steps were created after running the steps on the command line the first time.

*   Initialize software development folder and Git repository to receive files
    +   [Create Development Home Folder](home-folder.md) - manually create project home folder that will hold all the software development files
    +   [GitHub Git Repository](github.md) - create empty GitHub repository
*   Initialize Eclipse development environment
    +   [Eclipse Run Script](eclipse-run-script.md) - the script ensures that the proper version of Eclipse and Java are used
    +   [Eclipse Workspace](eclipse-workspace.md) - create an Eclipse workspace for the StateMod software project
    +   [Eclipse StateMod Project](eclipse-statemod-project.md) - configure the project connected to the Git repository files
    +   [Eclipse Folder Structure](eclipse-folder-structure.md) - implement the development folder structure
*   Initialize build utility scripts
    +   [Build Utility Scripts](build-util.md) - helpful build utility scripts for developers 
*   Initialize documentation
    +   [Documentation, Legacy (Word)](doc.md) - Word documentation
    +   [Documentation, Developer (MkDocs)](doc-dev.md) - create initial MkDocs project for developer documentation
    +   [Documentation, User (MkDocs)](doc-user.md) - create initial MkDocs project for user documentation
    +   [Doxygen](doc-doxygen.md) - configure Doxygen project to generate API documentation
*   Initialize repository with recent history of versions - the following was executed for each StateMod code version
    +   [Save StateMod version history in GitHub](git-statemod-history.md) - save StateMod versions in repository
