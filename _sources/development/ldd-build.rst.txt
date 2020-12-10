LDD Build Process
=============================

..  toctree::
    :maxdepth: 3

    /development/ldd-build


Build LDD Using Github
++++++++++++++++++++++

By default, as long as your Discipline LDD is using the `ldd-template repository <https://github.com/pds-data-dictionaries/ldd-template/>`_, all Discipline LDD schemas, schematrons, and other default LDDTool outputs are generated whenever a Pull Request is created with a change to an IngestLDD.

The new schemas/schematrons are posted to the `build/development` directory in your repository. See :doc:`LDD Update and Build Tutorial </support/tutorials>` for an example generating these schemas/schematrons.


For more details on how the dictionaries are generated, see `LDD Github Actions`.


---

Build LDD Using LDDTool
+++++++++++++++++++++++

See `LDDTool documentation <https://nasa-pds.github.io/pds4-information-model/model-lddtool/>`_.

----

Changing PDS4 Build Versions
++++++++++++++++++++++++++++

LDDTool is backwards compatible with PDS4 version 1.11.0.0 and later. When using the ldd-template repo, your LDD will automatically be built with the latest version of the PDS4 IM. Here are the steps to change that version:

1.  Open pds4_versions.txt (in the base of your repo)
2.  Change the add a new line with the applicable version you would like use::
 
        1.13.0.0
        1.14.0.0
        1.15.0.0



