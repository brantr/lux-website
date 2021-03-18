.. _email_brant: brant@ucsc.edu

.. _dedalus:

Installing Dedalus on Lux
=========================

And linking it to existing modules
----------------------------------

.. _what_is_dedalus:

What is Dedalus?
~~~~~~~~~~~~~~~~

`Dedalus <https://dedalus-project.org/>`__ is an open-source software
package that can be used to solve differential equations, like the
Navier-Stokes equation, using spectral methods. It solves equations
input by users as strings, and can handle initial value problems,
eigenvalue problems, and boundary value problems. Due to its
flexibility, `active
userbase <https://groups.google.com/forum/#!forum/dedalus-users>`__, and
user-friendly python interfaces, it is quickly becoming a widely-used
tool in astrophysical and geophysical fluid dynamics, plasma physics,
and `other fields <https://dedalus-project.org/citations/>`__.

.. _dedalus_warning:

Why installing Dedalus warrants a little care
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As explained on `Dedalus' installation
page <https://dedalus-project.readthedocs.io/en/latest/pages/installation.html>`__,
Dedalus relies on MPI, FFTW (linked to MPI), HDF5, Python3, and the
following Python packages: numpy, scipy, mpi4py (linked to that same
MPI), and h5py. There are several ways to install Dedalus. The easiest
is to use the `conda installation
script <https://dedalus-project.readthedocs.io/en/latest/pages/installation.html#conda-installation-recommended>`__,
which can build all of the prerequisite software (after first installing
Python using miniconda, as explained in the Dedalus installation
instructions), or be linked to existing MPI/FFTW/HDF5 installations.
This method is great if you're just starting out, or if you're
installing Dedalus on a machine that is missing some or all of the
prerequisite software packages. However, cluster/supercomputer support
staff generally discourage this sort of an installation when it can be
avoided, as it often fails to take advantage of various subtle
optimizations that are available on each machine depending on the
software environment and CPU architecture (granted, when it comes to
Dedalus, these subtleties are probably most important when installing
MPI and FFTW). Additionally, if you would like to `contribute to
Dedalus <https://github.com/DedalusProject/dedalus>`__, it helps to have
Dedalus installed in an editable form, which the conda installation
doesn't do without some tinkering. (If you would like to do that with
the conda installation, either reach out to `Adrian
Fraser <mailto:adfraser@ucsc.edu>`__ or ask about it on the `Dedalus
user group <https://groups.google.com/forum/#!forum/dedalus-users>`__.
It's pretty easy.)

If you would like to install Dedalus using the conda install script,
based on past experience, it should work pretty well without any major
difficulty.

.. _dedalus_installation:

Installing Dedalus on top of Lux's existing modules, from source
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Note that these instructions were written in March 2021. There are
several aspects that are likely to change over time. In particular, the
versions of various modules installed on Lux might change. Aspects that
are likely to require modification when these instructions become
outdated will be noted *(like this)*.

First, load the following modules (if you haven't already, do
``module list`` to see if you already have some of these loaded):

::

    module load slurm/18.08.4 openmpi/4.0.1 fftw/3.3.8 python/3.8.6

*(The versions of each of these modules might change over time)*

Next, set the ``MPI_PATH`` and ``FFTW_PATH`` environment variables,
which tell Dedalus where on Lux this software is installed:

::

    export MPI_PATH=/cm/shared/apps/openmpi/openmpi-4.0.1/
    export FFTW_PATH=/cm/shared/apps/fftw/fftw-3.3.8/

*(These paths will change if the openmpi or fftw modules change)* **Note
that you'll probably want to load these same openmpi and fftw modules
and set these same ``MPI_PATH`` and ``FFTW_PATH`` environment variables
if you're using the simpler conda install too.**

Then, fetch your Dedalus version of choice from
`github <https://github.com/DedalusProject/dedalus>`__ and place it in
whatever directory you want Dedalus to live (your best bet is usually to
either download the main AKA "master" branch, which is the default when
you click that link, or to download the latest official
`release <https://github.com/DedalusProject/dedalus/releases>`__ -- but
if you want to test out the new spherical bases/domains being developed,
check out their d3 branch). Use ``cd`` to enter the ``dedalus/`` folder
you just downloaded.

*The first time I installed Dedalus on Lux using this method, I hit a
strange error that I was not able to reproduce ever again. I document it
here in case others hit this error as well, but you can skip this step
if you don't hit this error. The error happened when I tried to
``pip3 install`` (explained in the next paragraph). The error was
relating to write permissions in the ``/tmp`` folder and the
``dedalus/.git`` folder, and googling around I saw that some others have
had similar errors somehow stemming from conflicts between pip3 and git.
At the time, I deleted the ``dedalus/.git`` folder and was able to
continue without any additional errors (you can re-initiate git tracking
after the fact if desired). Since then, however, I've been completely
unable to reproduce this error. I'm leaving this paragraph here for now
in case others encounter this issue.*

Once you've fetched the code and entered into the ``dedalus/``
directory, we need to add a modification to the file ``setup.py``
because for some reason ``pip3`` will otherwise not install Dedalus
correctly, because it will ignore half of the instructions we give it.
Open ``setup.py``. Near the top of the file, you should see a block of
``import`` statements. immediately after all those ``import``
statements, add the following:

::

    import site
    site.ENABLE_USER_SITE = "--user" in sys.argv[1:]

*(This is to circumvent an issue where ``pip3 install`` won't properly
do what the ``--user`` option tells it to do if you simultaneously use
the ``-e`` option, causing pip3 to install in a Lux-wide directory,
which will fail unless you have root privileges. Either this is a bug
with ``pip3`` that will be addressed in some later version of ``pip3``,
or this is an issue with Dedalus that will be addressed in some later
version of Dedalus, I'm not sure which.)*

Finally, run the command ``pip3 install --user -e .`` from this same
``dedalus/`` directory, and you should be all set!

Once the installation is finished, run the command
``python3 -m dedalus test`` and Dedalus will run through its testing
suite to make sure it's installed correctly. If everything worked out
ok, you should see several yellow warnings and xerrors (expected
errors), but no red (serious) errors. And you should be ready to get
simulating! Make sure to load all the same modules whenever you want to
use dedalus, whether in an interactive session or in an sbatch script
for queued jobs.

*(At the time of this writing, the latest "release" of Dedalus, which is
installed when you use the conda install script, has some minor problems
that, depending on OS and scipy release, may lead to errors when you do
``python3 -m dedalus test``. An example of these errors can be seen
`here <https://github.com/DedalusProject/dedalus/issues/110>`__. The
errors all mention Hermite bases. If you don't plan on using Hermite
bases anyway for your simulations, then you can disregard these errors.
If you do plan on using Hermite bases, then this was addressed in a
`recent
change <https://github.com/DedalusProject/dedalus/commit/efb13bdaa09816dde3eee897bc2a15fc284ea2f1>`__
on the main/"master" branch on github, so all you need to do is work
with the most recent github version rather than the most recent
"release" version.)*

*(Also: these instructions did not work with python3's virtual
environments ``venv``. When using ``venv``, python and pip3 are no
longer able to see any of the python packages installed as part of the
python/3.8.6 module, which leads to a longer and more involved
installation because you need to install numpy/scipy/etc locally.
Because the python/3.8.6 module seems to include every single python
prerequisite that Dedalus needs, I personally find virtual environments
to be less important in this situation. There are certainly instances
where you might want to use virtual environments anyway, depending on
your specific needs/workflow.)*
