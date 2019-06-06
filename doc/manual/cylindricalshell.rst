Cylindrical Shell
----------------------------

.. todo::

	Migrate from <http://openems.de/index.php/Cylindrical_Shell.html>



Description

A cylindrical shell is created by the command:

CSX = AddCylindricalShell(CSX, propName, prio, start, stop, rad, shell_width, varargin)

with the following parameters:

    CSX: default first argument, containing the CSXCAD data structure
    propName: name of the (previously defined) property (e.g. a metal or material)
    start, stop: [x y z] coordinates of the start and end points of the cylinder central axis
    rad: radius of the cylinder
    shell_width: width of the cylinder shell
    varargin: a key/value list of primitives variable arguments

Note:

    The inner radius of this shell is: rad – shell_width/2
    The outer radius of this shell is: rad + shell_width/2

See also

Box, Sphere, Cylinder

Example

    Create a cylindrical shell with radius 30 drawing unit and shell thickness of 5 drawing unit .

CSX=AddMaterial(CSX,'plexi_shield');
CSX=SetMaterialProperty(CSX,'plexi_shield','Epsilon',2.22);
start=[0 0 -40 ];
stop=[0 0 40 ];
CSX=AddCylindricalShell(CSX,'plexi_shield',5,start,stop,30,5);


CylindricalShell.png
