LDD Multifile Namespaces
=========================

..  toctree::
    :maxdepth: 3
    
    /development/ldd-multifile-namespace
    
----

What is a Multifile Namespace?
--------------------------------

A multifile namespace is a single namespace for which the definition has been
split across more than one *IngestLDD* file. These input files
are all fed into *LDDTool* in a single call, which produces a single, integrated set of output schemas. 

When Should I Create a Multifile Namespace?
++++++++++++++++++++++++++++++++++++++++++++

A namespace should be split into multiple files only when there is a significant benefit
to the dictionary steward(s) responsible for developing and maintaining the namespace. 
A namespace can be split structurally, so that different stewards can maintain separate class 
hierarchies within the namespace, or syntactically, to help a single steward wrangle a particularly
large namespace.

Structural Division
......................................

A multifile namespace is a reasonable way to deal with a very large namespace that naturally breaks into
several separate hierarchies that require
expertise from different people for definition and maintenance. Splitting the namespace definition into 
a set of *IngestLDD* files allows multiple stewards to focus on specific subsets of the namespace.
For example, a mission with both an orbiter and a lander may have a namespace model containing a small
mission class for common parameters and large, complex classes for each of the orbiter and lander.

Syntactical Division
.............................

It is also possible to split a namespace definition into 
separate files for attribute definitions, class definitions, and Schematron rules.
This might have bookkeeping benefits for a complex namespace that must be maintained by a 
single steward. 
Many humans, for example, find that a once an IngestLDD file is several thousand lines long, editing 
it becomes exponentially more onerous as it continues to grow. 
In a case like that, separate files can be used to create more easily managed pieces.

When Should I *Not* Create a Multifile Namespace?
+++++++++++++++++++++++++++++++++++++++++++++++++++

Splitting a namespace structurally into separate files will likely not help if the 
separate parts of the namespace 
have large areas of overlap, because the amount of coordination and cross-checking required when 
one part changes will likely negate any advantage to having separate files. 
A namespace in which the classes consist of different groupings of the same attributes, 
or that has many smaller classes that are "mixed and matched" into larger groups depending on the
observational circumstances, is probably best defined in a single IngestLDD file to avoid 
inadvertent duplication and name collisions.  

Splitting a namespace syntactically into separate files is not likely to have many benefits when 
the single IngestLDD version is less than a several thousand lines and well organized. In fact a
set of smaller, poorly organized files will probably not present an improvement on a single 
large, poorly organized file, either.

A multifile namespace solution is *not* recommended if there is no version control system
(like, for example, the `PDS Data Dictionaries repo <https://github.com/pds-data-dictionaries>`_) used 
by all stewards involved for managing the coordination of updating, building, and testing the 
LDDTool output.

Developing a Multifile Namespace 
-----------------------------------

Remember that a namespace is an *information model* for a specific context. It should be formally
designed even if it is expected to be rather small, and that design should include not just 
classes and attributes, but also the Schematron rules needed for validation of the associated
metadata.

** Structural division of a namespace should be done when the namespace is designed, NOT after it
is developed. Dividing a large, existing namespace is a complex and tedious process fraught with
peril. Avoid it if at all possible. **

Considerations for Splitting a Namespace Definition
++++++++++++++++++++++++++++++++++++++++++++++++++++

- Each *IngestLDD* containing part of the namespace definition *must* be a complete and syntactically
valid *IngestLDD* in its own right. When multiple files are used to coonstruct a single namespace, 
it is possible to have only attribute definitions in one file, only class definitions in another, 
and only Schematron rules in a third, but all files must have the same namespace identification
information at the top of the file.
- The requirements on what a namespace must contain (like at least one class defined with the
```<element_flag>``` attribute set to ```true```) apply across the set of files, not to individual
files.
- Any attribute or class defined in any of the files may be referenced in any of the other files.
While this means that no special syntax or ordering of files is required, it also means that the
stewards for the various parts need to coordinate attribute and class definitions entirely themselves
to avoid name collisions. It is possible to create name collision errors across files
that LDDTool would not be able to recognize and report.
- Likewise, the stewards of the individual parts must coordinate on the version numbering of the
namespace. All IngestLDD files comprising the namespace definition *must* have the same value for
```<ldd_version_id>```.

Recommended Development Practice
+++++++++++++++++++++++++++++++++++

It is easier to plan to partition a namespace structurally into multiple files from the start 
than attempt to break an existing namespace up. 
If separating your namespace into files for each major class hierarchy seems like a good
idea, start with a formal namespace design. 
Mapping the class structure and dependencies out explicitly
should make it clear whether the model is a good candidate to be partitioned into 
multiple input files.  If so, here are some addition development suggestions:

# If the design contains classes and attributes that would be referenced in multiple files of 
the namespace, consider grouping those into a "common" or "shared" file. Having one file
where common attributes and classes are defined will likely be easier to maintain than having to 
track inter-file dependencies among all your input files, at least in cases where the namespace 
is split among three or more files.
# The stewards should agree on and document (for themselves, at least) the nomenclature and 
name formation standards to
use across all the IngestLDD files. Inconsistency in use of capitalization, punctuation, and
abbreviations in class and attribute names within a single namespace tends to undermine
user confidence in the information provided, as well as annoying programmers trying to make
use of your namespace metadata.
# Similarly, stewards should probably agree on and certainly document how each constituent
IngestLDD file is ordered (are attributes alphabetical or grouped by function; are classes
defined in label order or some other order; etc.). This will make it easier for the steward
of one file to check another file for possible collisions/duplications rather than hoping
LDDTool can catch them all. 
# Test labels and user documents are recommended for all namespaces (they are required
for discipline namespaces). In the case of multi-file namespaces, it is *strongly* recommended
that stewards for each file supply regression test labels for the part of the namespace
they are developing to help insure that there is no inadvertent collision between input 
files that slips past LDDTool processing. Documentation is a further tool for helping to 
ensure harmony among the input files.

Coding the IngestLDD Files
++++++++++++++++++++++++++++

Once the namespace is designed and partitioned, the coding of the separate IngestLDD files is 
not much different from coding for a single-file namespace, but there are some things to
keep in mind:

- As with a single-file namespace, there must be one class defined as an XML *element* (with
```<element_flag>true</element_flag>``` in its definition in one of the input files. 
This will be the "wrapper class" or "entry point" for the namespace - the highest-level 
class a user can include in a label. Having more than one entry point is generally not
advised, although sometimes that makes sense (check with your PDS node when in doubt).
- It is harder to test
a single input file in isolation. LDDTool will do the best it can to produce valid output, 
but you will get errors
for missing attribute and class definitions (and other namespace compliance issues) if there
are any dependencies on things defined in other namespace files. 
o For testing the build of a single file of a multipart namespace, you might need a second
file to provide a *wrapper class* for testing only. Testing classes should *always* be in a
separate file from the "real namespace" because they should not be visible to end users
of your namespace schemas.
o If your part of the namespace depends on definitions in a common/shared file, you will need
that to build you test schemas with as well.

Examples
-----------

The Geometry Discipline namespace has been structurally divided.

As yet, no namespace has been divided syntactically.