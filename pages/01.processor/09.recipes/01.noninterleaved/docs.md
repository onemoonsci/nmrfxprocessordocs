---
title:  Processing Non-Interleaved Relaxation Experiments
taxonomy:
    category: docs
---

### Step 1: Process a single data set and generate a processing script

1. Launch the NMRFx Processor GUI.
2. In the plot window, choose **File → Open and Draw**. Navigate to the *.ser* file for experiment 1 and open it. You should see a FID plot.
3. In the processor window, select **Scripts → Auto Generate** to generate a processing script automatically. The auto generated script might not have all of the commands correctly, so some things might need to be changed.  For example in our Trosy R2 experiment the following need updating:
    - In the *Operations* tab, click the *TDCOMB()* list item, and change the *coef* submenu value from *echo-antiecho-r* to *echo-antiecho* (this shouldn't normally be necessary to change, but some pulse sequences generate data that is not consistent with parameters in the acqu2s file). The signal in the first row should now be much more intense.  
    - You'll need to adjust the phasing by clicking on the **Phasing** button and adjusting the **PH0** slider.  Click the **Process** button at the bottom of the window to process the data and see the 2D spectrum.
    - This data looks upside down in the 15N dimension so select **D1 → D2**, click the *FT()* list item, and uncheck *negateImag* and reprocess the data.
6. Select **D1** and **FID** again. Remove the solvent/water peak by selecting the **+** menu **→ TD-Solvent → TDSS** and reprocess the data.
7. To adjust the phasing for D1, turn on the phasing slices by making sure both the *Slices* and *Phasing* checkboxes are selected. Position a crosshair on peaks peaks in the dataset, and adjust the *PH0* and *PH1* slider values until the phase slices for the peaks have even baselines. A pivot point must be set (using the **Phase** menu's **Set Pivot** item) before adjusting PH1. Repeat for D2.
8. Finally, extract a region of interest in the data. Go to the D1 FID, and define region boundaries by clicking in the plot window. Right click to bring up a menu in the spectrum and select **Add Extract Region**.  Reprocess the spectrum and confirm that everything looks good.
9. It’s a good idea to save a copy of the processing script with a different file name than the default *process.py* using **Scripts → Save As**.

Here's the final processing script:

```
import os
from pyproc import *
procOpts(nprocess=7)
FID('/Users/brucejohnson/data/test/R2 experiments/1')
CREATE('/Users/brucejohnson/data/test/R2 experiments/1/0agp.r2.trosy3.nv')
acqOrder('21')
acqarray(0,0)
skip(0,0)
label('1H','15N')
acqsize(0,0)
tdsize(0,0)
sf('SFO1,1','SFO1,2')
sw('SW_h,1','SW_h,2')
ref('','N')
DIM(1)
TDCOMB(coef='echo-antiecho')
SB()
ZF()
FT()
PHASE(ph0=105.8,ph1=8.7,dimag=False)
EXTRACT(start=163,end=913,mode='region')
DIM(2)
SB(c=0.5)
ZF()
FT()
PHASE(ph0=0.0,ph1=0.0)
run()
```

### Step 2: Process and combine multiple datasets into one

1. In the plot window, select **View → Show Scanner**.
2. In the scanner window, select **File → Set Scan Directory**. Set the directory to the folder that contains the numbered subfolders with your data.
3. Set the output directory for the scanned data with **File → Set Output Directory**. You can use an existing directory or make a new one.
4. Scan the directory by selecting **File → Scan Directory**. The scanner table should now be populated with your data file information. 
5. Double click experiment 1 in the table. In the processor window, load the *process.py* file created earlier if necessary with **Scripts → Open (process.py)** or **Scripts → Open...** and click the **Process** button.
6. In the scanner window, select **File → Process and Combine**. This processes all of the datasets using the processing script from earlier and combines all of the separate experiments into one processed dataset with multiple planes.
7. At first the display won't show the processed spectrum.  Close the scanner window and hit the **Refresh** button in the plot window. You should now be able to step through all of the processed experiments as separate planes in a single dataset.  You can do this by using the **Z** controls on the bottom of the spectrum window.  Use the small up/down arrows to go up down planes, or use the **Z** menu items to choose the first, last or all planes. 

### Step 3: Measure peaks

1. On the main menu bar, select **View → Show Datasets**. Select the combined dataset and click the **Values** button. Enter the time delay values (in seconds) for each plane/experiment.  This entry window is not real user friendly.  Double-click in the Value cell for the first row, enter a value, hit Return, then use the keyboard arrow key to go to the next row.  Hit return in that next row to begin editing that value.  Repeat for all the rows, and then close up the Values window.
2. In the plot window, go to the first plane, place the crosshairs around the peaks of interest, and click the **Pick** button to pick peaks. 
3. Now select **Peaks → Show Peak Tool** menu item to bring up the Peak tool.
3. In the peak tool window, select **Measure → Evolumes**, go to the *Graph* tab, then select **List → process**. You should now be able to step through all of the picked peaks and see their calculated values. 
4. Save the entire project by selecting **Projects → Save** (if you've already in a project) or **Projects → Save As…** (if you need to create a project) from the main menubar.
5.  In the Project folder (that you just created) you'll find a **peaks** folder.  In there will be two files, one ending in .xpk2 and one ending in .mpk2.  The mpk2 file will have the integral values for each measured peak.
