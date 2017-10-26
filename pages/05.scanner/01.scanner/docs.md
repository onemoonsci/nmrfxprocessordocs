---
title:  Scanner
taxonomy:
    category: docs
---

The Scanner Tool can be used to process, visualize and analyze groups of spectra.  Intensity and integral measures are stored in a table and this tabular data is accessible via the R scripting interface.  You can either scan a folder of files to identify all the NMR datasets in the folder or load a table that lists the locations of the files and any metadata about each file.   When scanning a folder for files the scan is recursive, so folders containing folders are searched.  

After loading the table (directly from a table file) or via the folder scanning the **Table** tab region of the Scanner window will contain a table listing all the files.  At a minimum, the following columns in the table will be poplulated.

*   path: The file system path to the file.
*   sequence: The pulse sequence used to collect the data
*   ndim: The number of dimensions in the data
*   etime: The time the dataset was collected, in seconds from the time of the first (in chronological order) file
*   row: Processed files can be placed into a single dataset file.  This gives the row in the file (or plane if the data is 2D).
*   dataset: This gives the name of the dataset containing the processed data for this dimension. 

If you load data via a table file, your table file can contain additional columns that will appear in this table.



## Menus

### File

Set Scan Directory...

:    A directory chooser will be displayed. Browse to and choose a directory. That directory, and all sub-directories will used when scanning and processing the NMR datasets (using the Scan Directory command, described below).

Set Scan Output Directory...

:    A directory chooser will be displayed. Browse to and choose a directory. That directory will be used to write the processed data to as well as file containing information in the table display.

Scan Directory...

:    Search through the **scan directory** (specified with the "Set Scan Directory" menu item) and sub--directories to find a list of NMR datasets (with fid/ser files). The names of all the found datasets will be displayed in the Table tab.  If a **scan directory** hasn't already been specified a directory chooser will be displayed which you can use to choose one.

Open Table...

:    Load a table file that contains the locations of the data files that should be opened.  Additional columns can describe additional metadata about the datasets.  See information below about the format of the file..

Save Table...

:    Save the current table to a file.

Process and Combine

:    Process all the datasets using the current script. The processed files will be combined into single dataset.  If the original data files are one-dimensional a pseudo-2D dataset will be created, with one row for each original dataset.  If the original data files are two-dimensional, then a pseudo-3D dataset will be created, with one plane for each original dataset.  The dataset created will be named **process.nv** and will be written into the directory specified with the **Set Scan Ouput Directory** menu item.  If this hasn't already been specified a directory chooser will be displayed.

Process 

:    Process all the datasets using the current script.  The processed data will will be placed in a series of files named **processN.nv**, where N is the table row number (counting from 1).  The files will be written into the directory specified with the **Set Scan Ouput Directory** menu item.  If this hasn't already been specified a directory chooser will be displayed.

### Table

Use Current State

:    The table can be filtered and sorted (as described below).  This command will remove any rows that are not displayed (via the filtering tools) and will change the order of the rows to correspond to the current sorting.

### Analyze

Measure

:    Measure the intensities for each row of the pseudo-2D dataset.  The measurement is done for the region between the currently displayed vertical crosshairs.  The type of measurement is set by the Mode value in the Parameters tab.


