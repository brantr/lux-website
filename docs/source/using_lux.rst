.. _getting_started: ../html/getting_started.html#connecting_to_lux
.. _using_lux:


*******************************
Using *lux*
*******************************

We aim to create and maintain a great user experience with the
*lux* cluster. Below, we provide a description of how to use the
system.

Running Jobs
============

.. _login_nodes:

Starting Out
------------

Once you connect to *lux* (see `Getting Started <getting_started_>`_), you will be placed on 
one of three login nodes (*lux-0*, *lux-1*, *lux-2*). Connections are cyclically assigned
across these nodes to distribute the user load, but for most purposes the nodes will function identically for the user.

The user home directories are mounted at :file:`/home` across the system, as are the :file:`/data` directories. These global filesystems are imported from the DDN storage server via the HDR Infiniband network fabric, and support fast I/O from anywhere on the cluster. See `File System <file_system_>_` below

.. _software_and_modules:

Software Stack
--------------

The primary software stack for *lux* currently consists of 

	* :file:`gcc 4.8.5` for GNU compilers, including C, C++, and Fortran.
	* :file:`icc 4.8.5` for Intel compilers, including C, C++, Fortran, and Intel MPI.
	* :file: `openmpi ` for OpenMPI parallel compilers, based on :file:`gcc 4.8.5`.
	* :file: `python 3.6.7` for Python and related libraries.
	* :file:`slurm 10.1` for queueing and job submission.

Each of these elements of the software stack are either automatically loaded by default (:file:`gcc 4.8.5`, :file: `python 3.6.7`, and :file:`slurm 10.1`) or loadable as a :file:`module` (:file:`openmpi` and Intel compilers; See `Modules <modules_>`_ below).

Modules
--------------

.. _file_system:

File System
--------------------


.. _running_jobs:

Running Jobs
============

.. _slurm_batch:

Queues and Job Submission
-------------------------

.. _slurm_interactive:

Interactive Sessions
--------------------

To create an interactive session on a compute node, from a login node execute the following command::

	$ srun -N 1 --partition=[queue name]  --pty bash -i

Substitute the name of the queue you wish to use for :file:`[queue name]`. This will create a :file:`bash` shell in an interactive session on a single node (:file:`-N 1`). 

.. _walkthrough:

Tutorial Walkthrough
====================

Here we provide a walkthrough showing all the steps of connecting to *lux* and executing an interactive session via Slurm on a GPU node. We annotate the process to provide some useful information and references.