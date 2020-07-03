LDD Creation Process
====================

Proposing a New Discipline LDD
++++++++++++++++++++++++++++++

Creation of a new Discipline LDDs should be discussed and approved by the `PDS Dictionary Stewards Group <mailto:pdsddstewards@jpl.nasa.gov>`_. During this process the following must be determined:

1. Is this LDD needed?
----------------------

Does a similar dictionary exist? If so, what is the rationale for creating a new one instead of adding to an existing one?

2. Who will be the LDD Steward(s)?
----------------------------------

One or more discipline node staff members must be appointed steward of the LDD.

3. Who will be on the LDD Change Control Board?
-----------------------------------------------

If this LDD is of interest to your Discipline Node, request of the newly appointed LDD Steward(s) to be added to the CCB.

----

Proposing a New Mission LDD
+++++++++++++++++++++++++++

Contact your Discipline Node to help you along this process. Many of the best practices and review rigor described below may not be necessary for Mission LDD development.

----

Requesting A New Namespace ID
+++++++++++++++++++++++++++++

Upon receiving approval to begin development on your new LDD, a namespace ID must be reserved.

Contact `Steve Hughes <mailto:John.S.Hughes@jpl.nasa.gov>`_ to get your namespace added to the `PDS4 Namespace Registry <https://pds.nasa.gov/datastandards/schema/pds-namespace-registry.pdf>`_.

----

Kick-off Team and Repo Creation
+++++++++++++++++++++++++++++++

Contact the `PDS Dictionary Stewards Admin Team <https://github.com/orgs/pds-data-dictionaries/teams/pds-dictionary-steward-admins/members>`_ to assist you with creating the appropriate Github Teams and LDD Repository as laid out below. These actions all require Github Admin access. Please provide them with the following information:

* namespace_id
* Brief description of the LDD. spell out namespace_id if it is an acronym.
* LDD Steward Github username
* CCB member Github Usernames

----

Create LDD Google Groups and Github Teams
+++++++++++++++++++++++++++++++++++++++++

1. Create Google Group
----------------------

.. note::
    Responsible Party: LDD Steward

a. Go to the `Google Groups site <https://groups.google.com/forum/#!creategroup>`_ to create the LDD User Group mailing list

b. Enter information according to the following guidelines:
    * **Group name:** ``pds-ldd-<namespace_id>-users``
    * **Group description:** Enter an appropriate description
    * The remaining can be left the same:
        * **Group type:** Email list
        * **Group visibility:** Anyone on the web
        * **View Topics:** All members of the group
        * **Post:** All members of the group
        * **Join the Group:** Anyone can ask

c. Click ``Create group``

d. Select ``Invite people to join the group`` or ``Invite members`` (depending on the screen that appears)

e. Invite appropriate members.

f. Repeat steps a-e to create LDD CCB group. Set **Group name:** ``pds-ldd-<namespace_id>-ccb``


2. Create Github Team
----------------------

.. note::
    Responsible Party: Member of `PDS Dictionary Stewards Admin Team <https://github.com/orgs/pds-data-dictionaries/teams/pds-dictionary-steward-admins/members>`_

a. `Create the LDD CCB Team <https://github.com/orgs/pds-data-dictionaries/new-team>`_ - **Team name:** ``pds-ldd-<namespace_id>-ccb``

b. Add LDD CCB members based upon input from LDD Steward.

----

Creating New LDD Repository
++++++++++++++++++++++++++++

Once you have your `Namespace ID <#Requesting-A-New-Namespace-ID>`_, you are ready to create the new Github repo for maintaining the LDD.

.. note::
    Responsible Party: Member of `PDS Dictionary Stewards Admin Team <https://github.com/orgs/pds-data-dictionaries/teams/pds-dictionary-steward-admins/members>`_


1. Create new repo from ldd-template
------------------------------------
a. `Create new repo <https://github.com/pds-data-dictionaries/ldd-template/generate>`_

b. Set the following parameters:
    * ``Owner``: ``pds-data-dictionaries``
    * ``Repository Name``: should follow the naming scheme ``ldd-<namespace_id>``.
    * ``Description``: enter description sent by LDD Steward
    * Set visibility to ``Public``
    * Check the box ``Include all branches``


2. Update Repo Settings
-----------------------

We need to setup the teams and ``master`` branch protections.

a. Go to ``Settings``

b. Add appropriate teams with access to repo
    * Go to ``Manage Access``
    * Click on ``Invite teams or people``
    * Add ``@pds-data-dictionaries/pds-dictionary-steward-admins`` with Admin access
    * Add the LDD Steward with Admin access
    * Add the LDD CCB Team with Write access

b. Set branches protections
    * Go to ``Branches``
    * Under **Branch protection rules**, click ``Add rule``
    * Enter **Branch name pattern:** ``master``
    * Select ``Require pull request reviews before merging``
    * Select ``Require review from Code Owners``
    * Select ``Restrict who can push to matching branches``


3. Update CODEOWNERS
--------------------

Updating this file will ensure the LDD-CCB is required for review on each pull request.

a. Go to `PDS Data Dictionaries org <https://github.com/pds-data-dictionaries>`_ and the appropriate new repo

b. Open up the `.github/CODEOWNERS` file

c. Uncomment this line and add the appropriate CCB Github Team name::

    *       @pds-data-dictionaries/pds-ldd-<namespace_id>-ccb

d. Commit your changes.


4. Notify LDD Steward
---------------------

Notify the LDD Steward the new repo is ready.


----

Notify LDD CCB and User Groups
++++++++++++++++++++++++++++++

.. note::
    Responsible Party: LDD Steward

Send an email notification to the LDD CCB and User Groups notifying them of the new LDD repo and development effort.

----

Initial Repo Updates
+++++++++++++++++++++

.. note::
    Responsible Party: LDD Steward

Update the ``Contribute`` section of your new repos ``README.md`` to reference the newly created mailing lists and Github teams.

----

Start Development
++++++++++++++++++

Ready to start development. See the `LDD Update Process <ldd-update>`_ for more information on submitting LDD updates.

