---
title: Low-level Command Reference
taxonomy:
    category: docs
---


##bioppmscore


Scoring based on chemical shift ranges.

**Sub-commands**

:    bioppmscore add

:    bioppmscore clear

:    bioppmscore fragscore

:    bioppmscore get

:    bioppmscore score


**add**

:    **bioppmscore** **add**  *resName*  *atomName*  *shiftAvg*  *shiftSDev* 

:    Add an atom type to the internal library specifying the average shift and standard deviation range for the chemical shift of that type of atom.  This command is normally used when NMRViewJ starts up to input values from a database of shifts from the BMRB.

**clear**

:    **bioppmscore** **clear** 

:    Clear the internal database of atom type shifts.

**fragscore**

:    **bioppmscore** **fragscore**  *scoreLimit*  *dataList*  *residueList* 

:    This command works the same as the "bioppmscore score" command, but takes a list of data values and residues and returns a list of scores for each residue in the list.  If a given residue score is below the scoreLimit a "-" character will be present at that position in the score list.
:    
bioppmscore fragscore 0.2 {{ha 4.26 ca 54} {ha 4.5 cb 70}} {ala thr}
:    
0.922750375855 0.978495932196

**get**

:    **bioppmscore** **get**  *?resName*  *atomName*  *??* 

:    Without any arguments this returns a list of the residue names that are currently in the shift database.
:    
bioppmscore get
:    
ala arg asn asp cys gln glu gly his ile leu lys met phe pro ser thr trp tyr val
:    
If the resName argument is specified the command returns a list of the names of atoms in that residue.
:    
bioppmscore get ala
:    
ha ca c hn hb n cb
:    
If the resName and atomName arguments are included then return the average chemical shift and standard deviation of the chemical shift for that atom type.
:    
bioppmscore get ala ha
:    
4.26 0.44

**score**

:    **bioppmscore** **score**  *scoreLimit*  *atomName*  *atomPPM*  *?atomName2*  *atomPPM2*  *...?* 

:    Returns a list of residue names and scores based on the specified list of atom names and chemical shifts.  The score is calculated based on the average value and standard deviation of the chemical shifts for each residue and atom in the internal database.  The score value is a Chi Square based probability value that ranges from 0.0 to 1.0 with higher values indicating a higher probability of the residue type being consistent with the specified chemical shifts.
:    
Only residues with a score greater than the specified scoreLimit will be returned.
:    
bioppmscore score 0.6 ha 4.26
:    
ala 1.0 arg 0.946847071399 gln 0.981446217529 glu 0.98054133025 ile 0.90052355034 leu 0.915278497447 lys 0.981867820961 met 0.786519221361 pro 0.702199590874 thr 0.661748776082 val 0.876685395448
:    
bioppmscore score 0.6 ha 4.26 ca 54
:    
ala 0.922750375855 leu 0.740893981868
:    
bioppmscore score 0.6 ha 4.26 ca 54 cb 20
:    
ala 0.921281432229

##cluster


Multidimensional clustering of a list of data values.

**cluster** *tolerance*  *value0*  *value1*  *value2*  *...* 

:    Clusters the specified values.  The result consists of two lists.  The second list is a list of the positions of the "prototypes" (the center position of each cluster).  The first list consists of a pair of values for each input value.  The first member of the pair is the cluster (index of the prototypes 0, 1 ...) to which the pair belongs.  The second member of the pair is the index of the original value as input to the command.
:    
cluster 0.4 3.05 1.1 2.0 3.03  2.1 1.07 2.05 3.0 1.05 2.99
:    
:    
cluster 10 3.05 1.1 2.0 3.03  2.1 1.07 2.05 3.0 1.05 2.99
:    
:    
The elements of the tolerance and values can each themselves be a list, in which the clustering will happen in a dimensionality equal to the tolerance dimensions.  The number of elements in each value must be equal to the number of tolerance values.

##export


Export graphical representation of window to file.

:    **export** *?-mode*  *modeType*  *?-fileName*  *fileName??*  *windowName* 

:    Export a graphical representation of the specified window into a file.  If no optional arguments are specified then a dialog will appear in which the file format can be selected and a file name entered.  If a mode is specified without the fileName the file will be named export.mode (i.e. export.png or export.ps).  Currently supported vector modes are ps, pdf, svg and emf.  Bitmap modes are gif, jpg, png, and bmp.

##mmcif


Read MMCIF files.

**Sub-commands**

:    mmcif close

:    mmcif comp_atoms

:    mmcif comp_bonds

:    mmcif mmcifxyz

:    mmcif next

:    mmcif open

:    mmcif put




**close**

:    **mmcif** **close** 

:    Not yet documented

**comp_atoms**

:    **mmcif** **comp_atoms** 

:    Not yet documented

**comp_bonds**

:    **mmcif** **comp_bonds** 

:    Not yet documented

**mmcifxyz**

:    **mmcif** **mmcifxyz** 

:    Not yet documented

**next**

:    **mmcif** **next** 

:    Not yet documented

**open**

:    **mmcif** **open** 

:    Not yet documented

**put**

:    **mmcif** **put** 

:    Not yet documented

##mol


Interact with molecular structures.

**Sub-commands**

:    mol add

:    mol atoms

:    mol calcbonds

:    mol calcRMSD

:    mol canonname

:    mol center

:    mol color

:    mol colortype

:    mol coordsets

:    mol displaytype

:    mol distance

:    mol draw

:    mol entities

:    mol equiv

:    mol gencoord

:    mol getcenter

:    mol labeltype

:    mol lines

:    mol list

:    mol listatoms

:    mol listbonds

:    mol listresidues

:    mol molname

:    mol negshapetype

:    mol new

:    mol nstructures

:    mol points

:    mol posshapetype

:    mol radius

:    mol remove

:    mol selcyclecount

:    mol select

:    mol serial

:    mol setatomprop

:    mol setbondprop

:    mol setbonds

:    mol site

:    mol smiles

:    mol structures

:    mol tablemodel

:    mol tree

:    mol unselect




**add**

:    **mol** **add**  *molName*  *compound* | *water* | *polymer* | *name* 

:    Adds a new entity of the specified type and with the specified name to the specified molecule.

**atoms**

:    **mol** **atoms**  *molName* 

:    Return a list of all atoms in the specified molecule.

**calcbonds**

:    **mol** **calcbonds**  *molName* 

:    This command adds bonds between any pairs of atoms that are currently selected and whose inter-atom distance is less than 1.8 Angstroms.

**calcRMSD**

:    **mol** **calcRMSD**  *molName* 

:    Calculates the rms position across multiple structure models for each atom in the specified molecule.  The calculated rms is stored in the "bFactor" field for each atom (and can be queried with the "nv_atom elem bfactor atomSpecifier" command).

**canonname**

:    **mol** **canonname**  *molName* 

:    Rename the atoms in a molecule so that they canonical names.  That is, names that will be the same no matter what order the atoms or their bonds were input in.  The algorithm used does not conform to any standard.

**center**

:    **mol** **center**  *molName*  *?structureNum?* 

:    Centers the coordinates of the molecule so that the average x, y and z positions are 0.0.  If the optional structureNum argument is included then only the coordinates for the specified structure (model) will be centered.

**color**

:    **mol** **color**  *atoms* | *bonds* | *red*  *green*  *blue* 

:    Set the display color for selected atoms or bonds to the specified values.  The red, green and blue values are to be specified as floating point numbers between 0.0 and 1.0.

**colortype**

:    **mol** **colortype** 

:    Not yet documented

**coordsets**

:    **mol** **coordsets**  *molName* 

:    Return a list of the names of all the coordinate sets in the specified molecule.  In the terminology of NMRViewJ, a coordset is essentially the equivalent of an "assymetric unit" in crystallographic terminology.

**displaytype**

:    **mol** **displaytype** 

:    Sets the type of display to be used when displaying molecules.  With no arguments the command returns a list of acceptable types.  Currently the list is:
"none wire hwire bwire ball pball cpk"


**distance**

:    **mol** **distance**  *molFilter1*  *molFilter2* 

:    Returns the distance between the atom(s) selected with molFilter1 and the atom(s) selected with molFilter2.  If the filters match more than one atom then the distance between the average position of each set of atoms is used.

**draw**

:    **mol** **draw** 

:    unused

**entities**

:    **mol** **entities**  *molName* 

:    Return a list of the names of all entities (polymers, ligands etc.) in the specified molecule.

**equiv**

:    **mol** **equiv**  *atomSpecifier* 

:    Return a list describing atoms that are chemically? equivalent to this one.

**gencoord**

:    **mol** **gencoord**  *molName* 

:    Generate 3D coordinates from internal coordinates (bond lengths, bond angles and dihedral angles).

**getcenter**

:    **mol** **getcenter**  *molName*  *?structureNum?* 

:    Returns, as a three element list, the coordinates of the average position of all atoms in the specified molecule.  If the optional structureNum parameter is included then only the coordinates of that structure (model) are used.

**labeltype**

:    **mol** **labeltype**  *?molName*  *type?* 

:    Sets the type of label to be used when displaying molecules.  With no arguments the command returns a list of acceptable types.  Currently the list is:
"none label fc symbol number both ffc ss residue charge value title mname string bond custom name ppm"


**lines**

:    **mol** **lines**  *molName* 

:    Returns a list of coordinates representing 3D lines between all bonds with the DISPLAY property set.

**list**

:    **mol** **list** 

:    Return a list of all molecules currently in memory.

**listatoms**

:    **mol** **listatoms**  *?molName*  *display?* 

:    Returns a list of all currently selected atoms.  With the optional arguments returns a list of all atoms in the specified molecule that have their DISPLAY property set.

**listbonds**

:    **mol** **listbonds**  *molName* 

:    Returns a list of all currently selected bonds in the specified molecule.

**listresidues**

:    **mol** **listresidues**  *molName*  *entity* 

:    Return a list of residues in the indicated entity of the indicated molecule.  The list consists of alternating residue numbers and residue names:  "1 GLY 2 ARG 3 TYR ..."

**molname**

:    **mol** **molname**  *molName?* 

:    Returns the name of the currently active molecule.  If the optional argument is included sets the currently active molecule to the one named.

**negshapetype**

:    **mol** **negshapetype**  *molName*  *type?* 

:    The molecular display of atoms can be done with a shape based on the state of some molecular property.  This command gets, or sets, the type of shape to be used when the property is positive.  Current shape types are a circle, square or triangle.

**new**

:    **mol** **new**  *molName* 

:    Create a new molecule with the specified name.  If a molecule with this name already exists an error will be thrown.

**nstructures**

:    **mol** **nstructures**  *molName* 

:    Each molecule can multiple structure sets (models) associated with it.  This command returns the number of structures.

**points**

:    **mol** **points** 

:    Not yet documented

**posshapetype**

:    **mol** **posshapetype**  *molName*  *type?* 

:    The molecular display of atoms can be done with a shape based on the state of some molecular property.  This command gets, or sets, the type of shape to be used when the property is positive.  Current shape types are a circle, square or triangle.

**radius**

:    **mol** **radius**  *atoms* | *bonds* | *radius* 

:    Set the display radius for selected atoms or bonds to the specified value. 

**remove**

:    **mol** **remove**  *all* | *molName1* | *molName2...* 

:    Remove the specified molecules.  If the literal word "all" is used then all molecules are removed.

**selcyclecount**

:    **mol** **selcyclecount** 

:    Not yet documented

**select**

:    **mol** **select**  *atoms*  *?-inverse*  *?-append?*  *molFilter*  **  *bonds*  *mode*  **  *residues*  *mode* 

:    Mark atoms, bonds or residues in the current molecule as selected.  Selected items will be used in subsequent operations such as setting colors and other properties or listing selected items.
:    
Selecting atoms requires a molFilter argument to be used for matching atoms.  The molFilter has the format:
coordset.entity:residue.atom
:    
A.ubiq:32.ca would select the alpha carbon of residue 32 in the polypeptide named ubiq in the assymetric unit labeled A.
:    
Information not essential for a match does not need to be specified.  For example, if there is only one assymetric unit, the previous filter could be abbreviated ubiq:32.ca.  If there was only one entity (polypeptide, ligand etc.) it could be abbreviated 32.CA.
:    
If the -append flag is included then newly selected atoms are appended to the list of previously selected atoms.
:    
If the -inverse flag is included then atoms that do not match the selection filter are selected.
:    
Selecting bonds, at present, requires first selecting atoms.  Then the "mol select bonds atom" command will select any bonds between atoms that are currently selected.  The mode argument is currently required, but the actual value is ignored.
:    

Selecting residues, at present, requires first selecting atoms.  Then the "mol select residues atom" command will select all atoms in any residues that currently have selected atoms.  The mode argument is currently required, but the actual value is ignored.

**serial**

:    **mol** **serial**  *molName*  *fileName* 

:    Serialize the Java object representing the molecule and write to the specified file.  Expert use only.

**setatomprop**

:    **mol** **setatomprop**  *molName*  *propertyNum*  *0* | *1* |

:    Each atom can have a set of boolean properties associated with it.  This command sets the state of the property (at present specified with an integer value, 0, 1...,15) for any selected atoms.

**setbondprop**

:    **mol** **setbondprop**  *molName*  *propertyNum*  *0* | *1* |

:    Each bond can have a set of boolean properties associated with it.  This command sets the state of the property (at present specified with an integer value, 0, 1...) for any selected bonds.  In the current implementation the only property available is the DISPLAY property and the propertyNum value is ignored.

**setbonds**

:    **mol** **setbonds** 

:    unused

**site**

:    **mol** **site**  *set*  *siteName* | *get* | *siteName* | *within* | *siteName*  *tolerance* 

:    Sets of atoms can be grouped as sites within the molecule.  With the "set" option all currently selected atoms are stored in a site list with the specified name.  The get option selects all atoms within the named site and returns the number of selected atoms.  The within option sets the selected atoms to be all atoms that are both currently selected and within tolerance distance of any atom in the named site.

**smiles**

:    **mol** **smiles**  *newMolName*  *smilesString* 

:    Generates a molecule from the specified SMILES string.  Only available in dataChord (not NMRViewJ).

**structures**

:    **mol** **structures**  *molName*  *?active*  ** | ** | *select*  *args?* 

:    Each molecule can multiple structure sets (models) associated with it.
This command allows the user to select particular sets to be used for actions such as superimposing the structures.  If the optional argument active or select are not used this command returns a list of the integer numbers corresponding to each structure set in the molecule.  With the "active" argument the command returns a list of currently selected structures.  The "select" argument can be used with a list of selections to select or deselect specific structures.  The args are a series of structure numbers or the wildcard character "*" interspersed with optional "+" or "-" characters.  Any structure numbers occuring after a "+" character will be selected.  Any structure numbers occuring after a "-" character will be deseelcted.  For example, **mol select molName select + * - **3
would select all structures but structure 3.

**tablemodel**

:    **mol** **tablemodel** 

:    The list of atoms can be displayed in a Swank table.  This updates any tables to use the currently active model in their display.

**tree**

:    **mol** **tree**  *atomName*  *t* | *p* | *a* |

:    Operations on molecule as a "tree" structure.  Only available in dataChord.

**unselect**

:    **mol** **unselect**  *?last?*  ** | ** | *all* 

:    With no parameters or the literal word "last", the last atom that was selected is unselected.  With the literal word "all" then all atoms are unselected.

##nv_atom


Query and set atom-based values for current molecule.

**Sub-commands**

:    nv_atom add

:    nv_atom coords

:    nv_atom elem

:    nv_atom num

:    nv_atom remove




**add**

:    **nv_atom** **add**  *atomSpecifier*  *newName*  *newElement*  *bondOrder* 

:    Add an atom to the molecule bonded to the specified atom.
  Doesn't currently set up proper parent/child relationships.

**coords**

:    **nv_atom** **coords** 

:    Returns a list of coordinate values for the atom in the following format:
:    
molName coordSet.entityName:residueNum.atomName structureNum x y z

:    
If more than one structure (model) is available for the model the "structureNum x y z" values will be repeated for each structure.


**elem**

:    **nv_atom** **elem**  *elemName*  *atomNum*  *[value]* 

:    Returns the value of 'elemName' for 'atomNum'. If the optional argument is included the command sets the  element to the value specified.
The valid values for 'elemName' are:

symbol
:    The atomic symbol for the atom.

entity
:    The molecular entity to which the atom belongs.

equiv
:    A list describing the atoms that this atom is chemically? equivalent to.

resonance
:    The resonance, if any, that this atom belongs to.

dihedral
:    The dihedral angle set for this atom.  It corresponds to the angle between this atom and its three preceding parent atoms, but will only be consistent with this actual angle if a "mol gencoord" command (or its equivalent) has been executed to convert internal coordinates into cartesian coordinates.

value
:    Each atom can have a floating point value stored with it.

iseq
:    An integer number that can be associated with each residue.


bfactor
:    The bfactor of the specified atom.  The "mol calcRMSD" command puts its result into this parameter.

occupancy
:    The occupancy of the atom.

