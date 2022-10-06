# Software Design / Overview

**This documentation will be updated as more details about the StateMod code and design are included in
the Developer Documentation.**

The StateMod Fortran code is divided into separate files with `.for` extension.
Each subroutine is in a separate file and the name of the file generally matches the subroutine or function.
See also the following resources:

* [Code list](../code-list/code-list.md) - list of all code files, call sequence graphs, etc.
* [Resources](../resources/resources.md) - developer training documentation, flowcharts, etc.

Need to describe code modules at a high level:

* Main entry point (see: [`statem.for`](https://github.com/OpenCDSS/cdss-app-statemod-fortran/blob/master/src/main/fortran/statem.for))
* Code organization:  include files, parameter data, etc.
* Input
* Initialization
    + Global data
    + Main program data
* Calculations
* Output
* Data checks
* Logging
* Clean-up
* Integration with StateMod GUI
* etc.
