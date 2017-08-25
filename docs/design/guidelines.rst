#########################################################
Guidelines: POSIX Guidelines, GNU Standards & Portability
#########################################################

==========================
Cross-Platform Portability
==========================

Command-line utilities should comply with the `essential` components of:

1. The `POSIX.1-2008 Utility Syntax Guidelines`_.
2. The `GNU standards for Command Line Interfaces`_.

By following these guidelines and standards your command-line tools will
provide a level of consistency and familiarity to users working across many
different platforms, such as Linux, Mac OsX\ :sup:`®`, and Windows\
:sup:`®`.

.. hint::

    Do not blindly implement these guidelines & standards in their
    entirety; instead focus on the commonly practiced conventions within each.
    This document is designed to help highlight what those conventions are.

=========================
Cross-Version Portability
=========================

If you plan to share your utility with the world the Command-Line Interface
(CLI) and Input/Output (I/O) functions should be designed to work across all
standard versions of Python 2.6, 2.7 & 3.3+.  It's best to put your
cross-version compatiblity operations into a separate module named
``_compat.py``.

