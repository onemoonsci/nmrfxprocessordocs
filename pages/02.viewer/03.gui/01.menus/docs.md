---
title: Menus
taxonomy:
    category: docs
---


The Control Panel is the first window to be displayed when NMRView
starts up, and consists of a single menubar. Note that on Mac OS X the
menubar will generally be displayed not as a separate window, but on the
Desktops screen menu bar. The menus available through the menubar may be
used to bring up various other NMRView windows. The options available
through each menu item are summarized below.

###File

Projects

:   
    New

    :   Create a new project. You will be presented with a file browser to use in specifying the location
        and name of the new project.  The project will be created as a new folder with appropriate sub-folders. 

    Open

    :   Open an existing project. You will be presented with a file browser to use in selecting the existing project.

    Recent

    :   A menu displaying recently used projects (up to 20). Selecting a project name from the menu will open that project.

    Save

    :   Save the current project (including STAR3 file and open windows).

    Save...

    :   Save the current data as a new project.  (including STAR3 file and open
        windows).

    History

    :   Display a list of saved states of the current project.  Selecting an item from the list 
        and clicking Open will reload the project as contained in that saved state.

    Attributes

    :   Display the project attributes browser used to manage NMRVIEW projects. Use the
        attributes browser to set attributes like locations of dataset folders.

    Close 

    :   Close the current project. This removes all open information such as datasets, peak lists, and
        molecular structures.

STAR

:   

    Read STAR3

    :   Brings up a file selection panel for reading a BMRB Star file
        (NMRView database file). Almost any kind of analysis that
        NMRView can perform can be stored in a Star file.

    Save STAR3 As...

    :   Brings up a file selection panel for writing a BMRB Star File.

    Save STAR3 (Auto Increment)

    :   Saves a BMRB STAR file using a name automatically generated from
        the last saved STAR file. For example, if the last file saved
        was "myproject\_3.str" the new file will be "myproject\_4.str".
        This is a convenient way to make frequent updates of your data
        to a STAR file as you work on a project. To have this work
        properly you should start with an initial file name that ends
        with a non-integer character followed by an integer value (as in
        the above example).

    Fetch From BMRB...

    :   Load the set of files found in your last session. Each time you
        use Scan Directory (or Clear and Scan Directory) the files found
        will be stored in a file. The files in this table will be
        opened.

    STAR2 (deprecated)

    :   Earlier versions (before 8.0) of NMRViewJ used the STAR 2 file
        format. If you need to work with these older files use the
        choices in this menu. But some features of NMRViewJ (especially
        relating to RunAbout) can only be saved in STAR 3 files, so its
        a good idea to switch to the newer format. You can open a file
        in STAR 2 format, and save it out in STAR 3 format.

        Read STAR2 File

        :   Use a File Browser to Open and read a STAR (version 2.x)
            File

        Write STAR2 File

        :   Use a File Browser to Save a STAR (version 2.x) File.

Preferences...

:   Select Prefs to open up the Preferences Panel. This can be used to
    set various user preferences for NMRView. On Mac OS X this menu item
    will be found under the NMRVIEW menu

Print

:   Print the active spectrum.

Show Console

:   Show the NMRView console. The console can be
    used for command line input and displays the output of various
    commands. The NMRView console is based on the tkCon console
    developed by J. Hobbs.

Quit

:   Quit the NMRVIEW program.

###Datasets

Open Datasets

:   Select this to open a File Selection
    Panel that can be used to select datasets
    to be opened.

Open and Draw Datasets

:   Select this to open a File Selection
    Panel that can be used to select datasets
    to be opened. When the dataset is opened a window will be created
    and the dataset will be drawn

Datasets Table

:   Select this to open a window containing a table of all currently
    opened datasets. The use of this table is described in the chapter
    on Datasets.

Load Recent Datasets

:   When you quit from NMRViewJ the file paths for currently opened
    datasets are stored into a preferences area containing recently
    opened datasets. Selecting this menu item will load these recently
    opened datasets.

Convert Varian Phasefile

:   Varian phase files are stored as serial files (see Datasets chapter)
    and thus are less efficiently accessed than NMRView format files.
    Select this menu entry to get a file selection dialog to select a
    Varian phase file that can then be converted into an NMRView format
    file. The phase file must exist in the normal Varian directory
    hierarchy so that the procpar file can be read as well.

Manage Datasets

