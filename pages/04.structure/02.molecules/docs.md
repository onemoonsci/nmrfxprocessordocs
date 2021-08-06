---
title: Molecular Topology
taxonomy:
    category: docs
---
## Template Library

When generating a molecular structure in NMRFx by reading in a
sequence file it is necessary to translate the residue names into the
set of atoms and bonds that define the molecular topology. To do this,
NMRFx, looks at each residue name in the sequence file, and checks to
see if a file corresponding to that name with a ".prf" extension can be located.

NMRFx looks in two places for these files.  First, if a local residue library
directory has been set, it looks there.  Local residue libraries are specified
in the NMRFx Analyst GUI in the Preferences dialog (Structure section). In 
NMRFx Structure the location is specied in the project .yaml file as 
a "reslib" entry.  For example:

    molecule :
      reslib  :  reslib
    
      entities :
          - file : input/A.seq
            ptype : protein

If a local residue library is not specified, or the file is not found
there, then the built-in residue library is searched.


### PRF Files

If a residue file is found, that file is scanned to extract the topology
for that residue. NMRFx works with residues using an internal
coordinate system, where the molecular topology is determined by a
tree-like structure starting from the first atom in the structure. To
properly define the structure then, it is necessary to provide values
for the valance angles, dihedral angles, bond distances and
connectivity. Most of this information is defined in the ATOM and FAMILY
records. The .prf files, which are derived from information originally
published by Robson & Osguthorpe (J. Mol. Biol. 132:19-51) are described
below. Our original use of .prf files was in our structure calculation
program, PEGASUS (Johnson & Sugg, Biochem., 1992, 31,8151-8159). 

    LNAME Serine
    SNAME ser
    RCHAR S
    ATOM   N      N     1.32  114.00  -120.0  -0.41570
    ATOM   H      H     1.00  123.00  0.0     0.27190 middle
    ATOM   H      H     1.00  123.00  0.0     0.27190 end
    ATOM   H1     H1    1.08  109.00  60.0    0.27190 start
    ATOM   H2     H2    1.08  109.00  60.0    0.27190 start
    ATOM   H3     H3    1.08  109.00  60.0    0.27190 start
    ATOM   CA     CX    1.47  123.00  180.0   -0.02490
    ATOM   HA     H1    1.08  109.47  -120.0  0.08430
    ATOM   CB     2C    1.53  109.47  -121.5  0.21170
    ATOM   HB2    H1    1.08  109.47  -120.0  0.03520
    ATOM   HB3    H1    1.08  109.47  -120.0  0.03520
    ATOM   OG     OH    1.42  109.47  0.0     -0.65460
    ATOM   HG     HO    1.00  110.00  0.0     0.42750
    ATOM   C      C     1.53  109.47  120.0   0.59730
    ATOM   O      O     1.24  121.00  180.0   -0.56790 start
    ATOM   O      O     1.24  121.00  180.0   -0.56790 middle
    ATOM   O      O     1.24  180.00  120.0   -0.56790 end
    ATOM   OXT    OH    1.24  180.00  120.0   -0.56790 end
    FAMILY   -      N      H      CA    middle
    FAMILY   -      N      H      CA    end
    FAMILY   -      N      H1     H2     H3    CA    start
    FAMILY   N      CA     C      CB     HA
    FAMILY   CA     CB     OG     HB3    HB2
    FAMILY   CB     OG     HG
    FAMILY   CA     C      +      =O
    FAMILY   CA     C      OXT    =O  end
    ANGLE     CA      PHI 1
    ANGLE     CB     CHI1 2
    ANGLE     OG     CHI2 6
    ANGLE     C       PSI 1
    ATREE  CA  CB  C
    ATREE  CB  OG
    ATREE  OG
    ATREE  C  +
    PSEUDO QB HB2 HB3
    CRAD CA   4.0
                

**LNAME**

:   Full name of residue. Unused at present.

