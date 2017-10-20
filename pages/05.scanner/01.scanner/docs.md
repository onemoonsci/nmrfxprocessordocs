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

If you load data via a table file, your table file can contain additional columns that will appear in this table.

 Use this to scan a folder for all the contained NMR folders. A list will be displayed of all the datasets found, and then they can all be processed with the same script. 

## Menus

### File

Scan Directory...

:    A directory chooser will be displayed. Browse to and choose a directory. That directory, and all sub-directories will be scanned to find a list of NMR datasets (with fid/ser files). The names of all the found datasets will be displayed in a list. Double-click on an entry in the list to open up the selected dataset. Configure processing for that dataset as is normally done in NMRFx Processor.

Open Table...

:    Process all the datasets using the current script. At present, each processed dataset will be placed in the folder containing the FID file it was derived from.

Save Table...

:    Process all the datasets using the current script. At present, each processed dataset will be placed in the folder containing the FID file it was derived from.

Process and Combine

:    Process all the datasets using the current script. At present, each processed dataset will be placed in the folder containing the FID file it was derived from.

Process 

:    Process all the datasets using the current script. At present, each processed dataset will be placed in the folder containing the FID file it was derived from.

### Table

Use Current State

:    dddd

### Analyze

Measure

:    dddd


