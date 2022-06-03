LDD How-To Guides
===================

..  toctree::
    :maxdepth: 3

    /development/ldd-how-to

----

Trigger LDD Build
+++++++++++++++++

For this example we will be using the `IMG Discipline LDD <https://github.com/pds-data-dictionaries/ldd-img>`_ repo. For your repo, just replace the `ldd-img` or references to `IMG` with your appropriate discipline dictionary.

1. `Create a new branch for your updates <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/managing-branches>`_ (if you have not already created one).
2. Update your IngestLDD file (e.g. PDS4_IMG_IngestLDD.xml).
3. `Commit your changes <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/committing-and-reviewing-changes-to-your-project>`_.
4. `Push your branch to Github <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/pushing-changes-to-github>`_
5. Watch the magic happen on your Github Actions page: https://github.com/pds-data-dictionaries/ldd-img/actions
6. After the action has completed successfully (hopefully), `update your local branch <https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/syncing-your-branch>`_ to get the generated dictionaries from Github.com

----

Generate a Discipline LDD
+++++++++++++++++++++++++

To generate a Discipline LDD versus a Mission LDD, you must specify this information within the IngestLDD, for example::

        <name>Imaging Discipline Dictionary</name>
        <ldd_version_id>1.0.0.0</ldd_version_id>
        <dictionary_type>Discipline</dictionary_type>

See the `Imaging Discipline LDD <https://github.com/pds-data-dictionaries/ldd-img/blob/main/src/PDS4_IMG_IngestLDD.xml>`_ for a more detailed example.

Then execute LDDTool to generate the appropriate dictionary::

    lddtool -lp <my_ingest_ldd>

----

Generate a Mission LDD
++++++++++++++++++++++

To generate a Mission LDD versus a Discipline LDD, you must specify this information within the IngestLDD, for example::

        <name>Mars 2020 Mission</name>
        <ldd_version_id>1.0.0.0</ldd_version_id>
        <dictionary_type>Mission</dictionary_type>

See the `Mars 2020 Mission LDD <https://github.com/pds-data-dictionaries/ldd-m2020/blob/main/src/PDS4_M2020_IngestLDD.xml>`_ for a more detailed example.

Then execute LDDTool to generate the appropriate dictionary::

    lddtool -lp <my_ingest_ldd>


----

Generate a LDD with a specific PDS4 Version
+++++++++++++++++++++++++++++++++++++++++++

LDDTool is a reflection of the PDS4 Information Model (IM), and in turn, has a major build in sync with the `PDS4 Build Schedule <https://pds.nasa.gov/datastandards/about/>`_ (every 6 months).

By default, LDDTool builds with the latest version of the IM. As of LDDTool v12.0.0, it can now generate LDDs for older versions of the IM using the -V flag::

      -V, --IM Version - E.g., -V 1D00


----

Specify Enumerated Values for Attributes within Inherited Classes
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Classes from the PDS common dictionary (or discipline LDDs) are often inherited and used within Discipline and Mission LDDs (e.g. ``Internal_Reference.reference_type``, etc.). When inherited within the specific Discipline or Mission, you may want to provide a specific set of values applicable for that particular context. In this case you would want to use the `DD_Associate_External_Class <https://pds.nasa.gov/datastandards/documents/im/current/index_1E00.html#18.9%C2%A0%C2%A0class_pds_dd_associate_external_class>`_. For example:::

    <DD_Associate_External_Class>
      <namespace_id>pds</namespace_id>
      <class_name>Local_Internal_Reference</class_name>
      <minimum_occurrences>0</minimum_occurrences>
      <maximum_occurrences>1</maximum_occurrences>
      <DD_Context_Value_List>
         <attribute_name>local_reference_type</attribute_name>
         <attribute_relative_xpath>local_reference_type</attribute_relative_xpath>
         <DD_Permissible_Value>
             <value>spectral_characteristics_to_array_object</value>
             <value_meaning>
               The spectral parameters describe the array associated
               with the given 'local_identifier'.
             </value_meaning>
         </DD_Permissible_Value>
         <DD_Permissible_Value>
             <value>spectral_characteristics_to_table_object</value>
             <value_meaning>
               The spectral parameters describe the table or specific
               fields in the table associated with the given
               'local_identifier'.
             </value_meaning>
         </DD_Permissible_Value>
      </DD_Context_Value_List>
    </DD_Associate_External_Class>

----

Schematron (DD_Rule) Help
+++++++++++++++++++++++++

Specify Enumerated Values for Inherited Attributes
--------------------------------------------------

