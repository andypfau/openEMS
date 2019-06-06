.. _install_openems:

********************
openEMS
********************

Instructions on how to install CSXCAD and openEMS.


.. _install_openems_linux:

Linux
================

.. note::
	
	The recommended Linux distribution is Ubuntu 14.04 LTS or above. All instructions here are for Ubuntu.



Prerequisites
------------------------

1. Install all necessary packages and libraries (*git*, *qt4*, *tinyxml*, *hdf5*, *boost*):

	.. code-block:: bash

		sudo apt-get install build-essential git cmake libhdf5-dev libvtk5-dev libboost-all-dev libcgal-dev libtinyxml-dev libqt4-dev libvtk5-qt4-dev


	.. note::
		
		Ubuntu 16.04: Due to a bug in CGAL, the package ``libcgal-qt5-dev`` may be required.

2. Install additional packages for *hyp2mat* (optional):

	.. code-block:: bash

		sudo apt-get install gengetopt help2man groff pod2pdf bison flex libhpdf-dev libtool autoconf

3. Install *Octave* and *Octave* development packages (optional):

	.. code-block:: bash

		sudo apt-get install octave liboctave-dev epstool transfig


.. todo::
	
	When is it recommended to install the optional packages?
	I understand hyp2mat is to import something, but the octave and octave dev packages, couldn't we move that to "Development"?


.. _install_openems_linux_build:



.. _build_openems_from_source:

Build and Install
-----------------------

4. Get the *openEMS* source code, extract, build and install:

	* Assuming you will install openEMS to ``~/opt/openEMS``:

		.. code-block:: bash

			cd /tmp
			wget http://openems.de/download/src/openEMS-v0.0.35.tar.bz2
			tar jxf openEMS-v0.0.35.tar.bz2
			cd openEMS
			./update_openEMS.sh ~/opt/openEMS

	* Alternative possibilities for advanced users or developers:
		
		* to include *hyp2mat* and the *circuit toolbox*, change the last command to:

			.. code-block:: bash

				./update_openEMS.sh ~/opt/openEMS --with-hyp2mat --with-CTB
		
		* to exclude the GUI (e.g. for a server environment), change the last command to:

			.. code-block:: bash

				./update_openEMS.sh ~/opt/openEMS --disable-GUI
	
		* you can also build from the sources by cloning the :ref:`Git repo <gitrepo>`
		
			.. code-block:: bash

				git clone --recursive https://github.com/thliebig/openEMS-Project.git
				
			then build/install with ``update_openEMS.sh`` as shown above

5. Set up the :ref:`Matlab/Octave <install_matlaboctave>` or :ref:`Python <install_python>` interface



.. _install_openems_windows:

Windows
========================

1. Download the latest package from here: `Test <http://openems.de/download/win64/openEMS_x64_current.zip>`_ (64-bit only)

2. Unzip to a folder of your choice, e.g. ``C:\`` (the .zip-file contains an *openEMS* folder)

3. Set up the :ref:`Matlab/Octave <install_matlaboctave>` or :ref:`Python <install_python>` interface



OS X
=============

Support for OS X is only experimental. Check the folder ``brew`` in the :ref:`Git repo <gitrepo>`.
