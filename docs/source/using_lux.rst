.. _email_brant: brant@ucsc.edu
.. _connecting_to_lux: getting_started.html#connecting_to_lux
.. _using_lux:


*******************************
Using *lux*
*******************************

We aim to create and maintain a great user experience with the
*lux* cluster. Below, we provide a description of how to use the
system.

Software and Environment
========================

.. _login_nodes:

Starting Out
------------

Once you connect to *lux* (see `Connecting to lux <connecting_to_lux_>`_), you will be placed on 
one of three login nodes (*lux-0*, *lux-1*, *lux-2*). Connections are cyclically assigned
across these nodes to distribute the user load, but for most purposes the nodes will function identically for the user.

The user home directories are mounted at :file:`/home` across the system, as are the :file:`/data` directories. These global filesystems are imported from the DDN storage server via the HDR Infiniband network fabric, and support fast I/O from anywhere on the cluster. See `File System <file_system_>`_ below

.. _software_and_modules:

Software Stack
--------------

The primary software stack for *lux* currently consists of 

	* :file:`gcc 4.8.5` for GNU compilers, including C, C++, and Fortran.
	* :file:`icc 19.0.4.243` for Intel compilers, including C, C++, Fortran, and Intel MPI.
	* :file:`openmpi` for OpenMPI parallel compilers, based on :file:`gcc 4.8.5`.
	* :file:`python 3.6.7` for Python and related libraries.
	* :file:`slurm 18.08.4` for queueing and job submission.

Each of these elements of the software stack are either automatically loaded by default (:file:`gcc 4.8.5`, :file:`python 3.6.7`, and :file:`slurm 18.08.4`) or loadable as a :file:`module` (:file:`openmpi` and Intel :file:`icc/mpii*` compilers; See `Modules <modulefiles_>`_ below).

.. _modulefiles:

Modules
--------------

To load software and update environmental variables for path, library linking, etc., the *lux* system relies on the
`Modules <https://modules.readthedocs.io/en/latest/index.html>`_ package. To load a :file:`module`, just::

   $ module load [module_name]

where :file:`[module_name]` is an available module. To see
modules available on the system, type::

   $ module avail

To list all currently loaded modules, write::

   $ module list

By default, only :file:`slurm` and :file:`python/3.6.7` are loaded, along with the metapackage :file:`shared` that gives access to shared software modules installed in :file:`/cm/shared`. The default is set in your :file:`~/.bashrc` file and can be changed by altering the file. Note that :file:`slurm` is required
to run jobs on the system.

To remove a single module, simply type::

   $ module remove [module_name]

To remove all currently loaded modules, write::

   $ module purge

For more information, see :file:`man module`.  CHECK THAT MODULES ARE IMPORTED VIA SLURM BATCH AND INTERACTIVE JOBS

.. _file_system:

File System and Quotas
----------------------

The file system for the cluster is based on a DataDirect Networks Lustre appliance, which hosts the :file:`/home` and :file:`/data` user directory structures and the :file:`/cm/shared` directory
that contains common software and modules.

The filesystems on *lux* are subject to storage quotas. While there
is substantial storage available on the system, some members of the
*lux* project team and affiliated departments and divisions have directly purchased storage in support of research projects. Some limited free storage may be available by request (see below).

Your :file:`/home/[user name]` directory will have a storage quota of *5 GB*.

If you belong to a research group affiliated with a *lux* Co-I, you may have access to a :file:`/data/[research group]` directory
with significant storage. While these directories have storage
quotas, they should be sufficient for most research group needs. If you have questions about accessing the your research group's
:file:`/data` directories, please contact your affiliated Co-I.

For users who are not affiliated with a research group, please
contact `Brant Robertson <email_brant_>`_ for access to :file:`/data`. In all cases, :file:`/data` storage will be limited.

.. _running_jobs:

Running Jobs
============

The *lux* system uses `Slurm <https://slurm.schedmd.com/>`_ workload manager to schedule and execute jobs on the cluster nodes. If you are not familiar with Slurm don't worry, Slurm works like PBS, LSF, and other schedulers you may have used in the past. Below we provide information for running batch and interactive jobs on the *lux* nodes via Slurm.

.. _queues:

Queues
------

The *lux* system has a variety of job queues (called *partitions* in Slurm parlance) available for users. The currently available queues include:

* **defq** The default queue, submits to *node[001-080]*.
* **gpuq** The GPU-enabled node queue, submits to *gpu[001-028]*.

