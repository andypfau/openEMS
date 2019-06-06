Cylinder
----------------------------

.. todo::

	Migrate from <http://openems.de/index.php/Cylinder.html>



Description

A cylindrical primitive is added by

CSX = AddCylinder(CSX, propName, prio, start, stop, rad, varargin)

with the following parameters:

    CSX: The original CSX structure
    propName: name of the assigned material
    prio: priority of the primitive
    start: [x y z] start point of the cylinder (midpoint of the first cylinder face)
    stop: [x y z] stop point of the cylinder (midpoint of the second cylinder face)
    rad: radius of the cylinder
    varargin: a key/value list of primitives variable arguments

The axis of the cylinder will be along the start - stop points with the two cylinder faces being perpendicular to this axis.

Example:

CSX = AddCylinder(CSX,'metal',1,[0 0 -300], [0 200 300], 300);

Cylinder.png