sstereo
:    Chemical Shift Ambiguity Index Value Definitions

     |Index Value |Definition                        |
     |------------|----------------------------------|
     |1           |Unique (geminal atoms and geminal methyl groups with identical chemical shifts  are assumed to be assigned to stereospecific atoms) |
     |2           |Ambiguity of geminal atoms or geminal methyl proton groups                           |
     |3           |Aromatic atoms on opposite sides of symmetrical rings (e.g. Tyr HE1 and HE2  protons |
     |4           |Intraresidue ambiguities (e.g. Lys HG and HD protons or Trp HZ2 and HZ3 protons)  |
     |5           |Interresidue ambiguities (Lys 12 vs. Lys 27) |
     |9           |Ambiguous, specific ambiguity not defined   |


rnum
:    The sequence number of the specified atom (redundant with the "seq" elemenent.

stereo
:    A stereo specific assignment code.

class
:    The class is normally set from the force field value in NMRViewJ .prf residue library files, though is unused within the program.

child
:    A list of atoms that are bonded to the atom and are farther from the root when considering the molecule as a tree structure.

ppm
:    The chemical shift of the specified atom.

mass
:    The atomic mass of the atom (not currently valid).

x
:    The x coordinate of the specified atom.

y
:    The y coordinate of the specified atom.

z
:    The z coordinate of the specified atom.

parent
:    The atom number of the atom's parent.  The parent is the directly bonded atom that is closer to the root when considering the molecule as a tree.  Should always be a heavy atom for hydrogens.

seq
:    The sequence number of the specified atom.

aname
:    The name  of the specified atom.

rname
:    The residue name of the specified atom.

**num**

:    **nv_atom** **num**  *atomSpecifier* 

:    Returns 1 or -1 depending on whether the specified exists (1) or doesn't exist (-1).

**remove**

:    **nv_atom** **remove**  *atomSpecifier* 

:    Remove the specified atom.


##nv_dataset


Analyze NMR datasets

**Sub-commands**

:    nv_dataset analyze

:    nv_dataset blkheadersize

:    nv_dataset blksize

:    nv_dataset close

:    nv_dataset complex

:    nv_dataset compress

:    nv_dataset create

:    nv_dataset datatype

:    nv_dataset dims

:    nv_dataset fileheadersize

:    nv_dataset flush

:    nv_dataset freqdomain

:    nv_dataset get

:    nv_dataset hpick

:    nv_dataset label

:    nv_dataset littleendian

:    nv_dataset lvl

:    nv_dataset name

:    nv_dataset ndim

:    nv_dataset negcolor

:    nv_dataset nucleus

:    nv_dataset open

:    nv_dataset parsync

:    nv_dataset path

:    nv_dataset peakpick

:    nv_dataset poscolor

:    nv_dataset posneg

:    nv_dataset ppm2pt

:    nv_dataset property

:    nv_dataset pt2ppm

:    nv_dataset put

:    nv_dataset rdims

:    nv_dataset readpoint

:    nv_dataset ref

:    nv_dataset refpt

:    nv_dataset refunits

:    nv_dataset rename

:    nv_dataset rename

:    nv_dataset scale

:    nv_dataset scanget

:    nv_dataset scanput

:    nv_dataset scanstart

:    nv_dataset sf

:    nv_dataset size

:    nv_dataset solvent

:    nv_dataset sw

:    nv_dataset title

:    nv_dataset vector

:    nv_dataset wrhead

:    nv_dataset writable




**analyze**

:    **nv_dataset** **analyze**  *datasetName*  *[-d1*  *dimRange]*  *[-d2*  *dimRange]*  *...* 

:    Analyzes the data in the specified region of the spectrum 'spectrumName'.
:    The limits of each dimension are specified by 'dimRange'. If no range is given for a dimension the range of all points in that dimensioln are extracted. The default unit for 'dimRange' is ppm but appending "p" to the end of a number changes it to data points (for example "-d1 1p 113p" would extract all points between data points 1 and 113). For brevity, the second number of a range may be excluded if the span of the range is 0 (for example "-d1 1.2" is equivalent to "-d1 1.2 1.2").
:    Examples:
:    "nv_dataset analyze noesy -d1 0.3 1.2 -d2 7.0"
:    "nv_dataset analyze  noesy -d1 80p -d2 7.0 8.0"
:    "nv_dataset analyze noesy -d1 1.2"
:    The results of the command are returned in two ways.  Firstly, they are directly returned as a Tcl list of values:
:    center 0.982547 jitter 3.618867 min -0.70917875 max 4.420222 extreme 4.420222 volume 476.681676697 evolume 478.424618923 mean 0.0203823353443 sdev 0.292174502012 scale 1000000.0 n 23387 p0b 642 p0e 898 p1b 242 p1e 332 max0 8.48848862769 max1 111.181070777
:    Secondly, they are returned as values in a Tcl variable named Nv_Values, with elements like Nv_Value(volume), Nv_Value(scale) etc.
:    The elements of the list or Tcl variable are described below:

     |Element |Description       |
     |--------|------------------|
     |volume  |    the sum of the points in the region.|
     |evolume |    the sum of the points in an elliptical region around the center of the peak.  The width of each axis of the ellipse is determined as a ratio of the linewidth that should theoretically give an optimal signal to noise ratio of the volume estimate.|
     |max     |    the maximum value from the region.|
     |min     |    the minimum value from the region.|
     |extreme |    the most extreme (maximum or minimum) value from the region.|
     |center  |    the value at the center of the region.|
     |jitter  |    the largest value (of the same sign as center point) within a certain tolerance (+/- 25% of the region width) of the center of the cursor region.|
     |n       |    The number of datapoints in the region.|
     |mean    |    the mean of the values in the region.|
     |sdev    |    the standard deviation of the values in the region.|
     |scale   |    The current scale value for the dataset (same as retrieved with "nv_dataset scale")|
     |p1b     |    The first (beginning) data point along dimension 1 of the region.  Similar values are present for any other dimensions.|
     |p1e     |    The last (ending) data point along dimension 1 of the region.  Similar values are present for any other dimensions.|
     |max1    |    The position of the maximum along dimension 1 of the region.  Similar values are present for any other dimensions.|

     A convenient way to put the list of values into a Tcl array variable (other than the default Nv_Value variable) is the following:
     array set dataValues [nv_dataset analyze hsqc.nv -d1 8 9 -d2 110 117]
     You could print out these values like this:

         parray dataValues
         dataValues(center)  = 0.982547
         dataValues(evolume) = 478.424618923
         dataValues(extreme) = 4.420222
         dataValues(jitter)  = 3.618867
         dataValues(max)     = 4.420222
         dataValues(max0)    = 8.48848862769
         dataValues(max1)    = 111.181070777
         dataValues(mean)    = 0.0203823353443
         dataValues(min)     = -0.70917875
         dataValues(n)       = 23387
         dataValues(p0b)     = 642
         dataValues(p0e)     = 898
         dataValues(p1b)     = 242
         dataValues(p1e)     = 332
         dataValues(scale)   = 1000000.0
         dataValues(sdev)    = 0.292174502012
         dataValues(volume)  = 476.681676697</literallayout>

**blkheadersize**

:    **nv_dataset** **blkheadersize**  *dataset*  *[newValue]* 

:    Some datasets, like NMRViewJ's own, are divided into a series of blocks.  Each block may have a header of information and this command will return the size of the block header in bytes.  Of the dataset types commonly used by NMRViewJ, only VNMR files typically have non-zero blockheader size. If 'newValue' is given the block header size will be changed to that value. 'newValue' must be a integer.  Only change this if you really know what you are doing.

**blksize**

:    **nv_dataset** **blksize**  *datasetName*  *iDim*  *[newValue]* 

:    Returns the number of bytes per block in 'datasetName' for the dimension 'iDim'. If 'newValue' is given the block size will be changed to that value. 'newValue' must be a integer.   Only change this if you really know what you are doing.

**close**

:    **nv_dataset** **close**  *datasetName*  *[datasetName2]*  *...* 

:    Closes all datasets listed in the argument.

**complex**

:    **nv_dataset** **complex**  *dataset*  *iDim*  *[newValue]* 

:    Returns the complex flag of the dimension specified. If 'newValue' is given, it sets the flag to that value. Valid values are 0 (real data) and 1 (complex data).

**compress**

:    **nv_dataset** **compress** 

:    Experimental

**create**

:    **nv_dataset** **create**  *fileName*  *dim1Size*  *dim2Size*  *...* 

:    Create a dataset named 'fileName'. The number of dimensions is determined by the number of 'dim?Size' arguments. The size of each dimension should be specified with the dimSize parameters.
:    
Examples:
:    
"nv_dataset create noesy.nv 2048 1024"
:    
"nv_dataset create hnco.nv 512 128 64"
:    


**datatype**

:    **nv_dataset** **datatype**  *dataset*  *[newValue]* 

:    Returns the type of numbers used to represent data values.  0: four byte floating point, 1: four byte integers.  If 'newValue' is given the data type will be changed to that value.

**dims**

:    **nv_dataset** **dims**  *datasetName*  *nDims*  *dim1Size*  *dim1BlockSize*  *...* 

:    Sets the number of dataset dimensions and their sizes in one command.  For example **nv_dataset hsqc.nv 2 1024 64 512 65**
would set the dataset to have two dimensions, the first one having 1024 data points, divided into blocks of 64 datapoints, and the second one having 512 data points, also divided into blocks of 64 datapoints.

**fileheadersize**

:    **nv_dataset** **fileheadersize**  *dataset*  *[newValue]* 

:    Some datasets, like NMRViewJ's own, have a header. This is an area that precedes that actual data, and may contain reference information or information about the layout of the actual data. This command will return the size of the file header in bytes. If 'newValue' is given the file header size will be changed to that value. 'newValue' must be a integer.  Only change this if you really know what you are doing.

**flush**

:    **nv_dataset** **flush**  *datasetName* 

:    Flush the memory buffers for the dataset to disk. This is only relevant for datasets that have been opened with write access.

**freqdomain**

:    **nv_dataset** **freqdomain**  *datasetName*  *dim*  *[isFreqDomain]* 

:    This command returns whether or not the dataset values are in the time (0) or frequency (1) domain along the specified dimension.  This is used when vectors are read from the dataset.  Some operations on the vectors will, for example, properly adjust referencing based on whether the vector is in the time or frequencey domain.

**get**

:    **nv_dataset** **get**  *datasetName*  *[-d1*  *dimRange]*  *[-d2*  *dimRange]*  *...*  *-obj*  *vecName* 

:    Extracts the datapoints from the specified region of the spectrum. The data is read into the vector 'vecName'. 
	The limits of each dimension are specified by 'dimRange'. If no range is given for a dimension the range of all points in that dimensioln are extracted. The default unit for 'dimRange' is ppm but appending "p" to the end of a number changes it to data points (for example "-d1 1p 113p" would extract all points between data points 1 and 113). For brevity, the second number of a range may be excluded if the span of the range is 0 (for example "-d1 1.2" is equivalent to "-d1 1.2 1.2").
:    
Examples:
:    
"nv_dataset get noesy -d1 0.3 1.2 -d2 7.0 -obj work"
:    
"nv_dataset get  noesy -d1 80p -d2 7.0 8.0 -obj work"
:    
"nv_dataset get noesy -d1 1.2 -obj work"
:    


**hpick**

:    **nv_dataset** **hpick** 

:    Unsupported experimental tool for picking peaks based on an HSVD analysis

**label**

:    **nv_dataset** **label**  *datasetName*  *dim*  *[arg]* 

:    Returns the label name for the dimension 'dim' of dataset 'datasetName'. If the optional argument is specified, the label is changed to 'arg'.

**littleendian**

:    **nv_dataset** **littleendian**  *dataset*  *[newValue]* 

:    Returns whether the dataset uses little endian byte order. If 'newValue' is given the dataset parameter specifiying the byte order will be changed to that value.

**lvl**

:    **nv_dataset** **lvl**  *datasetName*  *[newLvl]* 

:    Returns the level the dataset will be drawn at in spectral windows.  This value is used when a dataset is initial assigned to a window.  Changing the contour level with "nv_win lvl"  will override this value.  If the 'newLvl' argument is given, the level will be set to it.

**name**

:    **nv_dataset** **name** 

:    Returns the full file name (including the directory path) of the dataset.

**ndim**

:    **nv_dataset** **ndim**  *datasetName*  *[dims]* 

:    Returns the number of dimensions of the dataset 'datasetName'. If the 'dims' argument is given the dataset's number of dimensions is set to it.  Changing this value should only be done if you know what you are doing.

**negcolor**

:    **nv_dataset** **negcolor**  *datasetName*  *[newValue]* 

:    Returns the color used for negative contours when the dataset is drawn in a spectral windows.  This value is used when a dataset is initially assigned to a window.  Changing the color with "nv_win negcolor" command will override this value.  If the 'newLvl' argument is given, the negative color will be set to it.

**nucleus**

:    **nv_dataset** **nucleus**  *datasetName*  *iDim*  *[newValue]* 

:    Returns the nucleus name assoiciated with the dimension iDim. If 'newValue' is given, the nucleus name is set the that value.

**open**

:    **nv_dataset** **open**  *[[-wr*  ** | ** | *-r]*  *[-name*  *newName]*  *fileName]* 

:    Opens a compatible dataset named fileName. The complete path to the file is required for 'fileName'. However, further references to the file within NMRView use only the name of the file, or by 'newName' if the -name option is set.
The -wr and -r options set the write access of the file. If -wr is set the file is opened with read/write access, if -r is set the file is opened read-only. The default option is read-only if no option is given.
If no options are specified the command returns a list of the currently open files.

**parsync**

:    **nv_dataset** **parsync**  *datasetName*  *dimNum* 

:    NMRViewJ can maintain two copies of the reference units, reference value, reference point, and sw for each dataset dimension.  One value (the write value) is updated when a vector is written to the dataset (with the value present in that vector).  The second value (the read value) is returned when a vector is read from the dataset.  After processing a dataset this command can be used to set all the read values to the write values for the specified dimension.

**path**

:    **nv_dataset** **path**  *datasetName* 

:    Returns the full file name (including the directory path) of the dataset.  (Same as the nv_dataset name command).

**peakpick**

:    **nv_dataset** **peakpick**  *datasetName* 

:    Picks peaks for 'datasetName' and places them in a new list named 'datasetName'.

**poscolor**

:    **nv_dataset** **poscolor** 

:    Returns the color used for positive contours when the dataset is drawn in a spectral windows.  This value is used when a dataset is initially assigned to a window.  Changing the color with "nv_win poscolor" command will override this value.  If the 'newLvl' argument is given, the negative color will be set to it.

**posneg**

:    **nv_dataset** **posneg**  *dataset*  *[newValue]* 

:    Returns whether the dataset should show positive, negative or both frequencies when the dataset is examined. Values of 1 and 2 coorespond to positive and negative frequencies only, respectively. A value of 3 corresponds to both frequencies. If the 'newValue' argument is given posneg is set to that value.

**ppm2pt**

:    **nv_dataset** **ppm2pt**  *datasetName*  *iDim*  *ppmVal* 

:    Returns the closest point to 'ppmVal' on the demension 'iDim' of the dataset 'datasetName'.

**property**

:    **nv_dataset** **property**  *datasetName*  *propertyName*  *[newValue]* 

:    Datasets can have a series of properties associated with them.  These are specified as name values.  Returns the value of a property with the specified propertyName.  If newValue is specified the property will be set to that value.  If the property doesn't exist it will be created.

**pt2ppm**

:    **nv_dataset** **pt2ppm**  *datasetName*  *iDim*  *point* 

:    Returns the ppm value that cooresponds with 'point' on the dimension 'iDim' of the dataset 'datasetName'.

**put**

:    **nv_dataset** **put**  *datasetName*  *[-d1*  *dimRange]*  *[-d2*  *dimRange]*  *...*  *-obj*  *vecName* 

:    Writes the datapoints from a vector specified by 'vecName' to the specified region of the spectrum.
	Only datapoints withing the range given for each dimention are written. The limits of each dimension are specified by 'dimRange'. If no range is given for a dimension the range of all points in that dimensioln are written. The default unit for 'dimRange' is ppm but appending "p" to the end of a number changes it to data points (for example "-d1 1p 113p" would write all points between data points 1 and 113). For brevity, the second number of a range may be excluded if the span of the range is 0 (for example "-d1 1.2" is equivalent to "-d1 1.2 1.2").
	The data is extracted from the dataset specified by 'datasetName'.
:    
Examples
:    
"nv_dataset put noesy -d1 0.3 1.2 -d2 7.0 -obj work"
:    
"nv_dataset put  noesy -d1 80p -d2 7.0 8.0 -obj work"
:    


**rdims**

:    **nv_dataset** **rdims**  *dataset*  *[newValue]* 

:    Returns the number of real dimensions of the dataset. If the 'newValue' argument is given, the number of real dimensions will be set to it.

**readpoint**

:    **nv_dataset** **readpoint** 

:    Not yet documented

**ref**

:    **nv_dataset** **ref**  *nv_datasetName*  *dim*  *[arg]* 

:    Returns the chemical shift at the reference point for dimension 'dim' of dataset 'nv_datasetName'. If the optional argument is specified, the chemical shift is changed to the new value. For example,
:    
nv_dataset ref hncoca.mat 2 182.3
:    
changes the chemical shift along dimension 2 of the nv_dataset named hncoca.mat to 182.3.

**refpt**

:    **nv_dataset** **refpt**  *nv_datasetName*  *dim*  *[arg]* 

:    Returns the datapoint at which the reference chemical shift is specified for dimension 'dim' of dataset 'nv_datasetName'. If the optional argument is specified, the data point used for reference is changed to 'arg'. For example,
:    
nv_dataset refpt hncoca.mat 3 17
:    
changes the datapoint along dimension 3 of the nv_dataset named hncoca.mat to 17.

**refunits**

:    **nv_dataset** **refunits**  *dataset*  *dim*  *[arg]* 

:    Returns the reference units for the dimension given. If the optional argument is given then the reference units are set to that value.

**rename**

:    **nv_dataset** **rename**  *dataset*  *newName* 

:    Changes the name of 'dataset' to 'newName', all further references to the dataset should be 'newName'.

**rename**

:    **nv_dataset** **rename**  *dataset*  *newName* 

:    Changes the name of 'dataset' to 'newName', all further references to the dataset should be 'newName'.

**scale**

:    **nv_dataset** **scale**  *dataset*  *[newScale]* 

:    All datasets in NMRView have a scale parameter.  This is used to put the numbers used for contouring or peak intensities or volumes in a more user friendly range.  The scale is typically set to 1.0e6.  This command returns the scale of the dataset. If the 'newScale' argument is given, the scale will be set to it.

**scanget**

:    **nv_dataset** **scanget**  *datasetName* 

:    Each time this command is called a vector will be read from 'datasetName' and stored into a vector. The dataset dimension and vector name must first be setup with the "nv_dataset scanstart" command.
	The vectors are not necessarily read in sequential order from the matrix. Instead, they are read in an optimal order as defined by the dataset layout. If data is succesfully read, the command will return "1", if the end of the matrix is reached the command will return "0". Thus the command
:    
"while [nv_dataset scanget]"
:    
will scan the entire matrix.

**scanput**

:    **nv_dataset** **scanput**  *datasetName* 

:    This command is analogous to the "nv_dataset scanget" command, but writes
data from a vector to the matrix, rather than reading it.

**scanstart**

:    **nv_dataset** **scanstart**  *datasetName*  *dimNumber*  *vectorName* 

:    Sets up various internal parameters for an optimized scan through the dataset using the "nv_dataset scanget" and "nv_dataset scanput" commands. The 'datasetName' parameter refers to the dataset that will be scanned. The axis that the data will be read from or written to is specified by 'dimNumber'. The 'vectorName' argument specifies the name of the vector in to which data will be read by the "nv_dataset scanget" command, or written to with the "nv_dataset scanput" command.
:    
Example: "nv_dataset scanstart hnco.nv 2 work"

**sf**

:    **nv_dataset** **sf**  *nv_datasetName*  *dim*  *[arg]* 

:    Returns the spectrometer frequency for dimension 'dim' of dataset 'nv_datasetName'. If the optional argument is specified, the spectrometer frequency is changed to the new value. For example,
:    
nv_dataset sf hncoca.mat 1 600.5
:    
changes the spectrometer frequency corresponding to dimension 1 of the nv_dataset named hncoca.mat to 600.5.

**size**

:    **nv_dataset** **size**  *datasetName*  *dimNum* 

:    Returns the number of points in 'datasetName' along the dimension 'dimNum'.

**solvent**

:    **nv_dataset** **solvent**  *datasetName*  *[newValue]* 

:    Returns the solvent used in the experiement, for reference. The value must first be set by including the 'newValue' argument.

**sw**

:    **nv_dataset** **sw**  *nv_datasetName*  *dim*  *[arg]* 

:    Returns the sweepwidth set for dimension 'dim' of dataset 'nv_datasetName'. If the optional argument is specified, the sweepwidth is changed to the new value. For example,
:    
nv_dataset sw hncoca.mat 3 1800
:    
changes the sweepwidth along dimension 3 of the nv_dataset named hncoca.mat to 1800.

**title**

:    **nv_dataset** **title**  *datasetName*  *[newValue]* 

:    Returns the title set for the dataset. This will initially be blank but can be set by including the 'newValue' argument. To create a title longer than one word place them in quotes.

**vector**

:    **nv_dataset** **vector**  *vectorName* 

:    Creates a new dataset from the vector 'vectorName'. The name of the dataset created will be the same as the vector given.

**wrhead**

:    **nv_dataset** **wrhead**  *datasetName* 

:    Writes the dataset header to disk. Do this after changing reference information. This is only operable for datasets that have been opened with write access.

**writable**

:    **nv_dataset** **writable**  *datasetName*  *writable* 

:    Datasets are generally opened as read-only files.  If you want to change values in the file, either information in the file header, or actual data values, you need to have the file open in a writable mode.  This can be done either when opening the file, or after it is opened using this command.  Changing the writable status of an already opened file will acually, at a low level, close the file and reopen it with the specified mode.

##nv_idpeak


Identify atoms consistent with chemical shift values.





****

:    **nv_idpeak** ****  *?-thresh*  *cutoff?*  *pattern1*  *pattern2*  *...* 

:    Search for assignments consistent with a set of patterns that specify chemical shifts, atom types, and tolerances.  Normally used to suggest assignments for a peak, but because the search parameters are explicitly specified values (rather than a specific peak) it can be used in more general searches.
:    
Search patterns are defined in the following format:
:    
<code>atomPattern(relation)@ppm~tolerance</code>

:    
Atom patterns are of the format residue.atom where residue is specified as the letter "i" or "j" and atom specifies an atom pattern, possibly using a wildcard character "*" to match multiple characters.  For example, "i.hn", "i.ca", or "j.c*".  In any given assignment, the patterns with the same residue character (i or j) must match the same residue.  That is, if the patterns are "i.hn" and "i.ha" a possible assignment could be 35.hn and 35.ha, but not 35.hn and 36.ha.  The relation parameter specifies that the assignment atom for one pattern is bonded to the assignment pattern for another atom.  Thus, with patterns "i.h*(D2)" and "i.n" a possible match could be 35.hn and 35.n since the 35.hn is the descendent (chemically bonded to) the atom matched for dimension 2 (this is represented by D2 on dimension 1).  Atoms 35.ha and 35.n would not match this pattern.  They have the same residue, but atom 35.ha is not directly bonded to 35.n.  For an atom to match its chemical shift must be within the specified tolerance of the ppm in the pattern.  A full pattern would look like: i.h*(D2)@7.3~0.2.

##nv_noe


Interact with lists of NOEs.

**Sub-commands**

:    nv_noe add

:    nv_noe check

:    nv_noe clear

:    nv_noe elem

:    nv_noe extract

:    nv_noe n

:    nv_noe off

:    nv_noe on

:    nv_noe uniq

:    nv_noe write




**add**

:    **nv_noe** **add**  *atomSpecifier1*  *atomSpecifier2*  *lower*  *upper* 

:    Add an NOE type constraint to the list.  Constraint will be between the atoms that match atomSpecifier1 and atomSpecifier2 and will have the specified lower and upper constraint distances.

**check**

:    **nv_noe** **check** 

:    Not present in NMRViewJ

**clear**

:    **nv_noe** **clear** 

:    Clear the noe list.

**elem**

:    **nv_noe** **elem**  *elemSpecifier*  *iNoe*  *[value]* 

:    Returns the value of the the element specified with the
'elemSpecifier'  for the NOE specified with the <emphasis role="italic"> iNOE </emphasis>
argument.  If the optional 'value' argument is specified the comand
sets the noe's element to that value.  The valid 'elemSpecifiers' :

class
:    Noe class to which this noe belongs.

int
:    The peak intensity of the peak this noe came from.

vol
		The peak volume of the peak this noe came from.

scale
:    The scale value for this noe.

low
:    The lower bound for this noe.

upper
:    The upper bound for this noe.

pseudo
:    The pseudoatom correction appropriate for this noe.

list
:    The peaklist number that this noe came from.

number
:    The peak number that this noe came from.

stereo.0
:    The stereo specificity of the first atom of this noe.

stereo.1
:   The stereo specificity of the second atom of this noe.

res.0
:    The residue number of the first atom of this noe.

res.1
:    The residue number of the second atom of this noe.

aname.0
:    The atom name of the first atom of this noe.

aname.1
:    The atom name of the second atom of this noe.

active
:    Set to "1" if noe will be used to generate a constraint. Set to "0" if noe will not be used to generate a constraint.


**extract**

:    **nv_noe** **extract**  *peakList*  *?-all?* 

:    Search the specified 'peakList' for entries that
have two named protons.  For each such peak enter an noe into the noe list.
If the optional argument '-all' is specified, extract NOEs for peaks that have multiplet (ambiguous) assignments.  Otherwise, only
extract unambiguous peaks.

**n**

:    **nv_noe** **n** 

:    Returns the number of noes in the noe list.

**off**

:    **nv_noe** **off**  *noeSpecifier* 

:    Inactivate constraint so it won't be used when exporting constraint lists.

**on**

:    **nv_noe** **on**  *noeSpecifier* 

:    Activate constraint so it willbe used when exporting constraint lists.

**uniq**

:    **nv_noe** **uniq** 

:    Not present in NMRViewJ

**write**

:    **nv_noe** **write** 

:    Unused

##nv_peak


Analyze and manipulate spectral peak lists.

**Sub-commands**

:    nv_peak add

:    nv_peak addlist

:    nv_peak analyze

:    nv_peak changelistener

:    nv_peak closest

:    nv_peak cluster

:    nv_peak compare

:    nv_peak compress

:    nv_peak couple

:    nv_peak dataset

:    nv_peak delete

:    nv_peak delregion

:    nv_peak dim

:    nv_peak display

:    nv_peak dmatch

:    nv_peak elem

:    nv_peak find

:    nv_peak fit

:    nv_peak fold

:    nv_peak getpeak

:    nv_peak idlast

:    nv_peak idnum

:    nv_peak idtol

:    nv_peak inbox

:    nv_peak inregion

:    nv_peak jfit

:    nv_peak labels

:    nv_peak lfit

:    nv_peak link

:    nv_peak lists

:    nv_peak maplink

:    nv_peak match

:    nv_peak mknoelist

:    nv_peak n

:    nv_peak name

:    nv_peak nearest

:    nv_peak panel

:    nv_peak pattern

:    nv_peak precision

:    nv_peak ref

:    nv_peak relation

:    nv_peak remove

:    nv_peak renumber

:    nv_peak scale

:    nv_peak score

:    nv_peak sf

:    nv_peak show

:    nv_peak sort

:    nv_peak status

:    nv_peak sw

:    nv_peak swap

:    nv_peak template

:    nv_peak undelete

:    nv_peak undelregion

:    nv_peak unlink

:    nv_peak updatecouplings

:    nv_peak write

:    nv_peak writexml

:    nv_peak zlink




**add**

:    **nv_peak** **add**  *peakList*  *?numPeaks?* 

:    Appends a peak to the end of the peak list 'peakList' and returns the new peak's number. The peak position, width and other attributes are set to zero.  If the optional argument numPeaks is specified then that number of peaks will be added to the list.  The peak number of the last peak added will be returned.

**addlist**

:    **nv_peak** **addlist**  *listName*  *label1*  *[label2]*  *[label3]*  *...* 

:    Creates a new list with the name 'listName'. The number of dimensions is determined by the number of 'label' arguments, and each of these arguments specifies the name of a dimension. For example,
:    
nv_peak addlist sqc 1HN 15N

**analyze**

:    **nv_peak** **analyze**  *datasetName*  *-p1*  *plane*  *-p2*  *plane*  *peakSpecifiers*  *...* 

:    Analyze the region of 'datasetName' contained within the bounds of the all peaks given as 'peakSpecifiers'. One or more peaks may be specified. If more than one peak is specified, then the region is the smallest region that can encompass all the specified peak bounds. If the number of dimensions of the peak is less than the number of dimensions of the spectrum, then the additional plane specifiers are necessary. For example, to evaluate the region of a 2D peak in a 3D spectrum, where each plane is a different relaxation time.
:    

"nv_peak analyze T1exp -p1 7 t1exp.32"
:    

See the documentation for the "nv_dataset analyze" command for information on the data returned by the command.

**changelistener**

:    **nv_peak** **changelistener**  *register* | *unregister* | *listName*  *procedure* 

:    Whenever a change is made to a peak or peak list a Tcl procedure can be called.  This command is used to register or unregister a particular procedure for a given peak list.  If changes are made in rapid succession to a peak list then the multiple events will be collapsed into a single event, otherwise the large number of calls to the event procedure could take too long to process.

**closest**

:    **nv_peak** **closest**  *peakList*  *?xppm1*  *xppm2*  *yppm1*  *yppm2*  *...?* 

:    Returns the number of the peak closest to the center of the specified region.  If the peakList argument is not specified, the peaklist used is the first peak list assigned to the currently active window.  If the position arguments are not specified, they are taken from the position of the crosshair cursors in the active window.  If positions are specified as arguments, the peakList to be used must also be specified.
.
:    
Note: when the position is take from the crosshair, the peak located will be that closest to the intersection point of the first (black) crosshairs), not the mouse position. For example, "peak closest noesy" would find the peak in the peak list named "noesy", that is closest to the crosshair position. If no peak is within a certain tolerance, nothing will be returned.
:    When using NvLite (non-windowing version) you must specify all the arguments.

**cluster**

:    **nv_peak** **cluster**  *peakList1*  *peakList2*  *...* 

:    This command clusters together the peaks in one or more peak lists. Lists can be clustered based on the chemical shifts in one or more dimensions. The dimensions and tolerances used are specified with the peak template command. All peaks that fall within the same cluster are linked together.

**compare**

:    **nv_peak** **compare** 

:    Not implemented

**compress**

:    **nv_peak** **compress**  *peakList* 

:    Compresses 'peakList' by permanently removing peaks that have been marked for deletion. Use care with this command, after compression deleted peaks cannot be restored!

**couple**

:    **nv_peak** **couple**  *[-ignore* | *-inphase* | *-anti]* | *-wDim*  *min*  *max*  *...*  *peakList* 

:    Couples together peaks that are within the specified tolerances. For example,
:    

nv_peak couple -inphase -w1 0 3 -w2 0 20
:    

would couple together any peaks whose centers were between 0 and 3 Hz apart in the first dimension, and between 0 and 20 Hz apart in the second dimension, and whose intensities had the same sign.

**dataset**

:    **nv_peak** **dataset**  *peakList*  *?dataset?* 

:    Returns the dataset associated with 'peakList'. If the 'dataset' argument is present, 'dataset' is set to be associated with 'peakList'.

**delete**

:    **nv_peak** **delete**  *peakSpecifier* 

:    Deletes one peak or an entire peak list.  If the peakSpecifier does not have any "." characters, that is it describes only a list not a specific peak, then the entire list will be removed. Deleting an entire peak list cannot be undone. Otherwise, it marks the peak described with 'peakSpecifier' for deletion. The peak can be restored with the "nv_peak undel" command, or from the peak analysis window. The peak is permanently lost if the peak list is compressed with the "nv_peak compress" command. Peaks marked for deletion are not saved in the database when the database is written.

**delregion**

:    **nv_peak** **delregion**  *peakList*  *?xppm1*  *xppm2*  *yppm1*  *yppm2*  *...?* 

:    Marks for deletion the peaks in the peak list whose centers are in the active box.  If the peakList argument is not specified, the peaklist used is the first peak list assigned to the currently active window.  If the position arguments are not specified, they are taken from the position of the crosshair cursors in the active window.  If positions are specified as arguments, the peakList to be used must also be specified.
.

**dim**

:    **nv_peak** **dim** 

:    Not yet documented

**display**

:    **nv_peak** **display**  *[peakList]* 

:    Draw boxs and labels at the position of all the peaks in the peak list. The peak list displayed is the active list if "LIST" argument is not specified, otherwise the specified list is displayed. For example, "peak display noesy", would display all the peaks in the peak list named "noesy". Display occurs in the active window. The peak-display list can also be set in the PEAK_ATTRIBUTES_PANEL.

**dmatch**

:    **nv_peak** **dmatch**  *[listA*  *listB]* 

:    Not implemented
:    
Execute the peak double-matching algorithm to compare the two peak lists, listA and listB. Prior to using this command use the peak template command to set up the search template. Only peak fields specified in the template will be compared. The command creates two tcl array variables, dmA, dmB. There is one element in each array for each peak from the corresponding list. If the element is positive, it is the index of the peak in the other list that double-matches. If it is negative, it is the index of the peak in the other list that was closest, but the match was not a double match. A double match occurs if the following conditions are met: Consider two peaks Ai and Bj from two peak lists listA and listB. The distance between peaks Ai and Bj must be within the specified tolerances for each dimension (specified with the search template). The peaks double match, if and only if, Bj is the peak in list B that is closest to Ai, and Ai is the peak in list A that is closest to peak Bj. If a negative tolerance is specified in the search template, nv_peaks match only if the dimensions with the negative tolerance are not within the tolerance. This can be used, for example, when comparing two 4D lists and one wants to exclude matches where all 4 dimensions agree. This command also returns as its result a list of the dimension names and the corresponding rms deviation between pairs of double matched peaks in the two lists.

**elem**

:    **nv_peak** **elem** 

:    Returns the value of the element specified by 'elemSpecifier' for the peak 'peakSpecifier'. If the optional argument is included the command sets the element to the value specified. The valid elements are:

     |Element |Description|
     |--------|-----------|
     |Labe  l |        The chemical shift of along the specified dimension.|
     |Label.P |        The chemical shift of along the specified dimension.|
     |Label.W |        The peak width for the specified dimension.|
     |Label.L |        The atom label for the specified dimension.|
     |Label.E |    The peak error message for the specified dimension.|
     |Label.B |    The bounds for the specified dimension.|
     |Label.J |    The J-coupling for the specified dimension.|
     |Label.U |    The user-comment for the specified dimension.|
     |int     |    The peak intensity.|
     |vol     |    The peak volume.|
     |status  |    The peak status (deleted or not)|
     |flag0   |    The peak lock status (locked or not)|
     |comment |    The peak comment|

     For example,
         `nv_peak elem 15N.W hnco.45`
     would return the peak width for the 15N dimension of peak 45 of the list hnco.

**find**

:    **nv_peak** **find**  *peakList*  *ppm1*  *ppm2*  *...* 

:    Returns a list of the numbers of the peaks in the specified peak list that are within a specified tolerance of the specified chemical shifts (ppm1, ppm2 ...). The tolerance and peak dimensions to test are specified with the "nv_peak template" command, see below.

**fit**

:    **nv_peak** **fit**  *dataset*  *-range*  *r1*  *r2?*  *peak1*  *?peak2*  *peak3*  *...?* 

:    Does a lineshape fit to the specified peaks.  Currently only works for 1D peaks.

**fold**

:    **nv_peak** **fold**  *peakSpecifier*  *up* | *down* |

:    Increments or decrements the chemical shift of the specified peak by an amount corresponding to one "sweep width". The peakSpecifier must include a dimension field. For example, "hnco.32.0".  The sweep width value is taken from that associated with the peak's list, and may be set with the "nv_peak sw" command.  By default it is the value in the dataset from which the peaks are derived.

**getpeak**

:    **nv_peak** **getpeak**  *peakSpecifier* 

:    Returns a list of parameters describing the peak.

**idlast**

:    **nv_peak** **idlast**  *peakList* 

:    Returns the identifier number of the last peak in the specified peakList

**idnum**

:    **nv_peak** **idnum**  *peakSpecifier* 

:    Returns the peakID corresponding to the ordinal of 'peakSpecifier'. For example, with a list that has peaks 0, 2, 3...,
:    
"nv_peak idnum list.0" returns 0
:    
"nv_peak idnum list.1" returns 2
:    
"nv_peak idnum list.2" returns 3

**idtol**

:    **nv_peak** **idtol**  *listName*  *[idTol1]*  *[idTol2]*  *...* 

:    Returns or sets the tolerance used by the idpeak command for 'listName'. A value must be specified for each dimension of the list. For example,
:    
nv_peak idtol noesy 0.1 0.3
:    
nv_peak idtol noesy3d  0.1 0.3 0.4

**inbox**

:    **nv_peak** **inbox**  *peakList*  *?xppm1*  *xppm2*  *yppm1*  *yppm2*  *...?* 

:    Returns a list of peaks in the specified region.  If the peakList argument is not specified, the peaklist used is the first peak list assigned to the currently active window.  If the position arguments are not specified, they are taken from a region between the crosshair cursors in the active window.  If positions are specified as arguments, the peakList to be used must also be specified.
 The peaks in the list are sorted according to their distance from the center of the box.  For example, "peak inbox hmqc" would find the peaks in the peak list named "hmqc" that are within the cursor box in the active window.

**inregion**

:    **nv_peak** **inregion**  *listName*  *ppm1_1*  *ppm1_2*  *?ppm2_1*  *ppm2_2?* 

:    Returns a list of peaks in the specified region.  There must be a pair of ppm limit values for each dimension of the peak list.

**jfit**

:    **nv_peak** **jfit**  *dataset*  *-range*  *r1*  *r2*  *-amp*  *-lwamp*  *-rms*  *-maxdev?*  *peak1*  *?peak2*  *peak3*  *...?* 

:    Does a lineshape fit to the specified peaks.  Currently only works for 1D peaks.

**labels**

:    **nv_peak** **labels**  *peakList*  *?label1*  *label2*  *...?* 

:    Returns the labels for the various dimensions of 'peakList'.  If the labels parameters are included then set the dimension labels for the peak list.  There must be one label argument for each dimension of the list.

**lfit**

:    **nv_peak** **lfit** 

:    Not yet documented

**link**

:    **nv_peak** **link**  *peakSpecifier1*  *?peakSpecifier2*  *...?* 

:    Creates a link between the first peak listed and any additional peaks listed. If only one peak is given a list of peaks linked that peak is returned.
	The format of the peakSpecifier must include the link dimension as well as the list name/number and peak number. For example, noesy.35.1 specifies dimension 1 of peak 35 of list noesy and noesy.40.N specifies the dimension labeled "N" of peak 40 of list noesy.

**lists**

:    **nv_peak** **lists** 

:    Returns the names of all peak lists currently loaded.

**maplink**

:    **nv_peak** **maplink** 

:    Experimental. Not yet documented

**match**

:    **nv_peak** **match**  *peakList*  *arg*  *...* 

:    Returns a list of peaks for which any of the peak labels match the argument(s). For example, "nv_peak match noesy 14.hn" returns the peak specifiers for any peaks in the list "noesy" that had a label of "14.hn" in any dimension. Wild cards are accepted. For example, "nv_peak match * 33.c*" returns the peak specifiers for peaks in any of the lists that had a carbon of residue 33 as the peak label. It is also possible to use multiple arguments. For example, "nv_peak -match noesy 14.ha 15.hn" returns peaks of the list "noesy" that had labels of 14.ha and 15.hn.


**mknoelist**

:    **nv_peak** **mknoelist**  *peakList*  *nDim*  *lab1*  *lab2*  *..*  *labnDim*  *maxDis*  *i0* 

:    Not implemented.
:    Creates a new list "peakList". The number of peak dimensions are specified by "nDim". The peak labels for each dimension are specified by the 'labN' arguments. Entries are made for any pairs of protons that are less than 'maxDis' apart. The intensity is calibrated with the isolated spin pair approximation using I=C*r^6. The constant C is calculated by assuming that a pair of protons with distance 2.0 E would have the intensity specified with the i0 argument. BUG: Not tested in new version.

**n**

:    **nv_peak** **n**  *peakList* 

:    Returns the number of peaks in 'peakList'.

**name**

:    **nv_peak** **name**  *peakList*  *newName* 

:    Changes the name of 'peakList' to 'newName'.

**nearest**

:    **nv_peak** **nearest**  *peakList*  *?xppm1*  *xppm2*  *yppm1*  *yppm2*  *...?* 

:    Returns a list of peaks close to the center of the specified region.  If the peakList argument is not specified, the peaklist used is the first peak list assigned to the currently active window.  If the position arguments are not specified, they are taken from a region around the positon of the first crosshair cursor in the active window.  If positions are specified as arguments, the peakList to be used must also be specified.
:    
The peak list examined is list associated with the current window if the 'peakList' argument is not given, otherwise 'peakList' is examined. Note: the peaks located will be closest to the cursor position (the black crosshair), not the mouse position. For example, "nv_peak nearest noesy" finds the peaks in the peak list named "noesy", that are close to the cursor position. The list of peaks returned is sorted in order of the distance of the peaks from the cursor. Thus, the first peak in the list is the closest. If no peaks are within a certain tolerance, an error message will be returned.

**panel**

:    **nv_peak** **panel**  *?peakSpecifier?* 

:    If the peakSpecifier argument is provided this command will changes the peak analysis window to display information about the specified peak. The command also returns as its result the nv_peakSpecifier for the peak active in the peak analysis window.  Implemented using the Tcl scripts NvPeakSetPeak and NvPeakGetPeak

**pattern**

:    **nv_peak** **pattern**  *listName*  *[pattern1]*  *[pattern2]*  *...* 

:    Returns or sets the pattern used by the idpeak command (and potentially other commands as well). The pattern is in the form of an atomSpecifier, typically with the letters "i" or "j" replacing the residue field. For example:
:    

i.hn, j.ca
:    

Wild cards may be used:  i.h*
:    

The residue field may include an integer offset: i-1.h*
:    

To set the pattern for an cbca(co)nnh experiment:
:    

nv_peak pattern cbcaconnh i-1.c* j.n j.hn
:    

This command needs to be extended to allow more complicated expressions.

**precision**

:    **nv_peak** **precision**  *peakList*  *?precision1*  *precision2*  *...?* 

:    Return, or sets, the precision used in returning chemical shift data for the peak list.  One value is returned for each of the list's dimensions.  If one value is included as an argument for each peak dimension then the precision parameter for the peak list will be set to the specified values.

**ref**

:    **nv_peak** **ref**  *peakList*  *ref1*  *ref2*  *...?* 

:    Get or set reference values for each dimension of the peak list.  These values are not presently used for anything???

**relation**

:    **nv_peak** **relation**  *peakList*  *?relation?* 

:    Returns the relation fields that specify the "familial" relation between peak dimensions of 'peakList'. If the 'relation' argument is given, the relation is set to that for 'peakList'. Dimensions that are the parent of other dimensions would be specified as P(1). Where the "1" is an integer that specifys the dimension that the specified field is the parent of. For example, a 1H, 15N sqc experiment might have the relation: "" P(1), indicating that the atom of the second dimension (the nitrogen) is the parent of the atom of the first dimension (the proton).

**remove**

:    **nv_peak** **remove**  *peakList* 

:    Removes the specified peak list.  Deprecated.  Use "nv_peak delete peakList" instead.

**renumber**

:    **nv_peak** **renumber** 

:    Renumbers the list so that there are no gaps in the id numbers for the peaks.

**scale**

:    **nv_peak** **scale**  *peakList*  *?scaleVale?* 

:    Gets or sets a scale value for the peak list.  The scale value is used in the peak table when calculating the normalized atom number (N).  The calculated value is the peak volume divided by the scale value.

**score**

:    **nv_peak** **score** 

:    Calculate a score of the fit of a peak with dataset values.  Only works with 1D data at present.

**sf**

:    **nv_peak** **sf**  *peakList*  *[sf1]*  *[sf2]*  *...* 

:    Returns the spectrometer frequency for each dimension of the peak list. The spectrometer frequencies for a peak list are set to those of the spectrum it was picked from. If the sf1, sf2 ... arguments are included the spectrometer frequencies are changed to the specified values.

**show**

:    **nv_peak** **show**  *[peakSpecifier]* 

:    Unused.  The functionality of this command from NMRViewC is now entirely implemented with Tcl scripts.

**sort**

:    **nv_peak** **sort**  *listName*  *?iDim*  *ascending?* 

:    Sorts the peaks in the specified list.  With no optional arguments the peaks are sorted based on the peak position in the first dimension and in ascending order.  The peak dimension can be specified with the iDim parameter (0, 1, ..  Warning: we may change the numbering from 1,2 ... in the future).  If the ascending option is specified as "0", the peaks will be sorted in descending order.

**status**

:    **nv_peak** **status**  *peakSpecifier*  *[peakStatus]* 

:    Returns the status flag for the peak specified with the peakSpecifier argument. If the optional peakStatus argument is included the status flag of the specified peak is set to the specified value. Peaks with negative status values are marked for deletion. They do not appear when the list is displayed on a spectra and will be permanently removed when the list is compressed.

**sw**

:    **nv_peak** **sw**  *peakList*  *[sw1]*  *[sw2]*  *...* 

:    Returns the sweepwidth for each dimension of 'peakList'. The sweepwidths for a peak list are initially set to those of the spectrum that it was picked from. If the optional sw1, sw2 ... arguments are included the sweepwidths are changed to the specified values.

**swap**

:    **nv_peak** **swap**  *peakList*  *label1*  *label2* 

:    Not yet implemented in NvJ.
:    
Locates any peaks in 'peakList' with labels label1 or label2 and exchanges the two labels. This command is useful for changing prochiral atoms. For example,
:    
nv_peak swap noesy 24.hb1 24.hb2
:    
could be used to exhange the labels for the beta-methylene protons of residue 24 in the peak list "noesy". If an asterisk, "*", is used for the 'peakList' argument, matching peaks from all open lists will have their labels swapped.

**template**

:    **nv_peak** **template**  *peakList*  *[name]*  *[ppm]*  *...* 

:    Specifies a template to be used by the nv_peak find and peak dmatch commands, and returns the current template. For example, if the template is specificied as,
:    
nv_peak template hmqc 1HN 0.1 15N 0.3
:    
then a peak find command like
:    
nv_peak find hmqc 8.3 118.2
:    
would find all peaks whose 1HN chemical shift is within 0.1 ppm of 8.3 ppm, and whose 15N chemical shift is within 0.3 ppm of 118.2 ppm. The number of name:ppm pairs in the peak template command should match the number of ppms specified in the peak find command for each peak list used.

**undelete**

:    **nv_peak** **undelete**  *peakSpecifier* 

:    Unmarks 'peakSpecifier' for deletion. A peak is permanently lost if it is marked for deletion when the peak list is compressed.

**undelregion**

:    **nv_peak** **undelregion**  *peakList*  *?xppm1*  *xppm2*  *yppm1*  *yppm2*  *...?* 

:    Undeletes the peaks in the peak list whose centers are in the active box.  If the peakList argument is not specified, the peaklist used is the first peak list assigned to the currently active window.  If the position arguments are not specified, they are taken from the position of the crosshair cursors in the active window.  If positions are specified as arguments, the peakList to be used must also be specified.
.
:    
Note: Once a peaklist has been compressed the peaks marked for deletion can not be restored. The peak list examined is the list associated with the current window if 'peakList' argument is not specified, otherwise 'peakList' is examined.

**unlink**

:    **nv_peak** **unlink**  *peakSpecifier* 

:    Removes any links between 'peakSpecifier' and all peaks currently linked to it.  If the peakSpecifier includes the dimension then only that dimension will be unlinked, otherwise all dimensions of the peak will be unlinked.

**updatecouplings**

:    **nv_peak** **updatecouplings** 

:    Not yet documented.

**write**

:    **nv_peak** **write**  *-xml*  ** | ** | *-star*  *listName*  *channelName* 

:    Write peaks in XML (non standardized version, subject to change) or STAR Version 2 formats.

**writexml**

:    **nv_peak** **writexml** 

:    Write peaks in XML (non standardized version, subject to change) format.

**zlink**

:    **nv_peak** **zlink**  *peakList* 

:    All links of peaks from 'peakList' are zeroed.

##nv_pkcluster


Worth with clusters of peaks.

**Sub-commands**

:    nv_pkcluster fragment

:    nv_pkcluster fragshifts

:    nv_pkcluster get

:    nv_pkcluster last

:    nv_pkcluster link

:    nv_pkcluster new

:    nv_pkcluster overlap

:    nv_pkcluster ppm

:    nv_pkcluster prune

:    nv_pkcluster scoreres

:    nv_pkcluster scoreseq

:    nv_pkcluster unlink




**fragment**

:    **nv_pkcluster** **fragment**  *clusterAnalyzerName*  *iClust* 

:    Return the fragment (a series of clusters) that contains contains the specified cluster.

**fragshifts**

:    **nv_pkcluster** **fragshifts**  *clusterAnalyzerName*  *fragment* 

:    Returns a list of chemical shifts and matching peaks for the clusters in the fragment.

**get**

:    **nv_pkcluster** **get**  *clusterAnalyzerName*  *clusterIndex* 

:    Return a list of all peaks in the specified cluster.

**last**

:    **nv_pkcluster** **last**  *clusterAnalyzerName* 

:    Return the peak identifier for the last peak in the reference list.  This should be the last possible cluster identififer.

**link**

:    **nv_pkcluster** **link**  *clusterAnalyzerName*  *iClust*  *?jClust?* 

:    If jClust is not specified, then return the clusters that are linked to iClust.  If it is specified then link the two clusters together.

**new**

:    **nv_pkcluster** **new**  *clusterAnalyzerName*  *refList*  *list1*  *linkDim1*  *list2*  *linkDim2*  *...* 

:    Creates a new cluster analyzer tool.  Multiple cluster analyzers can be present so each one needs a name (clusterAnalyzerName).  In RunAbout each cluster must contain one peak from a reference list.  The reference list is specified with the refList argument.  The remaining arguments come in pairs, a peak list to be included in the cluster analysis, and a dimension name for the list to be used when linking through the carbons.  The list used for a reference list can also be listed as a linking list.

**overlap**

:    **nv_pkcluster** **overlap**  *clusterAnalyzerName*  *iClust*  *jClust* 

:    Return the scores and overlapping peaks between the two specified clusters.  If either cluster index is set to -1, then all clusters are compared to the other cluster.
:    
The result is of the form:
matchingCluster overlapScore numberOfMatchingCarbons matchLists
:    
The matchList has the form:
dimensionName averagePPM intraresiduePeaks interresiduePeaks
:    
Examples:
:    
nv_pkcluster overlap pkc 1 -1
:    
:    
nv_pkcluster overlap pkc 1 30
:    

**ppm**

:    **nv_pkcluster** **ppm**  *clusterAnalyzerName*  *iClust*  *peakDimName* 

:    Return the average chemical shift of the specified peak dimension (either the proton or nitrogen) in the iClust cluster.

**prune**

:    **nv_pkcluster** **prune** 

:    Not yet documented.

**scoreres**

:    **nv_pkcluster** **scoreres**  *clusterAnalyzerName*  *iClust*  *jClust* 

:    Return a series of scores indicating how well this pair of clusters could match different residue types.
:    
Example output:
:    
arg 0.031 cys 0.858 gln 0.004 glu 0.009 his 0.053 ile 0.292 lys 0.167 met 0.15 phe 0.081 pro 0.012 trp 0.052 tyr 0.164 val 0.515

**scoreseq**

:    **nv_pkcluster** **scoreseq**  *clusterAnalyzerName*  *molName*  *entityName*  *fragmentList* 

:    Return a list of scores and possible matchings of the fragment (a sequence of clusters) against the specified molecular entity.  Each possible matching is a list consisting of the starting residue, the score (a Bayesian probability), and the chemical shift and peak matches for each cluster in the fragment.

**unlink**

:    **nv_pkcluster** **unlink**  *clusterAnalyzerName*  *clusterIndex1*  *clusterIndex2* 

:    Remove the link between the specified clusters.

##nv_residue


Deprecated





**resNum**

:    **nv_residue** **resNum**  *[varName]* 

:    Deprecated

##nv_resonance


Query and assign resonances.

**Sub-commands**

:    nv_resonance assign

:    nv_resonance clear

:    nv_resonance label

:    nv_resonance n

:    nv_resonance peakdims




**assign**

:    **nv_resonance** **assign**  *resonanceID*  *?atomSpecifier?* 

:    Return, or set, the atom assigned to the specified resonance.  The atomSpecifier must correspond to an existing atom.

**clear**

:    **nv_resonance** **clear** 

:    Clear the list of all resonances.  Use with caution.

**label**

:    **nv_resonance** **label**  *resonanceID*  *?label?* 

:    Return, or set, the label assigned to the specified resonance.  The label can be any arbitrary text, and doesn't need to correspond to an existing atom.

**n**

:    **nv_resonance** **n** 

:    Return the number of resonances.

**peakdims**

:    **nv_resonance** **peakdims**  *resonanceID* 

:    Return a list of all peak dimensions linked to the specific resonance.

##nv_sread


Read molecular structures.

**Sub-commands**

:    nv_sread pdb

:    nv_sread pdbx

:    nv_sread ressd

:    nv_sread sd

:    nv_sread seq

:    nv_sread xpsf

:    nv_sread xyz




**pdb**

:    **nv_sread** **pdb**  *fileName* 

:    Read Protein Data Bank format files. This is the standard way to read in pdb files.  NMRView first reads the pdb file to determine the amino acid sequence.  Next, it reads the corresponding residues from the PEGASUS residue library.  Finally, it reads coordinates from the pdb file for those atoms that have names matching the names in the residue library.  Atoms, that do not have a match in the residue library will not be entered into the PEGASUS structure list.  Atoms that are in the residue library but not in pdb file, will be included in structure list but will not be displayed. The file will be read from directory $SDIR where SDIR is a TCL variable.  SDIR can be set in the preference panel or on the command line.  The default value for SDIR is ".".

**pdbx**

:    **nv_sread** **pdbx** 

:    Not yet documented

**ressd**

:    **nv_sread** **ressd**  *fileName*  *?fileContent?*  *molName* 

:    Reads sdfile (also mol) files from specified fileName.  The molecule data read from the file (or fileContent string) is used to create a new compound within the specified molecule, rather than creating a new molecule. If fileContent is specified then the the molecular structure is read directly from the provided string.

**sd**

:    **nv_sread** **sd**  *fileName*  *?fileContent?* 

:    Reads sdfile (also mol) files from specified fileName.  If fileContent is specified then the the molecular structure is read directly from the provided string.

**seq**

:    **nv_sread** **seq**  *seqName* 

:    Read in residues from residue library based on sequence in file filename.

**xpsf**

:    **nv_sread** **xpsf**  *fileName* 

:    Not yet implemented.  Reads a file in the format produced by XPLOR.  This is a alternative method to the "nv_sread seq" command to obtain atom, residue and connectivity information.  Coordinates must be read in with the "nv_sread xyz" or "nv_sread grp" commands.  The directory used is the same as that used with "sread -pdb" command.

**xyz**

:    **nv_sread** **xyz**  *fileName*  *strct* 

:    Reads the PDB file filename and attempts to match the atoms to atoms in the
structure in memory.  If atoms match by residue name, atom name, sequence
number, chain id, and alternate identifier then the coordinates corresponding
to each atom matched are assigned the value of the coordinates of that atom in
file.  The coordinates are read into the structure specified by the "strct"
parameter.   The directory used
is the same as that used with "sread -pdb" command.

##nv_swrite


Write molecular structures.

**Sub-commands**

:    nv_swrite ppm

:    nv_swrite sxyz




**ppm**

:    **nv_swrite** **ppm** 

:    Not yet documented

**sxyz**

:    **nv_swrite** **sxyz** 

:    Not yet documented

##nv_win


Control spectral windows.

**Sub-commands**

:    nv_win aclear

:    nv_win active

:    nv_win addtag

:    nv_win adim

:    nv_win attributes

:    nv_win axis

:    nv_win axisline

:    nv_win bbox

:    nv_win bgcolor

:    nv_win bind

:    nv_win border

:    nv_win box

:    nv_win busy

:    nv_win caldelta

:    nv_win canvasx

:    nv_win canvasy

:    nv_win center

:    nv_win cget

:    nv_win clear

:    nv_win clm

:    nv_win closest

:    nv_win configure

:    nv_win coords

:    nv_win copy

:    nv_win copyimage

:    nv_win create

:    nv_win cross1

:    nv_win cross1x

:    nv_win cross1y

:    nv_win cross2

:    nv_win cross2x

:    nv_win cross2y

:    nv_win crosscolor

:    nv_win crosshair

:    nv_win crossmode

:    nv_win crossstate

:    nv_win cursor

:    nv_win czoom

:    nv_win dataset

:    nv_win datatitles

:    nv_win dcoffset

:    nv_win defer

:    nv_win delete

:    nv_win delregion

:    nv_win deltaoffset

:    nv_win dim

:    nv_win dispeaks

:    nv_win display

:    nv_win draw

:    nv_win drawlist

:    nv_win drawpeak

:    nv_win dtag

:    nv_win edit

:    nv_win erasepeak

:    nv_win expand

:    nv_win export

:    nv_win find

:    nv_win full

:    nv_win gettags

:    nv_win grid

:    nv_win hit

:    nv_win inbox

:    nv_win index

:    nv_win integrals

:    nv_win interp

:    nv_win itemcget

:    nv_win itemconfigure

:    nv_win jadd

:    nv_win jmode

:    nv_win label

:    nv_win links

:    nv_win lower

:    nv_win lvl

:    nv_win masked

:    nv_win maxveclen

:    nv_win mode

:    nv_win move

:    nv_win name

:    nv_win ndim

:    nv_win nearest

:    nv_win neg

:    nv_win negcolor

:    nv_win negwidth

:    nv_win new

:    nv_win newtype

:    nv_win nlvls

:    nv_win object

:    nv_win open

:    nv_win paste

:    nv_win peak_col_off

:    nv_win peak_col_on

:    nv_win peak_col_type

:    nv_win peak_dis_type

:    nv_win peak_lab_type

:    nv_win peak_off

:    nv_win peak_types

:    nv_win peakattributes

:    nv_win peaklist

:    nv_win pick

:    nv_win pix2ppm

:    nv_win plot

:    nv_win pos

:    nv_win poscolor

:    nv_win poswidth

:    nv_win ppm

:    nv_win ppmmax

:    nv_win previous

:    nv_win pt

:    nv_win raise

:    nv_win refreshcrosshairs

:    nv_win region

:    nv_win regioncolor

:    nv_win repfile

:    nv_win scale

:    nv_win scale1d

:    nv_win search

:    nv_win selectdataset

:    nv_win selectpeak

:    nv_win shift

:    nv_win show

:    nv_win showpeaks

:    nv_win slice

:    nv_win stop

:    nv_win svg

:    nv_win thread

:    nv_win transformer

:    nv_win type

:    nv_win wait

:    nv_win winpeak

:    nv_win xdim

:    nv_win xoffset

:    nv_win xshear

:    nv_win ydim

:    nv_win yoffset

:    nv_win z2dim

:    nv_win zdim

:    nv_win zoom




**aclear**

:    **nv_win** **aclear**  *clearMode?* 

:    Unused in NvJ

**active**

:    **nv_win** **active**  *windowName* 

:    Returns the pathName of the active window.  If the optional argument is present then it sets the active window to the specified window.

**addtag**

:    **nv_win** **addtag**  *tagOrId*  *?tagOrId*  *tagOrId*  *...?* 

:    Same as Tk canvas "addtag" subcommand

**adim**

:    **nv_win** **adim**  *dimNum* 

:    Sets the z2 (or a) display dimension of the active window to dimNum.

**attributes**

:    **nv_win** **attributes** 

:    Display the Spectrum Attributes window. Does this by calling the Tcl proc "spectrum::showAttrPanel"

**axis**

:    **nv_win** **axis**  *axis*  *axis1*  *axis2* 

:    Returns a 0 or 1 specifying whether or not the bottom and top axis (and left and right) labels and tick marks should be drawn. If the axis1 and axis2 arguments are specified the respective axes are turned on or off as specified. The values are specified as boolean values (0/1, yes/no, on/off or true/false).
For example,  to turn the labels and tic marks for both the bottom and top
axis off
:    
nv_win axis x 0 0
:    
use "nv_win axisline" to control the display of the acutal axis line."

**axisline**

:    **nv_win** **axisline**  *axis*  *axis1*  *axis2* 

:    Returns a 0 or 1 specifying whether or not the bottom and top axis (and left and right) line should be drawn. If the axis1 and axis2 arguments are specified the respective axis lines are turned on or off as specified. The values are specified as boolean values (0/1, yes/no, on/off or true/false).
For example,  to turn the axis lines for both the bottom and top
axis off
:    
nv_win axis x 0 0
:    
use "nv_win axis" to control the display of the tic marks and labels"

**bbox**

:    **nv_win** **bbox** 

:    Same as Tk canvas "bbox" subcommand

**bgcolor**

:    **nv_win** **bgcolor**  *newColor* 

:    Returns the current color used for the background of the active spectrum window.  If the optional parameter, newColor, is specified, then the background is set to that value.  This command is redundant to "nv_win configure -bg".

**bind**

:    **nv_win** **bind**  *bind*  *tagOrId*  *?sequence?*  *?command?* 

:    Same as Tk canvas "bind" subcommand

**border**

:    **nv_win** **border**  *axis*  *border1*  *border2* 

:    Returns the borders for the left and right sides, or top and bottom, of the plot region in the active window. If the border1 and border2 arguments are specified the appropriate borders are set to the specified values. The values are specified in units of pixels.
:    
The command, "nv_win border x 100 50", would set the border on the left side of the spectrum to 100 pixels, and on the right side of the spectrum to 50 pixels.

**box**

:    **nv_win** **box**  *xVal*  *yVal*  *0* | *1* |

:    Use this command to draw a temporary box on the spectrum.  Generally this would be used from a mouse binding to draw a resizable box.  With a mode value 0f "0", the xVal and yVal arguments set the position (in pixels) of the starting corner of the box.  With a mode value of "1", the xVal and yVal arguments set the ending corner of the box and redraws the box.

**busy**

:    **nv_win** **busy** 

:    Returns the value "1" if the spectrum is actively being drawn and "0" if the spectrum drawing is idle.

**caldelta**

:    **nv_win** **caldelta**  *mode* 

:    This determines how the ofsets between 1D vectors are calculated when more than one spectrum (or row) is drawn in a single window.
:    
With a setting of 0, there will be no DC ofset between spectra.
:    
With a setting of 1, the DC offset will be calculated so that spectra will be evenly spaced across the vertical range of the spectrum.
:    
With a setting of 2, the DC offset will be taken from the "deltaoffset" parameter, set with "nv_win deltaoffset".
:    
With a setting of 3, the DC offset will be calculated so that the spectra will be evenly spaced across the vertical range of the spectrum.
:    
With a setting of 4, the DC offset will be caculated from the "deltaoffset" parameter and the number of spectra to be displayed.

**canvasx**

:    **nv_win** **canvasx** 

:    Not yet documented

**canvasy**

:    **nv_win** **canvasy** 

:    Not yet documented

**center**

:    **nv_win** **center**  *?xPos*  *yPos?* 

:    Shift view displayed in spectrum window to center on the specified xPos and yPos positions (in ppm)  If these arguments are not included the x and y position is taken from the current position of the first crosshair (usually black).  The width and hieght of the displayed region is unchanged by this command.

**cget**

:    **nv_win** **cget** 

:    Not yet documented

**clear**

:    **nv_win** **clear** 

:    Has no observable effect in NMRViewJ

**clm**

:    **nv_win** **clm**  *?-dataset*  *datasetName?*  *contourLevelMultiplier?* 

:    Returns the contour level multiplier used in the active window. If the optional argument is specified the contour level multiplier in the active window is set to contourLevelMultiplier. For example, "nv_win clm 1.5", sets the contour level multiplier in active window to 1.5.

**closest**

:    **nv_win** **closest** 

:    Unused, use corresponding "nv_peak" command.

**configure**

:    **nv_win** **configure** 

:    Not yet documented

**coords**

:    **nv_win** **coords** 

:    Same as Tk canvas "coords" subcommand

**copy**

:    **nv_win** **copy** 

:    Copy data about active window into a buffer.

**copyimage**

:    **nv_win** **copyimage** 

:    Puts graphic representation of spectrum on to the system clipboard where it can be pasted into other applications.

**create**

:    **nv_win** **create** 

:    Same as Tk canvas "create" subcommand

**cross1**

:    **nv_win** **cross1**  *x*  *y?* 

:    Returns the coordinates (in ppm) of CrossHair_1 in the active window. If the optional arguments are specified the position of CrossHair_1 is set to x, y. For example, "nv_win cross1 3.2 4.3", sets CrossHair_1 in the active window to (3.2,4.3) in ppms.

**cross1x**

:    **nv_win** **cross1x**  *x?* 

:    Returns the x coordinate (in ppm) of CrossHair_1 in the active window. If the optional argument are specified the x value of CrossHair_1 is set to x. For example, "nv_win cross1x 3.2", sets x value of CrossHair_1 in the active window to 3.2 in ppms. The y value is unchanged.

**cross1y**

:    **nv_win** **cross1y**  *y?* 

:    Returns the y coordinate (in ppm) of CrossHair_1 in the active window. If the optional argument are specified the y value of CrossHair_1 is set to y. For example, "nv_win cross1x 3.2", sets y value of CrossHair_1 in the active window to 3.2 in ppms. The x value is unchanged.

**cross2**

:    **nv_win** **cross2**  *x*  *y?* 

:    Returns the coordinates (in ppm) of CrossHair_2 in the active window. If the optional arguments are specified the position of CrossHair_1 is set to x, y. For example, "nv_win cross2 3.2 4.3", sets CrossHair_2 in the active window to (3.2,4.3) in ppms.

**cross2x**

:    **nv_win** **cross2x**  *x?* 

:    Returns the x coordinate (in ppm) of CrossHair_2 in the active window. If the optional argument are specified the x value of CrossHair_2 is set to x. For example, "nv_win cross2x 3.2", sets x value of CrossHair_2 in the active window to 3.2 in ppms. The y value is unchanged.

**cross2y**

:    **nv_win** **cross2y**  *y?* 

:    Returns the y coordinate (in ppm) of CrossHair_2 in the active window. If the optional argument are specified the y value of CrossHair_2 is set to y. For example, "nv_win cross2x 3.2", sets y value of CrossHair_2 in the active window to 3.2 in ppms. The x value is unchanged.

**crosscolor**

:    **nv_win** **crosscolor**  *1* | *2* | *color* 

:    Returns the color used for drawing the first or second crosshair.  If the optional color argument is used the specified crosshair is set to that color.

**crosshair**

:    **nv_win** **crosshair**  *crossHair*  *xVal*  *yVal*  *mode*  *mouseType* 

:    Provides low level control of the crosshairs (as compared to the cross1, cross2 etc. commands).  The crossHair parameter should be 1 or 2, to specify the first or second crosshairs.  The "xVal" and "yVal" parameters set the crosshair positon (in pixels).  The mode parameter specifies the action that should happen when the command is executed.  The mouseType specifies whether the crosshair behaviour should be appropriate for a one (1) button or three (3) button mouse.  It defaults to "1" if not specified.  
:    
The actions taken depend on the mode value as follows.  Also, indicated is the mode value normally used for various mouse actions in the default crosshair programming
:    
<literallayout>
   0:  set when mouse is moved with button down,  move crosshair
   1:  set when mouse is pressed when in 1 button mode,
        figure out which crosshair to move, return without moving
   2:  set when mouse is released without mouse having been moved
   3:  when mouse is pressed when in 3 button mode 
   3:  figure out what to move when mouse is pressed when in 3 button mode 
   4:  set crosshair to position
</literallayout>

**crossmode**

:    **nv_win** **crossmode**  *1* | *2* | *x* | *y* | *xyMode* 

:    Returns the current mode for the specified crosshair line.  For example, <code>nv_win crossmode 1 x</code> would return the mode for the vertical (x) line of the first crosshaird.  The returned value is either 0 or 1, with 0 indicating that the crosshair line is inactive and will not appear on the dspectrum, and 1 indicating that the crosshair line is active and will appear on the spectrum.  The optional xyMode value can be specified to set the cross mode to inactive (0) or active (1).

**crossstate**

:    **nv_win** **crossstate**  *1* | *2* | *x* | *y* |

:    Returns the current state for the specified crosshair line.  For example, <code>nv_win crossmode 1 x</code> would return the state for the vertical (x) line of the first crosshair.  The returned value is either 0 or 1, with 0 indicating that the crosshair line is not currently displayed, and 1 indicating that the crosshair line is currently visible on the spectrum. Note that if a crosshair is visible, then the mode is set to 0, it will still return a state value of 1, even though setting the mode to 0 will have made the crosshair disappear.

**cursor**

:    **nv_win** **cursor**  *cursorType?* 

:    Returns, and optionally sets, the current cursor type for the window.  This command is redundant with the "nv_win configure -crosshair" command.  Note that changing the cursor will change the actions that happen when the mouse is clicked or dragged in the window.  For example, setting the cursorType to "crosshair" will cause crosshairs to be drawn when the mouse is clicked or dragged.

**czoom**

:    **nv_win** **czoom** 

:    Not yet implemented

**dataset**

:    **nv_win** **dataset**  *datasetName1*  *datasetName2*  *...?* 

:    Returns the name(s) of the dataset(s) used in the active window. If the optional argument is specified the datasets for the active window are set to the specified value(s). For example, "nv_win dataset noesy.mat", sets the dataset for the active window to "noesy.mat". The specified dataset must have been opened previously.  An unlimited number of datasets may be assigned to the window.

**datatitles**

:    **nv_win** **datatitles**  *drawTitles* 

:    Returns 0 or 1 to indicate whether or not the title of the dataset should be drawn in the spectrum window.  If the optional boolean value is included then the the state of title drawing will be changed to the specified value.  The title is normally drawn in the lower left corner of the spectrum.  By default, the title value for a dataset is set to the name of the dataset, but it can be changed with the "nv_dataset title" command.

**dcoffset**

:    **nv_win** **dcoffset**  *?0* | *1?* |

:    Returns, or sets if the optional argument is included, the state of automatic dcoffset mode.  This mode only effects the display of vectors (either true 1D spectra, or slices of higher dimensional spectra). If selected then the spectrum will be offset so that the edges of the spectrum will be displayed at zero. This is accomplished by subtracting a straight line calculated between the left and right edges. The offset is dynamically calculated as the spectrum plot limits are changed. The effect is only really appropriate when the spectrum is positioned so that the left and right eddges are "baseline" regions.

**defer**

:    **nv_win** **defer**  *on*  *off?* 

:    If set to "On" then don't defer drawing the  spectrum until set to "Off"

**delete**

:    **nv_win** **delete**  *tagOrId*  *tagOrID*  *...?* 

:    Delete eah of the spectrum canvas items given by each tagOrID, and return an empty string.

**delregion**

:    **nv_win** **delregion** 

:    Unused, use corresponding "nv_peak" command.

**deltaoffset**

:    **nv_win** **deltaoffset**  *?offsetValue?* 

:    Returns, or sets if the offsetValue argument is included, the offset between 1D spectra when multiple spectra are displayed in one window.  Whether or not this value is used depends on the state of the parameter set with the "nv_win caldelta" command.

**dim**

:    **nv_win** **dim**  *displayDimType?* 

:    Returns the display type as 0 (1Dx), 1 (1Dy) or 2 (2D). If the optional displayDimType argument the display type is set as specified.

**dispeaks**

:    **nv_win** **dispeaks**  *peakListName1*  *peakListName2*  *...?* 

:    Returns the name of the peak lists to be displayed in the active window. If the optional argument is specified the display peak list for the active window is set to the specified values. For example, "nv_win dispeaks list1", sets the peak list for the active window to "list1". Whenever this window is redrawn the peaks from the specified lists will be displayed. A practically unlimited number of peak lists may be specified.  To cancel peak display for the window use the "nv_peak dispeaks {}". See also the PEAK ATTRIBUTES PANEL.

**display**

:    **nv_win** **display** 

:    Not used

**draw**

:    **nv_win** **draw**  *?peaks?* 

:    Draws the current window.  If the optional "peaks" argument (literally the word "peaks") is added then only refresh the display of peaks and shapes in the spectrum.

**drawlist**

:    **nv_win** **drawlist**  *?-dataset*  *datasetName?*  *?"row1*  *row2*  *..."?* 

:    Returns or specifies a list of rows of a dataset that should be drawn.  This is only appropriate for arrayed one dimensional spectra or two dimensional spectra when they are drawn as a series of 1D vectors.  <code>
nv_win drawlist "1 5 30"
</code>would draw the first, fifth, and thirtieth, row of the spectrum.  Specifying an empty list <code>nv_win drawlist ""</code> will restore the drawing of all rows.

**drawpeak**

:    **nv_win** **drawpeak** 

:    Not yet documented

**dtag**

:    **nv_win** **dtag** 

:    Same as Tk canvas "dtag" subcommand

**edit**

:    **nv_win** **edit** 

:    Same as "nv_win copy".  Deprecated.

**erasepeak**

:    **nv_win** **erasepeak** 

:    Unused

**expand**

:    **nv_win** **expand** 

:    Draws expansion (area in cursor box) of active window.

**export**

:    **nv_win** **export** 

:    Export a graphical representation of the active window to a file.  The command first displays a dialog box from which the user can choose one of a variety of export formats including vector formats such as PDF, SVG EMF,and PostScript, and bitmap formats such as GIF, PNG, and JPEG.

**find**

:    **nv_win** **find**  *searchCommand*  *?arg*  *arg*  *...?* 

:    Same as Tk canvas find command.

**full**

:    **nv_win** **full** 

:    Draws full expansion of active window.

**gettags**

:    **nv_win** **gettags** 

:    Same as Tk canvas "gettags" subcommand

**grid**

:    **nv_win** **grid** 

:    Not implemented in NMRViewJ.  The grid command is a toggle command. If grids are off in the active window it causes a grid of points to be drawn in the active spectral window. The grid of points will be removed when the window is redrawn. If grids are currently on in the active window the grid command removes the grid. Each point in the grid is located at the position of a point in the file.

**hit**

:    **nv_win** **hit**  *tagOrID*  *x*  *y* 

:    Returns a parameter indicating the point on a displayed shape that is closest to the x and y values.  Only some shape types, for example molecules, support this feature.

**inbox**

:    **nv_win** **inbox** 

:    Unused, use corresponding "nv_peak" command.

**index**

:    **nv_win** **index** 

:    Same as Tk canvas "index" subcommand

**integrals**

:    **nv_win** **integrals**  *state* | *scale* | *offset* | *?value?* 

:    New experimental code for displaying 1D integrals

**interp**

:    **nv_win** **interp** 

:    Not yet documented

**itemcget**

:    **nv_win** **itemcget** 

:    Same as Tk canvas "itemcget" subcommand

**itemconfigure**

:    **nv_win** **itemconfigure** 

:    Same as Tk canvas "itemconfigure" subcommand

**jadd**

:    **nv_win** **jadd** 

:    For adding popup menus to spectrum.  Do not use.

**jmode**

:    **nv_win** **jmode**  *jmodType?* 

:    Returns the method for displaying peaks that have J-values (coupling constants) greater than 0.0. With jmodType 0, a single peak is displayed with the J-value added to the peak width. With jmodType 1, two peaks are displayed with their centers shifted by the J-value.

**label**

:    **nv_win** **label**  *axisName*  *axisLabel* 

:    Returns the label for the specified axis of the spectrum. If the optional argument 'axisLabel' is specified then set the label to the specified value. 


**links**

:    **nv_win** **links**  *?0* | *1?* |

:    Returns, or sets if the optional argument is included, the whether lines sould be drawn between linked peaks.  This feature is experimental.

**lower**

:    **nv_win** **lower** 

:    Same as Tk canvas "lower" subcommand

**lvl**

:    **nv_win** **lvl**  *?-dataset*  *datasetName?*  *Level?* 

:    Returns the contour level of the active window. If the optional argument is specified the contour level of the active window is set to Level. For example, "nv_win lvl 0.2" sets the contour level in active window to 0.2.

**masked**

:    **nv_win** **masked** 

:    Do not use

**maxveclen**

:    **nv_win** **maxveclen**  *?value?* 

:    Drawing of 1D vectors can be sped up by not drawing all data points.  The parameter returned or set by this command indicates the maximum number of points to be used in drawing a vector.  Defaults to 2048.  If set to 0, all points are drawn.

**mode**

:    **nv_win** **mode**  *live*  *record*  *play* 

: Returns the drawing mode.  Not currently supported
  

**move**

:    **nv_win** **move** 

:    Same as Tk canvas "move" subcommand

**name**

:    **nv_win** **name** 

:    Returns name of current window.

**ndim**

:    **nv_win** **ndim**  *?-dataset*  *datasetName?* 

:    Return the number of dimensions of the matrix currently displayed in the window.  If more than one dataset is displayed in the window, the number of dimensions of the first dataset will be returned.

**nearest**

:    **nv_win** **nearest** 

:    Unused, use corresponding "nv_peak" command.

**neg**

:    **nv_win** **neg**  *?-dataset*  *datasetName?*  *?0* | *1?* |

:    Return, or set if optional argument is included, whether or not negative contour levels should be drawn.

**negcolor**

:    **nv_win** **negcolor**  *?-dataset*  *datasetName?*  *colorName?* 

:    Returns the color corresponding to the color used for negative contours in the active window. If the optional argument is specified the color for negative contours in the active window is set to colorName. For example, "nv_win negcolor red" sets the color for negative contours in the active window to red.

**negwidth**

:    **nv_win** **negwidth**  *?-dataset*  *datasetName?*  *?width?* 

:    Returns the width of lines used for drawing negative contours in the active window. If the optional argument is specified the width for negative contours in the active window is set to width. For example, "nv_win negwidth 2" sets the width for negative contours in the active window to 2.

**new**

:    **nv_win** **new** 

:    Unused

**newtype**

:    **nv_win** **newtype** 

:    Allows adding a new type of canvas shape to the spectrum.  To do this custom Java code must be written to implement the new type.

**nlvls**

:    **nv_win** **nlvls**  *?-dataset*  *datasetName?*  *nLevels* 

:    Returns the number of contour levels used in the active window. If the optional argument is specified the number of contour levels in the active window is set to nLevels. For example, "nv_win nlvl 5", sets the number of contour levels in active window to 5. 

**object**

:    **nv_win** **object** 

:    Do not use

**open**

:    **nv_win** **open** 

:    Return a list of currently open spectrum windows.

**paste**

:    **nv_win** **paste** 

:    Paste data from the copy buffer into active window and draw contour plot.

**peak_col_off**

:    **nv_win** **peak_col_off**  *colorName* 

:    Returns the name of the color used to draw peak boxes that are not on (or between, if a range of planes is used) the displayed plane. If the optional argument is specified the color is set to that value in the active window.

**peak_col_on**

:    **nv_win** **peak_col_on**  *colorName* 

:    Returns the name of the color used to draw peak boxes that are on (or between, if a range of planes is used) the displayed plane. If the optional argument is specified the value is set in the active window.

**peak_col_type**

:    **nv_win** **peak_col_type**  *arg* 

:    plane, assigned, error, status

If set to the value "plane", peak boxes are colored according to their closeness to the display plane, as determined by the peak_off, peak_col_off, and peak_col_on parameters. If set to the value "assigned", peak boxes are colored according to the peak labels. If any peak dimension has a "?", in the label field the peak boxes is colored as specified by the peak_col_off argument, otherwise it is colored as specified with the peak_col_on.

**peak_dis_type**

:    **nv_win** **peak_dis_type**  *arg* 

:    "peak", "simulated","label", "none"

Returns a number (0-3) corresponding to the manner 
in which peaks from the peak list are displayed in the spectral window. 
If set to 0, peaks are drawn as boxes with widths corresponding to the peak width.
 If the value is 1, peaks are drawn as simulated contours.
If the value is 2, only the peak label is draw.
If the value is 3, the peak is drawn as a single ellipse.
The peak width parameter is then assumed to be the line width.
 The number of contours and their levels are determined by the "nv_win nlvl",
 "nv_win lvl", and "nv_win clm" commands. If the optional argument is specified
 the value is set in the active window. See also the PEAK ATTRIBUTES PANEL.

**peak_lab_type**

:    **nv_win** **peak_lab_type**  *labType* 

:    number label residue atom cluster user comment summary

This parameter determines what type of label is drawn next to each peak box. The choices are as follows:

number
:    The peak number.

label
:    The peak labels (for all peak dimensions).

residue
:    The residue number of the peak (for all peak dimensions that have unique values.

atom
:    The atom names of the peak (for all peak dimensions).

cluster
:    The number of the cluster that the peak is a member of (for all peak dimensions).

user
:    The value of the user field of the peak (for all peak dimensions).

comment
:    The comment assoicated with the peak.

summary
:    A summary of the chemical shift, normalized intensity,  and couplings (appropriate for 1D peaks).

**peak_off**

:    **nv_win** **peak_off**  *nPlanes* 

:    This parameter determines which peaks are displayed on 3 or 4 dimensional spectra. If the plane of a peak is closest to the display plane, it is displayed with the color specified by the peak_col_on parameter. If it is not on the display plane, but is within nPlanes of the display plane it is displayed with the color specified by the peak_col_off paramter. Otherwise it is not displayed. See also the PEAK ATTRIBUTES PANEL.

**peak_types**

:    **nv_win** **peak_types**  *?type1*  *type2*  *...?* 

:    compound minor solvent contaminant impurity chemshiftref quantityref comboref water artifact

**peakattributes**

:    **nv_win** **peakattributes** 

:    Not used in NMRViewJ

**peaklist**

:    **nv_win** **peaklist** 

:    Not used in NMRViewJ

**pick**

:    **nv_win** **pick**  *xVal*  *yVal*  *jiggle"* 

:    Find peak or dataset in window at within jiggle range of position specified with the xVal and yVal.  First, displayed peaks are scanned to find one overlapping the specified position.  If one or more are found the return value is "peak PeakSpecifier"  where "peak" is the literal word peak, and peakSpecifier is a value specifiying the closest peak to the position.  If no peaks are found within the jiggle range, the window is searched for a 1D spectra that is within range.  If one is found the return value is "dataset datasetName"  where "dataset" is the literal word dataset, and datasetName is the name of the dataset closest to to the specified position.

**pix2ppm**

:    **nv_win** **pix2ppm**  *xVal*  *yVal* 

:    Returns, as a Tcl list, the x and y chemical shifts that correspond to the specified pixel positions.  This is useful for converting positions returned from mouse or key bindings to a chemical shift position in the spectrum.

**plot**

:    **nv_win** **plot**  *all?* 

:    Unused in NMRViewJ.  Use the print command instead.

**pos**

:    **nv_win** **pos**  *?-dataset*  *datasetName?*  *?0* | *1?* |

:    Return, or set if optional argument is included, whether or not positive contour levels should be drawn.

**poscolor**

:    **nv_win** **poscolor**  *?-dataset*  *datasetName?*  *colorName?* 

:    Returns the color corresponding to the color used for positive contours in the active window. If the optional argument is specified the color for positive contours in the active window is set to colorName. For example, "nv_win poscolor black" sets the color for positive contours in the active window to black.

**poswidth**

:    **nv_win** **poswidth**  *?-dataset*  *datasetName?*  *?width?* 

:    Returns the width of lines used for drawing negative contours in the active window. If the optional argument is specified the width for negative contours in the active window is set to width. For example, "nv_win negwidth 2" sets the width for negative contours in the active window to 2.

**ppm**

:    **nv_win** **ppm**  *axis*  *?value1*  *value2?* 

:    Returns the plot limits, in units of ppm, for the specified axis.
If the optional value1 and value2 arguments are included, then set
the plot limits to those specified.
For example
:    
nv_win x 3.4 8.2

**ppmmax**

:    **nv_win** **ppmmax**  *axis* 

:    Returns the minimum and maximum plot limits, in units of ppm, for the specified dimension.

**previous**

:    **nv_win** **previous** 

:    Draw previous expansion (up to 8 previous expansions are stored.)

**pt**

:    **nv_win** **pt**  *axis*  *?value1*  *value2* 

:    Returns the plot limits, in units of points, for the specified axis.
If the optional minValue and maxValue arguments are included, then set
the plot limits to those specified.
For example
:    
nv_win pt z 10 11

**raise**

:    **nv_win** **raise** 

:    Same as Tk canvas "raise" subcommand

**refreshcrosshairs**

:    **nv_win** **refreshcrosshairs** 

:    Unused

**region**

:    **nv_win** **region**  *clear*  ** | ** | *get*  ** | ** | *add*  *x1*  *x2*  ** | ** | *adjust*  *x1*  *x2* | *set* | *x1*  *x2*  ** | ** | *display*  *0/1* 

:    Spectra can have colored regions displayed on them.  At present this is only useful for 1D spectra.  This subcommand allows the user to specify the regions to be displayed.
:    
clear: clear all existing regions
:    
get: return a list of all regions currently set
:    
add x1 x2:  Add a region from chemical shift x1 to x2.
:    
adjust x1 x2:  If any existing regions are found that overlap the range specified with x1 and x2, change the limits of the found region to correspond to x1 and x2.
:    

set x1 x2: Remove all existing regions and add a new one from x1 to x2.
:    
display 0|1: Turn on or off the display of regions.
:    
The color of the region can be set with the "nv_win regioncolor" command.

**regioncolor**

:    **nv_win** **regioncolor**  *?regionColor?* 

:    Return, or set, the color to be used when drawing regions on the spectrum.  Use the "nv_win region" command to set the regions to be displayed.

**repfile**

:    **nv_win** **repfile**  *datasetName*  *repFileName* 

:    This command can be used to assign a copy of a dataset to the window.  The datasetName specifies the dataset to be copied, and repFileName specifies the new name to be used when adjusting parameters for the new copy within the window.  An actual copy of the data is not made, the original dataset is the source of all data used for display.  But, the parameters such as contour levels and contour colors can be controlled independently for the original and "replica" dataset.  This command was originaly developed so sets of 1D vectors from a pseudo-2D file could be independently controlled.  Rows in each dataset (or replica) are selected for display with the "nv_win drawlist" command.  A given dataset can be replicated an unlimited number of times within the same spectrum window.

**scale**

:    **nv_win** **scale** 

:    Same as Tk canvas "scale" subcommand

**scale1d**

:    **nv_win** **scale1d**  *scaleValue* 

:    Returns the scale value used for drawing 1D spectra (including slices).  If
the optional argument, scaleValue, is included the command sets the scale
value to that specified.

**search**

:    **nv_win** **search** 

:    Unused

**selectdataset**

:    **nv_win** **selectdataset**  *?-append?*  *?datasetName* 

:    One dimensional datasets can be displayed in a highlighted mode if they are selected.  With no arguments, this command return a list of currently selected datasets.  If datasetName is specified then set that dataset to be selected.  If the "-append" flag is included then any previously selected datasets are left selected, otherwise only the specified dataset will be selected after completion of the command.

**selectpeak**

:    **nv_win** **selectpeak**  *?-append?*  *?peakSpecifier?* 

:    Peaks can be displayed in a highlighted mode if they are selected.  With no arguments, this command return a list of currently selected peaks.  If peakSpecifier is included then set that peak to be selected.  If the "-append" flag is included then any previously selected peaks are left selected, otherwise only the specified peak will be selected after completion of the command.

**shift**

:    **nv_win** **shift**  *xShiftPPM*  *yShiftPPM* 

:    Shift the displayed region of the spectrum by the specified amounts.

**show**

:    **nv_win** **show** 

:    Not used

**showpeaks**

:    **nv_win** **showpeaks** 

:    Unused

**slice**

:    **nv_win** **slice**  *state* | *position* | *offset* | *draw* | *dimName*  *?slice?* 

:    Returns the boolean state of the cursor slices.  If a slice is turned on
then a realtime vector slice is drawn across the spectra in a direction 
specified by the axis.  If the option on|off value is specified then set
the state to the value specified.
For example, to draw slices parallel to the x axis when the cursor is moved
:    
nv_win slice x on

**stop**

:    **nv_win** **stop** 

:    Stop drawing the current spectrum.  Useful if it is taking a long time to draw the spectrum and you want to intterupt the drawing process, perhaps so you adjust parameters.

**svg**

:    **nv_win** **svg** 

:    Unused.  Use "nv_win export" instead.

**thread**

:    **nv_win** **thread**  *0* | *1* |

:    Report or set whether the spectrum should be drawn in its own thread of execution.  Expert use only.

**transformer**

:    **nv_win** **transformer**  *transformerName*  *m0*  *m10*  *m01*  *m11*  *m02*  *m12* 

:    Sets the elements of the specified affine transform used in drawing shapes on the spectrum.  Expert use only.

**type**

:    **nv_win** **type**  *tagOrID* 

:    Return the type of the item given by tagOrId, such as rectangle or text.

**wait**

:    **nv_win** **wait** 

:    This command will not return until drawing in the active window is completed.  Useful in scripts to ensure that drawing is done before some parameter is changed and the spectrum drawn again.

**winpeak**

:    **nv_win** **winpeak**  *?off* | *expand* | *expandfix* | *plane?* |

:    Returns or sets a flag to be used by scripts that can update the spectrum region to display the region surrounding a specified peak.  This command only sets or returns the flag, any useful activity is done via scripts that scan the list of spectrum windows for ones that have the paramter set to something other than "off".

**xdim**

:    **nv_win** **xdim**  *dimNum* 

:    Sets the x display dimension of the active window to dimNum.

**xoffset**

:    **nv_win** **xoffset**  *offsetValue* 

:    Returns the offset value used for drawing 1D spectra parallel to the
x axis (including slices).  The value can range from 0 to 1 and specifies 
the position of the zero value for the spectra.  If
the optional argument, offsetValue, is included the command sets the offset
value to that specified.

**xshear**

:    **nv_win** **xshear**  *?shearValue?* 

:    Returns or sets a shearValue to be used when drawing 2D datasets.  Typically this is used in a stack plot mode so that subsequent rows of the spectra are drawn above and offset to the right relative to the previous row.

**ydim**

:    **nv_win** **ydim**  *dimNum* 

:    Sets the y display dimension of the active window to dimNum.

**yoffset**

:    **nv_win** **yoffset**  *offsetValue* 

:    Returns the offset value used for drawing 1D spectra parallel to the
y axis (including slices).  The value can range from 0 to 1 and specifies 
the position of the zero value for the spectra.  If
the optional argument, offsetValue, is included the command sets the offset
value to that specified.

**z2dim**

:    **nv_win** **z2dim**  *dimNum* 

:    Sets the z2 display dimension of the active window to dimNum.

**zdim**

:    **nv_win** **zdim**  *dimNum* 

:    Sets the z display dimension of the active window to dimNum.

**zoom**

:    **nv_win** **zoom**  *in*  ** | ** | *out*  ** | ** | *f1*  *f2*  *f3*  *f4* 

:    Zooms spectra region in or out.   If the argument is "in"  the window is zoomed in to show a smaller region of the spectrum.  The four directions (two each for x and y axes) are adjusted by 0.25 times the existing spectral width.  If the argument is "out" then the window is zoomed out to show a larger region of the spectrum.  If four numbers are specified then the zooming is done by the factors specified, with negative values zooming in and positive values zooming out.

##nv_xy


Non-linear regression fitting of XY data.

**Sub-commands**

:    nv_xy auxnames

:    nv_xy equations

:    nv_xy fit

:    nv_xy gen

:    nv_xy npar




**auxnames**

:    **nv_xy** **auxnames**  *equationNum* 

:    Return a list of the names of any auxiliary parameters.

**equations**

:    **nv_xy** **equations** 

:    Return a list of the equations available for fitting.

**fit**

:    **nv_xy** **fit**  *-xvec*  *xvec*  *-yvec*  *yvec*  *-xlist*  *xlist*  *-ylist*  *ylist*  *-clvl*  *clvl*  *-nsim*  *nsim*  *-equation*  *equationNum*  *-sdev*  *calc* | *input* | *set* | *sdev*  *-guesses*  *guessList*  *-aux*  *auxList* 

:    Fit the xy data to the specified equation.  Data for the fit can either come from vecmat objects, using the -xvec and -yvec arguments, or from Tcl lists, using the -xlist and -ylist arguments.
:    
nv_xy equations
:    
The result consists of three values for each parameter fit followed by the rmsd of the fitted line from the original data.  The three parameters consist of the best fit value and the maximum and minimum value corresponding to the specified confidence interval.  The range around the best fit is determined by a Monte Carlo simulation using nsim simulations.  The fitting algorithm will calculate estimates of the parameters prior to initiating the non-linear regression.  Alternatively a list of guesses can be provided with the -guesses parameter.
:    
Some equations require auxiliary parameters that are not fit.  These can be set with the -aux parameter.
:    
A*exp(-x*B)+C A*exp(-x*B) A*x*exp(-x*B) A*exp(-((x-B)/C)^2) ((D-A)*x^C)/(x^C+B^C)+A ((C-A)*x)/(x+B)+A A+(C-A)*((Pt+10^x+B)+((Pt+10^x+B)^2-4*Pt*10^x)^1/2))/(2*Pt) A*(exp(-x/B)+exp(-x/C)) A*exp(-x*C)*exp(-i*x*B) -2.0*A*exp(-x/B)+A {Gaussian Line} {Lorentzian Line}
:    
nv_xy fit -xlist "0 1 2 3 4 5 6" -ylist "1.0 0.75 0.5 0.4 0.3 0.22 " -equ 0
:    
1.37262116187 1.20605660985 1.88030125546 0.18544851486 0.116615463057 0.257768247272 -0.389289490936 -0.884688050313 -0.197205749315 0.0432962503491
:    
nv_xy fit -xlist "0 1 2 3 4 5 6" -ylist "1.0 0.75 0.5 0.4 0.3 0.22 " -equ 1
:    
1.01878267765 0.968322133438 1.06462207344 0.33931427053 0.309971711583 0.369542359523 0.0566615868428

**gen**

:    **nv_xy** **gen**  *[param1]*  *[param2]*  *...* 

:    Generate simulated data using the parameters specified with 'param1' 'param2' ...
The simulated data will be returned in the vector specified by the 'yObject'
parameter of the "nv_xy objects" method.  By default this is the vector fit_y.
:    
eval nv_xy gen -xvec $xobj -yvec $fobj -equation $equationNum -guess [list $bestValues] ]

