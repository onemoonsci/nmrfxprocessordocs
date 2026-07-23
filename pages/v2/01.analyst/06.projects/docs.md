---
title: Projects
taxonomy:
    category: docs
---


This chapter discusses managing projects, storing the state of NMRFx Analyst between sessions, and the reading and writing of what we'll refer to as derived data, which includes information such as peak lists, assignments , polymer sequences, and constraints.

NMRFx Analyst can export and import derived data from and to simple tabular files. Many users rely on this method for maintaining a persistent copy of their data between NMRFx Analyst sessions. Import and export of peak lists is invoked via the File menu of the Peak Tool (Read Peaks and Write Peaks), assignments through the File menu of the Atom Assignments panel (Read PPM and Write PPM), and sequences through the Molecule-\>Read\_Topology-\>Sequence menu item on the main control
panel.

While supported, the above protocol is **not** the most appropriate method for maintaining a persistent copy of the data. The various read/write methods were actually designed as a means for transferring data between NMRFx Analyst and other programs. Using an external program for automated assignments, for example, could be done by exporting the peak list from NMRFx Analyst and then using programs such as awk, tcl or perl to translate the list to the native format of the external program. It is particularly important to note that not all information about internal information such as peak lists is saved in to the peak list text files.  If you are working with an NMRFx Analyst module such as **RunAbout** you will lose essential information for the module if you use lists (instead of STAR files discussed below) to save your data. So don't do it.

The **preferred** method for persistent data storage in NMRFx Analyst is to write and read files in the NMR-STAR format developed by the [BMRB](http://www.bmrb.io).  This format was chosen for NMRFx Analyst because it is platform independent and conforms to a standard. Because it is the format developed and used by the BioMagResBank for archival of NMR data, the end results of user's NMR assignment process is already in the format necessary for uploading to the BMRB. Hopefully, this feature will encourage users to upload their data. Finally, NMRFx Analyst is one of the few programs that can actually read and display BMRB NMR-STAR files. This means it is possible to download files from the BMRB and load them directly into NMRFx Analyst. The large quantity of data available from the BMRB is thus available to NMR users for aiding in the assignment of homologous proteins or statistical analysis of chemical shift assignments of proteins.

NMRFx Analyst now also includes comprehensive project management features that relieves you of the need to explicitly manage your STAR files and window state files. When beginning to work with a new project you will find it very advantageous to set up an NMRFx Analyst project right at the start.

NMRFx Analyst stores derived information in a text file that uses a STAR format. This is the same type of format used by the BioMagResBank. NMR-STAR files from the BMRB can be read into NMRFx Analyst.  The files created by NMRFx Analyst are largely conformant with the NMR-STAR format. Minor changes have been made in order to ensure that all the relevant information is stored. In particular the format used for peak lists has been modified so as to store information about ambiguous assignments. 

The data for each category of NMR information, assignments, 3D structures peak lists etc., are grouped together within the STAR file in a so-called Saveframe. Within each saveframe the data is described by a series of keyword-data pairs. For example, the following are some of the keyword-data pairs describing a protein (ubiquitin).

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

Repetitive information is stored in the form of loops. For example, the amino-acid sequence of the above polymer is stored as:

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

The BMRB group has done a particularly thorough job of defining saveframes and the corresponding keyword-data pairs that can be used to define the types of NMR data that are typically measured on biological macromolecules. Included in the NMRFx Analyst database are the peaklists, the chemical shift assignments, the molecular topology of any sequence currently in use, and the coordinates of any structures that have been read into NMRFx Analyst.

NMRFx Analyst reads certain of the data in the database in a way that is optimized for speed. For example, chemical shifts, assignments, peaklists and coordinates are read by special routines and stored in optimized data structures. All other data are read and stored into Tcl variables. Any information in the database will be read as long as it corresponds to the STAR format (one exception is that, at present, nested loops are not read). Thus the end user can add new saveframes to store any information and know that NMRFx Analyst will read it and store it in an accessible manner.


If you're working with a Project (see next section) all reading and writing of STAR files will be done via the project tools. But if you want to work directly with STAR files without a project use the entries in the **Project -> STAR** menus. 

##Projects

Projects are managed as a set of folders (directories) under one project folder.

A project can be created before or after you start working with analyzed data.  A new project can be created by choosing Save As... (or Save if there isn't a project currently open)  from the **Project** menu.


After you select the **Save As** menu item a file chooser will appear.  Use it to browse to the location you want the new project to be created in, enter a project name and **Save**.

The new project folder will be created along with a set of project specific sub-folders. The structure of the project root and one example project folder as will be created in this process are shown here.

Six different sub-folders will be found in each project:

datasets

:   Any NMR datasets readable by NMRFx AnalystJ that are in this folder will
    be opened automatically whenever the project is opened.  When you create a project, or do Save on a currently opened project, any currently opened datasets will be saved in the datasets.  Datasets are not technically saved in the datasets folder.  Instead, links are made to the location where thedataset actually exists.  These are so-called hard links (rather than symbolic links).  That means that if you delete the original file (in a location other than the project datasets folder) the file will still exist in the datasets folder.

star

:   When you save a project, a STAR 3 format file will be created here containing the molecular topology, peak lists, atomic assignments, distance and dihedral constraints, and other information. The STAR file has the name of the project (with a .str extension).  Note: if you rename a project you currently need to go into the folder and rename the STAR file to be consistent with the new project name.

peaks

:   This folder will contain peak lists saved in the .xpk2 format.  But these are redundant with the information stored in the STAR file.  They are only here for the users convenience to access peaks in a simple text file format.

windows

:   When you save a project all open windows will be described in .yaml format files in this folder.  When you reopen a project these files will be read and the information in the file used to recreate the windows as they existed when the project was saved.  The folder also contains .yaml files for windows saved with the **Favorites** icon in the toolbar.

molecules

:   Molecules can be saved in text files here, but as with *peaks* the information is redundant with that in the STAR file.

shifts

:   Chemical shifts are stored in text files here, but as with *peaks* the information is redundant with that in the STAR file.

shifts

:   Reference Chemical shifts (typically generated with chemical shift prediction) are stored in text files here.


You can open an existing project (including newly created ones) by using the **Open** menu item in the Project menu.  If you have any existing project data open (peak lists and molecular structures) you will get a warning and the project won't be opened. . You can explicitly remove any existing project data by using the **Close** menu item. 

When you open the project all appropriate datasets will be loaded, the STAR file in the project will be read and the project window description file will be processed so that all spectral windows should be displayed as they were when you saved the project.

As you work with a project you should periodically use the **Projects -> Save** menu item to save the project data. Each time you do this a new STAR file will be written to the projects' star folder and the state of all windows will be saved.

When you're working with a project you can take advantage of the Favorites system. This lets you save and reload the state of any windows (this is separate from the saving of all window states that happens when you save the whole project). Just click the
Favorites icon on the Spectrum window's toolbar to save state of the currently active window. You'll
be prompted for a window name and then the window data will be written
into a ".yaml" file in the windows folder of the current project. You can
retrieve the window state by selecting the the **Spectrandows->Favorites** menu item. When you do this a list of all available window files for that project will be displayed. Just select one and click the Open button.
