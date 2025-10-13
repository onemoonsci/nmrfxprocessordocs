---
title: Building NMRFx and Plugins 
taxonomy:
    category: docs
---

# Building NMRFx

NMRFx is largely written in the Java programming language.  Some command line based tools 
are written in Python and execute using the embedded Jython (Python in Java) intepreter.


Building NMRFx requires the installation of several tools on your computer. Depending on your OS, you may have some of these already.
NMRFx can be built on MacOS, Linux and Windows.  We primarily build and test on MacOS and Linux.

1. Since the source code is  hosted on Github you'll need to have the Git version control system installed.
   One source of information on installing Git is [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

2. Since NMRFx is written in the Java programming language you need to have the JDK (Java Development Kit) installed. There are various
sources of OpenJDK (the open source version).  We generally build with one from [Azul](https://www.azul.com/downloads/?package=jdk#zulu). Not
all downloads of Java include JavaFX, the GUI toolkit.  It's easiest to build NMRFx if you choose one that does. At the Azul download site
you can select your Java version, operating system, architecture, and Java package.  For the latter choose "JDK FX". We generally use
recent versions of the JDK. At present (NMRFx 11.4.32) we are using JDK version 24, but JDK 25 should also work.

3.  The build (downloading dependencies, compiling the source code, and building packages) is done with [Maven](https://maven.apache.org).  You can find
installation instructions [here](https://maven.apache.org/install.html).  We use [Homebrew](https://brew.sh) on MacOS to intall it.

Once you have all the required tools you can download and build NMRFx.

1.  The source code is available on [Github](https://github.com/nanalysis/nmrfx).  You can clone it to your computer with git.  First
move to an appropriate folder on your computer. The software will be downloaded into a directory (within your current directory) named **nmrfx**.
    
    git clone https://github.com/nanalysis/nmrfx.git

2.  Build the software by moving into the **nmrfx** directory and run maven.  Use the **skipTests** argument to tell maven to skip running our test suite.  Performing the tests requires downloading a set of test NMR files and requires installation of the optional **lfs** package for Git.

     mvn -DskipTests clean install


3.  You can execute NMRFx by running the **nmrfx** shell script (or **nmrfx.bat** on Windows).  It will be located in a directory like (depending on version):

    nmrfx-analyst-gui/target/nmrfx-analyst-gui-11.4.33-SNAPSHOT-bin/nmrfx-analyst-gui-11.4.33-SNAPSHOT/nmrfx

The NMRFx source code is contained in six different modules

nmrfx-core
:  Core routines for datasets, peaks and projects (also used by RING NMR Dynamics).

nmrfx-utils
:  Various utilities (also used by RING NMR Dynamics)

nmrfx-structure
:  Molculear structure code including structure calculation and chemical shift prediction

nmrfx-analyst
:  Processing, dataset and peak tools

nmrfx-analyst-gui
:  Graphical user interface

nmrfx-plugin-api
:  Code for loading plugins

NMRFx can be run with three different shell (or Windows batch) scripts

nmrfx
:  Starts up the full graphical user interface (as described above).  The script is contained in a sub-directory of  the nmrfx-analyst-gui target folder


nmrfxa
:  Runs non-gui tools (for example, for command line processing). The script is contained in a sub-directory of the nmrfx-analyst target folder


nmrfxs
:  Runs non-gui tools for structure calculation and chemical shift prediction. The script is contained in a sub-directory of the nmrfx-structure target folder


Building full installers is not part of the open-source code.

We welcome contributions of source code, but recommend that users contact us before engaging in any significant projects.  The source code is still 
under rapid development so its good if we are aware of external projects.


# NMRFx Plugins

NMRFx supports plugins.  These are executable tools that can be built by external users,  and then downloaded and copied  nto the **lib** or **plugin** directory of
an installed version of NMRFx. On start-up, the  NMRFx application will check for plugins and load them if available.

We provide hooks to allow the plugins to appear in specified locations of the interface.  Restricting the locations ensures that users will have a more
consistent experience with the software.  The nine current locations are:

Plugin Menu
: The main menubar will have a plugin menu (if any available plugins are set to use this location).  This is where the RING NMR Dyanmics plugin will appear.
See the **NMRFxPluginMenuExamplePlugin.java** example. 

Atom Table
: A menu will appear at the right side of the main menu in the Atom Table
See the **NMRFxAtomTableExamplePlugin.java** example.

Molecule Viewer
: A menu will appear at the right side of the main menu in the 3D Molecular Viewer 
See the **NMRFxMoleculeViewerExamplePlugin.java** example.

Right Hand Tools
: A new titled pane will appear in the accordion tabs (where existing tools like the PeakPicker and Annotaions are ) displayed by clicking **Tools** in the top-right of the spectrum window.
See the **NMRFxRighthandToolsExamplePlugin.java** example.

Dataset Table
: A menu will appear at the right side of the main menu in the Dataset Table
See the **NMRFxDatasetTableExamplePlugin.java** example.

Dataset Table
: A menu will appear at the right side of the main menu in the Peak Table
See the **NMRFxPeakTableExamplePlugin.java** example.

File Menu 
: A cascade menu will appear of the File of the main menubar.
See the **NMRFxFileMenuExamplePlugin.java** example.

Status Bar  Menu 
: A cascade menu will appear of the Tools menu of the status bar at bottom of spectum windows.
See the **NMRFxStatusBarExamplePlugin.java** example.

Startup 
: Runs non-gui code at startup that may install some tool that doesn't require any GUI items.
This might be used, for example, to install some code that provides a new processing operation.
(we haven't tested this concept yet)
See the **NMRFxStartupExamplePlugin.java** example. 

Building a plugin will create a **.jar** file containing the plugin code.  Copy that file into the **lib** folder of the nmrfx-analyst-gui folder (where you'll find
the standard jar files included with nmrfx)

We provide, as listed above, examples of the use of each location.  At present, these examples demonstrate how to build a plugin that
appears in any of the available locations.  As we work on documenting the NMRFx API, we will provide more explicit examples of their use.

The plugin examples are located in the **nmrfx-example-plugin** folder.  You can copy this folder to another location and edit the files (most likely
removing any files for plugin locations you don't want to use and changing the package and file names).  Use the **mvn clean **package** command
to compile and build the plugin **.jar** file.  Prior to doing this you'll need to build and install NMRFx on your computer with **mvn -DskipTests clean install**
so that the required libraries are installed in the maven repository.

Please contact us if you wish more information on Plugin development.  As with contributing code
to the main project, we recommend discussing with us your plans for plugins so we can alert you to any planned API changes.


