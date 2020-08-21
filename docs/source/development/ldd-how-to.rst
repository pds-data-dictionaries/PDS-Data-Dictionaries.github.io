LDD How-To Guides
===================

..  toctree::
    :maxdepth: 3

    /development/ldd-how-to


How to trigger an LDD Build?
++++++++++++++++++++++++++++

For this example we will be using the `IMG Discipline LDD <https://github.com/pds-data-dictionaries/ldd-img>`_ repo. For your repo, just replace the `ldd-img` or references to `IMG` with your appropriate discipline dictionary.

1. `Create a new branch for your updates <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/managing-branches>`_ (if you have not already created one).
2. Update your IngestLDD file (e.g. PDS4_IMG_IngestLDD.xml).
3. `Commit your changes <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/committing-and-reviewing-changes-to-your-project>`_.
4. `Push your branch to Github <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/pushing-changes-to-github>`_
5. Watch the magic happen on your Github Actions page: https://github.com/pds-data-dictionaries/ldd-img/actions
6. After the action has completed successfully (hopefully), update your local branch (`Git Pull <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/syncing-your-branch#:~:text=onto%20another%20branch.%22-,Pulling%20to%20your%20local%20branch%20from%20the%20remote,branch%20you%20want%20to%20update.&text=To%20pull%20any%20commits%20from,or%20Pull%20origin%20with%20rebase.>`_) to get the generated dictionaries from Github.com


TBD
+++
Feel free to add some of your own or create a ticket in the `PDS4 LDD Issue Repo <https://github.com/pds-data-dictionaries/PDS4-LDD-Issue-Repo/issues>`_ so we can start to build up this documentation.