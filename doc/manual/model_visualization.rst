**********************************
Model Visualization
**********************************

Prior to running the openEMS FDTD simulation it is important to visualize the model to ensure that it is correct. There are two ways to view the model. First, the solid model can be viewed with the CSXGeomPlot command which is placed after writing the model to a file and before running openEMS like this:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
			
			WriteOpenEMS([Sim_Path '/' Sim_CSX], FDTD, CSX);
			CSXGeomPlot([Sim_Path '/' Sim_CSX]);
			RunOpenEMS(Sim_Path, Sim_CSX);	
			
	.. tab:: Python
	
		.. todo::
			
			Python missing


A viewer will pop up and the solid model can be rotated and components be made visible or invisible. Sources, excitations, and field measurement planes can be viewed as well. Although the mesh grid is visible in the background, the structure has not been gridded yet.

The second type of visualization is to look at the meshed structure. This is done by passing options to the RunOpenEMS command which tells it to dump the gridded structure to a file and not to execute the FDTD simulation:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
			
			openEMS_opts = '--debug-PEC --no-simulation';
			RunOpenEMS(Sim_Path, Sim_CSX, openEMS_opts);
			
	.. tab:: Python
	
		.. todo::
			
			Python missing

A file with the name PEC_dump.vtp is created in the local tmp directory. This file is opened with the ParaView client which will show whether or not the structure has been gridded correctly and if the mesh needs to be adjusted. Note that only PEC structures will be shown with this program.

Have a look into the :ref:`ParaView visualization tutorial <vis_paraview_tut>` for more details.
