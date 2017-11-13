---
title: Projects
taxonomy:
    category: docs
---


This chapter discusses managing projects, storing the state of NMRVIEW
between sessions, and the reading and writing of what we'll refer to as
derived data, which includes information such as peak lists, assignments
, polymer sequences, and constraints.

NMRView can export and import derived data from and to simple tabular
files. Many users rely on this method for maintaining a persistent copy
of their data between NMRView sessions. Import and export of peak lists
is invoked via the File menu of the Peak Analysis panel (Read Peaks and
Write Peaks), assignments through the File menu of the Atom Assignments
panel (Read PPM and Write PPM), and sequences through the
Molecule-\>Read\_Topology-\>Sequence menu item on the main control
panel.

While supported, the above protocol is **not** the most appropriate
method for maintaining a persistent copy of the data. The various
read/write methods were actually designed as a means for transferring
data between NMRView and other programs. Using an external program for
automated assignments, for example, could be done by exporting the peak
list from NMRView and then using programs such as awk, tcl or perl to
translate the list to the native format of the external program. It is
particularly important to note that not all information about internal
information such as peak lists is saved in to the peak list text files.
If you are working with an NMRVIEW module such as **RunAbout** you will
lose essential information for the module if you use lists (instead of
STAR files discussed below) to save your data. So don't do it.

