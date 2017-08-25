################################################
Patterns: Command-Line Interface Design Patterns
################################################

[Raym03]_

.. hint::

    Commands may have modes that fit more than one interface pattern. 

==============
Filter pattern
==============

  stdin --> transform-data --> stdout

===============
Cantrip pattern
===============

  do-something

.. note::

    No input or output.

==============
Source pattern
==============

  generate-data --> stdout

.. note::
    
    No input.

============
Sink pattern
============

  stdin --> process-data

.. note::

    No output.

================
Compiler pattern
================

  resource-name/file --> process-contents --> transformed-resource-name/file

.. note::

    Any of the patterns listed above can to write to stderr.

There are other patterns, but they are designed for highly interactive
environments and outside the scope of this publication.

