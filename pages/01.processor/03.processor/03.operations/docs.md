---
title:  Operations
taxonomy:
    category: docs
---

Processing in NMRFx Analyst is done by executing a series of operations.  These include common actions like apodization, zero-filling, and Fourier Transform.  Operations are normally executed in groups that correspond to the dimensions of the dataset.  Operations act on three different categories of data

Vectors
: Most operations read a vector of data values.  These vectors correspond to FIDs in the first (direct dimension) or columns of data values in the higher (2,3..) indirect dimensions of the data file. These are the most common operations and do the standard processing.  For example, a typical sequence of vector operations for a 1D file would be apodization (exponential multiplication), zero-filling, Fourier transformation, phasing, and baseline correction

Indirect Matrices
: These operations read in a matrix of values that correspond to the indirect dimensions (for example, the 2nd and 3rd dimension of a three-dimensional experiment.  These are typically used for processing of non-uniformly sampled datasets.  After the first dimension is processed (with a series of vector operations), matrices containing the indirect data are read in and processed to replace zero (non-measured) values with estimates of data values that would be present if they had been measured.

Dataset
: Operations on the entire dataset are used for automatically phasing (with the **DPHASE** operation) the entire dataset by examining all points in the dataset, not just values along individual vector slices.

The set of operations used to process a full dataset can be created in three ways. First, when you read in a one- or two-dimensional experiment the data parameters will be examined and an appropriate set of operations will be generated.  Second, you can generate the operations with the **Auto Generate** menu item in the **Script** menu at the bottom of the processor.  This can be used if there are no operations present (you've either deleted them, or it is a higher-dimensional experiment where auto-generation doesn't happen when the FID is loaded) or if you want to replace a set of operations with a new, automatically generated, set.  Finally, you can add individual operations with the **+** menu on each *Dimension* panel.  You can start from scratch (with an empty list of operations) or add new ones to an existing set.


####Configure Operation

Most operations have configurable parameters. Click on the operation's title bar list to expand the panel to show a control region. Different controls will be displayed depending on the type of the parameter . Boolean values get a check box and real or integer values with large ranges get a simple entry field. Values with defined ranges will generally be displayed as a slider. Sliders for real values have a "-" and "+" button at the right end which can be used to adjust the range of the slider. Parameters with a defined list of possible values will be displayed with a combobox. Any change to a parameter will immediately update the operation list.  If you are in **FID w/OPs** mode,  the processing to the current vector and the chart display will update with the processed vector.  If you are in **Auto Update** mode (choice box at the bottom of the processor), then the entire dataset will be processed with the updated parameters.

Some operations have button or menus that can be used to configure the operation.  For example, the **Phasing** operation has controls to be used for setting pivots, setting preset phase values, or automatically calculating phases.

####Add Operation

Operations can most conveniently be added by selecting one from the "+" menu on each *Dimension Panel*.
Operations can be deleted by right-clicking on the operation's title bar and selecting the "Delete" item in the menu that appears. Each operation is placed at a default position, relative to any existing operations in the list, but you can click on the arrows on the right side of the title bar and drag an operation to a new position in the list if you would like it at some other location.

The **+** menu has three submenus.

Commonly Grouped Operations:
:  These menu items insert multiple operations that are often used together

Common Operations
:  A subset of operations that are commonly used (placed here so they are easy to find)

Advanced Operations
:  All the possible operations, grouped into categories
