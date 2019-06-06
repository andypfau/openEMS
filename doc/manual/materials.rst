**********************************
Materials
**********************************

All geometric elements added to CSXCAD have a material assigned. When adding geometric object, it must be assigned a *property*, which typically is a material. However, note that there are some :ref:`special materials <special_materials>`.



Simple Materials
===========================

General
---------------

The material property is used for materials that are simply defined by the constant permittivity :math:`\epsilon_r`, magnetic permeability :math:`\mu_r` and electric conductivity :math:`\kappa`.

This material can be described as:

	.. math::

		\varepsilon(f) = \varepsilon_0\varepsilon_r - j\frac{\kappa}{2\pi f}

	and

	.. math::

		\mu(f) = \mu_0\mu_r - j\frac{\sigma_m}{2\pi f}
		
	where :math:`\sigma_m` is the non-physical magnetic conductivity.

.. todo::
	
	The way I see this there is no simple way to introduce a loss tangent tanD? <https://en.wikipedia.org/wiki/Dielectric_loss>
	
	When I just set Kappa=Epsilon*tanD (in the dielectric), it isn't frequency-dependent as tanD should be. Am I overlooking something, or is my observation correct that there is no way without touching openEMS?

More complex, dispersive Materials can be defined using the :ref:`Drude/Lorentz material <dispersive_materials>` models.

http://openems.de/index.php/Material_Property.html

Simple material example:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
			
			CSX = AddMaterial(CSX, 'FR4');
			CSX = SetMaterialProperty(CSX, 'FR4', 'Epsilon', 4.5);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing




Air
---------------

Air (actually vacuum) is very simple:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddMaterial( CSX, 'Air' );
			CSX = SetMaterialProperty( CSX, 'Air', 'Epsilon', 1, 'Mue', 1 );
	
	.. tab:: Python
	
		.. todo::
			
			Python missing

	.. todo::
		I copied this from <http://openems.de/index.php/Metal_sheet_with_cylindrical_holes.html>. Do I need to set eps and mue, or is that the default anyways? If not, what is a material without any param?



.. _metal:

Metal
---------------

Example for a perfect electrical conductor (PEC):

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddMetal(CSX, 'PEC');
	
	.. tab:: Python
	
		.. todo::
			
			Python missing

Example for lossy metal:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			conductivity = 56e6; % Siemens/m
			sheet_thickness = 70e-6; % m
			CSX = AddConductingSheet(CSX, 'Copper', conductivity, sheet_thickness);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing

	Note that this creates a "conducting sheet" material, which must be used for planar structures only. The actual resistance is derived from the sheet thickness.
	
	You could use a regular material with the conductivity (kappa) set instead, and create a volume from it. However, you would need extremely thin volumes, which slow down the simulation dramatically, often with no real improvement in the result.

	.. todo::

		Is this explanation OK?
		
		Also, is it correct that I have to apply the sheet thickness in AddConductingSheet in meters, not in the unit that I declared for the mesh?



.. _dispersive_materials:

Dispersive Materials
===========================


Drude Material
----------------------

Physical model:

.. math::
	
	\varepsilon(f) = \varepsilon_0\varepsilon_\infty \left( 1 - \sum_{p=1}^N \frac{f_{plasma,p}^2}{f^2-j f/(2\pi\tau_p)}\right) - j\frac{\kappa}{2\pi f}

with the parameters:

    * :math:`\varepsilon_\infty`: the relative permittivity for :math:`f \to \infty`
    * :math:`\kappa`: the electric conductivity
    * :math:`f_{plasma,p}`: the *p*-th "plasma" frequency
    * :math:`\tau_p` the *p*-th relaxation time (damping)
    
Script example:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddLorentzMaterial(CSX, 'drude');
			CSX = SetMaterialProperty(CSX, 'drude', 'Epsilon', eps_r, 'Kappa', kappa);
			CSX = SetMaterialProperty(CSX, 'drude', 'EpsilonPlasmaFrequency', 5e9, 'EpsilonRelaxTime', 5e-9);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing



