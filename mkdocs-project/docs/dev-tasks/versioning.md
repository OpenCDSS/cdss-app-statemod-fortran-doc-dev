# Development Tasks / Version Control with Git #

The OpenCDSS project is using Git and GitHub for version control.
Git protocols for StateMod follow OpenCDSS protocols and are summarized here for reference.

* [Git Training](#git-training)
* [Git Tools in Repository](#git-tools-in-repository)

---------------

## Git Training 

There are numerous resources on the internet for Git training.
See also the [CDSS / Learn Git](http://learn.openwaterfoundation.org/cdss-learn-git/) documentation.
**Need to update this link to point to the Google Cloud location when it is finalized.**

## Git Tools in Repository

Several scripts are installed in the `build-util` folder and can be used for StateMod development.
Run these scripts from the command line:

* `git-check-statemod.sh` - check the status of StateMod repositories
* `git-clone-all-statemod.sh` - clone all repositories, if not already cloned, after cloning the main repository
* `git-tag-all-statemod.sh` - tag all repositories for a StateMod version
