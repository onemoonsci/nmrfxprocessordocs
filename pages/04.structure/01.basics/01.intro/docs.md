---
title:  Basic Tutorial
taxonomy:
    category: docs
---

# NMRFx Structure

Documentation applies to versions 11.1.9 and later.

NMRFx Structure can be used to generate and analyze macromolecular structures and predict chemical shifts.  It can be run in two different ways.  First, if the command is invoked with one of several subcommands (batch, gen, predict, score, summary, super, or train) a predefined mode will be executed.  Alternatively, one can simply give as an argument a Python (actually [Jython](http://jython.org)) script which will be executed.  The script has access to standard Python functions (including the standard Python library) and to specific commands provided by the NMRFx Structure program's Java code. The predifined subcommands are listed below along with documentation for usage and an example for demonstration.

    usage: nmrfxs batch|gen|predict|score|summary|super|train|script.py

[gen](#genlink)
:  Generate a structure consistent with specified topology and restraints

[batch](#batchlink)
:  Submit multiple invocations of the [gen](#genlink) command to generate a family of structures

[predict](#predictlink)
:  Predict chemical shifts of proteins, RNA and small organic molecules

[score](#scorelink)
:  Analyze structure files (PDB) for consistency with restraints

[summary](#summarylink)
:  Summarize violations in the energy reports from a structure calculation

[super](#superlink)
:   Superimpose structures and report RMS deviations.

[train](#trainlink)
:   Train chemical shift prediction algorithm.


## Subcommands

### <a id="genlink">gen</a>

```
nmrfxs gen [ -s gen|all|refine ] [ -s seed ] [ -d directory ] [ -r report ] [ projectFile ] [ script.py ]
```

Generate a single structure using data specified in a project file and initializing the random number generator with a specified seed.  This is useful for testing out the project file before generating a whole family of structures with the batch command.  An *output* directory will be created if not present.  After successful execution, the generated PDB and violation files will be written to that directory.  The output files will have the seed number appended to them (i.e. temp0.pdb, temp0.txt, etc.). By default, the *output* directory gets placed in the current directory, however, the relative path to a different directory can be specified using the directory option. When debugging a structure generated, it may be useful to view the energy violations for all the constraints specified in the project file. To do this, specify the report option.  This will output constraint violations at prepartion stage into a file named energyDump$seed_prep.txt within the *output* directory. Lastly, define torsional angle molecular dynamic procedures in an executable script to replace the builtin annealing protocol. If a python script is specified as the last argument of the command, the script will be executed. The script can alternatively be placed inside the project file replacing the annealing data block.


Generating a structure requires specifying the molecular information, restraints and parameters for the rotational dynamics.  This can be done by specifying a YAML file and/or a NEF file.
[YAML](https://en.wikipedia.org/wiki/YAML) files are human readable data files that hava a relatively simple structure without a lot of "fluff".  Project yaml files are described [below](#yamllink).

The protocol used for structure calculation proceeds through a seris of [**stages**](#stagelink).  These stages involve preparation, high temperature dynamics, simulated annealing and low temperature dynamics.  The stages are predefined in code and have specific values for [Parameters](#parameterlink) and [Forces](#forcelink).  The user can adjust any of the parameters in a stage or introduce new stages by adding sections to the [yaml](#yamllink) file.

Structure calculations are typically constrained by experimental data.  NMRFx supports a variety of formats for importing these restraints.  See the [Data](#datalink) Section for more details.

Running a structure calculation will generate output as the structure calculation proceeds.  This output will be written to standard output and an example is shown [here](#genoutputlink).

__Examples__: 


    nmrfxs gen -s 0  project.yaml

    nmrfxs gen -s 0 -d ~/gen-structures  project.yaml

    nmrfxs gen -s 0  -f data.nef

    nmrfxs gen -s 0  -f data.nef project.yaml

**gen OPTIONS**:

**-h** 
:   Show help message and exit

**-s** *SEED*
:   Random number generator seed

**-d** *DIRECTORY*
:  Base directory for output files

**-v** 
:  Report violations during calculations 

**-y** *DUMPYAMLMODE*
:  Dump stages to .yaml file

**-r** *REFINEFILE*
:  Name of file to refine

**-f** *SOURCEFILE*
:  Name of file to load

**-n** *NEFoutFile*
:  Name of nef file to write.



### <a id="batchlink">batch</a>

```
nmrfxs batch [OPTIONS] projectFile
```

Generate a family of structures using the data specified in a project file.  An *output* directory and *final* directory will be created if not present.  All generated structures will be written to files (temp1.pdb, temp2.pdb, ...) in the *output* directory.  A violation file (temp1.txt, temp2.text ...) will also be written. The best structures, along with their violation files, will be written to the *final* directory. Multiple files are generated by repeatedly invoking the **nmrfxs gen** command with the specified project file and an incremented seed numbers. The number of invocations running simultaneously will be specified by the **-p** option.


**batch OPTIONS**:


-n *nStructures* 
:  The total number of structures to generate.
	
-k *keepNStructures*
:  The number of structures to keep (and write to the *final* directory).  The structures with lowest total target function will be kept.

-p *useNProcesses* 
:  Structure generation can be sped up by running multiple structure calculation processes simultaneously. This option specifies the number of simultaneous calculations to perform.

-s *startNumber* 
:  Starting number for seed. This defaults to 0, but if you want to run batch a second time and generate additional structures you can specify this value.  Also used when submitting batch commands to multiple computers for higher level of parallelization.

-a
:  If this option is specified then the structures will be automatically aligned and written to a new set of files (sup_final1.pdb, sup_final2.pdb ...).  During alignment defined regions of the structure (lower residue rms) will be identified and used for the alignmnent.

-b *baseName*
: Provide a base name for superimposed files. This option implies the structures are being aligned, or option **-a** is used.

-t *fileType*
: Provide a type for output of superimposed files.  Can be cif (for MMcif) or pdb.

-d *directory*
: Redirect output directories into a specified base directory using a relative path. By default, if this option isn't used, the output will be placed in the current directory.

-c 
: Remove output and final directores (if present)  before generating structures.  Don't do this if you are using the **-s** flag to generate additional structures.

-m *memory*
:  Allot a specific amount of heap memory to use in MegaBytes (MB). By default, 512MB of heap memory are used.

__Example__: 
`nmrfxs batch -n 100 -k 10 -p 5 -a project.yaml`


### <a id="predictlink">predict</a>

NMRFx Structure can predict chemical shifts of proteins and RNA and arbitrary small, organic molecules.
Protein predictions are done using geometric attributes (primarily dihedral angles and ring-current shifts).  RNA
predictions can be done using geometric attributes or secondary structure attribute based methods.
Attribute based methods for RNA can be done with a sequence and dot-bracket notation specified in a .yaml file or they can
be done by automatic recognition of the secondary structure from the 3D coordinates of the RNA read in from a strucutre (pdb or cif) file.
Small molecules are predicted with a HOSE code like method.

**predict OPTIONS**:

-h 
: show this help message and exit

-l *LOCATION*
: Location to store prediction in. Values less than one go into 'reference' locations. (-1)

-r *PREDMODE*
:  Prediction mode used for rna prediction. Can be **dist**, **rc** or **attr**.

-o *OUTPUTMODE*
: Output mode. Can be **star**, **protein** or **attr**. If set to **star** the output will be a portion of a BMRB chemical shift save frame. If **protein** it will be a table of backbone protein shifts. Mode **attr** is only appropriate to RNA predictions done with attributes.

Protein predictions are done for most hydrogen, carbon and nitrogen atoms.
RNA geometric predictions are done for all carbon bound protons and their carbons.
RNA attribute predictions are done for non-exchangable protons and their parent carbon and nitrogen atoms.


Prediction output in star format looks like the following.  This is an NMR-STAR3 chemical shift saveframe without the header.

         1 . 1 1   1  64 GLU N    N 15 120.210 2.470 . 1 . . . .  64 GLU N    .    . 1
         2 . 1 1   1  64 GLU CA   C 13  56.100 0.910 . 1 . . . .  64 GLU CA   .    . 1
         3 . 1 1   1  64 GLU HA   H  1   4.130 0.220 . 1 . . . .  64 GLU HA   .    . 1
         4 . 1 1   1  64 GLU CB   C 13  29.470 0.950 . 1 . . . .  64 GLU CB   .    . 1
         5 . 1 1   1  64 GLU HB2  H  1   2.000 0.190 . 1 . . . .  64 GLU HB2  .    . 1
         6 . 1 1   1  64 GLU HB3  H  1   2.070 0.200 . 1 . . . .  64 GLU HB3  .    . 1
         7 . 1 1   1  64 GLU CG   C 13  35.940 0.850 . 1 . . . .  64 GLU CG   .    . 1

Prediction output in protein format looks like the following.  This only includes "backbone* atoms, even if additional atoms have predictions:

    Num    Name      N     CA     CB      C      H  HA(2)    HA3
     64     GLU 120.21  56.10  29.47 175.45   _      4.13   _
     65     ASP 122.16  54.53  40.80 175.46   8.55   4.74   _
     66     PHE 119.86  54.86  39.16 172.19   9.03   4.76   _
     67     PRO   _     61.49  30.54 174.44   _      4.61   _
     68     PRO   _     62.14  31.80 175.47   _      4.95   _


RNA predictions based on attributes can be output in star format (as above) or the output can be a list of atom specifiers (residueNumber.atomName), predicted shifts
and various attriburtes about the prediction.

-  Atom
-  Predicted Shift 
-  N value: Value is the number of examples with the attributes this atom has.
-  Mean value: Value is the mean of the shifts of the examples.
-  +/- value: Value is the standard deviation of the shifts of the examples.
-  Range: lower upper:  The upper and lower limits of the examples.
-  A list of attributes that characterize this atoms residue (within a 5-residue window)

Output example:

    20.C2' 75.34 N  5 Mean 75.31 +/- 0.24 Range: 74.90 -75.45 Pp_AU_GC_CG_pP_-_-_-_-_-_-
    20.H2' 4.43 N  5 Mean 4.43 +/- 0.01 Range: 4.41 -4.44 Pp_AU_GC_CG_pP_-_-_-_-_-_-
    20.C1' 92.71 N  6 Mean 92.70 +/- 0.13 Range: 92.55 -92.83 Pp_AU_GC_CG_pP_-_-_-_-_-_-
    22.N4 97.53 N  6 Mean 97.57 +/- 0.42 Range: 97.22 -98.38 Pp_CG_CG_-_-_-_-_-_-_-_-
    22.H41 8.13 N 12 Mean 8.05 +/- 0.68 Range: 6.84 -8.67 Pp_CG_CG_-_-_-_-_-_-_-_-
    22.H42 7.30 N 11 Mean 7.41 +/- 0.64 Range: 6.95 -8.50 Pp_CG_CG_-_-_-_-_-_-_-_-
    22.C5 98.24 N 18 Mean 98.24 +/- 0.29 Range: 97.86 -99.20 Pp_CG_CG_-_-_-_-_-_-_-_-
    22.H5 5.46 N 34 Mean 5.46 +/- 0.10 Range: 5.23 -5.77 Pp_CG_CG_-_-_-_-_-_-_-_-
    22.C6 141.97 N 17 Mean 142.02 +/- 1.10 Range: 141.27 -146.07 Pp_CG_CG_-_-_-_-_-_-_-_-

The output for small molecules is a simple table of atom name and chemical shift:

    C6 136.60
    C7 129.30
    C8 157.70
    C9 168.20
    C10 45.40


__Examples__:

```
nmrfxs predict protein.pdb

nmrfxs predict -o protein protein.pdb

nmrfxs predict -o star -r attr  rna.pdb

nmrfxs predict project.yaml
```

### <a id="scorelink">score</a>

```
nmrfxs score [OPTIONS] projectFile [pdbFile1.pdb, pdbFile2.pdb, ...]
```

Analyze the quality of the structure(s) generated by using the score subcommand. Note: the *summary* command listed above 
analyzes the output files from a previous run of *nmrfx batch*.  This command will load pdb files and analyze them 
according to the constraints referenced in the .yaml and on the command line (see options below).

**score OPTIONS**:

**-y** *projectFile* 
:  The project file that defines constraints to be used in the analysis.

**-o** *outDir* 
:  The directory in which to write output files.  Defaults to *analysis*.

**-p** *pdbFilePattern* 
:  PDB files can be specified as an argument to this command.  This argument will result in execution of a Python level glob command to search for files that match the specified pattern. If wild card characters (*) are specified, then the whole pattern needs to be included in single quotes.

**-d** *directory*
: Specify a directory to redirect output directories generated.

**-s** *shifts*
: Add chemical shift files that are not specified in the YAML project file.

**-d** *distances*
: Add distance constraints files that are not specified in the YAML project file.

__Examples__:

* `nmrfxs score -y project.yaml pdb/\*.pdb`

* `nmrfxs score -y project.yaml -p 'pdb/\*.pdb'`


### <a id="summarylink">summary</a>

```
nmrfxs summary [final/final1.txt, final/final2.txt, ...]
```

**summary OPTIONS**:

-h
:   show this help message and exit


-l *LIMDIS*
:   Only violations with an error of at least this amount will be reported (0.2)

-n *NVIOLS*
:   Only violations that occur in at least this number of structures will be reported (2).


Analyze output files and create a summary file showing what constraints are violated.  If no output files are specified as arguments,
all final*.txt files in the final subdirectory of the current directory will be analyzed.  **Summary** is different than the **score** subcommand
in that the violation information is harvested from the output files from the structure calculation, whereas  the **score** command
loads in pdb files and analyzes them.

The output will be placed in a file named analysis.txt and wil have a format like this:

    Type            Atom1              Atom2 nViol      Bound       Mean        Max Structures
     Dis:        1:141.H3' -         1:141.H8    3       3.00       0.45       0.61 |+++.|
     Dis:         1:141.H2 -        1:142.H1'    3       5.00       0.49       0.69 |+++.|
     Dis:         1:130.H2 -         1:134.H8    3       5.00       0.25       0.39 |++.+|



### <a id="superlink">super</a>

Calculate the superpostion of a set of models.  Multiple cycles (specified with -n flag) of superpostion are done to identify
regions that are considered core.  Core residues are identified as those residues whose rms value is less than twice the median of the rms for all residues.  Superimmposed structures can be output into multiple pdb files 
or a single  MMcif file.

**super OPTIONS**:

-h
:    show this help message and exit

-r *RESLISTE*
:   Residues to exclude from comparison. Can specify residue ranges and individual values (e.g. 2-5 or 10).


-a *ATOMLISTE*
:  Atoms to exclude from comparison.

-R *RESLISTI*
:  Residues to include in comparison

-A *ATOMLISTI*
:  Atoms to include in comparison

-c
:  Whether to compare calculated structures to reference structure, and save output to a file.

-t *TYPE*
:  Type (cif|pdb) for saved aligned models. No files saved if this argument is not specified. (None)

-b *BASENAME*
:  Base name (prefix) for superimposed file names.

-n *NCORE*
:  Number of core residue cycles. Default is 5.

### <a id="trainlink">train</a>
*Information pending...*


### <a id="scriptlink">script</a>

If a python script is provided, instead of one of the above subcommands the script will be executed.


###<a id="yamllink">YAML Project Files</a>

The YAML files contain information about the molecular structure, restraints (distances, angles etc.) and parameters of the dynamics trajectory.
It is perhaps best illustrated with a few examples.

The following example indicates that a sequence file should be read from the file 1d3x.seq in the input folder and is  in **nv** format. The **nv**  format is that used by NMRViewJ and is similar to that of CYANA. 
Angle and distance restraints are read from the specified files, which are in XPLOR format.

The structure calculation happens through a process of simulated annealing with rotational dynamics and only happens if there is an **anneal** section in the file.  The dynOptions section specifies that 15000 steps of dynamics will be done starting at a temperature of 5000. Note the force field etc. is not calibrated such that temperature values have physical meanings.  Every 20 steps of dynamics atoms that have ambiguous stereochemistry (like HB2/3) are swapped and the configuration with lowest energy is retained.

```
molecule :
    file : input/1d3z.seq
    type : nv
    chain : 'A'

angles :
    - file : input/dih.tbl
      type : xplor

distances :
    -
      file : input/dis.tbl
      type : xplor
    -
      file : input/hydcon.tbl
      type : xplor

anneal:
    dynOptions :
        steps : 15000
        highTemp : 5000.0
    param :
        swap : 20
```

Here's an example of where the molecular structure and restraints are stored in a NEF file.

```
nef : input/1gb1.nef
  
anneal :
    dynOptions :
        steps : 15000
        highTemp : 5000.0
    param :
        swap : 20
```

Here's an example of .yaml file for an  RNA where the sequence is explicitly listed in the .yaml file.  
The indexing renumbers the sequence, in this case so it matches the numbering in the full virus sequence that this sequence is from.
The ptype parameter indicates that the sequence is RNA.  In this example there are no explicit distance or angle restraints give in separate files.
Instead the vienna (dot-bracket) sequence is used to specify the secondary structure.  Distance and angle restraints consistent with the helical (base-paired) region
are automaticallly generated.  The **ribose : Constrain** value generate distance restraints to close up the ribose rings.



```
molecule :
  entities :
      - sequence : GGCUCUGGUGAGAGCCAGAGCC
        indexing : '1:2 125:135 217:225'
        ptype : RNA

rna:
    ribose : Constrain
    vienna : (((((((((....)))))))))

anneal:
    dynOptions :
        steps : 15000
        highTemp : 5000.0
        dfreeSteps : 0
    force :
        tors : 0.1
        irp : -0.2
```

###<a id="datalink">Data</a>

Data files can be read in several formats.  

**NEF**

First, molecular structure and constraints can be read together from an NMR Exchange Format (NEF) file. [NEF](https://www.nature.com/articles/nsmb.3041) files are a relatively recent format for storing NMR restraints.  They are based on the STAR format that is used by both NMR-STAR (from the BMRB) and MMcif files.  NMRFx can read NEF files to import the molecular sequence and distance, angle and RDC constraints.  Indeed, one can generate a structure using default parameters by simply typing **nmrfxs gen file.nef** where **file.nef** is the name of the NEF file.  If a nef file is used then it can be referenced in the .yaml file like:

```
nef : file.nef
```

**Molecular Topology**

If you are not using NEF files, then you can read the molecular sequence and restraints from text files in a variety of formats.  The molecular sequence can be read from a file in NMRViewJ (similar to CYANA) format.  This is a file consisting of the three-letter amino acid code (one letter for RNA, and two letter for DNA).  Each residue is on a single line of the file and can optionally be followed by an integer number representing the residue number. For example, a sequence starting with Methionine with sequential number 1 would look like:

```
MET     1
GLN 
ILE
PHE4
VAL5
...
```

If the sequence starts at 1 the integer residue position is optional.  Any (or all) residue can have a sequential number next to it and gaps can be present in the numbering.

This file would be reference in the **molecule** section of the .yaml file:
```
molecule :
     file : input/1d3z.seq
     chain : A
     type : nv

```

Alternatively the sequence can be explicitly listed as a single letter code in the .yaml file with a section like:

```
molecule :
  entities :
      - sequence : GGCUCUGGUGAGAGCCAGAGCC
        indexing : '1:2 125:135 217:225'
        ptype : RNA
```


In the above example the indexing field is used to specify the residue numbering.  In this example the first residue would be 1, the second 2, the third 125.  Further residues would be 126, 127 etc. up to position 135.  Then the numbering continues with  217, 218 etc. through the last residue, 225.

**Restraints**

Restraints, as mentioned above, can be included in a NEF file along with the molecular topology.  Alternatively they can be specified in several other formats. Currently supported are CYANA, XPLOR and an NMRFx format.  Note: no attempt has been made to ensure comprehensive and fully accurate support of CYANA and XPLOR formats.  They are provided as a convenience to the user and for our own testing.  Our suite of test structures does, however, have a variety of examples of CYANA and XPLOR (and NEF) formats and all the examples run properly.

Here is the restraint section of a .yaml file (from our test suite)  with CYANA restraints for ubiquitin. Note that CYANA distance restraints are normally in pairs with one for upper bounds (.upl) and one for lower bounds (.lol).  The .yaml file need only mention the root name.  So this example will load both distances.upl and distance.lol.

```
distances :
    - file : input/distances
      type : cyana

angles :
    - file : input/dihedrals.aco
      type : cyana

```

And the corresponding example with XPLOR restraints.

```
angles :
    - file : input/dih.tbl
      type : xplor

distances :
    -
      file : input/dis.tbl
      type : xplor
    -
      file : input/hydcon.tbl
      type : xplor

```

The NMRFx format has tab-separated lines with fields:

id, group, atom1Specifier, atom2Specifier, lower, upper

```

0       0       1:64.H  1:64.H  1.8     2.8 
1       0       1:7.H   1:64.H  1.8     2.8
2       2       1:63.H  1:64.H  1.8     5.2
3       3       1:58.HA 1:64.H  1.8     4.3
4       3       1:64.HA 1:64.H  1.8     4.3
```


###<a id="anneallink">Annealing Options</a>

There are a variety of parameters that effect the protocol used for simulated annealing in structure generation.  The most likely ones that a user might want to change from the default value are **steps**, **highTemp** and **cffSteps**.  Most other parameters can be left at their default values. 

These parameters apply to the overall protocol and are set in the **dynOptions** section of the **anneal** section of the .yaml file.

steps
:  Total number of dynamics steps to execute in annealing protocol (15000)

cffSteps
:  If this is greater than 0 then two stages are added to the protocol that are 
performed with complex non-bond force field turned on (0).

highTemp
:  Initial dynamics are done at this temperature

medFrac
:  Medium temperature of annealing profile is highTemp times this value.(0.05)

update:
:  Update non bond contact list every *update* cycles. (20)


highFrac:
:  Run dynamics at high temperature for this fraction of total steps (0.3)

toMedFrac:
:  Fraction of steps during annealing phase that happen in first part of phase(0.5)

timeStep
:  Initial time step, but time step will be optimized automatically (4.0)

stepsEnd
:  Numer of steps of dynamics at the end at zero temperature (100)

econHigh
:  Energy conservation used in adjusting time steps at high temperature (0.005)

econLow
:  Energy conservation used in adjusting time steps at low temperature (0.001)

timePowerHigh
:  Exponent in power function used in annealing profile from high to medium temperature (4.0)

timePowerMed
:  Exponent in power function used in annealing profile from medium to low temperature (4.0)

minSteps
:  Numer of gradient minimization steps before annealing phases (medium and low) (100)

polishSteps
:  (500)

dfreeSteps
:  Numer of derivative free minimization steps before each stage (0)

dfreeAlg
:  Algorithm used for derivative free minimization steps (cmaes)

kinEScale
: Scaling parameter used in calculating kinetic energy  (200)


### <a id="parameterlink">Parameters</a>


coarse
:  If true, use coarse grain mode

dislim
:  Only include atoms in the non-bond contact list that are less than this distance apart.

end
:  Only include non-bond contacts and distances that are less than this number of residues apart.

hardsphere
:  A value added on to the radius of non-hydrogen atoms that have attached hydrogens, when explicit hydrogens aren't used.

shrinkValue
:  Reduce the size of non-hydrogens by this amount.

shrinkHValue
:  Reduce the size of hydrogen atoms by this amount

swap
:  Swap ambigous stereospecific atoms at intervals of this number of steps. After swapping test the energy and see if it is lower.  If so, keep the swap.

updateAt
:  Update the non-bond contact list at intervals of this number of steps.

useh
:  If true, include hydrogens in non-bond contacts.


### <a id="forcelink">Force Terms</a>

The force terms apply during the calculation of energy values and gradients of the energy during commands such as [gen](#genlink).  Generally, if a force term has a value < 0.0, then that component will not be included.

bondWt
:  The weight for distance restraints that involve bonds (for example, to close ribose rings).

cffnb
:  Complex Force Field repulsion function.  Currently based on AMBER non-bond contact values. By default it is set to -1.0, so not used.  Instead the default is the simple repulsive function.

dih
: The weight for experimental dihedral angle  restraints

dis
: The weight for experimental distance restraints

elec
:  Electrostatics.  Not currently used

irp
: The weight for intrinsic rotational potential.  Currently based on AMBER parameters.

nbmin
:  An value that attenuates the non-bond contact (when cffnb > 0.0).  Values can range from 0.5 - 1.25, and set a lower limit on the distance used as input to the non-bond force calculation.  So if set to 0.5, even if inter-atomic distance is 0.1, a distance of 0.5 will be used.  This prevents the energy for getting too high when the structure is in being calculated.

repel
:  Simple repulsion function to keep atoms apart.  Only used if cffnb < 0.0, which is the default

shift
: The weight for experimtal chemical shift values.  Derivatives are not currently available so this is only active in derivative-free steps.

stack
: The weight for RNA base stacking.
 
tors
:  The weight for the torsion angles of the RNA backbone.  Based on the the distance of the angles for a residue to the angles of the nearest suite.



### <a id="stagelink">Stages</a>

Structure calculation and refinement in NMRFX Structure proceeds through a series of stages that represent a process of simulated annealing.  Each stage has preset values for [Parameters](#parameterlink) and [Forces](#forcelink).  The values specify a static or falling temperature to be used during that stage as well as parameters that effect what atoms are included in the non-bond contacts and the forces used in the energy calculation.  These preset values can be overwritten by entering values for any stage in the .yaml file.  A normal structure calculation using the [gen](#genlink) command proceeds through the following stages.  The full set of parameters and force values for each stage can be seen [below](#allstageslink).


stage_prep
:  This stage prepares the structure for the dynamics by first minimizing bad contacts and violations.  It does this by a series of gradient minimization steps.  Hydrogen atoms are not included in the list of atoms to be checked for contacts.  This is partially compensated by increasing the diameter of atoms with attached hydrogens.  The size of the heavy atoms that are included are reduced somewhat to allow the structure to more easily change its conformation.

stage_hi
:  High temperature dynamics are performed for a number of steps calculated using the *highFrac* [Parameter](#parameterlink).  Performing dynamics at high temperature allows the structure to undergo large changes in conformation.

stage_anneal_hi
:  Annealing involves gradually lowering the temperature according to some predefined schedule.  In this stage the temperature is lowered from the value used in **stage_hi** to a medium temperature

stage_anneal_med
:  Annealing proceeds with the temperature falling from the medium temperature to the low temperature.  As the temperature falls the conformation will be less likely to undergo large changes.  The number of steps used is a fraction (switchFrac) of the number of steps in the annealing phase.  In this stage the reduction of size (shrinkValue) is set to 0.0 so that atoms are prevented from approaching as closely as was the case in the previous stage.  During this stage the *econVal* changes so that the adjustment of the time step is done in a way that the calculated kinetic energy more closely approximates that expected for the target temperature.

stage_anneal_low 
:  The temperature is dropped from the low temperature down to 0.0.  During this phase hydrogen atoms are included in the non-bond contact list.

stage_low
:  Additional dynamics steps are done at a temperature of 0.0

A final of gradient minimization is also included.  The number of steps of this polishing phase is set by the **polishSteps** parameter.  Otherwise this is not (yet) a full stage that can be modified like the other stages.

If the **cffSteps** parameter is set to a value greater than 0 then two additional stages will be inserted after the **stage_anneal_low** stage.  These two stages, **stage_cff_reduced** and **stage_cff_full** are done with the non-bond contact forces calculated using a more realistic, but slower, calculation.  These forces are based on parameters from the AMBER force field.

stage_cff_reduced
:  In this phase the non-bond contacts term is attenuated for closely contacting atoms so that the energies (and their gradients) don't get too high and cause problems in the dynamics calculations.  This is done by setting the **nbmin** value to 1.0 so that inter-atomic distances less than 1.0 are calculated as if the value was approximately 1.0.  By default 20% of the cff steps are done in this stage.

stage_cff_full
:  The nbmin value is reduced to 0.5.

All the built-in stages can be displayed using the **nmrfxs gen -y mode** command which will print out all the stages in yaml format.

The **mode** argument specifies what stages are reported and can be **gen**, **refine**, **cff** or **all**.  The output below was generated with:

    nmrfxs gen -y all

You can also specify the name of a **NEF** file and it will be inserted into the output to give a complete project file that can be executed.  For example to generate a full yaml file that will generate a structure based on data in **test.nef** you would use:

    nmrfxs gen -y gen -n test.nef > project_test.yaml

and then generate a structure with

    nmrfxs gen project_test.yaml

Note:  you don't need to generate a full yaml file for structure calculation as the normal gen command will use the default stages.  But generating one as described here allows you to inspect and modify the values used in each stage.

#### <a id="allstageslink">All Stages</a>

Here's the output listing all available stages:


```
anneal:
    dynOptions: 
        steps : 15000
        highTemp : 5000.0
    stage_prep:
        param : 
            dislim : 4.6
            swap : 20
            updateAt : 5
            hardSphere : 0.15
            useh : False
            shrinkValue : 0.2
        ends : [3, 10, 20, 1000]
        force : 
            dih : 5
            irp : 0.05
            dis : 1.0
            repel : 0.5
    stage_hi:
        timestep : 4.0
        dfreeSteps : None
        switchFracVal : None
        tempVal : 5000.0
        econVal : 0.005
        gMinSteps : None
        param : 
            updateAt : 20
            hardSphere : 0.15
            useh : False
            end : 1000
            shrinkValue : 0.2
        force : 
            dih : 5
            dis : 1.0
            repel : 0.5
        nStepVal : 4500
    stage_anneal_hi:
        switchFracVal : None
        tempVal : [5000.0, 250.0, 4.0]
        econVal : 0.005
        gMinSteps : None
        param : 
        force : 
        nStepVal : 5200
    stage_anneal_med:
        switchFracVal : 0.65
        tempVal : [250.0, 1.0, 4.0]
        econVal : [0.005, 0.5]
        gMinSteps : 100
        param : 
            hardSphere : 0.0
            useh : False
            shrinkValue : 0.0
        force : 
        nStepVal : 5200
    stage_anneal_low:
        switchFracVal : None
        tempVal : None
        econVal : None
        gMinSteps : 100
        param : 
            shrinkHValue : 0.0
            hardSphere : 0.0
            useh : True
            shrinkValue : 0.0
        force : 
            bondWt : 25.0
            repel : 1.0
        nStepVal : None
    stage_cff_reduced:
        switchFracVal : 0.2
        tempVal : [100.0]
        param : 
            dislim : 6.0
        force : 
            nbmin : 1.0
            dih : 5.0
            stack : 0.1
            irp : 0.5
            tors : -0.1
            dis : 40.0
            repel : -1.0
            cffnb : 1.0
        nStepVal : 0
    stage_cff_full:
        switchFracVal : None
        param : 
        force : 
            nbmin : 0.5
            repel : -1.0
            cffnb : 1.0
        nStepVal : None
    stage_low:
        switchFracVal : None
        tempVal : 0.0
        econVal : 0.001
        gMinSteps : 100
        param : 
        force : 
            repel : 2.0
        nStepVal : 100

```


### <a id="genoutputlink">Structure Calculation (gen subcommand) Output</a>

A structure calculation with the [gen](#genlink) subcommand generate several forms of output.  During structure calculation 
information is written to standard output and is described below.  At the completion of structure calculation 
three files are written into a folder named **output** (which is created if it doesn't already exist).  These three files
are tempN.pdb (PDB file of the generated structure), tempN.ang (dihedral angles of rotatable bonds in generated structure),
and tempN.txt (angle and distance violations and close non-bond contacts).  The **N** in these file names is the seed number used
(specified with -s flag to the gen subcommand).

As described above the structure calculation proceeds through a series of stages.  Each stage is characterized by a different set of
Forces and Parameters and at the start of each stage the [Forces](#forcelink) and 
[Parameters](#parameterlink) are reported.  Each stage can involve both gradient minimization (typically at start of the stage) and
rotational dynamics. The status of each of these protocols is periodically reported.  Lines starting with **GMIN** are reported 
during gradient minimization and the output includes the current number of iterations, the number of non-bond contacts and the energy. 

**Note: at present, numbers for physics based parameters (time, kinetic energy, potential energy etc.) are not calibrated in a way that
they are physically meaningful.**

Lines starting with RDYN are reported during rotational dynamics.

step
:  The number of rotational dynamics steps that have been performed when the report is done

time
:  The simulation time at this point. 

temp
:  Temperature calculated based on the kinetic energy (again, not currently

kinE
: Kinetic energy

potE
: Potential energy

totE
: sum of the kinetic and potential energy

deltaE
: fractional energy change averaged over steps since last report line.

timeStep
: The average time step since last report line.

rmsAngle
: Root mean square of the rotatable angles since last report line.

maxAngle
: Maximum angle change (degrees) in since last report line

contacts
: number of non-bond contacts (within specified distance range)

Here is the output of the calculation of the structure of ubiquitin using data in the [Example](https://nmrfx.org/downloads/structure) files.

    nmrfxs gen project.yaml
	
```
mass 8564.8
FORCES cffnb -1.00 nbmin  0.50 repel  0.50 elec -1.00 dis  1.00 dprob -1.00 dih  5.00 irp  0.05 shift -1.00 bondWt  1.00 stack -1.00
PARS   coarse False includeH False hard  0.15 shrinkValue  0.20 shrinkHValue  0.00 updateAt   5 deltaStart    0 deltaEnd    2 disLim  4.60
PARS   coarse False includeH False hard  0.15 shrinkValue  0.20 shrinkHValue  0.00 updateAt   5 deltaStart    0 deltaEnd    3 disLim  4.60
GMIN     iter contacts    energy
GMIN        0     2969   1251.01
GMIN       20     2389      2.77
GMIN       40     2421     -1.38
GMIN       60     2427     -1.73
GMIN       80     2431     -1.89
GMIN       84     2431     -1.90
PARS   coarse False includeH False hard  0.15 shrinkValue  0.20 shrinkHValue  0.00 updateAt   5 deltaStart    0 deltaEnd   10 disLim  4.60
GMIN     iter contacts    energy
GMIN        0     3016   8600.56
GMIN       20     4307    207.02
GMIN       40     4049    123.20
GMIN       60     4019     99.19
GMIN       80     4004     91.30
GMIN      100     3971     88.14
PARS   coarse False includeH False hard  0.15 shrinkValue  0.20 shrinkHValue  0.00 updateAt   5 deltaStart    0 deltaEnd   20 disLim  4.60
GMIN     iter contacts    energy
GMIN        0     6137   1231.51
GMIN       20     5264    169.32
GMIN       40     4870    135.81
GMIN       60     4760    124.97
GMIN       61     4760    124.97
PARS   coarse False includeH False hard  0.15 shrinkValue  0.20 shrinkHValue  0.00 updateAt   5 deltaStart    0 deltaEnd 1000 disLim  4.60
GMIN     iter contacts    energy
GMIN        0    10386  10989.17
GMIN       20     7221   1160.59
GMIN       40     7026    749.82
GMIN       60     6895    628.65
GMIN       80     6795    600.66
GMIN      100     6279    439.39
FORCES cffnb -1.00 nbmin  0.50 repel  0.50 elec -1.00 dis  1.00 dprob -1.00 dih  5.00 irp  0.05 shift -1.00 bondWt  1.00 stack -1.00
PARS   coarse False includeH False hard  0.15 shrinkValue  0.20 shrinkHValue  0.00 updateAt  20 deltaStart    0 deltaEnd 1000 disLim  4.60
init vel 5000.0 4999.999999999999
RDYN   step       time     temp     kinE     potE     totE     deltaE   timeStep rmsAngle maxAngle contacts
RDYN      0      0.000   4986.2    252.5    439.5    692.0   0.000000   0.000000    0.000    0.000     6290
RDYN    224   2908.659   4617.3    234.9    769.4   1004.3   0.007462  12.927374    1.703    6.469     5166
RDYN    449   4631.695   7885.3    387.3    433.9    821.2   0.004899   7.657937    1.221    4.583     4997
RDYN    674   7584.691   5314.4    263.9    610.0    873.9   0.006667  13.124428    2.034    6.996     6250
RDYN    899   9689.840   5171.8    278.5    503.7    782.1   0.005389   9.356217    1.544    5.482     5228
RDYN   1124  12177.481   5901.5    302.4    346.8    649.2   0.006183  11.056183    1.566    6.078     5229
RDYN   1349  15027.873   5291.9    269.0    673.5    942.5   0.007878  12.668408    2.154    7.802     6700
RDYN   1574  17785.140   5631.4    286.4    607.1    893.5   0.006683  12.254521    2.168    7.857     6442
RDYN   1799  20323.263   4740.6    242.2    503.8    746.0   0.007725  11.280546    2.020    7.575     5136
RDYN   2024  23152.798   5097.2    253.1    557.1    810.2   0.007492  12.575710    2.095    7.073     6087
RDYN   2249  25853.093   5964.4    291.0    524.9    816.0   0.006162  12.001310    1.808    6.832     5592
RDYN   2474  28249.377   5276.5    265.6    561.9    827.6   0.007235  10.650153    1.589    5.855     5132
RDYN   2699  30337.993   5189.4    266.9    516.1    783.0   0.005513   9.282740    1.613    6.068     5863
RDYN   2924  32649.062   5374.3    270.6    494.4    765.0   0.006198  10.271414    1.649    6.032     5211
RDYN   3149  35189.062   5252.3    264.4    715.4    979.7   0.006647  11.288890    1.923    6.707     7363
RDYN   3374  37311.469   5133.4    259.2    461.2    720.4   0.005736   9.432919    1.555    5.782     5604
RDYN   3599  40526.564   4426.2    229.6    614.7    844.3   0.006740  14.289312    2.052    7.699     6228
RDYN   3824  43259.732   5093.1    258.6    281.9    540.5   0.007406  12.147413    1.937    6.500     4765
RDYN   4049  45250.724   4978.3    254.1    462.0    716.1   0.005086   8.848856    1.341    5.192     5471
RDYN   4274  47776.677   5118.0    258.5    343.0    601.5   0.007157  11.226456    1.829    7.234     5278
RDYN   4499  50491.574   5133.2    259.5    592.3    851.8   0.005579  12.066210    1.942    6.799     4907
FORCES cffnb -1.00 nbmin  0.50 repel  0.50 elec -1.00 dis  1.00 dprob -1.00 dih  5.00 irp  0.05 shift -1.00 bondWt  1.00 stack -1.00
PARS   coarse False includeH False hard  0.15 shrinkValue  0.20 shrinkHValue  0.00 updateAt  20 deltaStart    0 deltaEnd 1000 disLim  4.60
RDYN   step       time     temp     kinE     potE     totE     deltaE   timeStep rmsAngle maxAngle contacts
RDYN      0  50491.574   5124.5    259.5    616.5    876.0   0.000000   0.000000    0.000    0.000     4912
RDYN    259  53241.191   4334.8    246.0    324.2    570.3   0.004950  10.575451    1.603    6.059     4592
RDYN    519  56691.129   3451.4    171.6    290.5    462.1   0.006564  13.268990    1.533    5.702     4853
RDYN    779  60552.463   2801.3    146.2    227.0    373.2   0.005992  14.851288    1.645    6.401     4861
RDYN   1039  63514.610   2247.4    110.6    250.1    360.7   0.006071  11.392872    1.294    4.683     4282
RDYN   1299  66603.363   1695.2     86.6    142.7    229.4   0.005608  11.879820    1.309    4.413     4747
RDYN   1559  69369.128   1385.9     69.5    178.7    248.3   0.005656  10.637557    1.121    3.736     4580
RDYN   1819  72710.496   1051.3     53.5    139.0    192.5   0.005747  12.851416    1.218    4.157     4561
RDYN   2079  75827.206    863.8     43.4    102.4    145.8   0.005732  11.987345    0.974    3.361     4599
RDYN   2339  79647.275    708.6     35.5     79.4    115.0   0.005905  14.692575    1.142    4.083     4776
RDYN   2599  83460.276    560.5     28.2     64.0     92.3   0.006189  14.665387    0.997    3.604     4399
RDYN   2859  86517.756    446.1     22.6     47.8     70.4   0.005459  11.759540    0.783    3.043     4334
RDYN   3119  89579.102    385.3     19.6     38.4     58.0   0.006560  11.774405    0.723    2.816     4135
RDYN   3379  92890.222    325.5     16.4     29.2     45.6   0.005777  12.735077    0.703    2.919     4004
RDYN   3639  96200.934    295.9     15.0     39.7     54.6   0.005741  12.733508    0.682    2.548     4346
RDYN   3899  99842.233    262.4     13.3     30.8     44.1   0.005823  14.004999    0.688    2.460     4166
RDYN   4159 103709.173    255.5     12.9     29.8     42.7   0.005980  14.872846    0.727    2.701     4103
RDYN   4419 107622.884    239.1     12.0     35.4     47.4   0.006024  15.052734    0.722    3.119     4175
RDYN   4679 112043.490    242.1     12.2     28.2     40.4   0.006578  17.002332    0.798    3.921     4170
RDYN   4939 115432.651    256.8     13.1     20.1     33.2   0.005417  13.035234    0.592    2.137     4075
RDYN   5199 119050.572    255.9     13.0     25.0     38.0   0.005758  13.915081    0.631    2.397     4167
FORCES cffnb -1.00 nbmin  0.50 repel  0.50 elec -1.00 dis  1.00 dprob -1.00 dih  5.00 irp  0.05 shift -1.00 bondWt  1.00 stack -1.00
PARS   coarse False includeH False hard  0.00 shrinkValue  0.00 shrinkHValue  0.00 updateAt  20 deltaStart    0 deltaEnd 1000 disLim  4.60
GMIN     iter contacts    energy
GMIN        0     4162     33.91
GMIN       20     3980     24.42
GMIN       33     3990     23.16
RDYN   step       time     temp     kinE     potE     totE     deltaE   timeStep rmsAngle maxAngle contacts
RDYN      0 119050.572    279.5     14.2     23.2     37.3   0.000000   0.000000    0.000    0.000     3991
RDYN    259 122208.906    200.1     10.2     31.8     42.0   0.005305  12.147438    0.524    1.911     3791
RDYN    519 125184.520    169.2      8.5     21.8     30.4   0.005121  11.444668    0.447    1.725     3820
RDYN    779 129409.778    132.9      6.7     15.3     22.1   0.005447  16.250994    0.593    2.078     3813
RDYN   1039 134108.677    107.6      5.4     15.1     20.6   0.005017  18.072686    0.577    2.035     3698
RDYN   1299 137968.677     80.7      4.1     12.9     17.0   0.005156  14.846157    0.419    1.588     3953
RDYN   1559 141240.646     62.8      3.2      8.9     12.1   0.004901  12.584495    0.318    1.343     3904
RDYN   1819 144177.171     46.5      2.4      3.1      5.4   0.005045  11.294328    0.250    0.842     3658
RDYN   2079 146403.431     34.5      1.7      1.6      3.3   0.004372   8.562537    0.172    0.642     3598
RDYN   2339 147651.564     24.1      1.2      1.0      2.2   0.004752   4.800511    0.084    0.314     3694
RDYN   2599 148096.764     16.8      0.8     -0.3      0.6   0.003911   1.712310    0.025    0.089     3601
RDYN   2859 148274.094     11.3      0.6     -0.5      0.0   0.004147   0.682038    0.008    0.032     3574
RDYN   3119 148312.818      7.5      0.4     -0.6     -0.2   0.004897   0.148939    0.001    0.004     3572
RDYN   3379 148424.632      4.8      0.2     -1.0     -0.7   0.003090   0.430052    0.003    0.009     3564
FORCES cffnb -1.00 nbmin  0.50 repel  1.00 elec -1.00 dis  1.00 dprob -1.00 dih  5.00 irp  0.05 shift -1.00 bondWt 25.00 stack -1.00
PARS   coarse False includeH  True hard  0.00 shrinkValue  0.00 shrinkHValue  0.00 updateAt  20 deltaStart    0 deltaEnd 1000 disLim  4.60
GMIN     iter contacts    energy
GMIN        0    17782     26.39
GMIN       20    16816     12.42
GMIN       40    16783     10.20
GMIN       60    16801      9.34
RDYN   step       time     temp     kinE     potE     totE     deltaE   timeStep rmsAngle maxAngle contacts
RDYN   3380 148424.632      7.8      0.4      9.3      9.7   0.000000   0.000000    0.000    0.000    16801
RDYN   3639 148734.054      3.3      0.2      4.3      4.4   0.002944   1.190086    0.008    0.046    16787
RDYN   3899 149036.606      2.1      0.1      1.9      2.0   0.003025   1.163663    0.007    0.051    16804
RDYN   4159 149336.382      1.5      0.1      0.8      0.9   0.002954   1.152981    0.005    0.032    16782
RDYN   4419 149547.240      1.2      0.1      0.3      0.4   0.002939   0.810992    0.003    0.015    16782
RDYN   4679 149664.833      1.0      0.1      0.1      0.2   0.002869   0.452281    0.002    0.008    16787
RDYN   4939 149724.268      1.0      0.1      0.0      0.1   0.002786   0.228596    0.001    0.004    16786
RDYN   5199 149753.403      1.0      0.1     -0.0      0.0   0.002690   0.112061    0.000    0.002    16794
FORCES cffnb -1.00 nbmin  0.50 repel  2.00 elec -1.00 dis  1.00 dprob -1.00 dih  5.00 irp  0.05 shift -1.00 bondWt 25.00 stack -1.00
PARS   coarse False includeH  True hard  0.00 shrinkValue  0.00 shrinkHValue  0.00 updateAt  20 deltaStart    0 deltaEnd 1000 disLim  4.60
GMIN     iter contacts    energy
GMIN        0    16794      4.18
GMIN       20    16683      3.71
GMIN       40    16698      3.47
GMIN       50    16691      3.46
RDYN   step       time     temp     kinE     potE     totE     deltaE   timeStep rmsAngle maxAngle contacts
RDYN      0 149753.403      1.0      0.1      3.5      3.5   0.000000   0.000000    0.000    0.000    16691
RDYN      4 149753.612      0.0      0.0      3.5      3.5   0.000001   0.041694    0.000    0.000    16691
RDYN      9 149753.848      0.0      0.0      3.5      3.5   0.000000   0.047173    0.000    0.000    16691
RDYN     14 149754.115      0.0      0.0      3.5      3.5   0.000000   0.053371    0.000    0.000    16691
RDYN     19 149754.358      0.0      0.0      2.8      2.8   0.050457   0.048579    0.000    0.000    16691
RDYN     24 149754.674      0.0      0.0      2.8      2.8   0.000000   0.063247    0.000    0.000    16691
RDYN     29 149755.032      0.0      0.0      2.8      2.8   0.000000   0.071558    0.000    0.000    16691
RDYN     34 149755.436      0.0      0.0      2.8      2.8   0.000000   0.080962    0.000    0.000    16691
RDYN     39 149755.894      0.0      0.0      2.8      2.8   0.000000   0.091601    0.000    0.000    16691
RDYN     44 149756.413      0.0      0.0      2.8      2.8   0.000000   0.103638    0.000    0.000    16691
RDYN     49 149756.999      0.0      0.0      2.8      2.8   0.000000   0.117257    0.000    0.000    16691
RDYN     54 149757.662      0.0      0.0      2.8      2.8   0.000000   0.132665    0.000    0.000    16691
RDYN     59 149758.413      0.0      0.0      2.8      2.8   0.000000   0.150098    0.000    0.000    16691
RDYN     64 149759.262      0.0      0.0      2.8      2.8   0.000000   0.169823    0.000    0.000    16691
RDYN     69 149760.223      0.0      0.0      2.8      2.8   0.000000   0.192139    0.000    0.000    16691
RDYN     74 149761.309      0.0      0.0      2.8      2.8   0.000001   0.217387    0.000    0.000    16691
RDYN     79 149762.539      0.0      0.0      2.8      2.8   0.000000   0.245954    0.000    0.000    16691
RDYN     84 149763.931      0.0      0.0      2.8      2.8   0.000001   0.278274    0.000    0.000    16691
RDYN     89 149765.505      0.0      0.0      2.8      2.8   0.000001   0.314841    0.000    0.000    16691
RDYN     94 149767.286      0.0      0.0      2.8      2.8   0.000000   0.356214    0.000    0.000    16691
RDYN     99 149769.301      0.0      0.0      2.8      2.8   0.000000   0.403024    0.000    0.000    16691
GMIN     iter contacts    energy
GMIN        0    16691      2.76
GMIN        6    16675      2.70
NNOE 7064 nRepel 16698
energy is 2.69516703654
etime  37.4120001793

```

### <a id="genoutputlink">Multiple Structure Calculation (batch subcommand) Output</a>

Generation of multiple structures with the [**batch**](#batchlink) subcommand results in 
muliple simultaneous instances of the [**gen**](#genlink) subcommand running.  The output of each of these
is redirected into files named cmdout_N.txt (where N is the seed number) in the **output** subdirectory.

Standard output of the **batch** command itself will be information about the progress of each calculation.

Lines like this indicate that a new NMRFx Structure process with the **gen** subcommand has been started and
indicates the seed used, which of the requested number of structures this job represents, and the 
process identifier (pid) for the job.

    submit 0 seed:   0 Structure #   1 of  50 pid    1509

The number after submit indicates which of the reserved number of processes is being used for that job.

The batch process monitors spawned processes and when each one is completed it will print a **Finish** line:

    Finish 1 seed:   1 Finished      1 of  50 pid    1511 eTime   56.2

The batch process monitors each spawned processes elapsed time.  If a process takes more than three times
the average time of the jobs that have already finished then that job is killed.  A new process
(with new seed number) will be submitted.

and then (if all structures have not been completed) submit a new job.

Here's part of the output for generation of 50 structures:

```
nmrfxs batch -n 50 -k 10 -p 5 -a -c project.yaml 

submit 0 seed:   0 Structure #   1 of  50 pid    1509
submit 1 seed:   1 Structure #   2 of  50 pid    1511
submit 2 seed:   2 Structure #   3 of  50 pid    1515
submit 3 seed:   3 Structure #   4 of  50 pid    1518
submit 4 seed:   4 Structure #   5 of  50 pid    1523
Finish 1 seed:   1 Finished      1 of  50 pid    1511 eTime   56.2
Finish 2 seed:   2 Finished      2 of  50 pid    1515 eTime   56.2
submit 1 seed:   5 Structure #   6 of  50 pid    1568
submit 2 seed:   6 Structure #   7 of  50 pid    1569
Finish 0 seed:   0 Finished      3 of  50 pid    1509 eTime   57.2
Finish 3 seed:   3 Finished      4 of  50 pid    1518 eTime   57.2
Finish 4 seed:   4 Finished      5 of  50 pid    1523 eTime   57.2
submit 0 seed:   7 Structure #   8 of  50 pid    1580
submit 3 seed:   8 Structure #   9 of  50 pid    1581
submit 4 seed:   9 Structure #  10 of  50 pid    1584
...
submit 0 seed:  47 Structure #  48 of  50 pid    2005
submit 4 seed:  48 Structure #  49 of  50 pid    2006
Finish 2 seed:  44 Finished     45 of  50 pid    1965 eTime   57.1
submit 2 seed:  49 Structure #  50 of  50 pid    2020
Finish 3 seed:  45 Finished     46 of  50 pid    1991 eTime   57.1
Finish 1 seed:  46 Finished     47 of  50 pid    1999 eTime   55.1
Finish 0 seed:  47 Finished     48 of  50 pid    2005 eTime   55.1
Finish 2 seed:  49 Finished     49 of  50 pid    2020 eTime   55.1
Finish 4 seed:  48 Finished     50 of  50 pid    2006 eTime   56.1
Done
  * ca,c,n,o,p,o5',c5',c4',c3',o3'
repModel 6 rms 0.971581149907 avgrms 1.13736317587
coreResidues [u'A:2-7', u'A:9-72']
coreResidues [u'A:2-7', u'A:11-71']
coreResidues [u'A:2-6', u'A:11-71']
coreResidues [u'A:2-6', u'A:11-71']
coreResidues [u'A:2-6', u'A:11-71']
repModel 3 rms 0.464075104455 avgrms 0.509412597497
```

When all requested structures are finished the output for each structure calculation will be analyzed
and the N (where N is set with the -k flag) best structures will be kept.  The best structures
(and their corresponding angle and violation files) will be copied from output to the final directory.
They will be given extensions starting with 1, for the best structure (final1.pdb, final1.ang, final1.txt).
The [super](#superlink) subcommand will be used to generate
an MMCif file with all the superimposed structures or a set of pdb files (sup_final1.pdb etc).
The choice of MMcif (default) or PDB file is set by the **-t** flag to the **batch** command.

A summary of the violation files (final1.txt, final2.txt etc.) will be
written to  final/summary.txt.  Each line of the summary corresponds to one final structure.
The value in the first column is the index of the file (1 for final1.pdb etc.).  The second 
column (34, 36, 15 etc. in example below) is the seed used to generate that structure.

```
1   34  Irp   307   -4.380 Dih    97    0.208 CFF     0    0.000 Repel 16565    4.692 Distance  7064    1.356    0.450 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    1.875
2   36  Irp   307   -4.122 Dih    97    0.343 CFF     0    0.000 Repel 17172    4.596 Distance  7064    1.323   -0.328 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.139
3   15  Irp   307   -4.502 Dih    97    0.246 CFF     0    0.000 Repel 17070    4.668 Distance  7064    1.799   -0.470 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.210
4   37  Irp   307   -4.349 Dih    97    0.323 CFF     0    0.000 Repel 17097    4.387 Distance  7064    1.860    0.455 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.221
5   10  Irp   307   -4.349 Dih    97    0.115 CFF     0    0.000 Repel 17043    4.500 Distance  7064    1.979    0.455 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.244
6   12  Irp   307   -4.430 Dih    97    0.250 CFF     0    0.000 Repel 17171    4.495 Distance  7064    1.951    0.350 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.266
7   21  Irp   307   -4.331 Dih    97    0.113 CFF     0    0.000 Repel 16955    4.895 Distance  7064    1.597    0.452 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.274
8   38  Irp   307   -4.534 Dih    97    0.275 CFF     0    0.000 Repel 17102    4.727 Distance  7064    1.891   -0.441 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.359
9   41  Irp   307   -4.566 Dih    97    0.128 CFF     0    0.000 Repel 17386    4.865 Distance  7064    1.932    0.439 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.360
10  35  Irp   307   -4.363 Dih    97    0.138 CFF     0    0.000 Repel 17419    4.774 Distance  7064    1.872    0.515 Shift     0    0.000 ProbT     0    0.000 Stack     0    0.000 Total    2.421
```
