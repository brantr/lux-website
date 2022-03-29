.. _jupyter_hub:


*******************************
*lux* Jupyter Hub
*******************************

Jupyter Hub Overview
--------------------------

The *lux* system has a Jupyter Hub that enables
users to run Jupyter notebooks remotely via a 
web interface. For more information, visit the
`Jupyter Hub <https://jupyter.org/hub>`_ website.

To connect to the *lux* Jupyter Hub:

1. Connect to the UCSC campus VPN.
2. Visit `https://lux-0.ucsc.edu:8000 <https://lux-0.ucsc.edu:8000>`_.
3. Login using your UCSC Gold credentials (same as used when connecting via ssh).

Once you have connected, you will see a Launcher window that contains a variety of Python 3.7 kernels that can execute directly on the nodes via slurm. In addition to the shared
*windfall*, *cpuq*, and *gpuq* partitions, each of the
*lux* group partitions have kernels available. You will
need to have membership in the corresponding partition to
run a Jupyter notebook.

Once you have completed using the notebook via the kernel
you select, please be sure to shut down the kernel before
exiting. Otherwise, the slurm job responsible for your
kernel will continue to run.


Python 3.7
--------------------------
To use Jupyter Hub, we must use Python 3.7 supplied
by the Bright Cluster Management software. If you have
a module that needs to be installed for use with 
Python 3.7, please use the *help* channel on the
*lux* Slack workspace.