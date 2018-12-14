# Setting Up MIK to Build Ingest Packages

MIK, aka Move to Islandora Kit, is the open-source tool that the LSU LDL Dev Team uses to build LDL batch ingest packages. Specifically, we use the "CSV to MODS Toolchain" to convert metadata in spreadsheets into MODS XML, and to match the XML records with content files.  

MIK is [available on GitHub](https://github.com/MarcusBarnes/mik) and has [excellent documentation](https://github.com/MarcusBarnes/mik/wiki).  

Note that MIK is independent from Islandora and does not need to be run on the same server as the LDL. Anyone can install and run MIK to create ingest packages, which can then be batch ingested by any Collection Administrator user in the LDL web interface, or by an LSU LDL Admin with Drush.  

## Running MIK Locally (Windows, OS X, Linux)

MIK can be run on Windows, but may be finicky. Please refer to the MIK documentation for [Running MIK on Windows](https://github.com/MarcusBarnes/mik/wiki/Cookbook:-Running-MIK-on-Windows) for possible failure points and troubleshooting assistance.  

To install MIK, you can follow the [installation instructions](https://github.com/MarcusBarnes/mik/wiki/Installation).

## Running MIK with LSU's MIK-Vagrant Box (from Windows)

The other option is to run MIK using a Linux Vagrant box. The LSU LDL Dev Team created the [mik-vagrant box](https://github.com/lsulibraries/mik-vagrant) to facilitate running MIK on Windows workstations, avoiding many of the common Windows troubles. The mik-vagrant box has a stable version of MIK installed, configured, and ready to use.  

Note that this is the method used by the LSU Metadata Librarian in 2017-2018 when the LSU MIK documentation was created. The documentation will use Vagrant box conventions, so you may need to make adjustments if running it locally.  

To use the mik-vagrant Box, you'll first need to download and install Git, Vagrant, and VirtualBox.

* [Download Git](https://git-scm.com/download/win)
* [Download Vagrant](https://www.vagrantup.com/downloads.html)
* [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads)

To install the mik-vagrant box:

* In the directory on your computer where you want to install it, right click and choose "Git Bash Here"
* Use "git clone" to copy the mik-vagrant box to your local directory:
    `git clone https://github.com/lsulibraries/mik-vagrant.git`

To start up the mik-vagrant box from a Git Bash window:

* Start Vagrant
    `vagrant up`
* Log into the box  
    `vagrant ssh`
* Change directory to use the MIK program
    `cd /vagrant/mik`
