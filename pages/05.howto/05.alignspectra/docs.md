---
title:  Aligning Spectra
taxonomy:
    category: docs
---


Even with careful attention to dataset referencing your datasets may not be perfectly aligned, but good alignment is generally important for subsequent analysis.  NMRFx Processor provides an alignment tool to make sure your datasets are properly aligned right after your done processing and before you've started doing further steps such as peak assignment.  

To align datasets display them in a single window.  They can be displayed as overlays in a single spectrum chart or in separate chart windows, they just need to be in a single window on the desktop.  Additionally, the dataset axes that are to be aligned should have the same axis labels.  If the datasets have more than two dimensions you'll probably be only aligning them on two of the dimensions.  For example, if you have a set of 1H,15N,13C backbone experiments you'll probably want to align them only on the 1H and 15N axes (as the carbon dimensions probably reprsent different atoms and won't align).  Adjust the display so that the two axes to be aligned are displayed on the X and Y axes of the spectrum chart.  You can easily do this with the X,Y menus in the toolbar at the bottom of the window.

The alignment algorithm works by optimizing the alignmnent of picked peaks.  If your spectrum already has peak boxes displayed on it those peaks will be used.  If not, peak picking will be performed automatically on the dataset at the currently displayed contour level  If this automatic picking is done, the peaks will be automatically discarded once the alignment is done.  You won't actually see them displayed.  It's best if the spectra are displayed with a contour level that is not too low, so that a lot of noise is not included.  Similarly, the display region shouldn't include noise regions.

Once you've got the spectra displayed as described, just chooses *Align* from the *Spectrum Menu*.  The spectra will be aligned, the display will be refreshed, and parameter files with the new reference information will be written to the folder containing each dataset.
