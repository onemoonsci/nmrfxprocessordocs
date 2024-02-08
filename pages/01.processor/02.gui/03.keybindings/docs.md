---
title:  Keyboard Bindings
taxonomy:
    category: docs
---

## Key Bindings

You can quickly navigate around spectra and peak-lists using keys on 
the keyboard. To use this feature the active window must have the
"focus", that is, it must be the last window you clicked the mouse in.

### Multi-key bindings

***Add peak***
These key sequence are used to add a peak at the position of the mouse.

**aa**

: Search for the local maxima and add a peak box there.  For
2D (contour) displays The cursor
must be positioned over a peak (contours displayed), but doesn't 
have to be exactly at the position of maximum intensity.

**as**

: Add a peak at the exact position of the mouse cursor.  There
doesn't have to be a peak displayed (local intensity above the 
display contour) at that position.

***Change cursor mode***
The cursor can be displayed in two (at present) modes, Crosshair
and Selector. The actions taken when clicking and dragging the
mouse depend on the cursor mode and these can be changed
with the following key bindings.

**c1**

: Change to single button mouse mode (both cursors can
be moved by pressing and dragging with the left mouse button down.

**c3**

: Change to three button mouse mode.  The black crosshairs
are moved with the left mouse button down, and the red
crosshairs moved with the middle mouse button down.

**cc**

: Change to the Crosshair cursor (from Selector).  Does not
change 1-button/3-button mode.

**cs**

: Change to the Selector cursor (from Crosshair).  Does not
change 1-button/3-button mode.

***Peak slider***
The peak slider is a tool that can be displayed at the bottom of the spectrum window
and is used in one of NMRFx's peak assignment modes.


**df**

: Freeze the currently selected peak. Frozen peaks
can no longer be slide, and their chemical shifts will
be sued to update that of the atoms assigned to 
each of the peaks dimensions.

**dt**

: Thaw the currently selected peak.  After thawing,
a previously frozen peak will be moveable again.

**ds**

: Tweak a peak box by sliding it into the postion of nearest
overlapping peak position. It will also be frozen.

**da**

: Add (show) the peak slider at bottom of current window.

**da**

: Quit (hide) the peak slider tool.


***Jump To(x,y,z,a)***
These key sequences allow you to quickly jump the spectrum view to specified plot limits. The jump key sequences start with a **j** key 
followed by a letter specifying the axis (x, y, ...) they act on.  The behaviour of some of the key patterns differ between the visible
axes (x and y) and planes (z, a ...).  In the following descriptions, the **?** stands for the axis name.  

**j?VALUE**

:   For axes representing planes (like **z**), this will jump the view to the specified plane. If the VALUE  has a decimal point (**jz117.3**), then
the value represents a position in ppm.  If there is no decimal point (**jz32**), the value represents a plane number.  For visible axes (x and y), 
the view will jump to be centered on the specified value.  Because the number of characters is dependent on the specified value, you
need to end the value by pressing the Enter key.


**j?b**

:    Jump to the bottom (first) plane.  Not allowed for visible axes (x and y).


**j?c**

:    Jump to the center plane.  Not allowed for visible axes (x and y).


**jzf**

:    Set the plot limits (or range of planes) for the specified axis to the full range. 


**jzm**

:    Jump to the plane that has the maximum intensity at the position of the intersecting black crosshairs.  Useful when showing a range of
planes to jump to the plane with a visible peak.


**jzt**

:    Jump to the top (last) plane.  Not allowed for visible axes (x and y).




***Jump To(x,y,z,a)***
These key sequences allow you to quickly jump the spectrum view to specified plot limits. The jump key sequences start with a **j** key 
followed by a letter specifying the axis (x, y, ...) they act on.  The behaviour of some of the key patterns differ between the visible
axes (x and y) and planes (z, a ...).  In the following descriptions, the **?** stands for the axis name.  

**j?VALUE**

:   For axes representing planes (like **z**), this will jump the view to the specified plane. If the VALUE  has a decimal point (**jz117.3**), then
the value represents a position in ppm.  If there is no decimal point (**jz32**), the value represents a plane number.  For visible axes (x and y), 
the view will jump to be centered on the specified value.  Because the number of characters is dependent on the specified value, you
need to end the value by pressing the Enter key.


**j?b**

:    Jump to the bottom (first) plane.  Not allowed for visible axes (x and y).


**j?c**

:    Jump to the center plane.  Not allowed for visible axes (x and y).


**jzf**

:    Set the plot limits (or range of planes) for the specified axis to the full range. 


**jzm**

:    Jump to the plane that has the maximum intensity at the position of the intersecting black crosshairs.  Useful when showing a range of
planes to jump to the plane with a visible peak.


**jzt**

:    Jump to the top (last) plane.  Not allowed for visible axes (x and y).

***Undo commands***
Changes in view (display region or contour level) can be undone and redone.
A history of changes is maintained so multiple actions can be undone and redone.

**uu""

: Undo last change.

**ur""

: Redo last undone change.


***View***
The View commands allow quickly changing the spectrum display plot limits.

**vc**

:    Center the spectrum at the position of the crosshair.  This moves the spectrum view, but doesn't change the overall plot range.


**ve**

:     Expand the view to represent the area inside the currently displayed crosshair box.


**vf**

:     Change the view to represent the full range of the current dataset.


**vi**

:    Zoom the view in (so it shows a smaller region of the dataset, centered on current view center).


**vo**

:    Zoom the view out (so it shows a larger region of the dataset, centered on current view center).


**vr**

:   Read Limits: Stores into a buffer the current plot limits of the
    window including the dataset dimensions assigned to each axis, and
    the chemical shift range displayed on each axis. Does not store
    parameters such as the assigned dataset, peak lists, colors etc. Use
    Copy/Paste (see above) for those parameters.


**vw**

:   Write Limits: Sets the plot limit parameters of the window to those
    store to the limits buffer with the read limits command (see above).


###  Arrow Keys

Use the cursor keys to move up or down planes in 3D and 4D spectra,
increment or decrement rows and columns in 1D displays of 2D,3D or 4D
spectra, change contour levels, and rotate spectra.  These keys are active
in both the legacy key binding and new (Extra) key binding modes.

**Down Arrow**

:   1Dx: Move up a row. 3D,4D Spectrum: Move Down a plane.

**Up Arrow**

:   1Dx: Move down a row. 3D,4D Spectrum: Move Up a plane.

**Left Arrow**

:   1Dy: Move left a column. 4D Spectrum: Move Down a Z2 plane.

**Right Arrow**

:   1Dy: Move right a column. 4D Spectrum: Move Up a Z2 plane.

**Control-Up Arrow**

:   Increase contour level.

**Control-Down Arrow**

:   Decrease contour level.

**Shift-Right Arrow**

:   Rotates the view of the spectrum by incrementing the dimension
    displayed on the y axis. For example, for a three-dimensional
    dataset, if the dataset dimensions displayed on the x, y and z axis
    are 1, 2 and 3, after this key-action, the dataset dimensions will
    be 1,3 and 2. Clicking again will rotate the view again, back to
    dimensions 1,2 and 3. Rotation is around the center of the currently
    displayed view, so that the new chemical shift of the z axis, is the
    value that was at the center of the previous y axis.

**Shift-Left Arrow**

:   Same as Shift-Right Arrow, but instead the dataset dimension on the
    y axis is decremented. The direction of rotation only matters if the
    dataset has more than three dimensions.

**Shift-Up Arrow**

:   Rotates the view of the spectrum by incrementing the dimension
    displayed on the x axis. For example, for a three-dimensional
    dataset, if the dataset dimensions displayed on the x, y and z axis
    are 1, 2 and 3, after this key-action, the dataset dimensions will
    be 3,2 and 1. Clicking again will rotate the view again, back to
    dimensions 1,2 and 3. Rotation is around the center of the currently
    displayed view, so that the new chemical shift of the z axis, is the
    value that was at the center of the previous x axis.

**Shift-Down Arrow**

:   Same as Shift-Down Arrow, but instead the dataset dimension on the x
    axis is decremented. The direction of rotation only matters if the
    dataset has more than three dimensions.
