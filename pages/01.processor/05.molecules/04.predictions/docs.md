---
title: Chemical Shift Prediction 
taxonomy:
    category: docs
---

NMRFx can predict the chemical shifts of proteins, RNA and small molecules. Each of these three molecule types has a specific type of predictor.  The Chemical Shift Predictor GUI is available from the **Predict** menu of the **Atom Table** (display it from the **Molecule** menu).

![Predictor](images/predictor.png)

Predictions are stored with each atom in a **Reference** chemical shift set. Each atom can have more than one prediction.  Use the **Ref Set** choice box to choose which set to store the prediction in (the default is **0**).

Some predictions can be done in more than one way.  You can select the prediction mode with the choice box next to each molecule type.

Protein
: The default mode is to use the three-dimensional structure (**3D**).  NMRFx has a predictor trained on data from the BMRB and uses parameters such as torsion angles and ring-current shifts.  Alternatively you can use the shells method that is normally used for small molecules (**Shells**).

RNA
: The default mode is to use attributes based on the secondary structure.  Every atom is classified by the type of atom, the two bases on each side and their (possible) base-pairing partners (**Attributes**).  You can also use two modes that are based on the three-dimensional structure.  The first (**3D-Dist**) is trained to use the distances to nearby atoms as parameters.  The second (**3D-RC**) exclusively uses ring-current shift calculations.

Small Molecules
: These predictions are done using atoms in surrounding shells (by bond).  This is similar to HOSE code methods.


Ust select the approriate settings as described above and click the Predict button.  You can do a prediction on a molecular assembly that includes protein, RNA and a small molecule.  Each entity will be predicted using the specified method.  The prediction values and error estimates can be seen in the **Ref** and **SDev** columns of the **Atom Table**.  If there are chemical shift assignments for the atoms then there will also be a value in the **Delta** column.  This is the difference between the assignment (in **PPM** column) and the prediction, divided by the prediction error estimate.

![Predictions in Atom Table](images/predtable.png)
