.. _email_brant: brant@ucsc.edu

.. _gcc:

Recent gcc versions on Lux
=========================

Lux uses by default gcc 4.8.5 owing to the version of CentOS
used by the cluster management system. Some people require
a more recent version of gcc, and we provide gcc 8.1 as an
alternative.

.. _loading_gcc:

Loading a more recent gcc version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To load a more recent gcc version, you may use the ``devtoolset``
module:

    module load devtoolset-8/8.1

This module should reset the gcc in your path to v8.1.
