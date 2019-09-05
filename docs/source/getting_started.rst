.. _policies: ../html/policies.html
.. _project_team: ../html/project.html#project_team
.. _acknowledgements: ../html/policies.html#acknowledgements
.. _email_brant: brant@ucsc.edu

.. _getting_started:


*******************************
Getting Started
*******************************

.. _getting_an_account:

Read the User Policies
==================================

First things first -- please read the *lux* `Policies <policies_>`_. All *lux* users must understand and abide by the system policies as a condition of using the computer. This includes `acknowledging lux in publications <acknowledgements_>`_ when used and following the user best practices.

Getting an account on *lux.ucsc.edu*
====================================

There are several ways to get an account on *lux*, described below, including special cases under which accounts may be granted. If you have questions about account access, please feel free to contact `Brant Robertson <email_brant_>`_.

Accounts for Co-I research group members
----------------------------------------
If you are a UCSC faculty, postdoc, or student with a CruzID and part of a Co-I research group (see `Project Team Members <project_team_>`_), your associated faculty member can directly grant you access to *lux*. Please contact the faculty member and ask them to add you to their group. Accounts added in this way will inherit the privileges of the faculty research group on *lux* and use their assigned system resources, and the faculty lead determines the duration and any special conditions of the access.

Accounts for general access by UCSC students, staff, and faculty
----------------------------------------------------------------
With prior approval and agreement, access to *lux* may be granted to UCSC students, staff, and faculty who are not associated with Co-I research groups. Please contact `Brant Robertson <email_brant_>`_ for more information.

Accounts for UCSC courses
-------------------------
By prior arrangement, temporary *lux* access may be granted to students in UCSC courses during the quarter of instruction. If you are interested, please contact `Brant Robertson <email_brant_>`_ for more information.

.. _external_collaborators:

Accounts for Co-I research group external collaborators
-------------------------------------------------------
Co-Is may grant external (outside UCSC) collaborators access by requesting a UCSC Sundry account (see instructions `here <https://its.ucsc.edu/accounts/forms.html>`_ or submit a Sundry account `request <https://ucsc.service-now.com/nav_to.do?uri=com.glideapp.servicecatalog_cat_item_view.do?sysparm_id=1141fa213c9799008065d4c384368f19&sysparm_stack=no>`_), which will provide a limited time but renewable CruzID for their collaborator. Once a CruzID is assigned and a Gold password set, the faculty lead can add their collaborator to their group directly. Please be mindful that *lux* was funded to support research at UCSC, and these external collaborators gain the same privileges as other UCSC Co-I research group members. External collaborators still must agree to acknowledge *lux* in their resulting publications.  Only Co-I faculty leads can grant external collaborators access to *lux*.

Accounts for UCSC visitors
--------------------------
Visitors to UCSC who are associated with Co-I research groups may be able to obtain accounts following the instructions for `external collaborators <external_collaborators_>`_. Groups of visitors may also be granted access under special circumstances, please contact `Brant Robertson <email_brant_>`_ for more information. All visiting users must agree to acknowledge *lux* in any resulting publications.

Connecting to *lux*
===================





You may already have sphinx `sphinx <http://sphinx.pocoo.org/>`_
installed -- you can check by doing::

  python -c 'import sphinx'

If that fails grab the latest version of and install it with::

  > sudo easy_install -U Sphinx

Now you are ready to build a template for your docs, using
sphinx-quickstart::

  > sphinx-quickstart

accepting most of the defaults.  I choose "sampledoc" as the name of my
project.  cd into your new directory and check the contents::

  home:~/tmp/sampledoc> ls
  Makefile	_static		conf.py
  _build		_templates	index.rst

The index.rst is the master ReST for your project, but before adding
anything, let's see if we can build some html::

  make html

If you now point your browser to :file:`_build/html/index.html`, you
should see a basic sphinx site.

.. image:: _static/basic_screenshot.png

.. _fetching-the-data:

Fetching the data
-----------------

Now we will start to customize out docs.  Grab a couple of files from
the `web site <https://github.com/matplotlib/sampledoc>`_
or git.  You will need :file:`getting_started.rst` and
:file:`_static/basic_screenshot.png`.  All of the files live in the
"completed" version of this tutorial, but since this is a tutorial,
we'll just grab them one at a time, so you can learn what needs to be
changed where.  Since we have more files to come, I'm going to grab
the whole git directory and just copy the files I need over for now.
First, I'll cd up back into the directory containing my project, check
out the "finished" product from git, and then copy in just the files I
need into my :file:`sampledoc` directory::

  home:~/tmp/sampledoc> pwd
  /Users/jdhunter/tmp/sampledoc
  home:~/tmp/sampledoc> cd ..
  home:~/tmp> git clone https://github.com/matplotlib/sampledoc.git tutorial
  Cloning into 'tutorial'...
  remote: Counting objects: 87, done.
  remote: Compressing objects: 100% (43/43), done.
  remote: Total 87 (delta 45), reused 83 (delta 41)
  Unpacking objects: 100% (87/87), done.
  Checking connectivity... done
  home:~/tmp> cp tutorial/getting_started.rst sampledoc/
  home:~/tmp> cp tutorial/_static/basic_screenshot.png sampledoc/_static/

The last step is to modify :file:`index.rst` to include the
:file:`getting_started.rst` file (be careful with the indentation, the
"g" in "getting_started" should line up with the ':' in ``:maxdepth``::

  Contents:

  .. toctree::
     :maxdepth: 2

     getting_started.rst

and then rebuild the docs::

  cd sampledoc
  make html


When you reload the page by refreshing your browser pointing to
:file:`_build/html/index.html`, you should see a link to the
"Getting Started" docs, and in there this page with the screenshot.
`Voila!`

We can also use the image directive in :file:`index.rst` to include to the screenshot above
with::

  .. image::
     _static/basic_screenshot.png


..Next we'll customize the look and feel of our site to give it a logo,
..some custom css, and update the navigation panels to look more like
..the `sphinx <http://sphinx.pocoo.org/>`_ site itself -- see
..:ref:`custom_look`.
