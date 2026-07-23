---
title:  Status Bar
taxonomy:
    category: docs
---

## Vector sliders

![](images/vector_slider.png)

This tool is only displayed in Processing mode.
At the left side of the data display are two controls, a combobox near the top, and a slider control along the left edge. Typically in 2D, phase sensitive, NMR spectra two data vectors are collected for each time point which differ from each other in the phase of one of the pulses by 90 degrees. With higher dimensional datasets an increasing number of data vectors are collected for each time increment. The combo box at top can be used to select which of the group of data vectors associated with a given time increment are to be displayed. This can be useful in determining whether you've set up the right type of data combination operations.

The slider control can be used to scroll through all the 1D vectors along the active dimension.  As you slide the control any current processing operations for the active dimension will be applied to the vector before display.

Show Measure Bar...

: Show a toolbar across the bottom of the spectrum with tools and displayed values used
for measuring positions, position deltas, intensities and signal/noise ratio.

Show Comparator...

: Show a toolbar across the bottom of the spectrum with controls for selecting
a pair from multiple datasets.  You can use it to do pairwise comparisons of
spectra.

Show Regions Analyzer...

:  Show a window with controls for analzying spectral regions.  Regions can be added, adjusted
split and removed. Peaks can be added to the region and an implementation of Objective
Deconvolution used to add peaks to the region to deconvolute overlapping signals.


Show Spectrum Library

: Display a toolbar at the bottom of the spectrum window that can be used
to select and display the spectrum of molecules from the built-in metabolite
library.

Show Peak Navigator

:    The Peak Navigator will appear as a tool bar at the bottom of the current spectrum window.  It allows stepping through a peak list and updating the spectrum display to a region around the current peak.

Show Peak Slider

:    The Peak Slider will appear as a tool bar at the bottom of the current spectrum window.  When present peaks that are linked to each other will move together when any one peak is moved.  The toolbar provides tools for freezing (and "thawing") peaks into the current position so they can't be moved.

Show Path Tool

:    Display a tool at the bottom of the spectrum window that can be used for
finding and measuring peak paths present in experiments such as ligand
or pressure titrations.

