---
title: Molecular Viewer
taxonomy:
    category: docs
---

The Moleculear Viewer has three tab panes.  One for a three-dimensional viewer, one for an RNA secondary structure viewre and one for a flat-2D viewer for small molecules.

### Three-Dimensional Viewer

The Three-Dimensional Molecular Viewer is, like all of NMRFx Analyst, a cross-platform tool written in the Java programming language. It makes use of the JavaFX 3D environment which gives access to hardware accelerated three dimensional graphics. The viewer is not designed to be a full featured molecular graphics program, but rather to be able to allow you to make effective use of molecular visualization while working on an NMR project. Because it is integrated directly inside NMRFx Analyst it is easy to use to visualize any internal 3D data. The viewer is implemented in a way that makes it analogous to other canvas windows in NMRFx Analyst. It can render various graphical items, from simple shapes like spheres and cylinders, to more complex items like full molecular structures. This allows us to use it to render molecules and associated information like constraints and the coordinate system of an orientation tensor. 

![Three Dimensional Viewer showing Ubiquitin in tube mode with one residue in stick mode](images/threedviewer.png)

The Molecular Viewer will display the currently active molecule. See the previous chapter (Molecules) for information about loading molecular structures. Displaying the molecule consists of two steps, selecting the atoms to be displayed, and selecting the mode, lines or spheres, in which they are to be rendered. Molecules can also be rendered as a tube that follows the backbone and is colored with colors that sequentially change from one end to the other end of the molecule.  When displaying a Tube, there is no need to first select atoms. A set of atoms appropriate to either a protein or nucleic acid will automatically be chosen when you click the Tube button.

#### Controls
The control sections at the top of the 3D molecular viewer are described here.

Select
:   Choose from the following menu items 

    Backbone
    :    Backbone atoms (N, Ca, C of proteins)

    Heavy
    :   All non-hydrogen atoms

    All
    :   All atoms

    Ligand
    :   All atoms of ligands (entities that are not in a polymer)

    Residues
    :   All atoms of any residues with a currently selected atom

Text Field
:   Type in selections like 3.\* to select all atoms in residue "3" or 5-10.N,C,CA to select backbone atoms in residues 5 through 10. After entering a value, hit the Enter key to activate the selection. 


Display

:   Use items in this menu to display selected atoms according.

    Lines
    : Draw bonds between selected atoms with thin lines

    Sticks
    : Draw bonds between selected atoms with sticks and atoms with larger spheres 

    Spheres
    : Draw Spheres at each selecte atom (but no bond lines)

    Tubes
    : Draw a tube that threads through backbone atoms of proteins or nucleic acid polymers.  Use a color that starts with red and gradually becomes yellow

    Box
    :  Draw the edges of a box that fully encloses the molecule

    Axes
    : Draw lines starting at the origin at extending along each of the three (x,y,z) axes

    SVD Axes
    : Calculate the principle components of the coordinates useing an SVD algorithm and draw lines along those components.

    RDC Axes
    : Calculate the the orientation of the molecule using RDC values and draw lines along those components.

View
:   Change the view of the molecule as follows

    Center on selection 
    : Translate the view so the average positoin of the currently selected atoms are at the center. Rotations will be around the this point.

    Reset Transform
    : Reset rotation and scale to the original view. 

    Rotate to SVD Axes
    : Calculate the principle components of the coordinates useing an SVD algorithm and rotate the view so those components align with x,y,z view.

    Rotate to RDC Axes
    : Calculate the the orientation of the molecule using RDC values and draw lines along those components and rotate the view so those components align with x,y,z view.

Remove
: When any item is drawn an entry is added to the Remove menu with the type of item and an index. Selecting the menu item will remove the corresponding item from the display.  As an example, successive drawing of objects with stick mode would add *stick*, *stick1* and *stick2* to the list. Selecting *stick* would remove all sticks, selecting *stick1* would remove just the subset of items labeled *stick1*. 

Calculate
: This menu item gives access to a several (still somewhat experimental) tools for 3D structure calculation.

    To3D
    : Used only for small molecules.  It will convert 2D coordinates into a low-energy 3D conformation.

    Calc Structure
    :  Will structure calculation on a polymer.  At present is not using any distance restraints.  Normally structure calculation in NMRFx is done with the command line, **NMRFx Structure** program

    Refine Structure
    : Do a low temperature refinement with torsion angle dynamics of a polymer.  Currently this is mostly of use for refining RNA structures generated with the 2D->3D calculation (from the Secondary Structure menu tab).

The molecule can be rotated, translated or scaled as follows.

Rotate

