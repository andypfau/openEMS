Sphere
----------------------------

.. todo::

	Migrate from <http://openems.de/index.php/Sphere.html>


Description

The sphere primitive is defined by its central point and radius. It is created with

 CSX = AddSphere(CSX, propName, prio, center, rad, varargin)

with the following parameters:

    CSX: The original CSX structure
    propName: name of the assigned property
    prio: priority of the primitive
    center: coordinate of the center point of the sphere
    rad: radius of the sphere
    varargin: a key/value list of primitives variable arguments

Example

    Create a sphere at (0,0,0) with radius 200:

CSX = AddSphere(CSX,'material',1,[0 0 0], 200);

Sphere.png