**npar**

:    **nv_xy** **npar**  *equationNum* 

:    Return the number of parameters for the specified equation.

##print


Print windows.





****

:    **print** ****  *?-landscape* | *-portrait* | *-autoselect?* | *?-silent?*  *?-sizetofit?*  *?-margin*  *marginValue?*  *windowName* 

:    Prints the specified window.  Page orientation can be set with the -landscape or -portrait flags.  If -autoselect is used then if the window is wider than it is high then landscape mode will be used, otherwise portrait will be used.  If -silent is specified then no print dialog will be displayed and the file will be printed to the default printer.  If -sizetofit is specified the page size will be based on the dimensions of the printed window.  The margin around the printed area can be set with the marginValue.

##star


Read NMR-STAR (version 2) files.

**Sub-commands**

:    star close

:    star discon

:    star mmcifxyz

:    star next

:    star open

:    star peak

:    star ppm

:    star put

:    star xyz




**close**

:    **star** **close** 

:    Not yet documented

**discon**

:    **star** **discon** 

:    Not yet documented

**mmcifxyz**

:    **star** **mmcifxyz** 

:    Not yet documented

**next**

:    **star** **next** 

:    Not yet documented

**open**

:    **star** **open** 

:    Not yet documented

**peak**

:    **star** **peak** 

