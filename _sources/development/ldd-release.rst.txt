LDD Release Process
===================

When a Local Data Dictionary (LDD) Steward is ready to submit a new version of an LDD for release you have two options:

..  toctree::
    :maxdepth: 3

    *


(preferred) Tag a Release In Github
+++++++++++++++++++++++++++++++++++

1. Add your IngestLDD to the ``src/`` directory in your repo
2. Create a branch with ``release`` in the name.
3. Add your changes to the branch, commit, and put to Github
4. You should then see the LDD auto-generated (after ~2-3 minutes) in both the ``build/development`` and ``build/release`` directories.
5. Once you get approval from the appropriate stakeholders, merge your pull request.
6. You should then see a new release tagged in your repo in a URL like https://github.com/pds-data-dictionaries/ldd-img/releases
7. Then move on to ``Submit Release Request``


Submit Manually
+++++++++++++++

If you are unable to submit to Github, see Submit Release Request to upload a zip of your generated artifacts.


Submit Release Request
++++++++++++++++++++++

Create a `request ticket here <https://github.com/NASA-PDS/pdsen-operations/issues/new?assignees=c-suh%2C+elawsgh&labels=ldd-release&template=pds-ldd-release-request.md&title=%5Bldd-release%5D+%3CLDD+Name%3E+LDD+Version%3A%3CLDD_version%3E+IM+Version%3A%3CIM_Version%3E>`_.