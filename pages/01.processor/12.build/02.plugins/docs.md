---
title: Building Plugins 
taxonomy:
    category: docs
---

### NMRFx Plugins

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


