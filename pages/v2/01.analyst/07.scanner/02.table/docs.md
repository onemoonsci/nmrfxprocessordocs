---
title:  Table
taxonomy:
    category: docs
---

The Scanner Table provides information on what files should be loaded and information about each of the files and a means to select one or more rows of data for display.  The path column is the directory (or sub-directory) containing the NMR data file.  The actual file location is relative to the specified (with the Set Scan Directory item in the File menu) scan directory.  For example, if the Scan Directory is set to

/Users/brucejohnson/data/metabolomics

a path entry of "100" will specify a file at

/Users/brucejohnson/data/metabolomics/100


Information in the **sequence**, **ndim**, and **etime** columns will be automatically populated when the directory is scanned.  The appropriate parameter files will be examined to extract this information.  The **etime** field is calculated from the time each dataset was acquired.  The first dataset will given a time of **0** and subsequent datasets will have an **etime** value equal to their acquisition time minus that of the firrst dataset (in seconds).

The **row** and **dataset** columns will be empty until the data is actually processed.

The Scanner Table can be used to update the current spectrum display.  The method for doing this depends on what data is available and the state of the Processor Controller Window.  If the Processor Control window is open, and it's display mode is set to FID you can load the corresponding dataset by double-clicking on a table row.  The FID will be loaded and the current processing script will be applied.

If the Processor Control window is hidden, or it's display mode is set to Dataset the spectrum chart is updated as you change which rows of the table are selected.  For this to work, processed data must be available for each row.  Just click once to select a single row, shift click to add a range of rows, or Command-click to select a multiple, possibly non-contiguous, rows.

The table can be sorted by clicking on the column header.  Clicking a second time will invert the sort order and a third time will remove the sorting.

The Scanner Table rows can be filtered based on their values. This is very useful to exclude certain rows based on a variety of criteria.  Right click on the column header to bring up a filter list with entries for each unique valu in the column.  Deselecting an entry and clicking **Apply** will hide all rows with that value.  You can deselect all values by clicking **None** and select all values by clicking **All**.  Filtering can be applied in multiple columns.  Any columns with filtering active will have a Funnel icon displayed in the column header.

It can be useful to permanently apply sorting or filtering.  After you've set up sorting or filtering choose the **Use Current State** entry in the **Table** menu.  Any rows that have been filtered out of the display will actually be removed from the table.  The current sort order will be applied to the actual data values so they will have this order without any sorting applied.

The table can be saved to a text file with **Save Table...** entry in the **File** menu.  Saved tables can be reloaded with the **Open Table...** entry.  When loading a table that has row and dataset entries the dataset in the first row of the table will be opened and displayed in the spectrum chart.
