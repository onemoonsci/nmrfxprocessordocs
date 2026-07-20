---
title:  Menus 
taxonomy:
    category: docs
---


## Menus

### File

Open...

:    Display a file dialog in which you can select the NMR dataset to open. You can open raw data (FIDs) in Bruker (fid and ser), Varian/Agilent (fid), Nanalysis (.dx), SpinIt (data.dat) and generic JCAMP (.dx) formats.  You can open processed data in NMRViewJ (.nv), Sparky (.ucsf), Bruker (1r, 2rr...), JCAMP, and SpinIt formats.  The opened data file will replace the current display.  If the data is an unprocessed 1D or 2D (FID) file, the Processor pane will open on the right side and a list of processing operations will be generated and applied.

Recent Files >

:  A menu of recently opened unprocessed (FID) or processed NMR datasets.  Selecting an item from the menu will cause it to be opened, and displayed in the active spectrum window.

Dataset Browser... >

: Open the Dataset Browser which allows you to browse directories and locate NMR datasets.

Export Graphics >

: Export the current spectrum display in SVG, PDF or PNG formats. SVG and PDF are vector formats which preserve the full resolution of the graphics.  PNG files are bitmaps at a fixed resolution.

Open Dataset (No Display)...

: Open processed datasets without displaying them in the current window.  This allows you to use them in non-gui operations, or to have more control over displaying multiple datasets in windows.


### Projects

NMRFx Projects are similar to NMRViewJ projects in that they consist of a main directory and a series of subdirectories.  Each subdirectory contains data for a particular data type (datasets, peaks, molecules etc.).  The primary storage for most information (molecular structure, peak lists, assignments etc.) is a BMRB NMR-STAR format file within the projects **star** subdirectory.  NMRFx has a built-in copy of Git, a version control system allowing it to keep a history of project changes.

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
and assignments will be discarded.  All spectral display windows, but one, will be closed.

Open STAR3

:  Read a BMRB STAR3 format file.

Save STAR3...

:  Write project information (peaklists, assignments, molecules etc.) to a BMRB STAR3 format file.

Open Sparky Project:

:  Open a Sparky project file.  Save files reference in the project file and corresponding
.ucsf datasets will also be opened.  This is a preliminary feature and some
attributes of the Sparky files might not be imported properly or at all.

### Spectra

New Window

:    Create a new spectrum display window.   


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

Copy Spectrum as SVG Text

:  The spectral display can be copied to the clipboard as SVG (scalable vector graphics) text.  The result can be pasted into some graphics applications, but at present this only works for some applications.  For example, we have used this successfully with Affinity Designer on MacOS.

Align Spectra

:    Adjust the referencing so spectra are aligned with each other.  Alignment happens between spectra that are displayed in the same window.  They can be in separate charts within the window, or multiple datasets within a single chart.  Alignment occurs only between the dataset dimensions on the x and y axes (not planes).  Alignment is done by peak picking the spectra (if peak picking has not already been done) and adjusting the referencing such that the distance between nearby peaks is minimized.  The first dataset of the active chart is the target dataset.  Other datasets are aligned to that dataset.  Dataset parameter files are written to save the new referencing.  This process (in current implementation) can be slow if there are a lot of peaks.  Because of this it's a good idea to have the window display zoomed in somewhat.

Analyzer...

:  Display the spectrum analysis window.  This allow you to measure intensities in a specified region of the spectrum (area with the crosshairs).

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
        file. This is the standard way to read in pdb files. NMRFx
        first reads the pdb file to determine the amino acid sequence.
        Next, it reads the corresponding residues from the residue
        library. Finally, it reads coordinates from the pdb file for
        those atoms that have names matching the names in the residue
        library. Atoms, that do not have a match in the residue library
        will not be entered into the structure list. Atoms that are in
        the residue library but not in pdb file, will be included in
        structure list but will not be displayed. See the section on
        Molecular Structures to learn about using
        molecular structures in NMRFx.

Read Coordinates...

:   Reads a file of atomic coordinates of a macromolecule and sets the coordinates of an existing molecule (in NMRFx) to the values found in the file.  File must be stored in the PDB format as defined by the Protein Data Bank.  The atoms and residues of the already in-memory molecule are not changed, only the xyz coordinates.

Read PDB XYZ...

:   Reads a file of atomic coordinates of a macromolecule. File must
        be stored in the PDB format as defined by the Protein Data Bank
        (now the RCSB). This command does not also read from the residue
        library so no connectivity information is available. If this is
        needed use the pdb command instead.

