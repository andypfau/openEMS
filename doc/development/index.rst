.. _development:

#####################################
Development
#####################################



**********************************
What's New?
**********************************

.. todo::
	
	Deev: what's new?

The most important changes come here.

For the rest, check the repo. Uh, since thliebig/openEMS-project and thliebig/openEMS are technically two independent repos, and one just added the other one as a module, is there any central bug tracker and log?



.. _dev_roadmap:

**********************************
Roadmap
**********************************

* Finish this documentation

* Finish on Python interface



.. _gitrepo:

**********************************
Source Code
**********************************

The complete source code of openEMS is available on GitHub:

	`thliebig/openEMS <https://github.com/thliebig/openEMS>`_

Since openEMS has some :ref:`dependencies <openems_dependencies>`, there is a "thin meta-repo" to put all Git repos as modules into one common repo. This makes :ref:`building openEMS from source <build_openems_from_source>` more convenient. That repo is also on GitHub:

	`thliebig/openEMS-Project <https://github.com/thliebig/openEMS-project>`_

.. note::

	Note that `thliebig/openEMS-project` repo includes other repos (e.g. openEMS, CSXCAD, etc.) as modules, so you must use a recursive clone; see also :ref:`installation instructions <install_openems_linux_build>`



.. _openems_dependencies:

**********************************
Dependencies
**********************************

Libraries used by openEMS:

* CSXCAD: Part of the openEMS project. Author: Thorsten Liebig
* `tinyxml <https://www.grinninglizard.com/tinyxml/>`_: A small and tiny xml parser written in C++
* `fparser <https://warp.povusers.org/FunctionParser/>`_: Function parser library for C++
* `Boost <https://www.boost.org/>`_: extensive C++ library
* `HDF5 <https://www.hdfgroup.org/>`_: Hierarchical Data Format
* `VTK <https://www.vtk.org/>`_: The Visualization Toolkit (VTK)
* `MPI <https://www.open-mpi.org/>`_: Message Passing Interface

.. todo::
	
	many of these links are dead; use <http://grinninglizard.com/tinyxml/> and <https://sourceforge.net/projects/fparser/>, or is that something else?



**********************************
How to Contribute
**********************************

.. todo::
	
	How to contrib
	
* report bugs, either in the Forum or on GitHub

* contribute on GitHub

	* to set up your build environment, :doc:`see here<buildenv>`



.. toctree::
	:hidden:
	
	buildenv
