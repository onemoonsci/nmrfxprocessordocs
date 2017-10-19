---
title:  Scanner
taxonomy:
    category: docs
---


Use this to scan a folder for all the contained NMR folders. A list will be displayed of all the datasets found, and then they can all be processed with the same script. This feature may become a "Premium Only" feature in subsequent NMRFx Processor releases. 

Scan
    A directory chooser will be displayed. Browse to and choose a directory. That directory, and all sub-directories will be scanned to find a list of NMR datasets (with fid/ser files). The names of all the found datasets will be displayed in a list. Double-click on an entry in the list to open up the selected dataset. Configure processing for that dataset as is normally done in NMRFx Processor.
Process All
    Process all the datasets using the current script. At present, each processed dataset will be placed in the folder containing the FID file it was derived from.

