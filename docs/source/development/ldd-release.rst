LDD Release Process
===================

When a Sub-Model Steward is ready to submit a new version of an LDD for release you have two options:

..  toctree::
    :maxdepth: 3

    /development/ldd-release

----

Release
+++++++

Nominal Development and Release
-------------------------------

The ideal workflow for tagging a release happens every 6 months in line with the `PDS4 Build Schedule <https://pds.jpl.nasa.gov/datastandards/about/>`_. Here is the process:

1. Develop
~~~~~~~~~~
**Responsible Party: Sub-Model Steward**

In between build cycles, you are free to develop/enhance/upgrade your sub-model, making sure to update the sub-model version as appropriate and all your updates are merged into the ``main`` branch.

2. Wait
~~~~~~~
**Responsible Party: Sub-Model Steward**

If you have completed development, you do not need to do anything else to prepare or tag your release. This will be done later by Engineering Node automation. See `Key Dates <https://nasa-pds.github.io/releases/current/plan.html#key-dates>`_ for more information on timeframe for release.

3. Staging Nominal Release
~~~~~~~~~~~~~~~~~~~~~~~~~~
**Responsible Party: Engineering Node**

EN will "stage the release" of the sub-model by automatically generating a Pull Request on your repository. The Pull Request will include an update to include the latest PDS4 Information Model version, all schemas/schematrons will be regenerated and tests executed via the Sub-Model Automation.

4. Review and Merge Pull Request
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Responsible Party: Sub-Model Steward**

Once you receive notification of the staged release, it is the responsibility of the **Sub-Model Steward** to:

a. `Review the pull request </development/ldd-how-to.html#reviewing-a-pull-request>`_ - the Sub-Model Steward and associated Stewardship Team (as applicable) should review the regression tests passed as expected, and the schemas/schematrons generated are correct.

b. `Merge the pull request </development/ldd-how-to.html#merging-an-approved-pull-request>`_ - merge the pull request to automatically tag a new version of the sub-model in GitHub.

.. note::
    If the Sub-Model Steward does not merge the pull request, the sub-model will not be released with the latest version of the Information Model. Text will be included on the web page notifying users they can submit a request that a new version be produced.

.. warn::
    Only the version of the sub-model associated with the new PDS4 Information Model will be included in the final "Deploy Nominal Release" step. A separate :ref:`Release Request` is required for any past version(s) of the sub-model you would like released.


5. Deploy Nominal Release
~~~~~~~~~~~~~~~~~~~~~~~~~
**Responsible Party: Engineering Node**

On the PDS System Release Date, EN will pull all the tagged releases from all the repos, generate the applicable web pages, and release all of the sub-models online.

.. note::
    Only the version of the sub-model associated with the new PDS4 Information Model will be included in the final "Deploy Nominal Release" step. A separate :ref:`Release Request` is required for any past version(s) of the sub-model you would like released.*

----

Off-Nominal Release 
-------------------

.. note::
    Please try to avoid this wherever possible. In order to minimize overhead of manual processing of sub-models, please coordinate with data providers to stick to the `PDS4 Build Schedule <https://pds.nasa.gov/datastandards/about/>`_ wherever posisble.

    At any time, you can direct providers to the ``build/development`` directory of your Sub-Model repository in order for them to have immediate access to the dictionaries for development and testing purposes.

If an immediate bug fix and release is needed off PDS4 Build cycle, see the :ref:`Preparing a Release` for instructions for how to tag a release.

----

Preparing a Release
+++++++++++++++++++

Check Github for Tagged Released
--------------------------------
Before you tag a release in Github, verify the version you would like released has not already been tagged by EN Automation.

1. Go to your repo's release page, e.g. https://github.com/pds-data-dictionaries/ldd-img/releases.
2. If the version you would like released appears in the list, proceed to :ref:`Submit Release Request`, otherwise proceed to "Tag a Release in Github".


Tag a Release In Github
-----------------------
1. Add your IngestLDD to the ``src/`` directory in your repo
2. Create a branch with ``release`` in the name, e.g. ``release/1.18.0.0_1.1.0.0``
3. If the intent is to release a sub-model with a past PDS4 Information Model version, see documentation for `Changing PDS4 Build Versions </development/ldd-how-to.html#how-to-change-pds4-build-versions>`_.
4. Add your changes to the branch, commit, and push branch to Github. Be sure to push your branch even if you have no changes to commit.
5. If you did not have any changes to commit, you can manually trigger the build of the LDDs by:
   a. Select the ``Actions`` tab
   b. Under the ``Actions`` left sidebar, select ``PDS4 Sub-Model Automation``
   c. From the blue row in the table, select the ``Run Workflow`` dropdown.
   d. Select your branch from the dropdown.
   e. Select the ``Run Workflow`` button.
6. Create a Pull Request for your branch.
7. Optional: monitor the generation of the dictionaries via the ``Actions`` tab in your Github repository.
8. Once the build completes, you should see the new LDD auto-generated (after ~2-3 minutes) in both the ``build/development`` and ``build/release`` directories.
9. Once you get approval from the appropriate stakeholders, merge your pull request.
10. You should then see a new release tagged in your repo in a URL like https://github.com/pds-data-dictionaries/ldd-img/releases
11. Then move on to :ref:`Submit Release Request` below to submit ticket to the EN Operations Github repo.


Submit Release Request
----------------------

Submit a ``PDS LDD Release`` request request ticket `here <https://github.com/NASA-PDS/pdsen-operations/issues/new/choose>`_.

----

Reviewing a Staged Release
++++++++++++++++++++++++++

See the :doc:`Review a Pull Request How-to </development/ldd-how-to>`

