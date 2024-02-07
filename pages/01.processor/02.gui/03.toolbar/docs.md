---
title:  Menus and Toolbars
taxonomy:
    category: docs
---

## Left Toolbar

![Left ToolBar](images/toolbar.png)

Datasets

:  Click this icon to get a pop-window listing all open datasets.  You can then
click on an entry and drag it into a spectrum window to display it.

Open

:    Display a file dialog in which you can select the NMR data set to open. Typically you will select an Agilent ".fid" directory, an Agilent "fid" file, or a Bruker "fid" or "ser" file. The file will be opened and the first row of raw data displayed.

Attributes

:    Display the attributes panel for controlling how your spectrum is displayed. The attributes panel in NMRFx is designed to work much like that in NMRViewJ (though the code is completely different). 

Refresh

:    Refresh the current display. Useful if a display parameter has been changed, but the display didn't update automatically.

Halt

:    Halt the drawing of the current display. Especially useful for datasets that take longer than a few seconds to draw.

Undo

:  Undo the last change in spectral view (display region and levels).  Multiple
undo actions are stored in a history so they can be redone.

Redo

:  Redo the last last undone command (from the history).

Full

:    Adjust the horizontal (and vertical for 2D spectra) plot limits so the entire dataset is displayed

Expand

:    Expand the view to display the area between the crosshairs.

In

:    Zoom the display in (showing a smaller region of the spectrum).  When the mouse pointer is over this icon you can use the scroll wheel (or scroll gesture on trackpad) to zoom in or out (Scroll control works the same on both the In and Out icons).

Out

:    Zoom the display out (showing more of the spectrum).  When the mouse pointer is over this icon you can use the scroll wheel (or scroll gesture on trackpad) to zoom in or out (Scroll control works the same on both the In and Out icons).

Auto

:    Adjust the vertical scale of 1D spectra so the displayed region of the data mostly fills the vertical expanse of the plot window. Adjust the contour level of 2D spectra to be 5 times an estimate of the noise level in spectrum.

Higher

:    Adjust vertical scale (or contour level for 2D) so peaks appear higher.  When the mouse pointer is over this icon you can use the scroll wheel (or scroll gesture on trackpad) to raise or lower the scale (Scroll control works the same on both the Higher and Lower icons).

Lower

:    Adjust vertical scale (or contour level for 2D) so peaks appear lower.  When the mouse pointer is over this icon you can use the scroll wheel (or scroll gesture on trackpad) to raise or lower the scale (Scroll control works the same on both the Higher and Lower icons).

Pick

:    Peak pick the spectrum.  The region picked is the currently displayed window or the region contained between the crosshairs (if they are present).  The threshold level used for picking 2D and higher dimension datasets will be the current contour level.  The threshold for 1D datasets will be the position of the black, horizontal crosshair.  Picked peaks will be displayed and the peak information immediately saved in a text file in the NMRViewJ .xpk format in a file in the directory containing the dataset.  If the spectrum already has a peaklist then the new peaks will add or replace existing peaks depending on whether peaks are present in the pick region.  If peaks are present, the current list will be cleared and replaced with the new peaks.  If no existing peaks are present in the region, then the new peaks will be appended on to the list of existing peaks.  Peaks can be selected, moved and resized with the cursor in Selection mode.

NvJ

:    NMRFx can display contour files of the processed spectra, but it does not have has many display controls as NMRViewJ.  Selecting this menu option will tell your operating system to open the dataset. Installations of NMRViewJ normally configure the program as the preferred renderer for NMRViewJ datasets so it should open and display the dataset. Versions of NMRViewJ before 9.1 would not open an already open dataset. Starting with 9.1 you will be prompted to reopen the dataset, so version 9.1 is the preferred renderer to use in combination with NMRFx.

Chart

:  The chart icon can be dragged onto the existing window to add a new chart into the current window.  As soon as you click and start dragging the item rectangles will appear on the sides of the current window.  Drag and drop the chart icon into one of these window to add a new chart at that location.  Once you have more than one chart you will only be able to add new charts in the existing orientation (horizontal or vertical).
![Adding Windows](images/window_add.png)

