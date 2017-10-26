---
title:  Table
taxonomy:
    category: docs
---

The Scanner Table provides information on what files should be loaded and information about each of the files.  The path column is the directory (or sub-directory) containing the NMR data file.  The actual file location is relative to the specified (with the Set Scan Directory item in the File menu) scan directory.  For example, if the Scan Directory is set to

/Users/brucejohnson/data/metabolomics

a path entry of "100" will specify a file at

/Users/brucejohnson/data/metabolomics/100


Information in the **sequence**, **ndim**, and **etime** columns will be automatically populated when the directory is scanned.  The appropriate parameter files will be examined to extract this information.  The **etime** field is calculated from the time each dataset was acquired.  The first dataset will given a time of **0** and subsequent datasets will have an **etime** value equal to their acquisition time minus that of the firrst dataset (in seconds).

The **row** and **dataset** columns will be empty until the data is actually processed.

The table can be sorted by clicking on the column header.  Clicking a second time will invert the sort order and a third time will remove the sorting.
