LDD Release Process
===================

When a Local Data Dictionary (LDD) Steward is ready to submit a new version of an LDD for release you have two options:

..  toctree::
    :maxdepth: 3

    /development/ldd-release

----

Release Timeframe
+++++++++++++++++

Nominal Release with PDS4 Information Model
-------------------------------------------

By default, all Discipline LDDs will be built at the time of PDS4 IM Release. See the `PDS4 Build Schedule <https://pds.jpl.nasa.gov/datastandards/about/>`_ for more details on the timing of those builds.


Off-Nominal Release 
-------------------

.. note::
    Please try to avoid this wherever possible. In order to minimize overhead of manual processing of LDDs, please coordinate with data providers to stick to the `PDS4 Build Schedule <https://pds.jpl.nasa.gov/datastandards/about/>`_ wherever posisble.

    At any time, you can direct providers to the `build/development` directory of your LDD repository in order for them to have immediate access to the dictionaries for development and testing purposes.

If an immediate bug fix and release is needed off PDS4 Build cycle, see the :ref:`Preparing a Release` for instructions for how to tag a release.

----

Preparing a Release
+++++++++++++++++++

(preferred) Tag a Release In Github
-----------------------------------

1. Add your IngestLDD to the ``src/`` directory in your repo
2. Create a branch with ``release`` in the name.
3. Add your changes to the branch, commit, and push to Github. If you do not have any changes to commit, you can perform an empty commit. For example::

    git commit --allow-empty "Prep for tagging release"

4. You should then see the LDD auto-generated (after ~2-3 minutes) in both the ``build/development`` and ``build/release`` directories.
5. Once you get approval from the appropriate stakeholders, merge your pull request.
6. You should then see a new release tagged in your repo in a URL like https://github.com/pds-data-dictionaries/ldd-img/releases
7. Then move on to **Submit Release Request** below.


Submit Manually
---------------

If you are unable to submit to Github, see **Submit Release Request** to upload a zip of your generated artifacts.


Submit Release Request
----------------------

Create a `request ticket here <https://github.com/NASA-PDS/pdsen-operations/issues/new?assignees=c-suh%2C+elawsgh&labels=ldd-release&template=pds-ldd-release-request.md&title=%5Bldd-release%5D+%3CLDD+Name%3E+LDD+Version%3A%3CLDD_version%3E+IM+Version%3A%3CIM_Version%3E>`_.

----

Reviewing a Staged Release
++++++++++++++++++++++++++

See the :doc:`Review a Pull Request How-to </development/ldd-how-to>`