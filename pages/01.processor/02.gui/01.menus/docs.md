---
title:  Menus and Toolbars
taxonomy:
    category: docs
---


## Menus

### File

Open FID...

:    Display a file dialog in which you can select the unprocessed (FID) NMR data set to open.
Typically you will select an Agilent ".fid" directory, an Agilent "fid" file, or a Bruker "fid" or "ser" file, or an NMRView (.nv). The file will be opened, the first row of raw data displayed,
and the Processor window will be opened.

Open Dataset...

:    Display a file dialog in which you can select the processed  NMR data set to open.
At present you can open NMRViewJ (.nv) and Sparky (.ucsf) format files.
The dataset will be displayed (vector for 1D or contour plot for 2D or higher)
in the currently active spectrum window.  If a dataset is already present it the
active window it will be replaced with the new dataset.


Open Dataset (No Display)...

:    Display a file dialog in which you can select a processed  NMR data set to open.
The dataset will be opened in NMRFx, but won't be immediately displayed in a spectrum
window.  You can select it for display later from the spectrum attributes window
or using the Dataset icon in the toolbar of a spectrum window.

Recent FIDS >

:  A menu of recently opened unprocessed (FID) NMR datasets.  Selecting an item
from the menu will cause it to be opened, and displayed in the active spectrum window.

Recent Datasets>

:  A menu of recently opened,  processed  NMR datasets.  Selecting an item
from the menu will cause it to be opened, and displayed in the active spectrum window.

New Window

:    Create a new spectrum display window.   

New NMRFx Server

:  Sets up a socket that can listen for commands from other applications.  Currently
this can be done from the CoMD/NMR Dynamics Software.

Export SVG...

:    Create an SVG file containing a rendering of the currently active spectrum.  Note:  at present, only the active spectrum chart in a single window will be exported to the file.

### Projects

NMRFx Projects are similar to NMRViewJ projects in that they consist of a main directory and a series of subdirectories.  Each subdirectory contains data for a particular data type (datasets, peaks, molecules etc.).  Data is stored in simple text files (rather than the STAR format used in NMRViewJ).  NMRFx has a built-in copy of Git, a version control system allowing it to keep a history of project changes.

Open...

:    Open an existing project.  Use the file browser that appears to browse to the directory containing the project directory.  Select the project directory and click *Open*.

Open Recent

: This is a sub-menu containing a list of recently used projects.  Choose an entry from the menu to open that project.  Entries in the list show the last three elements of the path to the directory to help you in recognizing projects and distinguishing projects with the same name.


Save

:    Save the project into the various project sub-directories.  All the component files of the project are over-written.  Then a Git commit is done to maintain to record the differences from the previous state of the project.

Save As...

:    Save the project into a new project directory. A file browser will appear that will allow you to choose a directory location in which to save the project.

Close

:  Close the current project.  After you confirm this action, all  molecules, peaklists
and assignments will be discarded.

Open STAR3

:  Read a BMRB STAR3 format file.

Save STAR3...

:  Write project information (peakliss, assignments, molecules etc.) to a BMRB STAR3 format file.

Open Sparky Project:

:  Open a Sparky project file.  Save files reference in the project file and corresponding
.ucsf datasets will also be opened.  This is a preliminary feature and some
attributes of the Sparky files might not be imported properly or at all.

### Spectra

Delete Spectrum

:    Delete the active spectrum chart from a window that has more than one chart in it.  The remaining charts will be resized to fill the empty space.

Arrange

:    Horizontal.  Arrange the spectrum charts in a window with multiple charts such that they occupy a single horizontal row.
:    Vertical.  Arrange the spectrum charts in a window with multiple charts such that they occupy a single vertical column.
:    Grid.  Arrange the spectrum charts in a window with multiple charts such that they occupy a grid of rows and columns.  The number of rows and columns is determined automatically.
:    Overlay.  Convert a grid (or row or column) of spectrum charts into a single chart with all the datasets displayed.  You can switch an overlay of spectra back to a grid (or row or column) using the Grid, Horizontal or Vertical menu items.
:    Minimize Borders. Only display the axis tic marks and labels for charts that are on the bottom or left edge of the spectra.  Those for "internal" spectra are removed to conserve space.
:    Normal Borders. Display the axis tic marks and labels for all charts in the current stage.

Sync Axes

:    Preliminary support for synchronized axes.  All the spectrum charts in a single window will be synchronized across dimensions that share the same label.  Changing the x, y and plane values in one window will result in the other windows being redrawn so that they share the same values on similar dimensions.  There is not currently a method to restrict the synchronization to specified axes, remove synchronization, or synchronize spectrum charts in different windows.  These features will be coming in a subsequent version.


Align Spectra

:    Adjust the referencing so spectra are aligned with each other.  Alignment happens between spectra that are displayed in the same window.  They can be in separate charts within the window, or multiple datasets within a single chart.  Alignment occurs only between the dataset dimensions on the x and y axes (not planes).  Alignment is done by peak picking the spectra (if peak picking has not already been done) and adjusting the referencing such that the distance between nearby peaks is minimized.  The first dataset of the active chart is the target dataset.  Other datasets are aligned to that dataset.  Dataset parameter files are written to save the new referencing.  This process (in current implementation) can be slow if there are a lot of peaks.  Because of this it's a good idea to have the window display zoomed in somewhat.

