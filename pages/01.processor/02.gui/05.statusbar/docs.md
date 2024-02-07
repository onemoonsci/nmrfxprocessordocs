---
title:  Menus and Toolbars
taxonomy:
    category: docs
---

## Bottom Toolbar

![Bottom ToolBar](images/status_bar.png)

CrossHair Mode

:   The crosshair can be in one of two modes.  In Crosshair mode it is used to position crosshairs.  In Selector mode, it is used to select, move and resize peaks.

X,Y

:   Zero, one (X) or two (X and Y) menus will be displayed depending on the dimensionality of the displayed dataset.  These can be used to specify which dataset dimension is displayed on the corresponding axis.  For example, a 2D HSQC dataset would have a single (X) menu with choices like 1:HN and 2:N.  Selecting 2:N, would switch the display so that the N15 dimension is along the X axis, and the H1 dimension is along the Y axis.  These menus are not displayed for FID display.

CrossHair Positions

:    Four text boxes display the current positions of active crosshairs.  You can also use these to change the crosshair positions to a specific value.  Just type a number into the box and hit the Return key or change the focus to another text box.  Note:  if the crosshairs are not currently displayed, then the posiiton values represent the current plot limits for the X and Y axes.


Z,A,...

:  Zero, one (Z), or more menus and plane display controls are displayed depending on the dimensionality of the displayed dataset.  The menu can be used to jump the displayed planes to selected values (Full: all planes, First: the first plane, Last: the last plane, Center: the center plane, and Max: the plane with the maximum intensity at the position of the black crosshairs). 
:    The first text box displays the plane position in ppm.
:    The second text box displays the plane position in plane numbers (pts).
:    The spinner control (up/down arrows) can be used to increment the plane number.
:    If the mouse pointer (cursor) is over either the ppm or plane display you can use a mouse scroll wheel or trackpad scrolling to scroll through the planes.
:    You can type a number into the plane field, and hit the Return key to jump to a plane.
If you have a range of planes displayed, the ppm and pt fields represent the center of the range.  The actual limits of the range can be seen (and controlled) in the spectrum attributes window View tab.

Phasing

:    Display the phasing tool along the left edge of the spectrum.  Phasing is not yet active for datasets that are not actively the result of processing an FID in the current session.

Slices

:    Display horizontal and vertical slices through the spectrum at the position of the black crosshairs.  This menu is not displayed for FID display.

Complex

:    Display both the real and imaginary parts of 1D vectors.  This menu is not displayed for dataset (spectrum) display.

## Vector sliders

![](images/vector_slider.png)

This tool is only displayed in Processing mode.
At the left side of the data display are two controls, a combobox near the top, and a slider control along the left edge. Typically in 2D, phase sensitive, NMR spectra two data vectors are collected for each time point which differ from each other in the phase of one of the pulses by 90 degrees. With higher dimensional datasets an increasing number of data vectors are collected for each time increment. The combo box at top can be used to select which of the group of data vectors associated with a given time increment are to be displayed. This can be useful in determining whether you've set up the right type of data combination operations.

The slider control can be used to scroll through all the 1D vectors along the active dimension.  As you slide the control any current processing operations for the active dimension will be applied to the vector before display.