:   Select this to open a Datasets Manage
    Panel that can be used to reference or
    close datasets.

Make Pseudo3D

:   Select this to combine a set of selected 2D datasets into a single
    3D dataset where each 2D dataset is on a plane. Choosing this menu
    item will display a file browser you can use to select the datasets
    with. After selecting datasets you'll be prompted for the name of
    the 3D dataset to create.

Peak Pick All

:   Select this to pick peaks in all currently opened datasets. As with
    the similar operation available from the Datasets table this is only
    useful if the datasets have reasonable default contour levels (or if
    a reasonable value can be automatically determined from the datasets
    signal to noise level).

###Windows

Copy

:   Select this to copy an image of the current spectrum window to the
    clipboard from where it can be pasted into another application

Synchronize...

:   Display an interface in which you can set up synchronization of the
    view between various specified spectral display windows.

Export...

:   Export a graphics file rendering of the current spectrum. You will
    be prompted for the file name and type of graphics file. Current
    formats include vector formats such as EPS, PDF and SVG and bitmap
    formats such as GIF, JPEG and PNG

Attributes...

:   Select this to open a File Selection
    Panel that can be used to select datasets
    to be opened. When the dataset is opened a window will be created
    and the dataset will be drawn.

Monitor Crosshair...

:   Open a window that will display the current chemical shift positions
    of the two crosshairs in the active window. If the window is
    displaying a dataset with three or four dimensions then the chemical
    shift ranges of the displayed planes will also be displayed. The row
    labeled "D:" in the monitor window will display the chemical shift
    difference between the two crosshairs for the x and y dimensions,
    and the difference between the top and bottom displayed plans for z
    and z2.

Manage...

:   Select this to open a Windows Management
    Panel that can be used to raise
    spectrum windows to the front of the display or to delete them.

Key Bindings...

:   Display the graphical interface for displaying the bindings that
    relate key presses in a spectrum window to actions that occur.

Strips (Canvas)...

:   Select this to open display a dialog from which you can create a
    series of strips of spectra, as documented in the "Strips" chapter.

Save Dataset Section

:   Select this to save the area of the dataset between the crosshair
    cursors into a new smaller dataset. You'll be prompted with a file
    dialog to choose the file name and after saving asked if you want to
    open up the new smaller dataset.

Favorites...

:   Display a list of currently saved spectral views (favorites). Only
    active if a project is open.

Jump Panel...

:   Display a graphical interface used for jumping around to various
    positions in spectra.

Hide all Spectra

:   Hide all windows with spectra.

Show all Spectra

:   Show all windows with spectra.

###Canvas

In premium mode, spectra can be displayed in windows that can include
not only spectra, but also a wide variety of graphical objects such as
rectangles, text, and lines. Canvases can also include various charts,
including xy and bar charts.

File

:   

    Save...

    :   Save a NMRViewJ/dataChord format canvas file. This will save all
        the graphic items on a single canvas (which may include multiple
        spectra).

    Open...

    :   Open a NMRViewJ/dataChord format canvas file. This will create a
        new toplevel window containing all the graphic items in the
        saved file. Spectrum items in the graphic file may depend for
        their display on the datasets used in originally drawing them.
        The software will check if the dataset are already opened,
        attempt to open them from locations specified in the graphics
        file or in your current project directories. If they can't be
        found you will be prompted with a file browser to explicitly
        open them.

    Browse...

    :   Display a browser to let you browse through saved canvas files.

    Export (Bitmap Image)...

    :   Export a graphics file rendering of the current spectrum in a
        bitmap format such as PNG, GIF, or JPG.. You will be prompted
        for the file name. The file format will be determined from the
        extension of the file name.

    Export (Vector Graphics)...

    :   Export a graphics file rendering of the current spectrum. You
        will be prompted for the file name and type of graphics file.
        Current formats include vector formats such as EPS, PDF and SVG
        and bitmap formats such as GIF, JPEG and PNG. This menu item
        will let you select both vector formats and bitmap formats, but
        it is preferable to use the previous menu item for bitmap formats.

New

:   

    New Spectrum

    :   Create a new toplevel canvas window with a spectrum item in it
        and the spectrum control iconbar across the top.

    New Spectra

    :   Create a new toplevel canvas window with a multiple spectra in
        it and the spectrum control iconbar across the top. You will be
        prompted for the total number of spectra and the number of rows
        in the display grid.

    New Figure

    :   Create a new toplevel canvas window without any content (or
        iconbar).