:    Not yet documented

**ppm**

:    **star** **ppm** 

:    Not yet documented

**put**

:    **star** **put** 

:    Not yet documented

**xyz**

:    **star** **xyz** 

:    Not yet documented

##star3


Read and write NMR-STAR (Version 3) files.

**Sub-commands**

:    star3 clear

:    star3 close

:    star3 get

:    star3 loop

:    star3 open

:    star3 process

:    star3 saveframe

:    star3 scan

:    star3 write




**clear**

:    **star3** **clear** 

:    Discard current STAR file.  This doesn't delete any molecules, peak lists or other data structures.

**close**

:    **star3** **close** 

:    Close the datafile that the STAR file was read from.

**get**

:    **star3** **get**  *starSpecifier* 

:    Get the value corresponding to the specified tag.
:    
star3 get bmr6960.save_entry_information._Entry.ID
:    
6960

**loop**

:    **star3** **loop**  *count*  *starSelector*  ** | ** | *tags*  *starSelector*  ** | ** | *values*  *starSelector*  ** | ** | *row*  *starSelector* 

:    count starName.saveframe.category: Return the number of rows in the loop.
:    
tags starName.saveframe.category: Return a list of the tags in the loop.
:    
values starName.saveframe.category.tag: Return all the values (one column) for the specified tag.
:    
row starName.saveframe.category.rowNum: Return all the values in the specified row of the loop.
:    
star3 loop count bmr6960.save_entry_information._Entry_author
:    
8
:    
star3 loop tags bmr6960.save_entry_information._Entry_author
:    
Ordinal Given_name Family_name First_initial Middle_initials Family_title Entry_ID
:    
star3 loop values bmr6960.save_entry_information._Entry_author.Family_name
:    
Sachchidanand Resnick-Silverman Yan Mujtaba Liu Zeng Manfredi Zhou
:    
star3 loop row bmr6960.save_entry_information._Entry_author.2
:    
3 S. Yan . . . 6960

