.. _tutorials:

#####################################
Tutorials
#####################################



.. _tutorials_primer:

**********************************
Before You Start
**********************************

1. Note that the scripts for the tutorials come with your :ref:`openEMS installation <install>`:

	* Windows:

		* Matlab/Octave: ``installation_path\matlab\Tutorials\``
		* Python: ``installation_path\python\Tutorials\``
		
	* Linux:

		* Matlab/Octave: ``installation_path/matlab/Tutorials/``
		* Python: ``installation_path/python/Tutorials/``

	.. todo::
		
		What's the real location for Python? I had to guess here
	
	Note that the installation path was provided by the user during :doc:`installation <../installation/index>`. For example, if you installed openEMS under Linux into ``/opt/openEMS``, the Matlab tutorial files should be in ``/opt/openEMS/matlab/Tutorials``.

2. If you run into any trouble, consult the :doc:`manual <../manual/index>` and/or the :doc:`troubleshooting guide <../manual/troubleshooting>`

3. It is recommended to start with the :doc:`first steps tutorial <first_steps>`



.. _intro_tuts:

**********************************
Introductional Tutorials
**********************************

.. toctree::
	:maxdepth: 1

	first_steps
	parallel_plate_waveguide
	visualization_paraview
	rectangular_waveguide
	circular_waveguide
	2d_cylindrical_waveguide
	metal_sphere_radar_cross_section
	importing_with_hyp2mat



**********************************
Planar Microwave Structures
**********************************

.. toctree::
	:maxdepth: 1

	msl_notch_filter
	crlh_parameter_extraction
	coax_to_waveguide_adapter
	stripline_to_msl_transition



**********************************
Antennas
**********************************

.. toctree::
	:maxdepth: 1

	simple_patch_antenna
	horn_antenna
	conical_horn_antenna
	crlh_leaky_wave_antenna
	helical_antenna
	bent_patch_antenna



**********************************
Advanced Topics
**********************************
.. toctree::
	:maxdepth: 1

	dipole_sar
	mri_loop_coil
	mri_lp_birdcage
	patch_antenna_phased_array
	uwb_radar



.. _tutorials_examples:

**********************************
Further Examples
**********************************

Some additional examples are also installed to your hard disk:

	* Windows:

		* Matlab/Octave: ``installation_path\matlab\examples\``
		* Python: ``installation_path\python\examples\``
		
	* Linux:

		* Matlab/Octave: ``installation_path/matlab/examples/``
		* Python: ``installation_path/python/examples/``
