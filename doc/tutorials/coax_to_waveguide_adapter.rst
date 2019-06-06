Coax to Waveguide Adapter
==============================



Preface
-----------------------
     
Covered in this tutorial:

* Setup of the FDTD parameters for waveguide
* Setup of the inhomogeneous FDTD mesh
* Devices with ports with different characteristic impedance
* Visualizing the Electric field in the time domain with Matlab


Simulation time: ≈ 5 minutes on a contemporary machine



Prerequisites
-----------------------

* make sure you read the :ref:`tutorials primer<tutorials_primer>`

* open the tutorial file

  * Matlab/Octave: ``???.m``

  * Python: ``???.py``

.. todo::
	
	Files missing



Instructions
-----------------------

This tutorial uses the same layout as the other tutorials. Only the key points to be illustrated will be covered here.

Excitation Setup
^^^^^^^^^^^^^^^^^^^^^^^^

In FDTD there is a conflict between using a wide frequency band pulse and the cutoff frequency of the waveguide. In FDTD, we prefer to use a wide frequency band pulse to study a broad range of frequencies and to shorten the simulation time. Waveguide has a cutoff frequency below which the wave will not propagate. In this example using WR-75 waveguide, the cutoff frequency is 7.87 GHz. The standard operating band is 10 to 15 GHz, which is not that far from the cutoff frequency. The only choice to study frequencies down to 10 GHz is to use a narrow frequency band of 10 to 15 GHz. Using 10 to 20 GHz is too wide, resulting in frequencies below cutoff frequency. The end result is the energy never decays out of the system and the post processing results are garbage. Simply using the standard operating band for the standard waveguide sizes with the code below will produce good results.

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				f_start = 10e9;    
				f_stop  = 15e9;   
				TE_mode = 'TE10';
				 
				%% setup FDTD parameter & excitation function %%%%%%%%%%%%%%%%%%%%%%%%%%%%%
				FDTD = InitFDTD('NrTS',NumTS,'EndCriteria', 1e-5); 
				FDTD = SetGaussExcite(FDTD,.5*(f_stop+f_start),.5*(f_stop-f_start));
		
		.. tab:: Python
		
			.. todo::
			
				Python missing



Grid Setup
^^^^^^^^^^^^^^^^^^^^^^^^

Other simulation techniques, such as finite elements, allow use of tetrahedral polygons to exactly represent curved surfaces. In FDTD, only rectangular cells are permitted. This forces use of a finer mesh to model curved surface regions in order to reduce the stair-casing effect caused by discretizing the curved surface into a rectangular grid. Unfortunately this smaller cell size causes longer simulation time. On the other hand, the total number of cells can be greatly reduced because FDTD allows a non homogeneous grid. The restriction is that neighboring cells cannot vary in dimension more than a factor of 2. The SmoothLines2 function is used to produce the locally dense mesh as well as gradually transition from the small cell size to the regular cell size of the problem. In this example, the neighbor cell dimension transition factor is set to 1.3

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				mesh_res = [.007 .01 .007];
				 
				mesh.x = SmoothMeshLines2( [a/2-OuterCondODSMA/2 a/2-InnerCondSMA/2 a/2+InnerCondSMA/2 a/2+OuterCondODSMA/2],mesh_res(1)/3,1.3);
				mesh.x = SmoothMeshLines([0 mesh.x a], mesh_res(1),1.3);
				 
				mesh.y = SmoothMeshLines2([b-ProbeDepth b b+WallThickness],mesh_res(2)/2,1.3);
				mesh.y = SmoothMeshLines([0 mesh.y b+WallThickness+SMALength], mesh_res(2));
				 
				mesh.z = SmoothMeshLines2([length-BackShort-OuterCondODSMA/2 length-BackShort-InnerCondSMA/2 length-BackShort+InnerCondSMA/2,length-BackShort+OuterCondODSMA/2],mesh_res(3)/3,1.3);
				mesh.z = SmoothMeshLines([0 mesh.z length], mesh_res(3));
		
		.. tab:: Python
		
			.. todo::
			
				Python missing



Post-Processing
^^^^^^^^^^^^^^^^^^^^^^^^

This is the key problem that is illustrated in this tutorial. In this example, the coax portion has a constant impedance of 50 ohms. However, the waveguide characteristic impedance is a function of frequency and it is typically a few hundred ohms. This presents a problem in the calculation of S21 because both ports do not have the same impedance. In the example, port 1 is the coax port and port 2 is the waveguide port. The calculation of S11 is standard. However, to the standard S21 calculation (port{2}.uf.ref./port{1}.uf.inc)a front multiplication factor is added which is the square root of the ratio of the characteristic impedances at each frequency of each port). After simulation, you will notice that the S21 is about 0.1 dB even though this is set up as a lossless device. This is due to discretization errors of the coaxial structure in the rectangular grid which cause the impedance of the coax port to be about 50.7 ohms instead of 50 ohms.

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				s11 = port{1}.uf.ref./ port{1}.uf.inc;
				s21 = sqrt(real(port{1}.ZL_ref)./port{2}.ZL_ref).*port{2}.uf.ref./port{1}.uf.inc;
		
		.. tab:: Python
		
			.. todo::
			
				Python missing



Visualization
^^^^^^^^^^^^^^^^^^^^^^^^

This is a great tool for debugging problems that may have occured in the simulation, for example, if the absorbing and PEC boundaries were accidently switched, you can see this by looking at the movie of the E field in the time domain.

The following code snippet is the set up before the simulation engine is run. SubSampling '4,4,4' indicates that only every 4th value is saved to the file in order to save disk space.

	.. tabs::
		
		.. tab:: Matlab/Octave
			
			.. code-block:: matlab
			  
				%% define dump box...
				CSX = AddDump(CSX,'Et','FileType',1,'SubSampling','4,4,4');
				start = [mesh.x(1)   mesh.y(1)   mesh.z(1)];
				stop  = [mesh.x(end) mesh.y(end) mesh.z(end)];

				The following code snippet is in the post processing section and is where the move is actually displayed. PlotArgs.slice is where the x, y, and z planes are positioned to display the electric field. In this example, the x and y planes are placed in the midle of the waveguide.

				%% Plot the field dumps 
				figure
				dump_file = [Sim_Path '/Et.h5'];
				PlotArgs.slice = {a/2*unit (b/2)*unit (.05)*unit};
				PlotArgs.pauseTime=0.01;
				PlotArgs.component=0;
				PlotArgs.Limit = 'auto';
				PlotHDF5FieldData(dump_file, PlotArgs);

		
		.. tab:: Python
		
			.. todo::
			
				Python missing