**open**

:    **star3** **open**  *fileName* 

:    Opens the specified NMR-STAR 3 file.  This only opens the actual file, but doesn't read (see "star3 scan") or process (see "star3 process") the data.

**process**

:    **star3** **process** 

:    Processes the imported STAR 3 file by looking for specific save frames that NMRViewJ handles (at present these are the ones for datasets, molecules, peak lists, resonance, chemical shifts, and RunAbout parameters).

**saveframe**

:    **star3** **saveframe**  *list*  ** | ** | *categories*  *starSelector*  ** | ** | *tags*  *starSelector* 

:    Retreive information about the save frames in the loaded STAR file.

:    list: Return a list of saveframes in the file.
:    
categories:Return a list of categories within the save frame. Each element of the list is a two element list where the first element is the name of the category and the second is either 0 or 1, with a value of 1 idicating that the category represents a loop within the saveframe.
:    
tags: Return a list of tags within the specified category.
:    


star3 open /Users/brucejohnson/data/bmrb3/bmr6960.str
:    
star3 scan
:    
star3 saveframe list
:    
save_entry_information entry_information save_entry_citation citations save_system assembly save_entity entity save_natural_source natural_source save_experimental_source experimental_source save_sample_1 sample save_sample_2 sample save_sample_cond_1 sample_conditions save_NMRPipe software save_NMRVIEW software save_X-PLOR software save_ARIA software save_NMR_spectrometer NMR_spectrometer save_spectrometer_list NMR_spectrometer_list save_experiment_list experiment_list save_NMR_applied_experiment NMR_spectrometer_expt save_NMR_spec_expt__0_1 NMR_spectrometer_expt save_NMR_spec_expt__0_2 NMR_spectrometer_expt save_NMR_spec_expt__0_3 NMR_spectrometer_expt save_NMR_spec_expt__0_4 NMR_spectrometer_expt save_NMR_spec_expt__0_5 NMR_spectrometer_expt save_NMR_spec_expt__0_6 NMR_spectrometer_expt save_chemical_shift_reference chem_shift_reference save_chemical_shift_set_1 assigned_chemical_shifts
:    
star3 saveframe categories bmr6960.save_entry_information
:    
:    
star3 saveframe tags bmr6960.save_entry_information._Entry
:    
Sf_framecode ID Title Version_type Submission_date Accession_date Last_release_date Original_release_date Origination NMR_STAR_version Original_NMR_STAR_version Experimental_method Experimental_method_subtype


