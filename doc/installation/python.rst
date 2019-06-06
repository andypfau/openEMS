.. _install_python:

********************
Python
********************

Instructions on how to install the CSXCAD and openEMS python interface.


Linux
==================

1. Make sure CSXCAD and openEMS was build and installed correctly (:ref:`see here <install_openems_linux>`)

2. Simple version (if installed to ``/usr/local``):

	.. todo::
		
		Do I have to CD into /usr/local first, or where is "CSXCAD"?

	.. code-block:: console

		cd CSXCAD 
		python setup.py install
		cd ..

		cd openEMS
		python setup.py install
		cd ..

3. Extended options, e.g. for custom install path at ``~/opt/openEMS``:

	.. todo::
		
		Is this extended instead of simple, or on top of simple? I assume instead, but the instructions are unclear

	.. code-block:: console

		python setup.py build_ext -I/opt/include -L/opt/lib -R/opt/lib"
		pyhton setup.py install

	.. note:
		
		The install command may require root on Linux, or add ``--user`` to install to *~/.local*

4. :ref:`Verify your installation <first_steps_tut>`



Windows
==================

.. note::
	
	The python interface for CSXCAD currently does not support MS Windows.
