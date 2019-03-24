# StateMod Documentation (for Software Developers) #

This documentation is the developer manual for Colorado's Decision Support Systems (CDSS) StateMod water allocation model software.

If you are reading this documentation, you have an interest in learning how StateMod is designed,
are a member of the software development team,
or perhaps wish to contribute software code enhancements or otherwise provide input to the project.
This documentation is intended to provide sufficient information to software developers
to streamline understanding of the StateMod code and developer environment.
It is expected that software developers are technically competent and
follow conventions of the open source StateMod project.

This documentation page includes the following sections:

* [How to Use this Documentation](#how-to-use-this-documentation) - guidance and list of main documentation sections
* [Colorado's Decision Support Systems](#colorados-decision-support-systems) - the system under which the software is maintained
* [License](#license) - license for software and this documentation
* [Source Repository on GitHub](#source-repository-on-github) - location of StateMod repository in GitHub

------------

## How to Use this Documentation ##

This website is a companion to the StateMod source code and provides guidance for
software developers that modify and support StateMod.

It is the intended to create StateMod executable programs for Windows (7, 10, +) and Linux, with Windows being the primary version.
32-bit and 64-bit versions will also be generated, although the Windows 32-bit version is the starting point and is initially the main focus.
This documentation includes information for these variants and will be filled out as resources can be applied to each configuration.
Icons for Linux ![Linux](images/linux-32.png) and Windows ![Windows](images/windows-32.ico) are included to help indicate documentation
specific to an operating system.

The documentation is organized with the first sections focusing on setup for a new developer and common development tasks.
The reference sections at the end provide information that may be of use but are typically not used day to day.
Use the search feature of this website to find specific information.

* [New Developer Setup](dev-new/overview/) - **new StateMod software developers should start here**
* [Development Tasks](dev-tasks/overview/) - describes common development tasks - **refer to this after new development environment is configured**
* [Code List](code-list/code-list) - list of code files with useful information
* [Resources](resources/resources) - useful resources, including training documents for developers
* [REFERENCE: Software Design](software-design/overview/) - provides details about the software code design
* [REFERENCE: Deployed Environment](deployed-env/overview/) - describes the deployed environment after software is installed
* [REFERENCE: Development Environment](dev-env/overview/) - describes development environment software installation (some tools are shared between CDSS software projects)
* [REFERENCE: Initial Project Setup](project-init/overview/) - describes how the StateMod software project was initially configured

The navigation menu on the left provides access to pages in the documentation.
The navigation menu on the right provides access to sections on the page.
If the page is viewed in a narrow window the navigation menus may be compressed into an icon.

## Colorado's Decision Support Systems ##

Colorado's Decision Support Systems (CDSS, [cdss.state.co.us](https://www.colorado.gov/cdss))
has been developed to answer important questions about Colorado's water resources.
CDSS efforts are led by the [Colorado Water Conservation Board (CWCB)](http://cwcb.state.co.us)
and [Colorado Division of Water Resources (DWR)](http://water.state.co.us).

![CDSS Website](index-images/CDSS-website.png)

One component of CDSS is the StateMod water allocation model, which estimates water allocation given water supply and demand and
physical and legal (water right) constraints on water decisions.
StateMod results are linked to the StateCU consumptive use model and in some basins the MODFLOW groundwater model.

In late 2016, the CWCB funded the OpenCDSS project to move StateMod and other CDSS software to open source licensing
and establish open source software projects.
The [Open Water Foundation](http://openwaterfoundation.org) was contracted to lead the OpenCDSS project.

## License ##

The license for this documentation is the [Creative Commons CC-BY 4.0 license](https://creativecommons.org/licenses/by/4.0/).

The StateMod software is licensed using the GPL v3 license.

## Source Repository on GitHub ##

The source files for this documentation are maintained in the
[StateMod GitHub repository](https://github.com/OpenCDSS/cdss-app-statemod-fortran-doc-dev).
