Helical Antenna
==============================



Preface
-----------------------
     
Covered in this tutorial:

* Setup of a helix using the wire primitive
* Setup a lumped feeding port (:math:`R_{in} = 120 \Omega`)
* Adding a near-field to far-field (nf2ff) box using an efficient subsampling
* Calculate the S-Parameter of the antenna
* Calculate and plot the far-field pattern


Simulation time: ≈ 10 minutes on a contemporary machine, plus ≈ 1 hour for the far field



Prerequisites
-----------------------

* make sure you read the :ref:`tutorials primer<tutorials_primer>`

* recommended: some experience with openEMS, e.g. by walking through earlier :ref:`tutorials <tutorials>`

* open the tutorial file

  * Matlab/Octave: ``Helical_Antenna.m``

  * Python: ``Helical_Antenna.py``



Instructions
-----------------------

This tutorial does not have detailed instructions. Open the tutorial file in Matlab/Octave or Python, and run it.



Results
-----------------------

.. figure:: images/Helical_Antenna_S11.png
	:alt: Antenna return loss
	:align: center
	:scale: 67%
	
	Antenna return loss
	
.. figure:: images/Helical_Antenna_RadPattern.png
	:alt: Antenna structure and radiation pattern
	:align: center
	:scale: 67%
	
	Antenna structure and radiation pattern
