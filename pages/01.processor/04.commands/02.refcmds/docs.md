---
title: Referencing Commands
taxonomy:
    category: docs
---


These commands are used to specify referencing information and to control the amount of the FID data that is used in processing.  Normally the values are entered in the parameter tab of the NvFX Processor window, but you can explicitly add them to scripts generated outside of NvFX.

**sw**

Sweep width values to set for each dimension.<br> Values can be either a numeric value (2000.0) or the name of a vendor specific parameter (in quotes). <br>Examples: <ul> <li>sw(5000.0,2000.0) Numeric values</li> <li>sw('sw','sw1') Agilent VNMR</li> <li>sw('SW_h,1','SW_h,2') Bruker</li> </ul>



**sf**

Spectrometer frequency at center of spectrum to set for each dimension.<br> Values can be either a numeric value (2000.0) or the name of a vendor specific parameter (in quotes). <br>Examples: <ul> <li>sf(5000.0,2000.0) Numeric values</li> <li>sf('sfrq','dfrq') Agilent VNMR</li> <li>sf('SFO1,1','SFO1,2') Bruker</li> </ul>



**ref**

Reference position (in ppm) at center of spectrum to set for each dimension.<br> Values can be either a numeric value (2000.0), the name of a vendor specific parameter (in quotes), or symbolic values. If symbolic values ('h2o', 'C', 'N') are used the sf and sw values must already be set correctly. <br>Examples: <ul> <li>ref(4.73,115.0) Numeric values</li> <li>ref('h2o','N') Set dimension 1 to the shift of water at the experimental temperature, and dimension 2 to value for N using indirect refrence ratio</li> </ul>



**label**

Set the label to be used for each dimension.<br> <br>Examples: <ul> <li>label('HN','N15') </li> <li>label('H','CA','N') </li> </ul>



**acqsize**

Set acquired size. This is not normally needed, but might be useful if the experiment did not run to completion and you need to specify the number of rows of data that were actually acquired.  Only the size for the indirect dimensions can be changed.  Specifying a value of 0, or an empty value indicates that the actual acquired size should be used.



**tdsize**

Set time domain size that should actually be used.  Normally set to a value less than or equal to the acqsize value. Only the size for the indirect dimensions can be changed.  Specifying a value of 0, or an empty value indicates that the actual acquired size should be used.  Useful if you want to see what the processed data would be like if fewer data rows were acquired, or if there is some corruption of data (by changes to sample or fault in instrument) after a certain point.



**printInfo**

Print out reference info. Useful to see what values the automatic parameter extraction found.

