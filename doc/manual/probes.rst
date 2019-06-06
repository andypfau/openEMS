.. _probess:

**********************************
Probe Boxes
**********************************

Probe boxes allow to record voltages, currents, field strengths, or waveguide mode amplitudes at certain points in space.



Files
============

If there is only one primitive, a text file with the name of the property is written. If there are several primitives, they are numbered consecutively and files named "propertyName_n" are written, where *n* is the number of the primitive. The text file can later be read with ``ReadUI`` in the case of voltages or currents when the openEMS job has finished.

.. todo::
	
	What's the Python command?

When a frequency array is provided via the Frequency key, a text file "propertyName_FD" is also written. This file contains the Fourier-transformed quantity at the given frequencies.



Adding Probe Boxes
================================

Adding a probe box in openEMS requires two steps:

1. Add a probe property to the CSX structure
	
	Here one defines which fields will be saved and other options such as the file type, interpolation mode, etc.

2. Add a geometrical primitive with the just defined probe property



Add a Dump
---------------------

A field dump is created by

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			% voltage probe
			CSX = AddProbe(CSX, 'ut1', 0);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing



Primitives
---------------------

The appropriate primitive depends on the observable to be recorded. For a (non-retarded?) voltage, a straigt line (e.g. an AddWire with two end points and zero radius) would be appropriate. The result will be the voltage between those two end poins. For a current probe, a two-dimensional shape is appropriate (e.g. an AddBox with zero extent in one dimension.

Field quantities (*E* and *H*) can also be read with ReadUI. However, in this case the structure delivered by ReadUI needs to be treated specially because these are vectors. For those quantities only the start coordinate of the primitive (e.g. a box) is used for the definition of the location of the probe.

.. todo::
	
	Again, this was only written with Python in mind

.. todo::
	
	Can we provide an example?
