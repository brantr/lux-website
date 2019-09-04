.. _Brant: brant@ucsc.edu

.. _policies:


*****************************
Policies
*****************************

.. _policies_overview:

Overview
--------

Thanks for becoming a user of the lux system at UCSC. Below, we highlight the user policies for the system. Anyone using the lux cluster assents to these policies as a condition of access to the lux cluster. For questions, please email Brant_.

Acknowledgements
----------------

Scheduler and Queues
--------------------
Users are expected to submit jobs and access nodes through the provided Slurm queues.

Storage and Quotas
------------------
 
Software and Libraries
----------------------

The usage of lux is shared among many disciplines, and this breadth makes the detailed management of the system challenging. Software from many different disciplines requires a large range of libraries and packages, and the maintenance of these AAAAA

Frontend system usage
---------------------

The lux system frontend servers (lux-0, lux-1, lux-2) are designed to support users of the cluster in its intended usage mode (i.e., distributed jobs running on the nodes). Any computationally or memory intensive job should not be run on the frontend, and instead should be executed on a node allocated via the Slurm scheduler. This policy especially includes the execution of python scripts, including simulation post processing and plotting – these are tasks that should be run on the nodes. Any job running on the frontend can be terminated without notice to the user.


Computational tasks explicitly permitted on the frontend system are text/code editing, compilation, data transfer, and job monitoring. If you have a question about how to use the lux frontend systems, please email Brant_.

Policy Violations
-----------------