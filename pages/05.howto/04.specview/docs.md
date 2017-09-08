---
title:  Spectrum View
taxonomy:
    category: docs
---


This page contains an assortment of descriptions of how to change the view of spectra in a spectrum chart.

1. [Synchronize views](#synchronize-spectrum-display)

### Synchronize Spectrum Display 

NMRFx provides a basic implementation of spectrum synchronization.  More complete tools are in development.  Synchronization is currently used to synchronize the spectrum charts contained within a single window.  Just choose *Sync Axes* from the *Spectrum Menu*.  Now whenever you change the X or Y axis view, or planes in one spectrum chart, the same view will be set in the other charts.  Synchronization only happens for dataset axes that share the same label, but the dataset axes do not need to be displayed on the same chart axis (X, Y, Z...).