Attributes from the PDS common dictionary (or discipline LDDs) are often inherited and used within Discipline and Mission LDDs (e.g. ``pds:name``, etc.). When inherited within the specific Discipline or Mission, you may want to provide a specific set of values applicable for that particular context. In this case you will need to specify a DD_Rule to provide the enumerated value list. For example:::

    <DD_Rule>
        <local_identifier>color_filter_array_state_check</local_identifier>
        <rule_context>//img:Color_Filter_Array</rule_context>
        <DD_Rule_Statement>
          <rule_type>Assert</rule_type>
          <rule_test>img:color_filter_array_state = ('Encoded', 'Decoded', 'No CFA')</rule_test>
          <rule_message>IMG:error:img:color_filter_array_state_check: img:color_filter_array_state must be equal to one of the following values:
            'Encoded', 'Decoded', 'No CFA'.
          </rule_message>
        </DD_Rule_Statement>
    </DD_Rule>

----

Using Schematron ``value-of`` functionality
++++++++++++++++++++++++++++++++++++++++++++

To use the ``sch:value-of`` in your ``DD_Rule`` descriptions, you simply need to escape the XML entities. For example::

    <sch:rule context="msn:mission_phase_name">
        <sch:let name="num_colons" value="string-length(.) - string-length(translate(., ':', ''))"/>
        <sch:let name="required_colons" value="4"/>
        <sch:assert test="$num_colons eq $required_colons">
            In Product_Collection, the number of colons found:
            (&lt;sch:value-of select="$num_colons"/&gt;)
            is inconsistent with the number expected:
            (&lt;sch:value-of select="$required_colons"/&gt;).
        </sch:assert>
        </sch:rule>
    </sch:pattern>

Note the ``&lt;``` and ``&gt;`` used to replace the ``<`` and ``>``

----

Mission LDD Namespace Formation Guidelines
++++++++++++++++++++++++++++++++++++++++++++

.. note::
    The determination of LDD namespaces is ultimately up to the discussion amongst the Mission Data Archive Working Group (DAWG). This is simply a guide to enable consistency wherever possible.

For **mission namespaces**, use the *mission acronym or shortened name*. For example:

* bc for BepiColombo
* m2020 for Mars2020
* insight for InSight
* orex for OSIRIS-REx

for **instrument-specific namespaces**, use the formation rule *mission_host_instrument*. For example:

* bc_mtm_mcam for the MCAM instrument on the Mercury Transfer Module (MTM) instrument host of the BepiColombo mission

----

Basics For Creating an Ingest LDD
+++++++++++++++++++++++++++++++++

See the `Small Bodies Node wiki <http://sbndev.astro.umd.edu/wiki/Creating_the_Ingest_LDD_Dictionary_Input_File>` on creating an Ingest LDD file.

----

Reviewing a Pull Request
++++++++++++++++++++++++

1. Go to ``Pull Requests`` tab of your repo, e.g. https://github.com/pds-data-dictionaries/ldd-spectral/pulls:

.. image:: /_static/images/screenshot_pull_requests.png
   :target: ../_static/images/screenshot_pull_requests.png

