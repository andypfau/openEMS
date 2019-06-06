.. _probes:

**********************************
Ports
**********************************

.. todo::

	migrate from <http://openems.de/index.php/Ports.html>


Ports are macro function that combine e.g. current and voltage probes, field excitations and other necessary properties and primitives.

General layout (example):

[CSX port] = Add...Port(CSX, prio, port_number, <a list of port dependent parameters>)

with the following parameters:

    CSX: The original CSX structure (in & out)
    prio: priority for all contained primitives
    port_number: number of this port (must be unique)

return values:

    CSX: The manipulated CSXCAD structure
    port: A new port structure containing all necessary information to use with calcPort for post-processing purposes

Defining Multiple Ports

In many cases you may want to create more than one port, e.g. to calculate the reflection and transmission parameters. In this case it is a good idea to create a cell array of port structures. Example:

% port 1 (maybe active)
[CSX port{1}] = Add...Port(CSX, prio, 1, <a list of port dependent parameters>)
 
% port 2 (maybe passive)
[CSX port{2}] = Add...Port(CSX, prio, 2, <a list of port dependent parameters>)

Note: Keep in mind that in order to calculate a reflection and transmission, only one port at a time can be active.

Concentrated Ports

Concentrated ports such as the lumped or curve port are supposed to be very small and compact ports. Their size should be much smaller than the wavelength.

Lumped Port

A lumped port is a 1D, 2D or 3D box containing a feeding resistance (e.g. 50 Ohms) and a current and voltage probe measuring the current through and the voltage along this resistance. As any port it can be active/include an excitation or not.

Example of an active 1D port with 50 Ohm:

start = [100 0 0];
stop  = [100 0 50];
[CSX port] = AddLumpedPort(CSX, 5 ,1 , 50, start, stop, [0 0 1], true);

The vector argument indicates that the direction of the port is z. The value "true" indicates that this port is active.

See also: Simple Patch Antenna Tutorial

Curve Port

Transmission Line Ports

Transmission line ports are the most complex ports available in openEMS.

The FDTD mesh must be already defined for this type of port!

Microstrip Port

General layout (example):

[CSX,port] = AddMSLPort( CSX, prio, portnr, materialname, start, stop, dir, evec, varargin )

with the following additional parameters:

    materialname: is the metal or conducting sheet property name used for the metallic property
    start/stop: the start/stop coordinates of a box defining the outer boundary of the port. The order of start/stop does matter in this case as the wave is assumed to travel from start to stop. Ensure that the box covers at least 2 grid cells in the direction of the excitation vector.
    dir: direction of propagation (0,1 or 2 for x-, y- or z-direction)
    evec: excitation vector, which defines the direction of the e-field

optional/variable parameters as key/values:

    ExcitePort: true/false to make the port an active feeding port (default is false)
    FeedShift: shift the port from start by a given distance in drawing units. Default is 0. Only used if port is active!
    Feed_R: Specify a lumped port resistance. Default is no lumped port resistance --> port has to start in an absorbing boundary such as a PML.
    MeasPlaneShift: Shift the measurement plane from start in propagation direction to a given distance in drawing units. Default is the middle of start/stop.

Example:

::

	CSX = AddMetal( CSX, 'PEC' );
	portstart = [ 0,    -MSL_width/2, substrate_thickness];
	portstop  = [ 5000,  MSL_width/2, 0];
	[CSX, port{1}] = AddMSLPort(CSX, 999, 1, 'PEC', portstart, portstop, 0, [0 0 -1], 'ExcitePort', true, ...
								'FeedShift', 10*resolution, 'MeasPlaneShift',  MSL_length/3);

See also: Microstip Notch Filter Tutorial, CRLH Parameter Extraction Tutorial

Waveguide Ports

Circular Waveguide Ports

Circular waveguide ports are set up with the following command:

[CSX,port] = AddCircWaveGuidePort(CSX, prio, portnr, start, stop, radius, mode_name, pol_ang, exc_amp, varargin);

