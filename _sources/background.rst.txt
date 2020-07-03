Getting Started
===============

Background
++++++++++

The PDS4 Information Model, PDS4 Data Dictionary, and their XML representation in the PDS4 Common Schema and Schematron serve as a library of generic definitions for each PDS4 product type. PDS also maintains data dictionaries for specialized disciplines such as geometry and cartography and for specific planetary missions; these are called Local Data Dictionaries or LDDs. They are also expressed as XML schemas for use in PDS labels. The PDS4 Schema and all current Local Data Dictionary schemas are available at https://pds.nasa.gov/datastandards/schema/released/.

When a schema is used in a PDS4 label it is associated with a namespace. A namespace is a
context for the terms defined in the schema. The common PDS4 schema has the namespace pds,
and it is the default namespace in a PDS4 label. Other namespaces correspond to Local Data
Dictionaries such as cart for the `Cartography Dictionary <https://pds.nasa.gov/datastandards/dictionaries/#cart>`_, disp for the `Display Dictionary <https://pds.nasa.gov/datastandards/dictionaries/#disp>`_, and mvn
for the `MAVEN Mission Dictionary <https://pds.nasa.gov/datastandards/dictionaries/#mvn>`_ If classes or attributes from other namespaces are used in the label, the terms are prefixed with that namespace, as in ``cart:map_projection_name`` and ``disp:vertical_display_direction``. Only namespaces that are registered in the Namespace Registry may be used in PDS4 labels (https://pds.nasa.gov/datastandards/schema/pdsnamespace-registry.pdf).

When you prepare data for delivery to PDS, you will certainly be involved in creating labels; you may also be involved in creating discipline- or mission-specific LDDs. This section will focus on the components of labels, design choices you will need to make, and tools you can use. Basic information about XML and XML schemas can be found in Appendix C, specific instructions for editing PDS XML labels are in Appendix D, and a discussion about creating Local Data Dictionaries is available on the Small Bodies Node PDS4 Wiki (https://sbnwiki.astro.umd.edu).

For more details, see the `PDS4 Data Provider's Handbook (DPH) <https://pds.jpl.nasa.gov/datastandards/documents/dph/current/>`_, `PDS4 Standards Reference (SR) <https://pds.jpl.nasa.gov/datastandards/documents/sr/current/>`_, and of the other `PDS4 Standards Documentation <https://pds.jpl.nasa.gov/datastandards/documents/>`_.


Additional Information
++++++++++++++++++++++

Here are some additional websites that may help provide more details about NASA Planetary Data System (PDS), our international partners at the International Planetary Data Alliance (IPDA), and the PDS4 Data Standard:

* Planetary Data System (PDS) Homepage - https://pds.nasa.gov/
* International Planetary Data Alliance (IPDA) Homepage - https://planetarydata.org/
* PDS4 Data Standards - https://pds.nasa.gov/datastandards/about/