2. Select the open Pull Request for the new release (e.g. https://github.com/pds-data-dictionaries/ldd-spectral/pull/13)

.. image:: /_static/images/screenshot_release_pull_request.png
   :target: ../_static/images/screenshot_release_pull_request.png

3. The first check should always be if the LDD Github Build completed successfully. You should see a green check mark next to the last commit on the branch:

.. image:: /_static/images/screenshot_action_success_1.png
   :target: ../_static/images/screenshot_action_success_1.png

.. image:: /_static/images/screenshot_action_failure_1.png
   :target: ../_static/images/screenshot_action_failure_1.png

Or you can go to the ``Actions`` tab (e.g. https://github.com/pds-data-dictionaries/ldd-spectral/actions) and verify the last build has a green checkmark next to it:

.. image:: /_static/images/screenshot_action_success_2.png
   :target: ../_static/images/screenshot_action_success_2.png

.. image:: /_static/images/screenshot_action_failure_2.png
   :target: ../_static/images/screenshot_action_failure_2.png


4. Once the build has been verified, there are now 2 ways you can review the changes the files:
    a. Select the ``Files changed`` tab, and look through the changed files (e.g. https://github.com/pds-data-dictionaries/ldd-spectral/pull/13/files). You can search on the page for `IngestLDD` if you simply want to review the changes to that file:

    .. image:: /_static/images/screenshot_pr_files_changed.png
       :target: ../_static/images/screenshot_pr_files_changed.png

    b. Select the applicable branch, and browse through the files in the repository. The `IngestLDD` is located under the `src/` directory.

    .. image:: /_static/images/screenshot_pr_branch.png
       :target: ../_static/images/screenshot_pr_branch.png

5. Once you have verified all changes, you can approve the Pull Request in Github by going to the ``Files changed`` tab of the Pull Request, and input your review:

.. image:: /_static/images/screenshot_pr_review.png
  :target: ../_static/images/screenshot_pr_review.png

----

Merging an Approved Pull Request
+++++++++++++++++++++++++++++++++

See applicable Github docs: https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/merging-a-pull-request

----

Generate Human Readable Versions of the LDD
+++++++++++++++++++++++++++++++++++++++++++++++++++++++

LDDTool + Oxygen can be used to generate human readable versions of the data dictionary, the XML file is processed into HTML, PDF, and a WebHelp format. For example:

* `PDS4 Data Dictionary (html) <https://pds.nasa.gov/datastandards/documents/dd/current/PDS4_PDS_DD_1F00.html>`_
* `PDS4 Data Dictionary (pdf) <https://pds.nasa.gov/datastandards/documents/dd/current/PDS4_PDS_DD_1F00.pdf>`_
* `PDS4 Data Dictionary (WebHelp) <https://pds.nasa.gov/datastandards/documents/dd/current/PDS4_PDS_DD_1F00/webhelp/all/>`_

This is described on the PDS4 Information Model and LDDTool wiki here: `<https://github.com/NASA-PDS/pds4-information-model/wiki/Generating-Data-Dictionary-Documentation>`_

----

Use Multiple Files to Define a Single Namespace
+++++++++++++++++++++++++++++++++++++++++++++++

Sometimes a namespace requires more than one steward to provide expertise on different aspects of the namespace. The
`Geometry Discipline namespace <https://github.com/pds-data-dictionaries/ldd-geom/tree/main/src>`_, for example, has separate
stewards for the classes related to fly-by/orbiter observations and lander observations. In a case like this you might find it preferable to split the namespace definition
into one file for each steward.

The LDD repo and LDDTool can build a single namespace from multiple files, but developing and maintaining this set of files comes with some special problems and considerations
you should be aware of before you start. If you're considering this option for your namespace,
read `Multifile Namespaces <https://pds-data-dictionaries.github.io/development/ldd-multifile-namespace.html>`_.

----

Merge A New Release Branch Into My Current Working Branch
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

In the event that you are working on updates to your LDD in a branch or pull request when a PDS4 system release is about to take place, you may wind up with a new branch and pull request being created.

If you plan to include your updates in the next release, the best route to take is to merge your updates into the newly created release branch.

Here are the steps to do so:

1. Checkout your branch from Github (e.g. ``my_working_branch_v1``)
2. Checkout the newly auto-generated release branch (e.g. ``release/1.17.0.0``)
3. Merge your working branch into the release branch.

.. note::
    Be sure to merge ``my_working_branch_v1`` into ``release/1.17.0.0`` (``release/1.17.0.0`` should become your new working branch) so ensure the release is tagged and included in the system release.

Via command-line::

    git merge origin my_working_branch_v1
    
Via Github Desktop:

.. image:: /_static/images/screenshot_merge1.png
  :target: ../_static/images/screenshot_merge1.png
  
.. image:: /_static/images/screenshot_merge2.png
  :target: ../_static/images/screenshot_merge2.png

----

How to Change PDS4 Build Versions
+++++++++++++++++++++++++++++++++

LDDTool is backwards compatible with PDS4 version 1.11.0.0 and later. When using the sub-model template repo, your sub-model automatically builds with the latest version of the PDS4 IM. Here are the steps to change that version or add additional versions:

1.  Open pds4_versions.txt (in the base of your repo), e.g. https://github.com/pds-data-dictionaries/template/blob/main/pds4_versions.txt

2.  Add new line with the applicable version you would like use::
 
        1.13.0.0
        1.14.0.0
        1.15.0.0

.. warn::
   The Sub-Model automated generation only builds the last 4 versions specified in the pds4_versions.txt file. For later versions of the PDS4 Information Model, move that version number to the end of the file.

----

TBD
+++
Feel free to add some of your own or create a ticket in the `PDS4 LDD Issue Repo <https://github.com/pds-data-dictionaries/PDS4-LDD-Issue-Repo/issues>`_ so we can start to build up this documentation.
