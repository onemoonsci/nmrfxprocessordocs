##Reference Commands##

Referencing commands are used at the beginning of each script to set the sweep width, spectrometer frequency, referencing and dataset axis labels.  The commands can take specific values that override anything in the FIDs parameter files, or they can be the names of parameters that are found in the vendors parameter files.  Bruker parameters are specified with the name, a comma, and a dimension number.  So, for example, "SFO1,1" would be the spectrometer frequency found in the "acqus" file, and "SFO1,2" would be the spectrometer frequency found in the "acqu2s" file.  The command "p" can be used to get the value of a parameter.  For example, p('sw2')/2.0  would get the value of the "sw2" parameter and divide it by 2.0.


**sw** 

Sweep width values to set for each dimension.<br> Values can be either a numeric value (2000.0) or the name of a vendor specific parameter (in quotes). <br>Examples: <ul> <li>sw(5000.0,2000.0) Numeric values</li> <li>sw('sw','sw1') Agilent VNMR</li> <li>sw('SW_h,1','SW_h,2') Bruker</li> </ul>


    sw()


**acqsize** 

Set acquired size. This is not normally needed, but might be useful if the experiment did not run to completion and you need to specify the number of rows of data that were actually acquired.  Only the size for the indirect dimensions can be changed.  Specifying a value of 0, or an empty value indicates that the actual acquired size should be used.


    acqsize()


**tdsize** 

Set time domain size that should actually be used.  Normally set to a value less than or equal to the acqsize value. Only the size for the indirect dimensions can be changed.  Specifying a value of 0, or an empty value indicates that the actual acquired size should be used.  Useful if you want to see what the processed data would be like if fewer data rows were acquired, or if there is some corruption of data (by changes to sample or fault in instrument) after a certain point.


    tdsize()


**sf** 

Spectrometer frequency at center of spectrum to set for each dimension.<br> Values can be either a numeric value (2000.0) or the name of a vendor specific parameter (in quotes). <br>Examples: <ul> <li>sf(5000.0,2000.0) Numeric values</li> <li>sf('sfrq','dfrq') Agilent VNMR</li> <li>sf('SFO1,1','SFO1,2') Bruker</li> </ul>


    sf()


**ref** 

Reference position (in ppm) at center of spectrum to set for each dimension.<br> Values can be either a numeric value (2000.0), the name of a vendor specific parameter (in quotes), or symbolic values. If symbolic values ('h2o', 'C', 'N') are used the sf and sw values must already be set correctly. <br>Examples: <ul> <li>ref(4.73,115.0) Numeric values</li> <li>ref('h2o','N') Set dimension 1 to the shift of water at the experimental temperature, and dimension 2 to value for N using indirect refrence ratio</li> </ul>


    ref()


**label** 

Set the label to be used for each dimension.<br> <br>Examples: <ul> <li>label('HN','N15') </li> <li>label('H','CA','N') </li> </ul>


    label()


**printInfo** 

Print out reference info. Useful to see what values the automatic parameter extraction found.


    printInfo()