Insert

:   

    Spectrum

    :   Insert a new spectrum item onto the canvas.

    Rectangle

    :   Insert a new rectangle item onto the canvas.

    Text

    :   Insert a simple text item onto the canvas. You can change the
        font and color of simple text items, but don't have control over
        individual characters or more complicated attributes.

    Formatted Text

    :   Insert a new formatted text item onto the canvas. Formatted
        items can have most any attributes (font, superscript, bold,
        italics, etc.) changed and special symbols added.

    Annotation

    :   Insert a new annotation item onto the canvas. Annotation items
        are a line with a simple text string at one end and an arrow
        head at the other.

    Table

    :   Insert a new table item onto the canvas. Table items are text
        formatted as a table.

    Line

    :   Insert a new line item onto the canvas.

    Arc

    :   Insert a new arc item onto the canvas.

    Oval

    :   Insert a new oval item onto the canvas.

    XY Plot

    :   Insert a new xy plot onto the canvas.

    Bar Plot

    :   Insert a new bar plot onto the canvas.

    Stat Plot

    :   Insert a new statistical bar plot item onto the canvas.

Edit

:   

    Cut

    :   Remove the currently selected item(s) from the canvas. Cut items
        will placed on the clipboard so they can be pasted elsewhere.

    Copy

    :   Copy the currently selected item(s) onto the clipboard.

    Paste

    :   Paste items on the clipboard into the current canvas. Items can
        be items that were cut or copied from a canvas, or various other
        item types copied from other programs including text and images.

Arrange

:   

    Send to Back

    :   Send the currently selected item to be below all other canvas
        items.

    Send Backward

    :   Send the currently selected item to be below the next lowest (in
        display order) item in the canvas.

    Bring Forward

    :   Send the currently selected item to be above all other canvas
        items.

    Bring to Front

    :   Send the currently selected item to be in front of the next
        highest (in display order) item in the canvas.

    Group

    :   Group together currently selected items. Grouped items will be
        moved together when they are dragged around the canvas with the
        mouse.

    UnGroup

    :   UnGroup the currently selected items.

    Lock

    :   Lock the currently selected items. Locked items can't be moved
        or resized. The selection handles of locked items will contain
        an "x" symbol.

    Unlock

    :   Unlock the currently selected items.

Arrange Spectra

:   

    Horizontal

    :   Distribute all spectra in the canvas so they are evenly
        distributed in a row across the canvas.

    Vertical

    :   Distribute all spectra in the canvas so they are evenly
        distributed in a column down the canvas.

    Grid

    :   Distribute all spectra in the canvas so they are displayed as a
        grid with a number of rows and columns that can accommodate all
        the spectra.

    Minimize Borders

    :   Adjust the display of axes and border sizes for efficient use of
        space in gridded windows. Only axes along the left and bottom
        sides of the canvas will be shown. This is the default when
        gridded windows are first created.

    Normal Borders

    :   Adjust the display of axes and border sizes so that the left
        vertical and bottom horizontal axes are shown for all windows.

    Stripify

    :   Open and setup the strip control dialog for the current canvas
        spectrum.

    By Type

    :   Arrange all spectra so they are in a reasonable layout based on
        type (for example, HSQC occupying most space, with proton across
        top and carbon across side).

Graphical Inspector...

:   Display the Graphical Inspector that can be used to view and change
    the attributes (colors, fonts, sizes etc.) of items on the canvas.

###Peaks

Show Peak Inspector...

:   Select this to bring up Peak Analysis Panel
    that can be used to display and edit information about peaks,
    including their assignment value, chemical shift positions, widths
    and intensities.

Add Peak Inspector

:   More than one peak inspector can be displayed. This will create a
    new one.

Show Peak Table...

:   Whereas the Peak Analysis Panel displays information about one peak
    at a time the Peak Table displays a table of information about every
    peak in a selected peak list. The table can be sorted and groups of
    peaks marked for deletion.

Add Peak Table...

:   More than one peak table can be displayed. This will create a new
    one.

Peak Lists Table

:   Show a table of all the open peak lists.  This will include a row for each peak list with the peak list name, the 
dataset (if any) assigned to that peak list, the number of peaks in the peak list, the number of deleted peaks, the number
of peaks with full assignments, the number 
of peaks with partial assignments, and the number of unassigned peaks.

File

