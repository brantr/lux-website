.. _email_brant: brant@ucsc.edu

.. _policies:


*****************************
Policies
*****************************

.. _policies_overview:

Overview
--------

Thanks for becoming a user of the lux system at UCSC. Below, we highlight the user policies for the system. Anyone using the lux cluster assents to these policies as a condition of access to the lux cluster. For questions, please email `Brant Robertson <email_brant_>`_.

.. _acknowledgements:

Acknowledgements
----------------

All users of *lux* must include the following acknowledgement in any publication resulting or benefitting from usage of the system:

	**We acknowledge use of the lux supercomputer at UC Santa Cruz, funded by NSF MRI grant AST 1828315.**

Including this funding statement is critical, and users and any related Co-I are responsible for adding this acknowledgement. Failure to include this statement in publications that used *lux* will be considered a `policy violation <policy_violations_>`_.

Notification of Publications
----------------------------
Please let `Brant Robertson <email_brant_>`_ know about any publications arising or benefitting from your access to *lux* (and please include the `acknowledgements <acknowledgements_>`_ in the published version!).

Scheduler and Queues
--------------------
Users are expected to submit jobs and access nodes through the provided Slurm queues.

Storage and Quotas
------------------
User accounts are subject to storage quotas.

Backups
-------
Backups of :file:/home will be performed infrequently. The :file:/data filesystem will not be backed up.
 
Software and Libraries
----------------------

The usage of lux is shared among many disciplines, and this breadth makes the detailed management of the system challenging. Software from many different disciplines requires a large range of libraries and packages, and the maintenance of all such libraries may be unmanageable. Widely-used libraries may be installed as system modules for use by multiple users. Research or custom-built software will need to be installed and maintained by their users.

Frontend system usage
---------------------

The *lux* system frontend servers (*lux-0*, *lux-1*, *lux-2*) are designed to support users of the cluster in its intended usage mode (i.e., distributed jobs running on the nodes). Any computationally or memory intensive job should not be run on the frontend, and instead should be executed on a node allocated via the Slurm scheduler. This policy especially includes the execution of python scripts, including simulation post processing and plotting – these are tasks that should be run on the nodes. Any job running on the frontend can be terminated without notice to the user.


Computational tasks explicitly permitted on the frontend system are text/code editing, compilation, data transfer, and job monitoring. If you have a question about how to use the lux frontend systems, please email `Brant Robertson <email_brant_>`_.

.. _policy_violations:

Policy Violations
-----------------
Users who violate the above policies risk losing temporary or permanent access to *lux*. The project Co-Is agree to help enforce policies for their affiliated users. If you have questions about policy violations, please email `Brant Robertson <email_brant_>`_.