with the following parameters:

    CSX: The original CSX structure (in & out)
    prio: priority for all contained primitives
    port_number: number of this port (must be unique)
    start: start coordinates of waveguide port box
    stop: stop coordinates of waveguide port box
    radius: circular waveguide radius in metres
    mode_name: mode name, e.g. 'TE11' or 'TM21'
    pol_ang: polarization angle (e.g. 0 = horizontal, pi/2 = vertical)
    exc_amp: excitation amplitude (set 0 to be passive)

Return values:

    CSX: The manipulated CSXCAD structure
    port: A new port structure containing all necessary information to use with calcPort for post-processing purposes

Note that the excitation will be located at the start position and the voltage and current probes will be located at the stop position.

The stop coordinate of the port box defines the reference plane for the port.

An example using a cylindrical coordinate system (cartesian coordinates also work in a similar manner):

   % create a TE11 circular waveguide mode, using cylindrical coordinates
   start=[mesh.r(1)   mesh.a(1)   0  ];
   stop =[mesh.r(end) mesh.a(end) 100];
   [CSX,port] = AddCircWaveGuidePort( CSX, 99, 1, start, stop, 320e-3, 'TE11', 0, 1);

Rectangular Waveguide Ports

Rectangular waveguide ports are set up with the following command:

[CSX,port] = AddRectWaveGuidePort( CSX, prio, portnr, start, stop, dir, a, b, mode_name, exc_amp, varargin);

with the following parameters:

    CSX: complete CSX structure (must contain a mesh)
    prio: priority of primitives
    start: start coordinates of waveguide port box
    stop: stop coordinates of waveguide port box
    dir: direction of port (0/1/2 or 'x'/'y'/'z'-direction)
    a,b: rectangular waveguide width and height (in metre)
    mode_name: mode name, e.g. 'TE11' or 'TM21'
    exc_amp: excitation amplitude (set 0 to be passive)

Return values:

    CSX: modified CSX structure
    port: port structure to use with calcPort

Ports are in the form of a box with the excitation plane located at the start position and the voltage and current probes located at the stop position.

The stop coordinate of the port box defines the reference plane for the port.

An example of an active port directed along the z-direction:

start=[mesh.x(1)   mesh.y(1)   mesh.z(11)];
stop =[mesh.x(end) mesh.y(end) mesh.z(15)];
[CSX, port{1}] = AddRectWaveGuidePort( CSX, 0, 1, start, stop, 'z', a*unit, b*unit, TE_mode, 1);

Port Post Processing

Time Domain Currents and Voltages Data

After calling calcPort() one can obtain the time-domain voltages and currents for ports i=1,2,3 ...:

    Time values: port{i}.raw.U.TD{1}.t
    Voltage values: port{i}.raw.U.TD{1}.val
    Current values: port{i}.raw.I.TD{1}.val

Example of plotting out an input (port{1}) and output (port{2}) voltage and current are shown below

port{1} = calcPort(port{1}, Sim_Path, freq);
port{2} = calcPort(port{2}, Sim_Path, freq);
 
% plot time domain response voltage
figure
plot( 1E12*port{1}.raw.U.TD{1}.t,port{1}.raw.U.TD{1}.val ,'k-', 'Linewidth', 2 );
hold on
grid on
plot( 1E12*port{2}.raw.U.TD{1}.t,port{2}.raw.U.TD{1}.val ,'r--', 'Linewidth', 2 );
title( 'Voltage vs Time' );
xlabel( 'Time (pS)' );
ylabel( 'Voltage (V)' );
legend( 'port 1','port 2');
axis ([0 100]);

Frequency Domain Data

After calling calcPort() one can obtain the frequency-domain parameters for ports i=1,2,3 ...:

    Incident voltage: port{i}.uf.inc
    Reflected voltage: port{i}.uf.ref
    Total voltage: port{i}.uf.tot
    Incident current: port{i}.if.inc
    Reflected current: port{i}.if.ref
    Total current: port{i}.if.tot

Example of calculating s-parameters:

port{1} = calcPort(port{1}, Sim_Path, freq);
port{2} = calcPort(port{2}, Sim_Path, freq);
 
s11 = port{1}.uf.ref./ port{1}.uf.inc;
s21 = port{2}.uf.ref./ port{1}.uf.inc;
ZL = port{1}.uf.tot./port{1}.if.tot;