**scan**

:    **star3** **scan** 

:    Reads the previously opened file into memory.

**write**

:    **star3** **write**  *fileChannel* 

:    Writes the current STAR file data to the specified file channel.  The file channel must have been opened with Tcl commands.
:    

    set f1 [open test.str w]
    star3 write $f1
    close $f1


##vecmat


Math and statistics with vectors and matrices. 

**Sub-commands**

:    vecmat add

:    vecmat addmul

:    vecmat apsl

:    vecmat autophase

:    vecmat axscale

:    vecmat base64todouble

:    vecmat base64tofloat

:    vecmat bcmed

:    vecmat bcpoly

:    vecmat bcsmooth

:    vecmat bcwhit

:    vecmat bucket

:    vecmat bytes

:    vecmat cnew

:    vecmat comb

:    vecmat complex

:    vecmat compress

:    vecmat convert

:    vecmat copy

:    vecmat copyrange

:    vecmat cow

:    vecmat cshift

:    vecmat cwtd

:    vecmat cwtidbaseline

:    vecmat dalist

:    vecmat dc

:    vecmat dcfid

:    vecmat decompress

:    vecmat deconv

:    vecmat delete

:    vecmat dm1d

:    vecmat dwell

:    vecmat esmooth

:    vecmat exchange

:    vecmat expd

