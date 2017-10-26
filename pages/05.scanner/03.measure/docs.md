---
title:  Measurement
taxonomy:
    category: docs
---

The Scanner Tool can be used to measure intensities and integrals across specified regions of all the dataset rows referenced in the table.  Measurement is performed by selecting a region of the spectrum with the vertical crosshairs and choosing **Measure** from the Scanner Tool's **Analyze** menu.  The exact measurement performed is based on settings in the **Parameters** tab.  

The measurment type is specified by the **Mode** setting and can be set to the following values.

*  Volume: The integral of intensities across the region of the dataset row between the vertical crosshairs.
*  Max: The maximum intensity in the region of the dataset row between the vertical crosshairs.
*  Min: The minimum intensity in the region of the dataset row between the vertical crosshairs.
*  Extreme: The intensity with the largest absolute value in the region of the dataset row between the vertical crosshairs.


A local baseline correction can be done based on the state of the **Offset** setting.  A local correction is useful when the measured region is "riding" on a hump or other baseline distortion.  The baseline can be calculated locally and subtracted without needing to apply a baseline correction to the entire spectrum.  The following choices are available:

*  None: Don't do a baseline correction.
*  Region: Subtract a baseline correction based on the intensities of the points at the edge of the selected region (as defined by the crosshairs).  In the intensity modes (Max, Min, Extreme) the interpolated intensity at the position of the measurment is subtracted from the measured value.  In the volume mode, the integral of a line between the edge points is sbutracted.
*  Windoe:  This works the same as the **Region** mode, except the edge points are taken to be the edge of the display window.  This allows using a different region for defining the measurement and for defining the local baseline.

After the measurement is performed the table is updated with the new measurment values.  A new column is added to the table with a name that corresponds to the measurment type and region.  For example, a column named V.0:max_2.531_2.405_re_ indicates that the measured value is the maximum intensity in the region between 2.531 and 2.405 ppm and a local baseline correction was done based on the edges of the region.  The V.0 prefix to the column name can be used as a the column name when referring to the table data using the R scripting interface.  Each added column will begin with Vn:, where *n* is an index incremented for each new column (V0:,V1: etc.).

You can save the table at anytime using the *File>Save Table...* menu item.  The measured values will be saved in the table.  The table can be reloaded into NMRFx Processor or analyzed in some other software application.
