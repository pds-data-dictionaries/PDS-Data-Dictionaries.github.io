Tutorials
=========

..  toctree::
    :maxdepth: 3

    /support/tutorials


LDD Update and Build Tutorial
++++++++++++++++++++++++++++++

**Objective:**
    * create a test LDD Repository from the LDD Template
    * create a branch and pull request with the link to an issue
    * merge a pull request
    * see :doc:`Github Actions and LDD Continuous Integration <getting-started#ldd-generation-and-validation>` in action

**Pre-requisites:**
* :doc:`Github Recommended Training </support/github-help>`
* Github Desktop has been installed
* Github Desktop has been opened and you have logged into your Github.com account


1. Clone the ldd-template repository
-------------------------------------

Let's first, clone the repo from Github.com to our local computer.

a. Go to the `ldd-template repo`

b. Click the ``Use this template`` button to create a new repo from this template

..  image:: /images/screenshot_use_this_template.png
    :target: ../images/screenshot_use_this_template.png

c. You will then be taken to a screen to create your repo. Make sure ``Owner`` is set to your personal account, give it a name, and click ``Create repository from template``

..  image:: /images/screenshot_create_repo.png
    :target: ../images/screenshot_create_repo.png

d. Open Github Desktop. In the right column, either browse to or search for your repository, select ``Clone <username>/<repo-name>``

..  image:: /images/screenshot_clone_to_desktop.png
    :target: ../images/screenshot_clone_to_desktop.png

e. Choose the path your would like to save the repository to on your file system, and click ``Clone``.

TBD screenshot

e. You should now see a screen in Github Desktop that says ``No Local Changes``, indicating your repo is connected and there are no changes to that repo on your local system (as expected).

..  image:: /images/screenshot_github_desktop_init.png
    :target: ../images/screenshot_github_desktop_init.png

2. Create a Branch for Your Proposed Changes
--------------------------------------------

Now that we have the repo on our local machine, let's create a new branch to put our changes.

a. From Github Desktop, select the ``Current Branch`` dropdown, and select ``New Branch``.

..  image:: /images/screenshot_create_branch.png
    :target: ../images/screenshot_create_branch.png

f. Give some name to your branch (e.g. my_first_branch) and select ``Create Branch``

..  image:: /images/screenshot_create_branch.png
    :target: ../images/screenshot_create_branch.png

e. You should now be taken back to the main Github Desktop screen, and notice your ``Current Branch`` is now ``my_first_branch``.

..  image:: /images/screenshot_my_first_branch.png
    :target: ../images/screenshot_my_first_branch.png

f. We now want to edit the IngestLDD in the repo. This file is located within your new repo under ``my-ldd-test/src/PDS4_EXAMPLE_IngestLDD.xml``. This file can be opened from your favorite Editor. The Github Desktop main screen should also provide a button to ``View the files of your repository``, which will take you to the directory where the files exist on your local file system.

g. Once you have the file open