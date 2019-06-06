**********************************
Frequently Asked Questions
**********************************

How can I create a "hole" in a structure?
	Use the priority system: Primitives#Priorities
	
	.. todo::
		
		Reference missing

How can I create polygons out of a Gerber- or DXF-file from PCB layout software?
	The common way of generating polygons out of PCB structures (e.g. antennas) is using :ref:`hyp2mat <tut_hyp2mat>`. However, sometimes the HyperLynX export of commercial software suites is somehow awkward or clumsy. On the other hand there is no open source PCB layout software that can export HyperLynx. Therefore, a way to obtain polygons from Gerber or DXF files is described in the following. These file types can be exported from almost any PCB layout software.

	PCB layers in Gerber files can be converted to PDF by means of gerber2pdf which can be found on Sourceforge. The PDF can be imported into inkscape just as it is the case for DXF files. Within inkscape, the usually closed paths can be modified (either manually or with filters) such that they result in a suitable list of polygon nodes for openEMS.

	Sometimes these polygons or curves have too many nodes. The number of nodes can be reduced with the inkscape function "Path" > "Simplify". The amount of reduction is controlled by the parameter "Simplification Threshold" which can be found under "Preferences" > "Behavior". These paths are still Bézier curves which must be converted into polygons. This is achieved with "Extensions" > "Modify Path" > "Flatten Béziers". The parameter in this dialog also controls the number of resulting points.

	When all nodes are as required, the paths can be exported as a HTML5 Canvas. The resulting file can then be processed with an ASCII Editor. The numbers after the moveTo and lineTo statements are the polygon nodes X- and Y- coordinates respectively. However, they still must be transformed ba a liner transform given in the transform statement. The first four numbers a matrix by which the node coordinates have to be multiplied and the remaining two numbers are a vector which has to be added.

	The result will be the node coordinates in HTML pixels with X counting from left to right and Y counting from top to bottom, which does not conform to the coordinate system of the inkscape canvas.

	In order to have the same axes as in inkscape (X left to right and Y bottom to top), the fourth an sixth number have to be multiplied by -1 and the image height has to be added to the sixth number. Now the coordinates are in the usual coordinate system but still in HTML5 pixels. The ratio of pixels to mm or other units of length can finally be found under the document properties in inkscape. This factor can be applied in Octave/Matlab. This finally gives polygons which can be processed by openEMS.

How can I abort the simulation without losing my data/post-processing?
	Create a file called "ABORT" inside the simulation folder, and openEMS will stop the simulation cleanly (including all post-processing) at the next interval. The name has to be all capital letters (except if your OS is case-insensitive, such as Windows), with no extension (such as ".txt"), and can be an empty file.