The **preferred** method for persistent data storage in NMRView is to
write and read files in the NMR-STAR format (http://www.bmrb.wisc.edu).
This format was chosen for NMRView because it is platform independent
and conforms to a standard. Because it is the format developed and used
by the BioMagResBank for archival of NMR data, the end results of user's
NMR assignment process is already in the format necessary for uploading
to the BMRB. Hopefully, this feature will encourage users to upload
their data. Finally, NMRView is one of the few programs that can
actually read and display BMRB NMR-STAR files. This means it is possible
to download files from the BMRB and load them directly into NMRView. The
large quantity of data available from the BMRB is thus available to NMR
users for aiding in the assignment of homologous proteins or statistical
analysis of chemical shift assignments of proteins.

NMRVIEW now also includes comprehensive project management features that
relieves you of the need to explicitly manage your STAR files and window
state files. When beginning to work with a new project you will find it
very advantageous to set up an NMRVIEW project right at the start.

As of version 4.0.0, NMRView stores derived information in a text file
that uses a STAR format. This is the same type of format used by the
BioMagResBank. NMR-STAR files from the BMRB can be read into NMRView.
The files created by NMRView are largely conformant with the NMR-STAR
format. Minor changes have been made in order to ensure that all the
relevant information is stored. In particular the format used for peak
lists has been modified so as to store information about ambiguous
assignments. Earlier versions of NMRVIEW used the STAR 2.x format.
Starting with NMRViewJ 8.0 we support the new STAR 3.0 format which
allows us to support additional information in the STAR files. For
example, the RunAbout module makes extensive use of Resonances, which
are newly supported in STAR 3.0.

The data for each category of NMR information, assignments, 3D
structures peak lists etc., are grouped together within the STAR file in
a so-called Saveframe. Within each saveframe the data is described by a
series of keyword-data pairs. For example, the following are some of the
keyword-data pairs describing a protein (ubiquitin).

    save_ubiq
    _Entity.Sf_category                 entity
    _Entity.framecode                           ubiq
    _Entity.ID                           1
    _Entity.Name                        ubiq
    _Entity.Type                          polymer
    _Entity.Polymer_type                  polypeptide(L)
    _Entity.Polymer_strand_ID            A
    _Entity.Polymer_seq_one_letter_code_can  ?
    _Entity.Polymer_seq_one_letter_code
    ;
    MQIFVKTLTGKTITLEVEPSDTIENVKAKIQDKEGIPPDQ
    QRLIFAGKQLEDGRTLSDYNIQKESTLHLVLRLRGG
    ;
    _Entity.Number_of_monomers            76
    _Entity.Nstd_monomer                  no
    
    _Entity.Nomenclature                  IUPAC
    _Entity.Capped                  yes

Repetitive information is stored in the form of loops. For example, the
amino-acid sequence of the above polymer is stored as:

    loop_
    _Entity_comp_index.ID
    _Entity_comp_index.Auth_seq_ID
    _Entity_comp_index.Comp_ID
    _Entity_comp_index.Comp_label
    _Entity_comp_index.Entity_ID

    1 1 MET . 1
    2 2 GLN . 1
    3 3 ILE . 1
    4 4 PHE . 1
    5 5 VAL . 1

The scientists at the BMRB have done a particularly thorough job of
defining saveframes and the corresponding keyword-data pairs that can be
used to define the types of NMR data that are typically measured on
biological macromolecules. Included in the NMRView database are the
peaklists, the chemical shift assignments, the molecular topology of any
sequence currently in use, and the coordinates of any structures that
have been read into NMRView.

NMRView reads certain of the data in the database in a way that is
optimized for speed. For example, chemical shifts, assignments,
peaklists and coordinates are read by special routines and stored in
optimized data structures. All other data are read and stored into Tcl
variables. Any information in the database will be read as long as it
corresponds to the STAR format (one exception is that, at present,
nested loops are not read). Thus the end user can add new saveframes to
store any information and know that NMRView will read it and store it in
an accessible manner.

Describe accessing STAR data (to be written).

If you're working with a Project (see next section) all reading and
writing of STAR files will be done via the project tools. But if you
want to work directly with STAR files without a project use the entries
in the <span class="menuchoice">File \> STAR</span> menus. When you
first create a STAR file it is a good idea to name the file something
like myfile1.str, where the name ends with a non-integer character
followd by an integer value. Then you, as you're working you can
periodically use the <span class="menuchoice">File \> STAR \> Save STAR3
(Autoincrement)</span> menu entry. This will generate a name for the
star file that increments the integer portion of the name (myfile2.str,
myfile3.str etc.).

For new projects you should be working with STAR version 3.x format
files, but if you need to work with existing files in the version 2.x
format you can use the entries in the <span class="menuchoice">File \>
STAR2 (deprecated)</span> menu. It is possible to load a version 2.x
file, and write out a version 3.x file to upgrade the format of the
file.

NMRVIEW can directly load STAR 3 files from the BMRB. Note, that the
BMRB has not updated all of the entries to the new STAR 3.x format so
there may be entries that you want, but which are unavailable through
this Fetch method. Available entries can be downloaded within NMRVIEW by
choosing the <span class="menuchoice">File \> STAR \> Fetch from
BMRB</span> menu item. In the dialog that appears enter the accession
number (e.g. 15430) and click the Fetch button. The selected entry will
be downloaded to a file on your computers disk and loaded into NMRView.
Before downloading another entry you should use the Clear button in the
Project browser This will clear out the existing entry. Tip: if your are
behind a firewall you may need to enter a proxy name and port number in
order to access the BMRB.

##Projects

Projects are managed as a set of folders (directories) under one project
folder. Prior to NMRViewJ version 9.2 the folder for each project
was always placed inside another folder that stored a group of projects.
Starting with version 9.2, projects can be placed anywhere.  

A project can be created before or after you start working
analyzed data.  A new project can be created by choosing New from
the File>Project menu.

> **Warning**
>
> Creating a new project does not immediately save any current data 
> such as peak lists and assignments.  You must explicitly use the Save
> menu item.  As an alternative, use Save... from the Project menu
> to create a new project and save the current data into it.


After you select the **New** menu item a file chooser will
appear.  Use it to browse to the location you want the
new project to be created in, enter a project name
next to **Save As:**, and click **Save**.

Versions of NMRViewJ prior to 9.2 presented you with the option
to use XPLOR style naming rather than IUPAC naming for atoms. 
Current versions default to using IUPAC naming (there are 
workarounds for this if needed, see the useIUPAC flag listed
in the section below on the project.txt file).

The new project folder will be created along
with a set of project specific sub-folders. The structure of the project
root and one example project folder as will be created in this process
are shown here.

Six different sub-folders will be found in each project:

datasets

:   Any NMR datasets readable by NMRViewJ that are in this folder will
    be opened automatically whenever the project is opened, if the
    Datasets check button is selected.

star

:   When you save a project, a STAR 3 format file will be created here
    containing the molecular topology, peak lists, atomic assignments,
    distance and dihedral constraints, and other information. When you
    open a project, the latest STAR file as defined by the numerical
    extension (file1.str, file2.str etc.) will be opened, if the STAR
    check button is selected.

list

:   The default directory when you read and write peak lists is this
    directory. But, please remember, you shouldn't need to explicitly
    write peak lists as all peak information will be stored in the STAR
    file.

win

:   You can save the state of any opened spectral window by clicking the
    Spectrum icon bar Favorites icon. The window state will be saved in
    this folder.

tcl

:   Any Tcl scripts that are stored in this folder will be sourced in
    when the project is opened. This is the appropriate place to put any
    project specific scripts.

structures

:   The default directory when you read and write structure (PDB) files
    is this directory.

When a project is loaded datasets are automatically opened from a a set
of specified directories. The project's own dataset directory is always
scanned and you can add additional directories in the **Data Dirs**
section of the **Project Attributes** window.  You can
display this window from the **Attributes** menu item in the Project menu.
Click the Browse button in this
section to select directories you wish to include. As you select
directories they will appear in the list. You can remove a directory by
highlighting the entry in the list and clicking the Delete key.

When NMRVIEW scans the listed directories it looks not only in each
specified directory, but recursively through any sub-folders. Thus it
will fid any datasets contained anywhere below the listed directories.

When a new project is created a 
a project file (project.txt) containing the state of various
parameters will be created inside the project folder.
 A typical project file is shown here and contains parameters
specifying whether to load datasets, load the latest STAR file, and
whether to use IUPAC mode for atom nomenclature. Note that by default,
the if the dataPath entries refer to folders in your HOME directory
they will be specified relative to the symbolic home location. That way
you can copy the project folder to another computer where you have
datasets in a similar relationship to the home directory.

    loadStar 1
    loadDatasets 1
    useIUPAC 1
    dataPath {$env(HOME)/nvprojects2/test2/datasets}
    dataPath {$env(HOME)/data/titrationkg}

You can open an existing project (including newly created ones) by
using the **Open** menu item in the Project menu.  
the project in the Available Projects list and clicking the Open button.
If you have any existing project data open (peak lists and molecular
structures) you will get a warning and a request that data needs be be
cleared first. You can explicitly remove any existing project data by
clicking the the Clear button located next to the name of the **Active
Project.** Note you can use this button even if you're not working with
a project and simply want to remove data such as molecules and peak
lists so that you can, for example, load a new **STAR** file.

When you open the project all appropriate datasets will be loaded, the
latest STAR file will be read and the project window description file
will be processed so that all spectral windows should be displayed as
they were when you saved the project.

As you work with a project you should periodically use the <span
class="menuchoice">File \> Projects \> Save</span> menu item to save the
project data. Each time you do this a new STAR file will be written to
the projects' star folder and the state of all windows will be saved.

When you're working with a project you can take advantage of the
Favorites system. This lets you save and reload the state of any windows
(this is separate from the saving of all window states that happens when
you save the whole project). Just click the
![](images/nuvola/22x22/actions/bookmark_add.png) button on the Spectrum
window's icon bar to save state of the currently active window. You'll
be prompted for a window name and then the window data will be written
into a ".nvw" file in the win folder of the current project. You can
retrieve the window state by selecting the the <span
class="menuchoice">Windows \> Favorites</span> menu item. When you do
this a list of all available window files for that project will be
displayed. Just select one and click the Open button.
