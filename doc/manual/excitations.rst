.. _excitations:

**********************************
Excitations
**********************************

.. todo::
	
	All the arguments explained here have to go away. They are too Octave-specific.
	
openEMS supports a variety of field sources. There are functions to easily define time signals such as a continuous wave sinusoidal signal, as well as Gaussian pulses and completely user defined signals. The shape of the source is defined in the CSX excitation primitive. Both standard sources and total-field/scattered-field type sources are available.



Temporal properties
===============================

The temporal properties of the sources are stored in the FDTD object.



Sinusoidal excitation
---------------------------------

For simulations where a continuous wave is required, a sinusoidal excitation is the method of choice which is simply defined by its frequency.

A sinusoidal excitation is added by

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				FDTD = SetSinusExcite(FDTD, f0)
		
		.. tab:: Python
		
			.. todo::
			
				Python missing

with the parameters

    FDTD
		the original FDTD object of the simulation
    f0
		the frequency of the excitation



Gaussian excitation
---------------------------------

A Gaussian type excitation is needed when simulating the response to a light pulse or the steady state response to a range of frequencies. A Gaussian excitation is a sinusoidal wave with a Gaussian envelope function. It is defined by its its center frequency and the cutoff frequency.

A Gaussian excitation is added by

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				FDTD = SetGaussExcite(FDTD, f0, fc);
		
		.. tab:: Python
		
			.. todo::
			
				Python missing

with the parameters

    FDTD
		the original FDTD object of the simulation
    f0
		the center frequency of the pulse
    fc
		20dB cutoff frequency → bandwidth is :math:`2 \cdot f_C`



Custom excitation
---------------------------------

If a source cannot be described by a continuous wave or a Gaussian pulse one can define a custom excitation. The source can be defined by any function of time.

A custom source is added by

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				FDTD = SetCustomExcite(FDTD, f0, funcStr)
		
		.. tab:: Python
		
			.. todo::
			
				Python missing

with the parameters

    FDTD
		the original FDTD object of the simulation
    f0
		nyquist rate
    funcStr
		string desribing the excitation function :math:`e(t)`



Spatial properties
==============================



Standard excitation
---------------------------------

A standard E-field or H-field excitation is added with the AddExcitation() function. The source has to be assigned to a box primitive which defines its position and size. The standard excitation is added by

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				CSX = AddExcitation(CSX, name, type, excite, varargin)
		
		.. tab:: Python
		
			.. todo::
			
				Python missing

with the parameters

    CSX
		CSX-struct created by InitCSX
    name
		property name for the excitation
    
    type
		can be one of the following:

			* 0 E-field soft excitation
			* 1 E-field hard excitation
			* 2 H-field soft excitation
			* 3 H-field hard excitation
			* 10 plane wave excitation
   
    excite
		e.g. ``[2 0 0]`` for excitation of 2 V/m in X-direction

Additional options for openEMS:

    Delay  : setup an excitation time delay in seconds
    PropDir: direction of plane wave propagation (plane wave excite only)


A hard excitation forces the field at the source points to exactly take the field values of the source, ignoring any other incoming wave e.g. from reflections. For soft sources the field values at source points are the superposition of the defined source and other travelling waves



Total-field/scattered-field excitation
-------------------------------------------------

To create a plane wave excitation in the sense of a total-field/scattered field approach, the AddPlaneWaveExcite() function is used. This type of source is very useful if only the scattered field of an object is of interest. The field from the excitation is confined to the box defined for the source, the scattered field will propagate beyond the box. A plane wave excitation must not intersect with any kind of material. This excitation type can only be applies in air/vacuum and completely surrounding a structure. The plane wave source has to be assigned to a box primitive which defines the position and extend of the field. The excitation is added by

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				function CSX = AddPlaneWaveExcite(CSX, name, k_dir, E_dir, <f0, varargin>)
		
		.. tab:: Python
		
			.. todo::
			
				Python missing

With the parameters

    CSX
		CSX-struct created by InitCSX
    name
		property name for the excitation
    k_dir
		unit vector of wave progation direction
    E_dir
		electric field polarisation vector (must be orthogonal to ``k_dir``)
    f0
		frequency for numerical phase velocity compensation (optional)



Examples
=======================

Add a gaussian pulse as a total-field/scattered-field source:

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				FDTD = SetGaussExcite( obj.FDTD, 0.5*(f_start+f_stop), 0.5*(f_stop-f_start) );
				inc_angle = 0 /180*pi; %incident angle on the x-axis
				k_dir = [cos(inc_angle) sin(inc_angle) 0]; % plane wave direction
				E_dir = [0 0 1]; % plane wave polarization --> E_z
				f0 = 500e6;      % frequency for numerical phase velocity compensation
				  
				CSX = AddPlaneWaveExcite(CSX, 'plane_wave', k_dir, E_dir, f0);
				start = [-100 -100 -100];
				stop = [100 100 100];
				CSX = AddBox(obj.CSX, 'plane_wave', 0, start, stop); % source is in the box defined by start and stop
		
		.. tab:: Python
		
			.. todo::
			
				Python missing

Add a sinusoidal line excitation (short dipole):

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				FDTD = SetSinusExcite(FDTD,f0)
				CSX = AddExcitation( CSX, 'infDipole', 1, [1 0 0] );
				start = [-dipole_length/2, 0, 0];
				stop  = [+dipole_length/2, 0, 0];
				CSX = AddBox( CSX, 'infDipole', 1, start, stop );
		
		.. tab:: Python
		
			.. todo::
			
				Python missing