:    vecmat extend

:    vecmat fconvert

:    vecmat fdss

:    vecmat fp

:    vecmat freqdomain

:    vecmat fromasdf

:    vecmat ft

:    vecmat genbase

:    vecmat gensignal

:    vecmat genspec

:    vecmat get

:    vecmat getbytes

:    vecmat gf

:    vecmat gm

:    vecmat gmb

:    vecmat hft

:    vecmat hsvd

:    vecmat idbase

:    vecmat idintegrals

:    vecmat ift

:    vecmat imag

:    vecmat input

:    vecmat integrate

:    vecmat list

:    vecmat list2vec

:    vecmat mag

:    vecmat max

:    vecmat min

:    vecmat negatepairs

:    vecmat new

:    vecmat object

:    vecmat ones

:    vecmat output

:    vecmat phase

:    vecmat poly

:    vecmat power

:    vecmat psmooth

:    vecmat random

:    vecmat range

:    vecmat real

:    vecmat ref

:    vecmat resize

:    vecmat reverse

:    vecmat rft

:    vecmat sb

:    vecmat scale

:    vecmat sdev

:    vecmat set

:    vecmat setcolumn

:    vecmat setrow

:    vecmat shift

:    vecmat size

:    vecmat sort

:    vecmat split

:    vecmat status

:    vecmat svd

:    vecmat sw

:    vecmat swap

:    vecmat tdpoly

:    vecmat trap

:    vecmat tri

:    vecmat trim

:    vecmat zero

:    vecmat zf

:    vecmat zv_mlt




**add**

:    **vecmat** **add**  *vecName*  *value* 

:    Add the specified value to each element of the specified vector.  If the vector is complex the value is added only to the real part of each element.

**addmul**

:    **vecmat** **addmul**  *vecName1*  *vecName2*  *?scale?* 

:    Add the two vectors element by element and store the result in vector vecName1.  If the scale parameter is present each element of vector vecName2 is multiplied by the scale value before being added to the corresponding element of vector vecName1.  The vectors must be of the same length and same type (real or complex).  The command returns vecName1 as a result.

**apsl**

:    **vecmat** **apsl**  *center*  *start*  *width*  *asym* 

:    Calculate a zero order phase value that will optimize the symmetry of a spectral peak.  The center of the peak is specified by the center argument, the first data points to compare the symmetry of are the points at center-start and center+start.  The last points to be compared are at center-start-width and center+start+width.  The asym value should normally be set to 0.

**autophase**

:    **vecmat** **autophase**  *vecName*  *?-mode*  *flat* | *max?* | *?-first*  *firstPoint?*  *?-last*  *lastPoint?*  *?-winsize*  *winSize?* 

:    Calculate a zero order phase parameter.  If mode is "flat" (the default), then a systematic search is done for a phase parameter that maximizes the flatness of the spectral baseline.  The winsize parameter (default = 60) is used in identifying baseline regions and is only used in "flat" mode.  If mode is "max", a search is done to maximize the integral of the spectrum.  This method is only appropriate for spectra that do not have significant negative components in the well phased spectrum.  The first and last parameter values are used only in the "max" mode and are used to specify the region over which the integral is calculated.  If they are not specified the entire spectrum is used.

**axscale**

:    **vecmat** **axscale**  *vecName*  *?value?* 

:    Used as a generic equivalent of the spectrum frequency.  Used when calculating referencing and adjusting referencing during some vector manipulations.  When a vector is loaded from an NMR dataset this value is set to the spectometer frequency for the dimension that the vector is parallel to.

**base64todouble**

:    **vecmat** **base64todouble**  *vecName*  *values* 

:    Convert a string of base 64 encoded data points that represent double precision floating point values into values in the vector.  The vector will be resized to exactly accomadate the number of values in the string.

**base64tofloat**

:    **vecmat** **base64tofloat**  *vecName*  *values* 

:    Convert a string of base 64 encoded data points that represent double precision floating point values into values in the vector.  The vector will be resized to exactly accomadate the number of values in the string.

**bcmed**

:    **vecmat** **bcmed**  *vecName*  *frac* 

:    Correct the baseline of the specified vector using the median method.  The window size used in the analysis is set by multiplying the frac parameter times the number of extrema in the vector.

**bcpoly**

:    **vecmat** **bcpoly**  *vecName*  *?-winsize*  *winSize?*  *?-ratio*  *ratioValue?*  *?-order*  *orderValue?* 

:    Correct the baseline of the specified vector using a polynomial fit to the values of the baseline data points of the vector.  The fitted polynomial is then subtacted from the original vector to produce the corrected vector.  Baseline regions are identified as regions with signals that exceed the standard deviation of the noise of the vector by more than a ratio of ratioValue (default = 10.0).  The standard deviation of the spectrum is estimated by dividing the vector into regions of size winSize, calculating the standard deviation in each range, and then estimating the overall noise standard deviation from a sorted list of the standard deviations of each region.

**bcsmooth**

:    **vecmat** **bcsmooth**  *vecName*  *smoothSize*  *winSize*  *ratio* 

:    Correct the baseline of the specified vector by calculating a smoothed baseline.  The smoothed baseline is then subtacted from the original vector to produce the corrected vector.  Baseline regions are identified as regions with signals that exceed the standard deviation of the noise of the vector by more than a ratio of ratioValue (default = 10.0).  The standard deviation of the spectrum is estimated by dividing the vector into regions of size winSize, calculating the standard deviation in each range, and then estimating the overall noise standard deviation from a sorted list of the standard deviations of each region.  The smoothed baseline is calculated within each baseline region by averaging adjacent datapoints over a region of size smoothSize.  Smoothed baseline points in non-baseline regions are calculated by linear interpolation between the adjacent smoothed baseline points.

**bcwhit**

:    **vecmat** **bcwhit**  *vecName*  *?-winsize*  *winSize?*  *?-lamda*  *lambda?*  *?-order*  *order?*  *?-minsize*  *minSize?*  *?-baseline*  *0* | *1?* |

:    Correct the baseline of the specified vector using a calculating a smoothed baseline using the Whitaker "perfect smoothing" algorithm.  The smoothed baseline is then subtacted from the original vector to produce the corrected vector.  Baseline regions are first identified as regions of low intensity after calculating the derivative of the spectrum using a continuous wavelet transform.

**bucket**

:    **vecmat** **bucket**  *vectorName*  *nBuckets* 

:    The vector is bucketed by adding adjacent data points.  The vector size after this operation will be equal to the specified number of buckets. Thre original vector size must be a multiple of the number of buckets.  Each resulting data point will represent the sum of winSize data points where winSize is equal to size/nBuckets.

**bytes**

:    **vecmat** **bytes**  *byteValues* 

:    Returns a handle to a Java object corresponding to an array of bytes (byte[]) containing the values in the supplied argument.

**cnew**

:    **vecmat** **cnew**  *length*  *vecName* 

:    Creates a complex vector with the name 'vecName' and the size 'length'.  The vector will be initialized with all real and imaginary components set to zero.

**comb**

:    **vecmat** **comb** 

:    Not yet documented

**complex**

:    **vecmat** **complex**  *vecName* 

:    Converts a real vector into a complex vector of the same number of components.  The real part of each value is set to the corresponding value in the original vector.  The imaginary part of each value is set to zero.  If the original vector is already complex no action is taken and no errors are reported.

**compress**

:    **vecmat** **compress**  *vecName* 

:    Experimental vector compression.  Not yet documented

**convert**

:    **vecmat** **convert**  *?-swap* | *-noswap?* | *?-float* | *-int?* | *vecName*  *data* 

:    Imports a byte array stored in data into the specified vector.  If -swap is specified the byte order of the data will be reversed as it is imported.  If -float is specified the data bytes are converted as if they represent 4 byte floating point numbers, otherwise they are converted as 4 byte integers.  Note: the actual data stored in vectors is always 8 byte double precision floating point.  The type of the vector refered to by vecName determines whether the data is converted as real or complex values.  The vector will be resized to exactly accomadate the number of data values in data.
:    
This command is often used to convert data read with the Tcl "read" command into a vector.

**copy**

:    **vecmat** **copy**  *vecName1*  *vecName2* 

:    Copy vector vecName1 into vector vecName2.  If the destination vector doesn't exist it will be created.  It's type (real/complex) and size will be adjusted if necessary to conform to that of the source vector.

**copyrange**

:    **vecmat** **copyrange**  *vecName1*  *vecName2*  *srcPos*  *destPos*  *length* 

:    Copy the specified range of values of vector vecName1 into vector vecName2.  If the destination vector doesn't exist it will be created.  It's type (real/complex) and size will be adjusted if necessary to conform to that of the source vector.

**cow**

:    **vecmat** **cow** 

:    Not yet implemented.

**cshift**

:    **vecmat** **cshift**  *vecName*  *shiftAmount* 

:    Circular shift of the data points in the specified vector by the specified amount.

**cwtd**

:    **vecmat** **cwtd**  *vecName*  *winSize* 

:    Calculate the first derivative of the vector using a continuous wavelet transform.

**cwtidbaseline**

:    **vecmat** **cwtidbaseline**  *vecName*  *?-winsize*  *winsize?*  *?-minsize*  *minSize?* 

:    Indentify baseline regions by using a continous wavelet transform calculation of the first derivative of the vector.  After the derivative is calculated the data values are replaced by their power (r*r+i*i).  An estimate of the noise level of the vector is then calculated.  Baseline regions are set as areas where intensities are never higher than a certain multiple of the noise level.  The result is a list of points demarcating the start and end of baseline regions.

