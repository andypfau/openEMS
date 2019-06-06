#####################################
Appendix
#####################################


.. _how_to_reference:

**********************************
Reference
**********************************

We kindly ask you to reference openEMS in any publication that you were using openEMS for:

	BibTex:
	
	
	.. code-block:: bibtex

		@ELECTRONIC{openEMS,
		  author = {Thorsten Liebig},
		  title = {openEMS - Open Electromagnetic Field Solver},
		  organization = {General and Theoretical Electrical Engineering (ATE), University of Duisburg-Essen},
		  url = {https://www.openEMS.de}
		}



.. _publications:

**********************************
Publications
**********************************

This is a collection of publications referencing openEMS. Feel free to send an email to include a reference (and link) to your publication.

2012
==============================

* T. Liebig, A. Rennings, S. Held, and D. Erni, "openEMS - A free and open source equivalent-circuit (EC) FDTD simulation platform supporting cylindrical coordinates suitable for the analysis of traveling wave MRI applications," International Journal of Numerical Modelling: Electronic Networks, Devices and Fields, online, `DOI: 10.1002/jnm.1875 <https://dx.doi.org/10.1002/jnm.1875>`_, Dec. 10, 2012. `JNM_2012_Liebig_Online.pdf <https://www.ate.uni-due.de/data/dokumente_2012/JNM_2012_Liebig_Online.pdf>`_ (*requires Universität Duisburg Essen login*)

* T. Liebig, A. Rennings, and D. Erni, "openEMS - A free and open source FDTD software package supporting Cartesian and cylindrical coordinates ideally suited for MRI applications," Magnetic Resonance in Physics, Biology and Medicine (MAGMA), vol. 25, no. suppl 1, pp. 627-628, Oct. 2012, special supplement on Europ. Soc. for Magn. Reson. in Med. and Biol. 29th Annual Sci. Meeting (ESMRMB 2012), Oct. 4-6, Lisbon, Portugal, paper 857 (demo and poster), 2012. `ESMRMB_2012_Liebig.pdf <https://www.ate.uni-due.de/data/dokumente_2012/ESMRMB_2012_Liebig.pdf>`_ (*requires Universität Duisburg Essen login*)

* T. Liebig, A. Rennings, and D. Erni, "openEMS – A Free and Open Source Cartesian and Cylindrical EC-FDTD Simulation Platform Supporting Multi-Pole Drude/Lorentz Dispersive Material Models for Plasmonic Nanostructures," 8th Workshop on Numerical Methods for Optical Nano Structures (organized by OptETH and the Fred Tischer Lecture Series), July 2-4, ETH Zurich, Session on Metamaterials, Periodic Structures, and Numerical Methods I, Switzerland, 2012. `ETH_Workshop_2012_Liebig.pdf <https://www.ate.uni-due.de/data/dokumente_2012/ETH_Workshop_2012_Liebig.pdf>`_ (*requires Universität Duisburg Essen login*)



2011
==============================

* T. Liebig, D. Erni, A. Rennings, N. H. L. Koster, and J. Fröhlich, "**MetaBore - A fully adaptive RF field control scheme based on conformal metamaterial ring antennas for high-field traveling-wave MRI**," Magnetic Resonance in Physics, Biology and Medecine (MAGMA), vol. 24, no. suppl 1, pp. 37-38, special supplement on the Europ. Soc. for Magn. Reson. in Med. and Biol. 28th Annual Sci. Meeting (ESMRMB 2011), paper 49 (talk and poster), pp. 22, Oct. 6-8, Leipzig, Germany, 2011. `ESMRMB_2011_Liebig.pdf <https://www.ate.uni-due.de/data/dokumente_2011/ESMRMB_2011_Liebig.pdf>`_ (*requires Universität Duisburg Essen login*)

* D. Erni, T. Liebig, A. Rennings, N. H. L. Koster, and J. Fröhlich, "Highly adaptive RF excitation scheme based on conformal resonant CRLH metamaterial ring antennas for 7-Tesla traveling-wave magnetic resonance imaging," 33th Annual Intern. Conf. of the IEEE Engineering in Medicine and Biology Soc. (IEEE EMBS 2011), Aug. 30 - Sept. 3, Boston, MA, USA, pp. 554-558, 2011. `EMBC_2011_Erni.pdf <https://www.ate.uni-due.de/data/dokumente_2011/EMBC_2011_Erni.pdf>`_ (*requires Universität Duisburg Essen login*)


**********************************
Migration from Wiki
**********************************

.. warning::
	
	This section must be manually updated!

Pending/Ongoing
==================

* Basics
	
	* NF2FF
	* Introduction
	* Primitives
	* Remote SSH
	* Ports
	* Overview
	* ReadUI

* Geometry

	* Ellipsoid primitive
	* AddDiscMaterial
	* Box
	* CalcPort
	* Curve
	* Cylinder
	* Cylindrical Shell
	* Metal sheet with cylindrical holes
	* Polygon
	* Polyhedron
	* Sphere
	* Sphere Aggregation
	* Spherical Shell
	* Wire



Done
==================

Note that in most cases Python code is still missing. I mainly ported everything.

* openEMS                                    --> this is the start page; skipped "about", as it is redundant with "Features"
* FDTD Boundary Conditions                   --> complete
* Publications                               --> complete
* OpenEMS                                    --> complete
* Compile from Source                        --> merged into existing documents
* Tutorial: First Steps                      --> complete
* Tutorials                                  --> complete
* Tutorial: Microstrip Notch Filter          --> complete
* FDTD Mesh                                  --> some TODOs are open
* Tutorial: Parallel Plate Waveguide         --> complete
* Tutorial: Helical Antenna                  --> complete
* Tutorial: Horn Antenna                     --> complete
* Tutorial: Metal Sphere Radar Cross Section --> complete
* Tutorial: UWB Radar                        --> complete
* Tutorial: Patch Antenna Phased Array       --> complete
* Tutorial: MRI LP Birdcage                  --> complete
* Tutorial: MRI Loop Coil                    --> complete
* Tutorial: Dipole SAR                       --> complete
* Material Property                          --> complete
* Metal Property                             --> complete
* Dispersive Material Property               --> complete
* Model Visualization                        --> complete
* Visualization of Results                   --> complete
* Dump Box Property                          --> complete
* Probe Box Property                         --> complete
* Properties                                 --> complete
* Frequently Asked Questions                 --> complete, re-organized with troubleshooting
* Troubleshooting                            --> complete, re-organized with FAQ
* Tutorial: 2D Cylindrical Wave              --> complete
* Tutorial: Bent Patch Antenna               --> complete
* Tutorial: Circular Waveguide               --> complete
* Tutorial: Coax to Waveguide Adapter        --> complete
* Tutorial: Conical Horn Antenna             --> complete
* Tutorial: CRLH Leaky Wave Antenna          --> complete
* Tutorial: CRLH Parameter Extraction        --> complete
* Tutorial: Importing with hyp2mat           --> complete
* Tutorial: Rectangular Waveguide            --> complete
* Tutorial: Stripline to MSL Transition      --> complete
* Tutorial: Simple Patch Antenna             --> complete
* Excitation                                 --> complete



Skipped
==================

* OpenEMS pt                                 --> do we really want to maintain Portuguese?
* Mickey                                     --> low-prio
* Binaries                                   --> are the binaries maintained at all?
* List of Functions                          --> will hopefully be done by auto-doc
* Paraview                                   --> has no real content, is covered better by the tutorial
* Examples                                   --> has no real content, is covered better by the tutorial
* CSXCAD                                     --> not needed any more, according to Thorsten
* AppCSXCAD                                  --> has no real useful content in the context of openEMS...



**********************************
Open TODOs in Documentation
**********************************

Automatically generated TODO-List:

.. todolist::
