---
title: Introduction
taxonomy:
    category: docs
---


If NMR spectroscopy were as simple as UV, IR or most other
spectroscopies the life of an NMR spectroscopist would be much less
interesting. Fortunately, the physics of NMR is such that the
spectroscopist can perform an almost limitless variety of experiments.
Different experiments can be used to tease out different sorts of
information from the molecular system which can ultimately be used to
understand both the structure and dynamics of a molecular system. A
downside of this flexibility is the tremendous amount of data that may
need to be interpreted. A series of experiments on a reasonably
complicated molecule like a protein or nucleic acid can generate
literally gigabytes of data. Furthermore, to interpret these data
requires correlating the information from the multitude of different
experiments. NMRView exists to help the spectroscopist manage and use
this vast quantity of information. Other excellent programs, with
similar goals, exist. Why use NMRView instead of these?

*Useful* NMRView is developed by and for NMR spectroscopists. The
features are those needed by practicing NMR spectroscopists in their
day-to-day work. Of course that doesn't mean that the features we need
coincide exactly with features that every other NMR spectroscopist
needs. On the other hand, many of the features we have added are likely
to be of use to others. We do listen to requests for new features, and
we try to incorporate them as time allows.

*Scriptable* One of the first features requested after the basic version
of NMRView was completed was the ability to automate frequently used
operations. The logical way to accomplish this was by incorporating the
ability to write scripts: lists of instructions for NMRView to carry
out. The best decision made in the development of NMRView was to not
develop a new scripting language. Instead, NMRView incorporates the
scripting language Tcl (Tool Command Language) into NMRView.

With Tcl, NMRView gained not just the ability to automate simple tasks,
but the ability to write complex programs that could be used to carry
out novel analyses. Thus the end-user was to a large extent freed from
the limitations placed on NMRView by the author's limited time. They
could extend it in entirely new directions.

Starting with version 3.0, NMRView incorporated not just the Tcl
language, but its amazing companion, Tk. Tk is a library of Tcl commands
that can be used to create graphical user interfaces (GUIs). With this
version of NMRView, the entire GUI is created using Tk. Thus, not only
can the end-user write new analysis techniques or simple scripts to
automate actions, they could add a GUI to these extensions.

Newer versions (since 9.0) also include Jython, the Java implementation of
Python, and we're gradually expanding the number of operations that 
can be accessed through this scripting language.

*Free* Finally, NMRView is free software, available to anyone who wishes
to use it. This is one way that the developers can contribute to the
overall growth of the technique of NMR.  While the software is free,
we encourage commercial users or academic users with adequate 
grant funding to maintain annual support contracts.