**dalist**

:    **vecmat** **dalist**  *vecName* 

:    Many mathematical and statistical calculations can be done using access to the built Colt library.  Some of these calculations require the data in the format of a Java object of the DoubleArrayList class.  This command will return a double array list containing the data values in the vector.  If the vector is complex an ObjectArrayList is returned containing complex value objects.

**dc**

:    **vecmat** **dc**  *vecMat*  *?-fraction*  *fraction?* 

:    Subtracts from each data point the average value of two regions, one at the begining and one at the end of the vector.  The optional fraction argument (default = 0.05) specifies the fractional size of the vector used for each of the two regions.  The vector must be real (not complex).

**dcfid**

:    **vecmat** **dcfid**  *vecMat*  *fraction*  *fraction* 

:    Subtracts from each data point the average value of the set of data points at the end of the vector.  The  fraction argument specifies the fractional size of the vector used for the region.  The vector must be complex (not real).

**decompress**

:    **vecmat** **decompress**  *vecName* 

:    Experimental vector decompression.  Not yet documented

**deconv**

:    **vecmat** **deconv** 

:    Not yet documented


**delete**

:    **vecmat** **delete**  *vecName1*  *vecName2*  *...* 

:    Delete the specified vectors.


**dm1d**

:    **vecmat** **dm1d**  *vecName*  *dm1D* 

:    Many mathematical and statistical calculations can be done using access to the built Colt library.  Some of these calculations require the data in the format of a Java object of the DoubleMatrix1D class.  This command will such an object containing the data values in the vector. This only works for vectors of type real.  If the optional dm1D object is provided data in the provided object will be put into the vector.  The vector will be resized to conform to the size of the DoubleMatrix1D object.


**dwell**

:    **vecmat** **dwell**  *vecName*  *?dwell?* 

:    Vectors have a dwell time associated with them.  This corresponds to the time between data points in time domain mode, and 1/sweepwidth in frequency domain mode.  The dwell time is updated when vectors are read from datasets, and is used for adjusting the referencing of the data and calculating time-dependent apodization functions.


**esmooth**

:    **vecmat** **esmooth** 

:    Not yet documented


**exchange**

:    **vecmat** **exchange**  *vecName* 

:    Interchange the real and imaginary components of each data point of a complex valued vector.  Throws an error if the dataset is not complex.


**expd**

:    **vecmat** **expd**  *vecName*  *?-lb*  *lb?*  *?-firstpoint*  *firstPoint?* 

:    Multiply vector by an exponentially decaying apodization function.  The decay rate is specified as a "line-broadening" parameter in Hz.


**extend**

:    **vecmat** **extend**  *vecMat*  *?-fitstart*  *fitStart?*  *?-fitend*  *fitEnd?*  *?-ncoef*  *nCoef?*  *?-predictstart*  *predictStart?*  *?-predictend*  *predictEnd?*  *?-threshold*  *threshold?*  *?-mode*  *mode?* 

:    Performs linear prediction to extend the data at either the beginning or end of the original data.  Linear prediction is performed by using the SVD (Singluar Value Decomposition) algorithm.  


**fconvert**

:    **vecmat** **fconvert**  *vecName*  *data* 

:    Equivalent to "vecmat convert -noswap -float vecName data"


**fdss**

:    **vecmat** **fdss**  *vecMat*  *-center*  *center*  *-start*  *start*  *-end*  *end* 

:    Perform a frequency domain solvent suppression on the specified vector.  This is done phasing the spectrum to optimally symmetrize the baseline around the solvent peak, converting the data from complex to real, zeroing the solvent region, converting the data back to complex with a hilbert transform, and then restoring the original phase.  The parameters used are the same as described in the "vecmat apsl" command.


**fp**

:    **vecmat** **fp**  *vecName*  *?-fp*  *fpValue?* 

:    Multiply the first piont of the vector by the specified fpValue (default = 0.5).


**freqdomain**

:    **vecmat** **freqdomain**  *vecMat*  *0*  *1?* 

:    Return, or set if the optional argument is included, the state of the frequency domain flag.  A value of 0 indicates the data is in the "time domain" and a value of 1 indicates that the data is in the "frequency domain".  Changing this value does not modify the data in any way, but will effect automated adjustment of the referencing that may happen after other data manipulations.


**fromasdf**

:    **vecmat** **fromasdf**  *vecName*  *data* 

:    Import data stored in the data argument into the specified vector.  The data must be values in the ASDF format.


**ft**

:    **vecmat** **ft**  *vecName* 

:    Execute a Fast Fourier Transform on the data.  An error will be thrown if the data is not complex.  If the data size is not equal to a power of 2 it will be resized to the next higher size that is a power of 2.


**genbase**

:    **vecmat** **genbase**  *vecName*  *order*  *winSize*  *bcVec* 

:    Perform the same operation as that done by "vecmat bcpoly", but do not modify the input vector.  Instead the calculated baseline is stored in the vector named with the bcVec argument.  The bcVec vector must already exist.


**gensignal**

:    **vecmat** **gensignal**  *vecName*  *?-f*  *freq?*  *?-d*  *decay?*  *?-p*  *phase?*  *?-a*  *amplitude?* 

:    Add a sinusoidal signal with the specified parameters to the vector.  The vector must exist and be complex.  The new signal is added to any data values already present.


**genspec**

:    **vecmat** **genspec**  *vecName*  *parameterVec* 

:    Add Lorentzian signals to the vector.  The vector must exist and be real.  Parameters for the signal are stored in the vector parameterVec in the order amplitude, phase, frequency, decay rate.


**get**

:    **vecmat** **get**  *vecMat*  *index* 

:    Returns the data value stored at position index (counts from 0).  If the vector is complex the real and imaginary values will be returned as a list of two values.


**getbytes**

:    **vecmat** **getbytes**  *vecName* 

:    Return a handle to an object containing an array of bytes corresponding to the data in the vector.


**gf**

:    **vecmat** **gf**  *vecName*  *-gf*  *gf*  *-gfs*  *gfs*  *-firstpoint*  *firstPoint* 

:    Apply a gaussian apodization.  Vector must have an appropriate dwell time set.
:    
    for (int i = 0; i < size; i++) {
        double t = i * dwellTime;
        double x = ((t - gfs) / gf);
        apodVec[i] = Math.exp(-(x * x));

**gm**

:    **vecmat** **gm**  *-g1*  *g1*  *-g2*  *g2*  *-g3*  *g3*  *-firstpoint*  *firstPoint* 

:    Apply a gaussian multiplication to vector.
:    

    double e = Math.PI * g1 * dwellTime;
    double ga = 0.6 * Math.PI * g2 * dwellTime;
    double gb = ga * g3 * (size - 1);
    
    for (int i = 0; i < size; i++) {
        double g = gb - (ga * i);
        apodVec[i] = Math.exp((e * i) - (g * g));
    }

**gmb**

:    **vecmat** **gmb**  *vecName*  *?-gb*  *gb?*  *?-lb*  *lb?*  *?-firstpoint*  *firstPoint?* 

:    Gaussian multiplication
:    

    double e = Math.PI * g1 * dwellTime;
    double ga = 0.6 * Math.PI * g2 * dwellTime;
    double gb = ga * g3 * (size - 1);
    
    for (int i = 0; i < size; i++) {
        double g = gb - (ga * i);
        apodVec[i] = Math.exp((e * i) - (g * g));
    }

**hft**

:    **vecmat** **hft**  *vecName* 

:    Hilbert transform of the specified vector.  Vector must be real or an error will be thrown.


**hsvd**

:    **vecmat** **hsvd** 

:    Not yet documented


**idbase**

:    **vecmat** **idbase**  *vecName*  *winSize*  *?ratio?* 

:    Returns a list of data point positions that mark the beginning and end of baseline regions.


**idintegrals**

:    **vecmat** **idintegrals**  *vecName*  *winSize*  *?ratio*  *regionWidth*  *joinWidth*  *extendSize*  *minThreshold?* 

:    Returns a list of data point positions that mark the beginning and end of integral regions.


**ift**

:    **vecmat** **ift**  *vecName* 

:    Inverse Fourier Transform


**imag**

:    **vecmat** **imag**  *vecName* 

:    Converts a complex vector to a real vector with values that correspond to the imaginary components of the original vector.  If the vector is already real it is unchanged and no error is thrown.  Returns the name of the input vector.


**input**

:    **vecmat** **input**  *vecName*  *fileName*  *?columnNum?* 

:    Reads values from a text file of numbers.  If columnNum is specified and the data is arranged as columns values will be taken from the specified column (counting from 0).  Columns are formed by splitting each row on any white space (space or tab characters).  If the specified vector is complex then each row must have at least two columns and the real value will be taken from the first (or columnNum) column and the imaginary from the next value on the row.


**integrate**

:    **vecmat** **integrate**  *vecName*  *?firstIndex*  *lastIndex?* 

:    Replace the data points in the vector with the cumulative sum of data points over the specified range.  If the optional parameters are not included the entire vector is integrated.


**list**

:    **vecmat** **list** 

:    Return a list of existing vector names.


**list2vec**

:    **vecmat** **list2vec**  *vecName*  *list* 

:    The specified vector is resized to the length of the specified Tcl list and then the values in the list are stored in order into the vector.  Values in the list must be parsable as floating point numbers or an error will be thrown.  If the vector is complex then real and imaginary values will be taken from alternate values in the list.


**mag**

:    **vecmat** **mag**  *vecName* 

:    If the specified vector is complex then replace each value with the magnitude "sqrt(r*r+i*i)" of each existing complex value.  The resultant vector will be real.  If the specified vector is already real no action will be taken and no error will be thrown.


**max**

:    **vecmat** **max**  *vecName*  *?firstPoint*  *lastPoint?* 

:    Locate the maximum value in the vector.  Return, as the result, a two element list where the first value is the maximum value and the second value is the index at which it occurred.  If the vector is complex the maximum located is the value with largest magnitude.  If the optional arguments are included then the search for a maximum is done only in the specified range.


**min**

:    **vecmat** **min**  *vecName*  *?firstPoint*  *lastPoint?* 

:    Locate the minimum value in the vector.  Return, as the result, a two element list where the first value is the minimum value and the second value is the index at which it occurred.  If the vector is complex the minimum located is the value with smallest magnitude.  If the optional arguments are included then the search for a minimum is done only in the specified range.


**negatepairs**

:    **vecmat** **negatepairs**  *vecName* 

:    Set every other pair of data values to the negative of the current value.


**new**

:    **vecmat** **new**  *size*  *vecName* 

:    Create a new vector with name vecName and the specified size.


**object**

:    **vecmat** **object**  *vecName* 

:    Returns a handle to the underlying vector object.


**ones**

:    **vecmat** **ones**  *vecName* 

:    Sets all values in the vector to 1.0 if the vector is real, and 1.0+i0.0 if the vector is complex.


**output**

:    **vecmat** **output**  *vecName*  *fileName?* 

:    Output the vector values to either standard output (if there is no fileName argument) or to the named file.


**phase**

:    **vecmat** **phase**  *vecName*  *p0*  *p1* 

:    Phase correct the vector using the provided zero order (p0) and first order (p1) phase values.


**poly**

:    **vecmat** **poly**  *xVector*  *yVector*  *order*  *coefVector* 

:    Fit a polynomial equation of the specified order to the x and y values taken from xVector and yVector.  The polynomial coefficients are stored in the coefVector.  The command returns as a result the rms deviation between the fitted polynomial and the original data.


**power**

:    **vecmat** **power**  *vecName* 

:    If the specified vector is complex then replace each value with the power "(r*r+i*i)" of each existing complex value.  The resultant vector will be real.  If the specified vector is already real no action will be taken and no error will be thrown.


**psmooth**

:    **vecmat** **psmooth**  *vecName*  *?-lambda*  *lambda?* 

:    Smooth the values in the vector using the Whitaker perfect smoother algorithm.


**random**

:    **vecmat** **random**  *vecName* 

:    Set values to the random numbers generated with the Java Math.random() method.


**range**

:    **vecmat** **range**  *vecName*  *first*  *last*  *value* 

:    Sets data points in the range of the specified vector starting at point first to point last to value.


**real**

:    **vecmat** **real**  *vecName* 

:    Converts a complex vector to a real vector with values that correspond to the real components of the original vector.  If the vector is already real it is unchanged and no error is thrown.  Returns the name of the input vector.


**ref**

:    **vecmat** **ref** 

:    Not yet documented


**resize**

:    **vecmat** **resize**  *vecmat*  *newSize* 

:    Resize the vector to the specified size (which can be either larger or smaller than existing size).  If the vector doesn't already exist it will be created.


**reverse**

:    **vecmat** **reverse**  *vecName* 

:    Reverse the vector.


**rft**

:    **vecmat** **rft**  *vecName* 

:    Apply a Fast Fourier Transform optimized for real data.


**sb**

:    **vecmat** **sb**  *vecName*  *?-offset*  *offset?*  *?-end*  *end?*  *?-power*  *power?*  *?-size*  *size?*  *?-c*  *firstPoint?* 

:    Multiply the specified vector by a "sine bell" apodization window with the specified parameters.


**scale**

:    **vecmat** **scale**  *vecMat*  *scaleValue* 

:    Multiply each element of the vector by the specified scaleValue.


**sdev**

:    **vecmat** **sdev**  *vecName*  *winSize*  *?nWindows?* 

:    Estimates the standard deviation of values in noise regions of the spectrum.  This is done by first dividing the vector into regions of size winSize.  Then the standard deviation of each region is calculated.  The region standard deviations are sorted and the average of the standard deviation is taken over the nWindows regions with smallest standard deviations.


**set**

:    **vecmat** **set**  *vecName*  *index*  *realValue*  *?imagValue?* 

:    Sets the value at position index in the specified vector.  If the vector is of type real then only one value (realValue) should be provided.  If the vector is of type complex then both a real and imaginary value can be provided.  If the imaginary value is not provided it is set to 0.0.


**setcolumn**

:    **vecmat** **setcolumn** 

:    Not yet documented


**setrow**

:    **vecmat** **setrow** 

:    Not yet documented


**shift**

:    **vecmat** **shift**  *vecName*  *shiftAmount* 

:    Shift each data point right or left by the specified number of data points.  Positive shiftAmounts shift points to the right and negative to the left.


**size**

:    **vecmat** **size**  *vectorName* 

:    Returns the size of the specified vector.


**sort**

:    **vecmat** **sort** 

:    Not yet documented (does not sort the vector).


**split**

:    **vecmat** **split**  *vecName*  *realVecName*  *imagVecName* 

:    Puts the real values of complex array vecName into the real vector realVecName and the imaginar values of vecName into imagVecName.  If realVecName or imagVecName don't exist they will be created.


**status**

:    **vecmat** **status**  *vecName* 

:    Return status information about the vector.  Three values are returned:
r/c indicating real/complex, the size of the vector, and the capacity of the vector.  The capacity is the size the vector can grow to without allocating additional memory.


**svd**

:    **vecmat** **svd** 

:    Not yet documented


**sw**

:    **vecmat** **sw**  *vecName*  *sw* 

:    Vectors have a dwell time associated with them.  This corresponds to the time between data points in time domain mode, and 1/sweepwidth in frequency domain mode.  The dwell time is updated when vectors are read from datasets, and is used for adjusting the referencing of the data and calculating time-dependent apodization functions.  This parameter allows setting or getting the dwell via its inverse, the sweep width.


**swap**

:    **vecmat** **swap**  *vecName* 

:    Swaps the byte order in vector.  Doesn't just change a flag, but actually reverses the order of bytes in each data value.


**tdpoly**

:    **vecmat** **tdpoly**  *vecName*  *?-order*  *order?*  *?-start*  *start?*  *?-winsize*  *winsize?* 

:    Fits a polynomial equation to the vector and then subtracts the calculated polynomial from the original data.  Useful for solvent suppression.


**trap**

:    **vecmat** **trap**  *vecMat*  *?-pt1*  *pt1?*  *?-pt2*  *pt2?* 

:    Multiply the vector by a trapazoidally shaped apodization function.


**tri**

:    **vecmat** **tri**  *vecMat*  *?-pt1*  *pt1?*  *?-lheight*  *lHeight2?*  *?-rheight*  *rHeight?* 

:    Multiply the vector by a triangularly shaped apodization function.


**trim**

:    **vecmat** **trim**  *vecMat*  *?-left* | *-middle* | *-right?* | *?-pt1*  *pt1?*  *?-newsize*  *newSize?* 

:    Trim the vector to a new size.  If the -left, -middle,  or -right arguments are specified the new vector size will be half the original size and the vector will contain the data points from the indicated region.  If the -pt1 and -newsize arguments are used, the vector will be of newSize size and contain the original points starting at pt1.


**zero**

:    **vecmat** **zero**  *vecName* 

:    Sets all values in the vector to 0.0 if the vector is real, and 0.0+i0.0 if the vector is complex.


**zf**

:    **vecmat** **zf**  *vecMat*  *-factor*  *factor* 

:    Extend the vector with zeros up to a size that is a power of 2.  With a factor of 0 the vector is extended to the first size that is a power of 2.  With each additional increment of factor the final size is twice that with the previous factor.


**zv_mlt**

:    **vecmat** **zv_mlt** 

:    Not yet documented


##vnmr


Load and VNMR parameter files.

**Sub-commands**

:    vnmr exists

:    vnmr get

:    vnmr load

:    vnmr remove




**exists**

:    **vnmr** **exists**  *handleName*  *parameterName* 

:    Returns 0 or 1 indicating whetherspecified parameter exists in the parameter set specified with handleName.
:    
vnmr exists vpar4 sw

:    1


**get**

:    **vnmr** **get**  *handleName*  *parameterName* 

:    Get the value of the specified parameter from the parameter set specified with handleName.
:    
vnmr get vpar4 sw

:    7509.62


**load**

:    **vnmr** **load**  *procParFileData* 

:    Reads in the specified VNMR procpar file data.  Returns a handle that can be used to refer to these parameters.  The data must have been previously read and stored in to a Tcl variable.  For exampe:
:    

    set f1 [open /Users/brucejohnson/data/proton.fid/procpar]
    set d [read $f1]
    close $f1
    vnmr load $d

By working this way data can be loaded not only from normal files, but other sources such as network sockets.


**remove**

:    **vnmr** **remove**  *handleName* 

:    Remove the specified parameter set from memory.


