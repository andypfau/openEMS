Spherical Shell
----------------------------

.. todo::

	Migrate from <http://openems.de/index.php/Spherical_Shell.html>



Description

The spherical shell primitive is defined by its central point, radius and thickness. It is created with

 CSX = AddSphericalShell(CSX, propName, prio, center, rad, shell_width, varargin)

with the following parameters:

    CSX: The original CSX structure
    propName: name of the assigned property
    prio: priority of the primitive
    center: coordinate of the center point of the sphere
    rad: radius of the spherical shell
    shell_width: thickness of the shell
	
	* the inner radius of this shell is rad-shell_width/2
	* the outer radius of this shell is rad+shell_width/2
    
    varargin: a key/value list of primitives variable arguments

Example

    Create a metal sphere at (0,0,0) with radius 50 and thickness 10:

CSX = AddMetal(CSX,'metal'); %create PEC with propName 'metal'
CSX = AddSphericalShell(CSX,'metal',10,[0 0 0],50,10);

Sphere.png
