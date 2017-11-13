---
title: File Commands
taxonomy:
    category: docs
---


These commands are used in processing scripts to specify the raw dataset to read from and the NMRViewJ format dataset to create.  Normally they are inserted automatically during script generation in NvFX, but you can use them explicitly if you're creating a script outside of NvFX.

**FID**

Open a raw  NMR dataset (FID file).<br>


* **fidFileName**
Name of the file to open.
    * *optional* : False
* **tdSize**
Size of each time domain dimension.  Automatically determined from paramter files if not specified.
    * *default* : None
    * *optional* : True
* **keywords**
Optional list of arguments describing data
    * *default* : None
    * *optional* : True

**CREATE**

Create a new NMRViewJ format dataset.  If file already exists it will be erased first.<br>


* **nvFileName**
Name of the dataset file to create.
    * *optional* : False
* **dSize**
The size of the dimensions.  If not specified the size automatically determined from processing script.
    * *default* : None
    * *optional* : True
