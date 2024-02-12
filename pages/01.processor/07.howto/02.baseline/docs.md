---
title:  Baseline correction
taxonomy:
    category: docs
---


Two separate operations are involved in baseline correction. The first operation, REGIONS, is used to select regions that are to be considered baseline. The second operation (for example, BCWHIT or BCPOLY) is used to specify what type of baseline calculation is to be done. Both operations need to be present in the script for baseline correction to be accomplished. The functionality is split into these two operations as the identified regions can be used in multiple types of baseline correction, indeed they could be used for additional operations besides baseline correction. When a REGIONS command is present the displayed spectrum will be highlighted in orange to show the baseline regions. REGIONS can be identified automatically or manually. Automatic region identification is active as long as the regions parameter is empty. A convenient method for manually adding regions is to position the black and red crosshairs at the edge of a region and press the "r" (for region) key. This will add the specified region (in fractional units) to the regions parameter of the REGION operation. For this to work, the REGIONS operation must have been added to the operation list for the current dimension, and be the currently selected item in the list. We find very good results by using a set of regions with the BCWHIT baseline correction operation. 
