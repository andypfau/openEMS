.. _dumps:

**********************************
Dump Boxes
**********************************

Dump boxes allow to dump fields into VTK or HDF5 files, which can then e.g. be visualized with ParaView.

For a practical example, see e.g. the :ref:`ParaView tutorial <vis_paraview_tut>`.




Adding Dump Boxes
================================

Adding a dump box in openEMS requires two steps:

1. Add a dump property to the CSX structure
	
	Here one defines which fields will be saved and other options such as the file type, interpolation mode, etc.

2. Add a geometrical primitive with the just defined dump property



Add a Dump
---------------------

A field dump is created by

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddDump(CSX, name, varargin)
	
	.. tab:: Python
	
		.. todo::
			
			Python missing

.. note::
	
	The name given to a dump box will be used as filename, or part of a series of filenames (e.g. VTK time domain dump)

The arguments of these methods deserve a bit of explanation:

	DumpType
		Can be one of the following:
			
			* 0: E-field time-domain dump (default)
			* 1: H-field time-domain dump
			* 2: electric current time-domain dump
			* 3: total current density (rot(H)) time-domain dump
			* 10: E-field frequency-domain dump
			* 11: H-field frequency-domain dump
			* 12: electric current frequency-domain dump
			* 13: total current density (rot(H)) frequency-domain dump
			* 20: local SAR frequency-domain dump
			* 21: 1g averaging SAR frequency-domain dump
			* 22: 10g averaging SAR frequency-domain dump
			* 29: raw data needed for SAR calculations (electric field FD, cell volume, conductivity and density)
    
    Frequency
		a frequency vector (required for dump types ≥ 10)

    DumpMode
        * 0: no-interpolation
        * 1: node-interpolation (default; see :ref:`pitfalls <dump_pitfalls>`)
        * 2: cell-interpolation (see :ref:`pitfalls <dump_pitfalls>`)

    FileType
        * 0: VTK-file dump (default)
        * 1: HDF5-file dump

    SubSampling
		Field domain sub-sampling
		
		Example: '2,2,4', which means: dump only every second line in X- and Y- and only every forth line in Z-direction.
    
    OptResolution
		Field domain dump resolution, e.g. '10' or '10,20,5', which means, choose lines to dump in such a way, that they are about 10 (drawing units) apart from another (or e.g. 10 in x-, 20 in y- and 5 in z-direction). This can mean in some area that every line is dumped (as they may be about 10 drawing units or more apart), or maybe only every second, or tenth etc. line to result in an average distance of <10 drawing units apart. The first and last line inside the dump box are always choosen. Note: The dumped lines must not be homogeneous, they only try to be as much as possible. This option may be useful in case of a very inhomogeneous FDTD mesh to create a somewhat more homogeneous field dump.

For more details, refer to the Matlab/Octave or Python reference.



Add a Primitive to the field dump
----------------------------------

The coordinates that are used for the field dump can be defined with a box primitive. Other primitives may be used by their bounding box or result in an invalid field dump. The property name assigned to the box is the name of the field dump defined before.



Examples
=======================

Save the electric field for each time step (i.e. time domain) inside the dump box:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddDump(CSX, 'Et');
			CSX = AddBox(CSX, 'Et', 10, [0 0 0], [100 100 200]);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing



Save the complex field amplitudes at the frequencies 1 GHz and 2 GHz for each point inside the dump box:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddDump(CSX, 'Ef', 'DumpType', 10, 'Frequency', [1e9 2e9]);
			CSX = AddBox(CSX, 'Ef', 10, [0 0 0], [100 100 200]);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing

Save the time-domain magnetic field with sub-sampling:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddDump(CSX, 'Ht', 'Subsampling', '2,2,4', 'DumpType', 1);
			CSX = AddBox(CSX,'Ht', 10, [0 0 0], [100 100 200]);
	
	.. tab:: Python
	
		.. todo::
			
			Python missingb



.. _dump_pitfalls:

Pitfalls
=====================

There are some common FDTD interpolation abnormalities:

No-Interpolation:
	Recall that fields are located on the edges of the Yee-cell (FDTD), and the dumped mesh only specifies E- or H-Yee-nodes.
	
	Be aware of the offset, or use node- or cell-interpolation

E-/J-Field Dump and Node-Interpolation:
	Normal electric fields on boundaries will have false amplitude due to forward/backward interpolation in case of (strong) changes in material permittivity, or on metal surfaces
	
	If this poses a problem, use no- or cell-interpolation in this case

H-Field Dump and Cell-Interpolation
	Normal magnetic fields on boundaries will have false amplitude due to forward/backward interpolation in case of (strong) changes in material permeability
 
	If this poses a problem, use no- or node-interpolation
