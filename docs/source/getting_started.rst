.. _policies: policies.html
.. _using_lux: using_lux.html
.. _project_team: project.html#project_team
.. _acknowledgments: policies.html#acknowledgments
.. _email_brant: brant@ucsc.edu

.. _getting_started:


*******************************
Getting Started
*******************************


.. _read_the_docs:

Read the User Policies
==================================

First things first -- please read the *lux* `Policies <policies_>`_. All *lux* users must understand and abide by the system policies as a condition of using the computer. This includes `acknowledging lux in publications <acknowledgments_>`_ when used and following the user best practices.

.. _getting_an_account:

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
Co-Is may grant external (outside UCSC) collaborators access by requesting a UCSC Sundry account (see instructions `here <https://its.ucsc.edu/accounts/forms.html>`_ or submit a Sundry account `request <https://ucsc.service-now.com/nav_to.do?uri=com.glideapp.servicecatalog_cat_item_view.do?sysparm_id=1141fa213c9799008065d4c384368f19&sysparm_stack=no>`_), which will provide a limited time but renewable CruzID for their collaborator. *When requesting a Sundry account please request that the account receive the Gold Active Directory (AU) resource to enable access to the lux cluster.* Once a CruzID is assigned and a Gold password set, the faculty lead can add their collaborator to their group directly. Please be mindful that *lux* was funded to support research at UCSC, and these external collaborators gain the same privileges as other UCSC Co-I research group members. External collaborators still must agree to acknowledge *lux* in their resulting publications.  Only Co-I faculty leads can grant external collaborators access to *lux*.

Accounts for UCSC visitors
--------------------------
Visitors to UCSC who are associated with Co-I research groups may be able to obtain accounts following the instructions for `external collaborators <external_collaborators_>`_. Groups of visitors may also be granted access under special circumstances, please contact `Brant Robertson <email_brant_>`_ for more information. All visiting users must agree to acknowledge *lux* in any resulting publications.

.. _connecting_to_lux:

Connecting to *lux*
===================

Here are step-by-step instructions for connecting to *lux*:

  1) Request an authorized account, following the above `instructions <getting_an_account_>`_.

  2) Connect to the UCSC Campus VPN using your CruzID and Gold password via the UCSC VPN client. Installation instructions for the VPN client are available on the ITS `website <https://its.ucsc.edu/vpn/installation.html>`_. If you have not reset your Gold password recently, you may need to do so in order to connect to the system (visit `cruzid.ucsc.edu <https://cruzid.ucsc.edu>`_). You will need to enroll a device in Duo for Multifactor Authentication to connect to the VPN.

  3) Connect to the *lux* system via Secure Shell::

      $ ssh [cruzid]@lux.ucsc.edu

    Where [cruzid] is your CruzID. When prompted, provide your Gold password and select a Duo MFA method. You will be directed to one of the three login nodes (*lux-0*, *lux-1*, or *lux-2*) where you can submit jobs to the system queues.

  4) See `Using lux <using_lux_>`_ for further instructions.