:   

    Write List

    :   Write the peak list displayed in the current peak inspector to a
        text file (.xpk).

    Write Aria XML List

    :   Write the peak list displayed in the current peak inspector to a
        text file in the XML format used by ARIA.

    Read List

    :   Read an NMRVIEW format (.xpk) file in.

    Make New List

    :   Create a new empty peak list. You will be prompted for the names
        for the dimensions the list will have. This command is for
        various advanced uses.

    Read All Lists

    :   Read all the peak list files (.xpk) in the current working
        directory.

    Write All Lists

    :   Write all the current peak lists to NMRVIEW format (.xpk) files.

    Read Sparky Save File

    :   Read in a text file created with the Sparky save command. A new
        peak list with the contents of the file will be created.

Edit

:   

    Compress

    :   Remove peaks that have been marked for deletion. This is not
        reversible, and will create gaps in the peak numbering.

    Degap

    :   Renumber peaks (after compressing the list) so that there are no
        gaps in the peak numbering.

    Compress and Degap

    :   Combination of compress, followed by degap. Peaks will be
        permanently deleted, and the list will be sequentially numbered
        with no gaps.

    Delete List

    :   Delete the current list displayed in the peak inspector.

    Reference

    :   Display a graphical interface for setting various attributes of
        the current peak list.

    Couple

    :   Display a graphical interface that can be used to collapse
        multiple peaks separated by defined splittings into a single
        centered peak.

    Cluster

    :   Cluster peaks in the current list based on their chemical shifts
        in certain dimensions. Dimensions used and the tolerance that
        determines whether peaks are clustered are set with a peak
        template. Peak dimensions that are clustered will have a common
        resonance id after clustering.

    Fit

    :   Not yet active.

    Partners

    :   Search all lists for peaks whose chemical shifts (for matching
        dimensions) are similar (within the id tolerance) of the shifts
        of the current peak. Matching peaks are listed to console.

    Identify

    :   Display the Peak Identification interface. This interface will
        suggest possible assignments for the current peak based on the
        chemical shifts of assigned atoms, and distances in the current
        structures.

    Filter

    :   Display the Peak Filtering interface. This interface allows you
        to delete peaks based on various criteria.

Analyze

:   

    HNHA

    :   Display an interface for measuring HN-HA coupling constants as
        described in Kuboniwa et al. J. Biomol. NMR 4 (1994), 871-878:

    HetNOE Analysis

    :   Display an interface for measuring the heteroncuclear NOE using
        peaks in the current list and two datasets, one with, and one
        without, the NOE active.

    Minimum Chemical Shift

    :   Display an interface for measuring the minimal chemical shift
        change for each residue in a chemical shift perturbation
        experiment (typically in the presence of a ligand).

    Peak Peak Matching

    :   Display an interface for coming up with the optimal matching of
        peaks in two different lists.

    Atom Peak Matching

    :   Display an interface for coming up with the optimal matching of
        peaks in one list with the chemical shift assignments of the
        current molecule.

Check

:   

    Check Pattern

    :   Each peak list can have a set of patterns (like i.hn, i-1.c
        etc.) for the types of atoms that give rise to the peaks. This
        command displays an interface used to check the consistency of a
        peak lists assignments with its patterns.

    Check Assignments

    :   Check the assignments of a selected peak list with expected
        values for the assigned atom types (based on BMRB statistics).

    Search Peaks

    :   Display an interface used to search peak lists for peaks based
        on various criteria.

Integrate

:   

    Associate Dataset

    :   Each peak list has an associated dataset. By default this
        dataset is the one from which the list was originally picked.
        You can use this command to select a dataset to be assigned to a
        list.

    Get Volumes

    :   For each peak in the list, integrate the intensities over the
        "footprint" of the peak in the dataset associated with this
        list.

    Get eVolumes

    :   For each peak in the list, integrate the intensities over the
        optimal elliptical "footprint" of the peak in the dataset
        associated with this list.

    Get Intensities

    :   For each peak in the list get the intensity at the peak center
        from the dataset associated with this list.

    Plot Vol. vs. Intensities

    :   Plot an XY chart with the one symbol for each peak positioned on
        the X axis at the peaks intensity, and the Y axis at the peaks
        volume.

    Plot Intensities

    :   Sort the peaks by their intensities and plot the peak
        intensities in decreasing order.

    Plot Volumes

    :   Sort the peaks by their volumes and plot the peak volumes in
        decreasing order.

