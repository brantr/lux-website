.. _getting_started: ../html/getting_started.html
.. _using_lux: ../html/using_lux.html
.. _system:


*******************************
*lux* System Configuration
*******************************

Compute System Overview
--------------------------

The *lux* system is based on 3 login servers (*lux-0*, *lux-1*, and *lux-2*)
and 108 Dell compute nodes. The compute nodes each have 2x 20-core Intel Xeon Gold 6248 (Cascade Lake) CPUs, 192GB RAM, 2.4TB SSD local scratch space, and 100 GB/s Mellanox HDR non-blocking Infiniband networking. There are 80 CPU-only nodes (*node001*-*node080*) and 28 GPU-enabled nodes (*gpu001*-*gpu028*) that have 2x NVIDIA 32GB V100 GPUs.

Instructions for getting access and using the system are available on the `Getting Started <getting_started_>`_ and using_lux_ pages.


Facilities Statement for Grants
-------------------------------

You may wish to include a description of *lux* in your facilities / equipment statement for grant or national supercomputing applications:

    UC Santa Cruz hosts a new high-performance computer *lux* funded by NSF MRI grant AST 1828315, currently being installed at the UCSC Data Center. This new Dell system features 108 nodes, each with 2x 20-core Intel Xeon Gold 6248 (Cascade Lake) CPUs, 192GB RAM, 2.4TB SSD local scratch space, and 100 GB/s Mellanox HDR non-blocking Infiniband networking. Of the compute nodes, 28 include 2x NVIDIA V100 32GB GPUs (56 total). The *lux* system also features a 1.7PB DataDirect Networks Lustre storage system Infiniband-connected directly to the compute nodes, allowing for high throughput attached storage.