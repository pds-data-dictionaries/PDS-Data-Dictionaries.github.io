LDD Build Process
=================

Using Github
++++++++++++++++++++

Nominal Release with PDS4 Information Model
-------------------------------------------

By default, all Discipline LDDs will be built at the time of PDS4 IM Release. See the `PDS4 Build Schedule <https://pds.jpl.nasa.gov/datastandards/about/>`_ for more details on the timing of those builds.


Off-Nominal Release 
-------------------

In order to minimize overhead with releasing of LDDs, please coordinate with data providers to use the released dictionaries deployed during the Nominal Release process on the PDS4 Information Model build cycle. At any time, you can direct providers to the `build/development` directory of your LDD repository in order for them to have immediate access to the dictionaries for development and testing purposes.

If an immediate bug fix and release is needed off PDS4 build cycle, see the :doc:`LDD Release Process </development/ldd-release>` for instructions for how to tag a release.

----

Development Release
+++++++++++++++++++

By default, as long as your Discipline LDD is using the ldd-template repository (TBD link), all Discipline LDD schemas, schematrons, and other default LDDTool outputs are generated whenever a Pull Request is created with a change to an IngestLDD.

The new schemas/schematrons are posted to the TBD directory in your repository. See :doc:`LDD Update and Build Tutorial </support/tutorials>` for an example generating these schemas/schematrons.


For more details on how the dictionaries are generated, see `LDD Github Actions`.


----

Changing PDS4 Build Versions
++++++++++++++++++++++++++++

LDDTool is backwards compatible with PDS4 version 1.11.0.0 and later. When using the ldd-template repo, your LDD will automatically be built with the latest version of the PDS4 IM. Here are the steps to change that version:

1.  Open .github/workflows/ldd-ci.yml
2.  Change the ``strategy.matrix.pds4_version`` to be the version(s) you want (note: be sure to keep the brackets surrounding the version(s) [ ] ). For example to change to built with PDS4 versions 1.12.0.0 and 1.13.0.0::
 
        strategy:
          matrix:
            pds4_version: [ '1.12.0.0', '1.13.0.0' ]