###Assign

Atoms...

:   Select this to bring up the Assignments Panel that is
    used to keep track of chemical shift assignments.

Resonances...

:   Add a peak at the position of the black crosshair.

Sequence...

:   Select this to bring up a sequence
    display panel to display the residue sequence
    of the molecule.

NOEs...

:   Select this to bring up a panel for creating and editing
    NOE restraint lists.

Constraint Table...

:   Display a table for identifying NOES, and generating and analyzing
    distance constraints.

Dihedral Table...

:   Display a table for generating and analyzing angular constraints.

###Analysis

RunAbout

:   Select this to open up the RunAbout tool used for assigning proteins
    using triple resonance NMR experiments.

Rate Analysis

:   Select this to bring up a panel for analyzing
    time-dependent properties (e.g., relaxation).

Titration Analysis

:   Select this to bring up a titration panel for analyzing titration
    data.

IPAP

:   IPAP is a set of experiments and an analysis protocol for measuring
    dipolar coupling constants in partially oriented media.

###Molecule

Read/Write Topology

:   

    Sequence GUI

    :   Distribute all spectra in the canvas so they are evenly
        distributed in a row across the canvas.

    Sequence File

    :   Bring up a file selection dialog to select and open a file
        containing an amino acid, DNA, or RNA sequence. See the section
        on Molecular Structures to learn about the
        format of this file.

    PDB File (using library)

    :   Bring up a file selection dialog to select and open a PDB format
        file. This is the standard way to read in pdb files. NMRView
        first reads the pdb file to determine the amino acid sequence.
        Next, it reads the corresponding residues from the residue
        library. Finally, it reads coordinates from the pdb file for
        those atoms that have names matching the names in the residue
        library. Atoms, that do not have a match in the residue library
        will not be entered into the structure list. Atoms that are in
        the residue library but not in pdb file, will be included in
        structure list but will not be displayed. See the section on
        Molecular Structures to learn about using
        molecular structures in NMRView.

    PDB File

    :   Reads a file of atomic coordinates of a macromolecule. File must
        be stored in the PDB format as defined by the Protein Data Bank
        (now the RCSB). This command does not also read from the residue
        library so no connectivity information is available. If this is
        needed use the pdb command instead.

    Ligand File (.mol, .sdf)

    :   Open a small molecule (.mol or .sd) file and add it to the
        current molecular topology.

    Write ARIA XML Molecule

    :   Write a text file representation of the current molecule in the
        ARIA XML format.

Nomenclature

:   

    Check/Change Nomenclature...

    :   Analyze the names of the atoms in the current molecule to
        determine if you are using the IUPAC or XPLOR style of
        nomenclature. A selection of atoms violating the most-likely
        nomenclature will be listed.

    Renumber...

    :   Offset the residue numbering (and any assigned peaks) by a
        specified number.

Read Coordinates

:   

    PDB File...

    :   Bring up a file selection dialog to select and open a PDB format
        file. Reads the PDB file filename and attempts to match the
        atoms to atoms in the structure in memory. If atoms match by
        residue name, atom name, sequence number, chain id, and
        alternate identifier then the coordinates corresponding to each
        atom matched are assigned the value of the coordinates of that
        atom in file.

    PDB File (multiple files)...

    :   Reads in coordinates from a series of PDB files. All PDB files
        in the directory are read that whose name ends in an integer
        value (like file1.pdb, file03.pdb, file41.pdb etc.). Each
        coordinate set is stored a separate structure identified by the
        integer number in the file name. The command only reads in the
        coordinates, the topology must have been read in previously.

    PDB File (representative)...

    :   Reads in coordinates from a single file and stores it in
        structure 0. Information about the structure is stored in the
        STAR Saveframe for a representative structure.

    SD File...

    :   Bring up a file selection dialog to select and open an SD format
        file (commonly used for "small" molecules)

Analysis

:   

    Structures...

    :   Display an interface for selecting which structures will be used
        in other tools like the peak identification and constraint
        table, and for calculating superpositions and residue rms
        values.

    Viewer...

    :   Display a molecular viewer for visualizing the current structure
        and constraints(Premium feature).

###Help

About...

:   Display a window showing various details about the currently running
    instance of NMRVIEW

Manual...

:   Display the full manual for NMRVIEW

Send Bug Report...

:   Display an interface in which you can compose a bug report to be
    sent via your email program.


