---
title:  Operations
taxonomy:
    category: docs
---


Create and display a list of processing operations for each dimension. Besides adding individual operations there are two choices in the operation menu for adding multiple operations. Choosing "Common Scripts->Gen All Dims" will analyze the parameters in the FIDs parameter files and generate a script for processing all dimensions. After execting this command you can go to each dimension and add, modify and delete individual operations. This feature has not been tested on a wide variety of datasets yet, so it may not always be correct (for example, some dimensions may need to be reversed). Indeed, it is not always possible to deduce the most appropriate processing operations as there may be actions in the pulse sequence that are not reflected in specific parameters. Choosing "Common Scripts->Basic 1 Dimension" will insert a set of standard operations for the current dimension. 

####Add Operation

Operations can most conveniently be added by selecting one from the "+" menu. Alternatively the name of an operation can be typed in the text entry field to the right of the "+" menu. Typing in an entry can be useful if one wants to add a second instance of the same operation. Using the menu will replace any operations of the same name, but if you precede the name of an operation with a "+" character (like +ZF) an additional copy of the operation can be added. When typing, you can either enter just the name of the operation (ZF) or the operation along with parameters ( ZF(size=1024) ). Operations can be deleted by selecting it and then hitting the "Delete" key. Each operation is placed at a default position, relative to any existing operations in the list, but you can click and drag an operation to a new position in the list if you would like it at some other location.

####Configure Operation

Most operations have configurable parameters. Click on the operation in the list to display a control region below the list. Different controls will be displayed depending on the type of the parameter . Boolean values get a check box and real or integer values with large ranges get a simple entry field. Values with defined ranges will generally be displayed as a slider. Sliders for real values have a "-" and "+" button at the right end which can be used to adjust the range of the slider. Parameters with a defined list of possible values will be displayed with a combobox. Any change to a parameter will immediately update the operation list and apply the processing to the current vector. It is of course possible to enter values that generate an invalid set of operations. An error message will be displayed near the bottom of the interface, and the errant operation will be highlighted in red.