Lorentz Material
----------------------

Physical model:

.. math::
	
	\varepsilon(f) = \varepsilon_0\varepsilon_\infty \left( 1 - \sum_{p=1}^N \frac{f_{plasma,p}^2}{f^2-f_{Lor,p}^2-jf/(2\pi\tau_p)}\right) - j\frac{\kappa}{2\pi f} 

with the parameters:

	* :math:`\varepsilon_\infty`: the relative permittivity for :math:`f \to \infty`
	* :math:`\kappa`: the electric conductivity
	* :math:`f_{plasma,p}`: the *p*-th "plasma" frequency
	* :math:`f_{Lor,p}`: the *p*-th Lorentz pole frequency
	* :math:`\tau_p`: the *p*-th relaxation time (damping)
    
Script example:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			CSX = AddLorentzMaterial(CSX, 'lorentz');
			CSX = SetMaterialProperty(CSX, 'lorentz', 'Epsilon', eps_r, 'Kappa', kappa);
			CSX = SetMaterialProperty(CSX, 'lorentz', 'EpsilonPlasmaFrequency', 5e9, 'EpsilonLorPoleFrequency', 10e9, 'EpsilonRelaxTime', 5e-9);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing



Relation to other formulations
----------------------------------------

.. math::
    
    \varepsilon(\omega) = \varepsilon_0\varepsilon_\infty + \varepsilon_0 \sum_{p=1}^N \frac{(\varepsilon_{dc,p}-\varepsilon_\infty)\omega^2_{p}}{\omega_{p}^2+2j\omega\delta_p-\omega^2}


Conversion:

.. math::

	f_{Lor,p} = \frac{\omega_{p}}{2\pi}

	f_{plasma,p} = \omega_{p}\frac{\sqrt{(\varepsilon_{dc,p}-\varepsilon_\infty)}}{2\pi}

	\tau_p = \frac{1}{2\delta_p}

	\kappa = 0

Researchers in Physics often adopt a different sign convention, in which they use :math:`e^{- i \omega t}` for time-harmonic quantities, rather than :math:`e^{i \omega t}` as in engineering. Therefore in some textbook the Lorentz model is:

.. math::

	\epsilon(\omega) = \epsilon_0\epsilon_{\infty} (1+ \frac{\omega_p^2}{\omega_0^2 - \omega^2 - i\gamma \omega})

And the Drude model is:

.. math::

	\epsilon(\omega) = \epsilon_0\epsilon_{\infty} (1- \frac{\omega_p^2}{\omega^2 + i\gamma \omega})

Where :math:`\omega_p` is the plasma frequency, and :math:`\omega_0` is the plasmonic resonant frequency, while :math:`\gamma` represents the damping effect in material.



.. _special_materials:

Special Materials
===========================


Lumped Elements
------------------------

With this special kind of material you can define resistors, capacitors and inductors.

Example for an SMD capacitor, size 0805, 1 pF:

.. tabs::
	
	.. tab:: Matlab/Octave
		
		.. code-block:: matlab
		  
			capacity = 1e-12; % F
			width  = 2.0e-3; % m
			length = 1.2e-3; % m
			height = 0.8e-3; % m
			CSX = AddLumpedElement(CSX, 'Capacitor', 1, 'Caps', 1, 'C', capacity);
			CSX = AddBox(CSX, 'Capacitor', 0, [-width/2 -height/2 -height/2], [width/2 height/2 height/2]);
	
	.. tab:: Python
	
		.. todo::
			
			Python missing

.. todo::

	Is this explanation and example OK?



Dumps, Probes, Excitations
-------------------------------

Note of these are physical materials, but are used in a very similar way. See :ref:`dumps <dumps>`,  :ref:`probes <probes>`,  :ref:`excitations <excitations>`.