:   The molecular view can be rotated by pressing and then dragging with the left mouse button.

Scale

:   The molecular view can be scaled by pressing and then dragging with the right mouse button. Dragging right will increase the size of the viewed molecule, and dragging left will decrease it.

Selection

:    Click with the left mouse button on atoms or bonds to select them.  If the shift key is held down you will select an additional atom/bond without deselecting any existing ones.

### RNA Secondary Structure Viewer

This tool allows displaying the secondary structure of RNA and can include the display of distance constraints and deuterium labeling.  Open the tool up by choosing the **RNA Sec Structure** menu item from the Molecule -> Analysis menu.  If you're RNA molecule has not had a secondary structure assigned within NMRFx Analyst using the dot-bracket notation, then click the Dot-Bracket button.  This will display the following dialog.

![RNA Secondary Structure](images/rnass.png)

The dot-bracket notation is used to indicate base-pairing.  A left parenthesis, is base paired to the corresponding base with a right parenthesis.  Either a dot ("."), or the nucleotide base character can be used to indicate the base is not paired.

The first row of the display shows the sequence of RNA bases.  The row below shows the dot-bracket assignment.  By default this will consist of all "." values, indicating that there are no base pairs.  You can update the assignment by typing dot-bracket notation into the text box, and hitting the Return key, or by clicking with the mouse on the assignment symbol below each base pair character.  Clicking the mouse will toggle through values in the following order: "(",")","X","." (where X is the base pair character.  If the number of left and right parentheses are not equal, the background will be displayed in yellow.

Clicking the Draw button will generate a layout of the sequence in a manner consistent with the base-pairing specified with the dot-bracket notation.  This works well for relatively small RNAs.  We have not yet optimized it for larger RNAs (which may take some time to layout).  We plan to add the ability to import a file of x,y positions, so that the layout could be done in an external program.

Various tools for interacting with the secondary structure and rendering the display are available.

Sec. Structure
: This menu has tools for interacting with the secondary structure

    From 3D
    : Determine the secondary structure from the current 3D structure.  Various rules are used to determine what bases are paired.

    Predict 2D
    : This is an experimental feature that uses a deep-learing model to predict secondary structure from the primary sequence.  Currently it requires separate download of a trained model.

    To 3D
    : This is an experimental feature that will generate 3D coordinates consistent with the secondary structure.

Atoms
: Use the choices in this menu to select what atoms are displayed. Displayed atoms are used to show what atoms have been assigned and whether the assignment is consistent with predictions for that atom type.  Atoms colored gray are unassigned, and atoms in green, light green, or red are assigned (in decreasing order of consistency).  You can select all ribose, all base, all exchangeable or a subset of ribose atoms.

Peaklist
:  The display can be annotated with lines indicating the presence of distance constraints.  Use the choices in this menu to select what peak list is used for displaying connectivities between atoms.  Any peaks in the list with complete assignments will be used to draw a connecting line between the pair of peaks.  This is only used for peaks with two hydrogen atom dimensions.

Modes
: Turn on or off various display modes.
    
    Numbers
    :  Display the residue number instead of residue name (G,C etc.) on each residues circle.

    Probabilities
    : If a secondary structure prediction has been done turn on this mode to display the probability that a selected residue is base-paired to other residues.  Any residue with a probability above a limit will have the probability displayed.

    Active
    : If the **Active** checkbox is selected, then the display of hydrogen atoms (the smaller circles) will reflect the "active" state of atoms.  The "active* state is normally used in the tool used to generate RNA Peaks (RNA Peak Generator).  Atom types that are marked as deuterated (turned off in the Peak Generator) are inactive.  Atom types marked as non-deuterated are active.  Thus, the tool can be used to display the deuteration profile of the molecule.

    Frozen
    : If the **Frozen** checkbox is selected, then only peaks that have been marked as Frozen in the Peak Slider will be used for generating constraints.  This allows a visual display of the location of frozen peaks.  If the checkbox is not selected, then all peaks with assignments will be used.

    Predictions
    : If you click on an atom it will display the prediction data for that atom.  This lets you switch between showing hydrogen and carbon predictions

    Peak Intensities
    : This has a submenu that lets you choose an intensity level for display of connectivities between atoms.  Levels are s)trong, m)edium, w)eak and v)ery w)eak.

Peak Type
: Select All, Intra-residue, or inter-residue to display peak based connectivities based on atom types.


Zoom buttons
: At the left side of the window are **+** and **-** buttons that can be used to zoom in the display.  Use can use the scrollbars to move the view.  Alternatively, you can Use a trackpad to zoom in, out or pan the view.
