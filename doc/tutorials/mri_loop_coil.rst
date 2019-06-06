MRI Loop Coil
==============================



Preface
-----------------------
     
Covered in this tutorial:

* Setup of a MRI Loop Coil for 7T
* Converting and including a Virtual Family Body Model
* Adding two SAR dump box planes
* Calculate the S-Parameter and input-impedance of the loop coil
* Calculate and plot :math:`B_1^+` and :math:`B_1^-`
* Calculate and plot the SAR distribution



Prerequisites
-----------------------

* make sure you read the :ref:`tutorials primer<tutorials_primer>`

* recommended: some experience with openEMS, e.g. by walking through earlier :ref:`tutorials <tutorials>`

* the "Virtual Family Model" from `here <https://www.itis.ethz.ch/itis-for-health/virtual-population/overview>`_ (note the alternatives mentioned in the instructions below)

* open the tutorial file

  * Matlab/Octave: ``MRI_Loop_Coil.m``

  * Python: ``???.py``
  
  .. todo::
	
	Python script missing


Instructions
-----------------------

This tutorial does not have detailed instructions. Open the tutorial file in Matlab/Octave or Python, and run it.

.. note::
	
	If you don't have access to Matlab (to convert the body model once) or have no access to the virtual family body models, you may want to replace the discrete material with a simple phantom model:
	
	.. code-block:: matlab
	
		CSX = AddMaterial(CSX, 'phantom_head');
		CSX = SetMaterialProperty( CSX,'phantom_head', 'Epsilon', 60, 'Kappa', 0.7, 'Density', 1040);
		CSX = AddSphere(CSX, 'phantom_head', 0, [0 0 0], 110,'Transform',{'Scale',[1 0.8 1]} ); 

.. figure:: images/MRI_Loop_Coil_Setup.png
	:alt: MRI Loop Coil and VF human body model
	:align: center
	:scale: 67%
	
	MRI Loop Coil and VF human body model



Results
-----------------------

.. figure:: images/MRI_Loop_Coil_3D_SAR.png
	:alt: MRI Loop Coil, VF human body model and SAR plot in Paraview
	:align: center
	:scale: 67%
	
	MRI Loop Coil, VF human body model and SAR plot in Paraview

.. figure:: images/MRI_Loop_Coil_B1_xy.png
	:alt: Logarithmic B_1 field distribution on a XY-plane
	:align: center
	:scale: 80%
	
	Logarithmic :math:`B_1` field distribution on a XY-plane

.. figure:: images/MRI_Loop_Coil_B1_xz.png
	:alt: Logarithmic B_1 field distribution on a XZ-plane
	:align: center
	:scale: 80%
	
	Logarithmic :math:`B_1` field distribution on a XZ-plane

.. figure:: images/MRI_Loop_Coil_SAR.png
	:alt: Local SAR distribution on a XY- and XZ-plane
	:align: center
	:scale: 80%
	
	Local SAR distribution on a XY- and XZ-plane



Literature
-----------------

Christ A, Kainz W, Hahn E G, Honegger K, Zefferer M, Neufeld E, Rascher W, Janka R, Bautz W, Chen J, Kiefer B, Schmitt P, Hollenbach H P, Shen J X, Oberle M,Szczerba D, Kam A, Guag J and Kuster N: The Virtual Family – Development of surface­based anatomical models of two adults and two children for dosimetric simulations, Phys. Med. Biol. 55 (2010)