**SNAME**

:   Short name of residue. Unused at present.

**RCHAR**

:   Single letter name of residue. Unused at present.

**ATOM**

:   Properties of the atoms in the residue. There should be one line for
    each atom. The line is composed of at least 8 fields separated by white space
    (spaces or tabs).

    1.  Atom name

    2.  Atom type, these are currently specified as atom types as used in the AMBER force field 
        The type is used for getting atomic number and non-bond contact parameters 
        when doing structure calculations.

    3.  Bond length, from this atom to the previous atom in the tree
        structure of the residue (as defined in the FAMILY lines).

    4.  Valance Angle, between this atom, its parent, and grandparent,
        as defined in the tree structure of the molecule.

    5.  Torsion Angle, between this atom, its parent, grandparent, and
        great grandparent (as defined in the tree structure of the
        molecule). The angle for the first "child" atom bonded to a
        given parent, as defined in the FAMILY lines, is an absolute
        torsion angle. The angles for subsequent atoms are relative to
        the previously defined dihedral.

    6.  Charges.  These are currently taken from AMBER parameter files.

    7.  Position specifiers.  These optional flags specify atoms that are only present 
        when the residue is at a particular position in the sequence.  Atoms without 
        a specifier are always present.
           * start: only present for first residue
           * middle: only present for residues that are not the first or last residue
           * end: only present for last residue
        
	

**FAMILY**

:   Defines the tree structure of the residue. Each line can be
    considered of the form

    "**FAMILY parentAtom thisAtom childAtom1 childAtom2...**".

    For example, a line like, "**FAMILY N CA C CB HA**", implies that
    the atom **CA**, is bonded to the **N** atom (the parent of **CA**
    is **N**), and it has three children, C, CB and HA. If the parent is
    specified as "-", then it is a connector atom in the previous
    residue. If a child is specified as "+", then it is the connector
    atom in the subsequent residue. Child atom names preceded with a
    "-", like**-CD2** imply that this child atom will actually be
    defined in the tree structure in some other FAMILY entry in the
    structure, but that there should be a bond drawn between this child
    atom and the main atom of this FAMILY line. This is used to define
    bonds that close rings.

**ANGLE**

:   Each rotatable bond in the residue has an ANGLE entry.

    1.  The rotatable bond is that between the specified atom and its
        parent.

    2.  The name of the angle (PHI, PSI, CHI etc.)

    3.  A number indicating an entry in the file irp.def, which gives
        energy parameters for the intrinsic rotation potential for this
        atom. Only used in structure calculations.

**ATREE**

:   One entry for each rotatable bond. The order in which they are
    specified gives the tree of rotation groups.

**PSEUDO**

:   Mapping of actual atoms in structure to pseudo atom names, "**PSEUDO
    pseudoAtomName atom1 atom2 ...**". The pseudo atom position would be
    at the geometric mean of all the actual atoms that are listed. At
    present this is only used when reading in constraint files using
    pseudo atom names (like CYANA .upl files) and is used to translate
    the pseudo atom name into the set of actual atoms stored in the
    molecular structure.

**CRAD**

:   This specifies the name of an atom near the center of the residue
    and the approximate radius of a sphere around the central atom that
    would encompass all atoms of the residue. Used for accelerating
    calculation of non-bond contact list. Unused at present in NMRFx.

### PDB or Mol Files

Residue files can also be specified with .pdb or .mol files if they
are located in local residue libraries. Residue files stored
as .pdb or .mol files do not have information, as the .prf files do, on
how to make connections to the preceding and succeeding residues.
The sequence file should contain -entry and -exit lines
before the residue name.  For example,
   leu
   -entry C1
   -exit C8
   phq

These lines specify the names of atoms in the residue that are used to make the
 connection to the adjacent residues.
**Note**: this is an experimental feature, and may be subject to changes and require bug fixes.
Please contact us for more information.

