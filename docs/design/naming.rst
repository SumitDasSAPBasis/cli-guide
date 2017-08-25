######################
Naming: Best Practices
######################

Per the POSIX guidelines the `utility_name` of our commands should start
with a lowercase letter followed by any combination of 1 to 8 lowercase
letters or digits.  In EBNF_ format it looks like this::

    name  ::= lower (lower | digit){1, 8}
    digit ::= "0"..."9"
    lower ::= "a"..."z"

Although the guidelines allow for single letter commands, don't do it.
Your command names should be at least two characters in length.

Naming your commands is a bit of an art, there is balance between:

    1. Making commands intuitive and easy to remember via meaningful,
       mnemonic names.

    2. Keeping command names short, simple and easy to type.

    3. Avoiding collisions with existing command names in popular operating
       systems, shells, vendor applications & community packages.

If the plan is to distribute your command to the community at-large then
it's a good idea run a Internet search on the name you intend to use and
search the `Git Hub`_ repository as well.  If the name is associated with a
popular program than choose a different name to avoid any confusion.

===========
Subcommands
===========
When naming subcommands you don't have to wory about name conflicts with
external commands, just keep them short, simple and inuitive.

By default Click uses the function name as the name of the subcommand.  This
can be overriden by using the @command `name` parameter.

**********
References
**********

.. target-notes::

.. _EBNF: https://www.ics.uci.edu/~pattis/ICS-33/lectures/ebnf.pdf

.. _Git Hub: http://www.github.com