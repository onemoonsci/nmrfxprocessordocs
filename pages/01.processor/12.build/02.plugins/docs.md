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

Peak Table
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
removing any files for plugin locations you don't want to use and changing the package and file names).  Use the **mvn clean package** command
to compile and build the plugin **.jar** file.  Prior to doing this you'll need to build and install NMRFx on your computer with **mvn -DskipTests clean install**
so that the required libraries are installed in the maven repository.

#### Plugin class structure

The source code for a plugin must contain the following file:

    src/main/resources/META-INF/services/org.nmrfx.plugin.api.NMRFxPlugin

whose contents specify the full name of an Plugin classes that should be loaded:

    org.nmrfx.example.plugin.NMRFxPluginMenuExamplePlugin

the specified Plugin classes must implementthe NMRFxPlugin interface:

    public class NMRFxPluginMenuExamplePlugin implements NMRFxPlugin {


Each Plugin class can support one or more Entry Points.  These are the locations where the plugin will appear in the GUI.
The Entry Points are specified as the return of the **getSupportedEntryPoints** method.  For example, this example specifiies that this
plugin can appear in, and only in, the main menubar Plugin menu.

    @Override
     public Set<EntryPoint> getSupportedEntryPoints() {
    
         return Set.of(
                 EntryPoint.MENU_PLUGINS
         );
     }

When NMRFx starts up, at each code location where a plugin could be loaded, it checks the Plugin classes specifed in the 
NMRFxPlugin file to see if that Entry Point is supported.  If the Entry Point is supported by a class the plugin is regstered
with a call to the following method:

    @Override
    public void registerOnEntryPoint(EntryPoint entryPoint, Object object) {
        switch (entryPoint) {
            case MENU_PLUGINS -> addToPluginMenu(object);
            case null, default ->
                    throw new IllegalArgumentException("Only " + EntryPoint.MENU_PLUGINS + " is supported by this plugin " + entryPoint);
        }
    }

In our examples we use a Java switch statement to show that you could respond to multiple Entry Points.  There
should be a case for each Entry Point that was returned by a call to **getSupportedEntryPoints**.  If the 
call to registerOnEntryPoint has an argument for an unsupported Entry Point then the IllegalArgumentException is thrown.
So the EntryPoints returned by **getSupportedEntryPoints** should always be matched to a supported case.

The **registerOnEntryPoint** method calls some method to update the GUI with appropriate code.
In this example, the code adds a menu entry to the Plugin menu:

    private void addToPluginMenu(Object object) {
        Menu menu;
        Function<String, String> nmrfxFunction;
        if (object instanceof PluginFunction(Object guiObject, Function<String, String> pluginFunction)) {
            menu = (Menu) guiObject;
            nmrfxFunction = pluginFunction;
        } else if ((object instanceof Menu)) {
            menu = (Menu) object;
        } else {
            throw new IllegalArgumentException("Expected a menu, but received " + (object == null ? "null" : object.getClass().getName()) + " instead");
        }
        menu.getItems().add(createExampleMenu());
    }

    private Menu createExampleMenu() {
        Menu exampleMenu = new Menu("Example");
        MenuItem exampleMenuItem = new MenuItem("Show Plugin");
        exampleMenuItem.setOnAction(e -> showPlugin());
        exampleMenu.getItems().addAll(exampleMenuItem);
        return exampleMenu;
    }

The type of Object passed into **registerOnEntryPoint** depends on the location that the method
is being called from.  In this case the object is a PluginFunction which has a field to specify the
GUI menu that the new menu should be added to, and a function that can be called to respond to calls from the plugin.
In this case, and most use cases, that PluginFunction is unused.  It exists for cases like RING NMR Dynamics
which doesn't have full access to all the NMRFx code (since its built as a program that can run both as a plugin
and as a standalone application).

A simpler example shows the call to create a new Titled Tool Pane in the right hand tool region (set up 
by a EntryPoint.RIGHT_TOOLS Entry Point).  Here the object passed in is the controller that manages this tool region:

    @Override
    public void registerOnEntryPoint(EntryPoint entryPoint, Object object) {
        switch (entryPoint) {
            case RIGHT_TOOLS -> addToToolController((ToolController) object);
            case null, default ->
                    throw new IllegalArgumentException("Only " + EntryPoint.MENU_PLUGINS + " is supported by this plugin " + entryPoint);
        }
    }

    private void addToToolController(ToolController toolController) {
        TitledPane titledPane = new TitledPane();
        titledPane.setText("Plugin example");
        toolController.getAccordion().getPanes().add(titledPane);
        Label label = new Label("Hello");
        titledPane.setContent(label);
    }

The real work of a plugin is triggered by the various GUI controls added.  These could be  MenuItems that
call some Java method when the object passed in is a Menu object, or a full set of GUI items that might appear in more
complex plugin GUIs where the object is more complex like ToolController of the above tool.


Please contact us if you wish more information on Plugin development.  As with contributing code
to the main project, we recommend discussing with us your plans for plugins so we can alert you to any planned API changes.


