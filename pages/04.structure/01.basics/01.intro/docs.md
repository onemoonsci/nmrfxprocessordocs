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


## Subcommands :

### <a id="genlink">gen</a>

```
nmrfxs gen [ -s gen|all|refine ] [ -s seed ] [ -d directory ] [ -r report ] [ projectFile ] [ script.py ]
```

Generate a single structure using data specified in a project file and initializing the random number generator with a specified seed.  This is useful for testing out the project file before generating a whole family of structures with the batch command.  An *output* directory will be created if not present.  After successful execution, the generated PDB and violation files will be written to that directory.  The output files will have the seed number appended to them (i.e. temp0.pdb, temp0.txt, etc.). By default, the *output* directory gets placed in the current directory, however, the relative path to a different directory can be specified using the directory option. When debugging a structure generated, it may be useful to view the energy violations for all the constraints specified in the project file. To do this, specify the report option.  This will output constraint violations at prepartion stage into a file named energyDump$seed_prep.txt within the *output* directory. Lastly, define torsional angle molecular dynamic procedures in an executable script to replace the builtin annealing protocol. If a python script is specified as the last argument of the command, the script will be executed. The script can alternatively be placed inside the project file replacing the annealing data block.


Generating a structure requires specifying the molecular information, restraints and parameters for the rotational dynamics.  This can be done by specifying a YAML file and/or a NEF file.
[YAML](https://en.wikipedia.org/wiki/YAML) files are human readable data files that hava a relatively simple structure without a lot of "fluff".  Project yaml files are described [below](#yamllink).

The protocol used for structure calculation proceeds through a seris of [**stages**](#stagelink).  These stages involve preparation, high temperature dynamics, simulated annealing and low temperature dynamics.  The stages are predefined in code and have specific values for [Parameters](#parameterlink) and [Forces](#forcelink).  The user can adjust any of the parameters in a stage or introduce new stages by adding sections to the [yaml](#yamllink) file.



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

* `nmrfxs predict protein.pdb`

* `nmrfxs predict project.yaml`

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
### Annealing Options (DynOptions)

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


### <a id="forcetermslink">Force Terms</a>

The force terms apply during the calculation of energy values and gradients of the energy during commands such as [gen](#genlink).  Generally, if a force term has a value < 0.0, then that componnet will not be included.

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
