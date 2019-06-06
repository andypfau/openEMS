.. _troubleshooting:

**********************************
Troubleshooting
**********************************

openEMS warns about an unused property or primitive. What does it mean?
	It means that you placed a primitive (e.g. a box), but openEMS didn't use it. It may have one of the following reasons:
	
	* Usually this points to an error in the mesh. E.g. if you create a 2D metal plane but have no mesh line at the plane level
	* Your primitive may be shadowed by some other primitive with a higher priority
	* Maybe you defined a property without any primitive assigned to it
	
	Also have a look into :ref:`the meshing article <meshing>`.

My timestep seems to be very small, and the simulation takes a long time. Why?
	A (very) small timestep usually means that the mesh contains one or more cells that are very small. The timestep is defined by the smallest cell.
	
	In most cases you should check if you can avoid small cells.
	
	If you really need small cells (e.g. to resolve some important feature of your structure) you will have to live with long execution times, or perhaps FDTD is not the right method for your problem.

Why is the energy going up and down during the simulation?
	Until the excitation is finished the energy will go up and down, depending on how much energy is lost (e.g. through open boundaries or heating losses), and how much energy is fed in by the excitation.
	
	After the excitation is done, the energy should only decay.
	
	Note that the calculation of the energy is only a rough estimation (to be fast), e.g. it will completely neglect materials etc. That means that the energy temporarily even may go up again after the excitation is gone because of that estimation not being a correct energy calculation.

Why does the energy not decay after the excitation is done?
	This might happen e.g. if you place an element inside a boundary condition. A common pitfall is to place a port inside a PML_x, because the PML extends inside the mesh.
	
	Also have a look into :ref:`the boundary conditions article <boundarycond>`.

How can I debug PECs (perfect electrical conductors?
	Add two options to the RunOpenEMS command in your script:

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
			  debug_options = '--debug-PEC --no-simulation';
			  RunOpenEMS(Sim_Path, Sim_CSX, debug_options);
		
		.. tab:: Python
		
			.. todo::
				
				Python missing
				

	This tells openEMS to dump the PECs into the file "PEC_dump.vtp" in the simulation folder, then stop.

	Now open Paraview to visualize the generated file. All PEC edges as detected by openEMS will be shown.

	.. note::
		
		FDTD represents planes or volumes of metal by a metal mesh, with all mesh lines being PEC
	
	.. figure:: images/Helical_antenna_gridding.png
		:alt: Example of gridding using the helical antenna from tutorials.
		:align: center
		:scale: 67%
		
		Example of gridding using the helical antenna from tutorials.
