.. _install_matlaboctave:

********************************
Matlab/Octave Interface
********************************

Instructions on how to install the CSXCAD and openEMS Matlab/Octave interface.

1. Make sure CSXCAD and openEMS was build and installed correctly (:ref:`see here <install_openems>`)

2. Install Matlab or Octave (this is beyond the scope of this documentation)

3. Find the matlab script folders for CSXCAD and openEMS in your openEMS installation, and remember them for later

	* CSXCAD: should be in a subfolder ``share/CSXCAD/matlab`` below your openEMS installation path
	
	* openEMS: should be in a subfolder ``share/openEMS/matlab`` below your openEMS installation path

4. Open the configuration file for Matlab/Octave:

	* Matlab: there should be a ``startup.m`` in your Matlab startup folder; otherwise, create it

	* Octave under Linux: there should be a file ``~/.octaverc``; otherwise, create it

	* Octave under Windows: **TODO**

5. In that file, add the script paths for CSXCAD and for openEMS to the search path of Octave/Matlab

	* use the the Matlab/Octave command ``addpath(path);``

	* Example:

		.. code-block:: matlab


			addpath('~/opt/openEMS/share/CSXCAD/matlab')
			addpath('~/opt/openEMS/share/openEMS/matlab')
	
	* Alternative possibilities for advanced users or developers:
		
		* if you installed *hyp2mat* or the *circuit toolbox*, add them as well (``share/hyp2mat/matlab``, ``share/CTB/matlab``)

6. :ref:`Verify your installation <first_steps_tut>`
