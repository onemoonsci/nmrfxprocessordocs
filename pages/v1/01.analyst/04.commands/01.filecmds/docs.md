##File Commands##

The File commands are used at the beginning of each script to specify the raw NMR file (the FID) to open, and the NMRView dataset to create.


**FID** 

Open a raw  NMR dataset (FID file).<br>


    FID(fidFileName,tdSize=None,nusFileName=None)

* **fidFileName**
Name of the file to open.
    * *optional* False
* **tdSize**
Size of each time domain dimension.  Automatically determined from paramter files if not specified.
    * *default* None
    * *optional* True
* **keywords**
Optional list of arguments describing data
    * *default* None
    * *optional* True

**CREATE** 

Create a new NMRViewJ format dataset.  If file already exists it will be erased first.<br>


    CREATE(nvFileName,dSize=None,extra=0)

* **nvFileName**
Name of the dataset file to create.
    * *optional* False
* **dSize**
The size of the dimensions.  If not specified the size automatically determined from processing script.
    * *default* None
    * *optional* True