Read mmCIF...

:   Open a macromolecular structure file (the successor to PDB files).  Support for mmCIF files is still under development..


Read Mol...

:   Open a small molecule (.mol or .sdf) file.

Read Mol2...

:   Open a small molecule (.mol2) file.

Read SMILEs...

:   Open a file containing one or more SMILE molecule descriptions.


Input  SMILE...

: Input a molecule in SMILE format.  You will be prompted for the SMILE string and a name for the molecule.  The SMILE string will be parsed and two-dimensional coordinates for the molecule generated.

Clear Molecules...

: Remove all existing molecules (you will be prompted to confirm this action)

Sequence Editor...

: Display a window in which you can enter the single letter sequence
for an Protein, RNA or DNA polymer.

Atom Table...

:   Select this to bring up the Assignments Panel that is
    used to keep track of chemical shift assignments.

Viewer

: Display the molecular viewer.  This can be used to display the 3D structure,
a 2D RNA secondary structure, or a flat (2D) view of a small molecule.

RDC Analysis...

: Display the RDC Analysis window

RNA Label Scheme

: Show a window that can be used to specify the isotopic labeling scheme for RNA
molecules.


### View

Show Console

:    Display the Console window.  The console can be used in Jython (Java version of Python) or R (statistical language) modes.


Show Log Console

:    Display the Log Console window.  The Log Console shows error, information and warning  messages that might be generated during various actions.


Show Datasets

:   Show a table of currently opened datasets.  Each row of the table shows the dataset name, number of dataset dimensions, default contour level, scale value, default contouring parameters and reference information.  Reference information is displayed for a single dimension at a time.  A pop-up menu on the DimN header allows you to choose the display dimension.  The Draw menu at top of the Dataset Table window allows you to draw selected datasets in a variety of arrangements.

Show Regions Table

: Show a table of spectral regions.  The tool has actions for saving, loading, adding, removing and integrating regions.


### Peaks

Show Peak Tool

:    The Peak tool allows the user to work with peaks and their peak lists.  Users of NMRViewJ will recognize it as being similar to the Peak Inspector and having capabilities of the Peak Reference tool.  

Show Peak Table

:    The Peak Table shows a table of all the peaks in a particular list.  


Show Peak List Table

:    The Peak List Table shows a table of all the current Peak Lists.  The table includes information on what dataset the peak list is associated with, the assignments, the number of peaks in the list and the number of peaks that have been marked for deletion or assigned.


Link By Labels

:    This menu action will link peaks that have common labels.  Once linked they will move in synchrony when using the Peak Slider, and changing the label for one peak will change the label for all linked peak dimensions.

Show Ligand Scanner

:  Display a window containing tools for analyzing shifted peaks including minimum chemical shift changes and PCA analysis.

Show NOE Table

:  Display a window containing tools for calibrating and exporting NOE constraints.


Show ZZ Tool

:  Display a window containing tools for fitting ZZ (chemical exchange) datasets
.

**Assign Tools**

   These are all prototypes of new tools for assigning proteins and RNA.  Under rapid
development
    
Assign on Pick

: If this is active then when you pick a peak (in cursor peak-pick mode) you will be prompted for an assignment of the peak. The chemical shift of the pick position will be shown and if that positon overlaps existing assignments you will be given a list of assignments to choose from.  If you close the window without clickign the **Assign** button the peak will be removed.


Show Atom Browser

: Experimental tool for RNA assignments


### Window

Various menu items for showing windows.  The menu items available are platform dependent.

### Help

Online Documentation

:    Open the default web browser and display the online documentation.

NMRFx Web site

:    Open the default web browser and display the [NMRFx web site](http://nmrfx.org).

NMRFx Mailing List 

:    Open the default web browser and display the [NMRFx mailing list site](https://groups.io/g/NMRFx).


NMRFx Publication

:    Open the default web browser and display the first [NMRFx Processor publication](https://link.springer.com/article/10.1007/s10858-016-0049-6).  Please cite this reference when publishing manuscripts describing research that used NMRFx Processor in the analysis.

Check Version

:    Check the NMRFx web site to see what the latest version of NMRFx is.

Open Source Libraries

:    NMRFx uses various open-source libraries.  Open the default web browser and display information on the  open source [libraries](https://nmrfx.org/downloads/oss/dependencies.html) used by NMRFx