In the following, please substitute on of these queues when instructed to specify the :file:`[queue name]`.

To get information on the status of the queues, use the :file:`sinfo` command::

    $ sinfo

    PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
    defq*        up   infinite     80  idle node[001-080]
    gpuq         up   infinite     28  idle gpu[001-028]



This shows the queue names (PARTITION), their availability (AVAIL), any time limit (TIMELIMIT), the state of nodes (STATE), the number of nodes in that state (NODES), and the list of nodes in that state (NODELIST).

To see the list of jobs in the queues, use the :file:`squeue` command::

    $ squeue

This shows the id of each job (JOBID), the queue the job is assigned to (PARTITION), the name of the job (NAME), the job owner (USER), the job state (ST), the runtime of the job (TIME), the number of nodes used or requested by the job (NODES), and the list of nodes assigned to the job or the reason the job is still queued [NODELIST/(REASON)].

Detailed information about the queues can be retrieved using :file:`scontrol show partition`::

    $ scontrol show partition

To cancel a job::

    $ scancel [JOBID]

where [JOBID] is the job you wish to cancel.

.. _slurm_batch:

Batch Job Submission
--------------------

To run a batch job across multiple nodes, from a login node execute the following command::

	$ sbatch --partition=[queue name] [script name]

Substitute the name of the queue you wish to use for :file:`[queue name]`. This will submit a slurm batch script file :file:`[script name]` to the specified queue.

.. _slurm_example:

Example Batch Script
--------------------

We provide below an example slurm batch script, which executes an mpi job with 80 mpi processes distributed across 2 nodes, with 40 mpi processes per node (e.g., one per core)::

    #!/bin/bash
    #SBATCH --job-name=mpi_job_test      # Job name
    #SBATCH --mail-type=END,FAIL         # Mail events (NONE, BEGIN, END, FAIL, ALL)
    #SBATCH --mail-user=[USER ID]@ucsc.edu   # Where to send mail
    #SBATCH --ntasks=80                  # Number of MPI ranks
    #SBATCH --nodes=2                    # Number of nodes
    #SBATCH --ntasks-per-node=40         # How many tasks on each node
    #SBATCH --time=00:05:00              # Time limit hrs:min:sec
    #SBATCH --output=mpi_test_%j.log     # Standard output and error log

    pwd; hostname; date

    echo "Running program on $SLURM_JOB_NUM_NODES nodes with $SLURM_NTASKS total tasks, with each node getting $SLURM_NTASKS_PER_NODE running on cores."

    module load openmpi
    
    mpirun -N 2 --map-by ppr:40:node ./mpi_test

    date


This example can be submitted to the queues following the instructions in `Batch Job Submission <slurm_batch_>`_ above. 

.. _slurm_job_arrays:

Job Arrays
----------

To submit a job array, use the :file:`--array=[range]` option (examples taken from the slurm website)::

    # Submit a job array with index values between 0 and 31
    $ sbatch --array=0-31    -N1 tmp

    # Submit a job array with index values of 1, 3, 5 and 7
    $ sbatch --array=1,3,5,7 -N1 tmp

    # Submit a job array with index values between 1 and 7
    # with a step size of 2 (i.e. 1, 3, 5 and 7)
    $ sbatch --array=1-7:2   -N1 tmp

.. _slurm_interactive:

Interactive Sessions
--------------------

To create an interactive session on a compute node, from a login node execute the following command::

	$ srun -N [Num of nodes] --partition=[queue name]  --pty bash -i

Substitute the name of the queue you wish to use for :file:`[queue name]`. This will create a :file:`bash` shell in an interactive session on [Num of nodes] nodes (:file:`-N [Num of nodes]`). 

Here is an example of combining srun + mpirun to run 3610 mpi processes interactively on 79 nodes using openmpi::

    $ srun -N 79 -n 3160 --partition=defq --pty bash -i
    $ mpirun -n 3160 --map-by ppr:40:node ./mpi_test



To allocate a multi-node interactive session, use the :file:`salloc` command::

    $ salloc -n[ncores] sh
    > srun [executable]
    > exit

This set of command allocates :file:`[ncores]` cores on the system and starts a shell :file:`sh`.  Then :file:`srun` command executes the job :file:`[executable]`, and :file:`exit` ends the session.

.. _walkthrough:

Tutorial Walkthrough
====================

Here we provide a walkthrough showing all the steps of connecting to *lux* and executing an interactive session via Slurm on a GPU node. We annotate the process to provide some useful information and references.

COMING SOON!