Analyzer...

:  Display the spectrum analysis window.  This allow you to measure intensities in a specified region of the spectrum (area with the crosshairs).

Show Measure Bar...

: Show a toolbar across the bottom of the spectrum with tools and displayed values used
for measuring positions, position deltas, intensities and signal/noise ratio.

Show Comparator...

: Show a toolbar across the bottom of the spectrum with controls for selecting
a pair from multiple datasets.  You can use it to do pairwise comparisons of
spectra.

Show Regions Analyzer...

:  Show a window with controls for analzying spectral regions.  Regions can be added, adjusted
split and removed. Peaks can be added to the region and an implementation of Objective 
Deconvolution used to add peaks to the region to deconvolute overlapping signals.

Copy Spectrum as SVG Text

:  The spectral display can be copied to the clipboard as SVG (scalable vector graphics)
text.  The result can be pasted into some graphics applications, but at present
this only works for some applications.  For example, we have used this
successfully with Affinity Designer on MacOS.

### Molecules
NMRFx can read in molecular structures in several different formats, including
reading in a sequence and building a molecule from a residue library, reading
PDB files and reading .mol/.sdf files.


***File Menu***

Read Sequence...

:   Bring up a file selection dialog to select and open a file
        containing an amino acid, DNA, or RNA sequence. See the section
        on Molecular Structures to learn about the
        format of this file.

Read PDB...

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

Read PDB XYZ...

:   Reads a file of atomic coordinates of a macromolecule. File must
        be stored in the PDB format as defined by the Protein Data Bank
        (now the RCSB). This command does not also read from the residue
        library so no connectivity information is available. If this is
        needed use the pdb command instead.

Read Mol...

:   Open a small molecule (.mol or .sdf) file.


Sequence GUI

: Display a window in which you can enter the single letter sequence
for an Protein, RNA or DNA polymer.

Atoms

:   Select this to bring up the Assignments Panel that is
    used to keep track of chemical shift assignments.

Viewer

: Display the molecular viewer.  This can be used to display the 3D structure,
a 2D RNA sequence, or a 2D small molecule view.

RDC Analysis...

: Display the RDC Analysis window

Show Spectrum Library

: Display a toolbar at the bottom of the spectrum window that can be used
to select and display the spectrum of molecules from the built-in metabolite
library.

### View

Show Console

:    Display the Console window.  The console can be used in Jython (Java version of Python) or R (statistical language) modes.


Show Datasets

:   Show a table of currently opened datasets.  Each row of the table shows the dataset name, number of dataset dimensions, default contour level, scale value, default contouring parameters and reference information.  Reference information is displayed for a single dimension at a time.  A pop-up menu on the DimN header allows you to choose the display dimension.  The Draw menu at top of the Dataset Table window allows you to draw selected datasets in a variety of arrangements.


Show Attributes

:    Display the spectrum attributes window.


Show Processor

:    Display the Processor control window (it appears automatically if you open an FID)

Show Scanner

:    Display the Scanner window.  The scanner can be used to process, display and analyze sets of spectra.

RNA Label Scheme

: Show a window that can be used to specify the isotopic labeling scheme for RNA
molecules.


### Peaks

Show Peak Tool

:    The Peak tool allows the user to work with peaks and their peak lists.  Users of NMRViewJ will recognize it as being similar to the Peak Inspector and having capabilities of the Peak Reference tool.  

Show Peak Navigator

:    The Peak Navigator will appear as a tool bar at the bottom of the current spectrum window.  It allows stepping through a peak list and updating the spectrum display to a region around the current peak.

Link By Labels

:    This menu action will link peaks that have common labels.  Once linked they will move in synchoriny when using the Peak Slider, and changing the label for one peak will change the label for all linked peak dimensions.

Show Peak Slider

:    The Peak Slider will appear as a tool bar at the bottom of the current spectrum window.  When present peaks that are linked to each other will move together when any one peak is moved.  The toolbar provides tools for freezing (and "thawing") peaks into the current position so they can't be moved.

Show Path Tool

:    Display a tool at the bottom of the spectrum window that can be used for
finding and measuring peak paths present in experiments such as ligand
or pressure titrations.

Show Multiplet Analyzer

:  Display a window containing tools for analyzing multiplets in one-dimensional spectra.

Show Ligand Scanner

:  Display a window containing tools for analyzing shifted peaks including
minimum chemical shift changes and PCA analysis.

**Assign Tools**

   These are all prototypes of new tools for assigning proteins and RNA.  Under rapid
development
    
    Show Peak Assigner

    Show Assign on Pick

    Show Atom Browser

    Show RunAboutX

### Window

Various menu items for showing windows.  The menu items available are platform dependent.

### Help

Online Documentation

:    Open the default web browser and display the online documentation.


NMRFx Publication

:    Open the default web browser and display the first NMRFx Processor publication.  Please cite this reference when publishing manuscripts describing research that used NMRFx Processor in the analysis.

