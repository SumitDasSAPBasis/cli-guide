.. Getting Started with Click documentation master file, created by
   sphinx-quickstart on Thu Jun  1 19:25:47 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

*The Unofficial Guide to* ...

#########################################
Building Command-Line Utilities in Python
#########################################

    "Arguably, Python is the best language for making UNIX\ :sup:`®` command line
    tools, period, due to its batteries-included philosophy, and its
    emphasis on readable code. Just a warning, though; these are dangerous
    ideas when you find out how easy it is to create a command line tool in
    Python, you might be spoiled for life." [Gift08]_

.. code::

    @command()
    def hello():
        print('You might be spoiled for life!')

.. hint::

    A function becomes a command line tool by decorating it with
    **@command**. At its simplest, just decorating a function with this
    decorator will make it into a callable script. [Rona17]_

====================================
Choose Your Preferred Learning Style
====================================

1. Just show me the code! 
2. I want to design better command-line utilities.
3. I want to watch Click eat its own dog food.
4. I'm coming from the world of argparse.
5. I'm coming from the world of docopts.
6. I just want a cheatsheet & reference material.

=================
Table of Contents
=================

.. toctree::
   :maxdepth: 1

   design/guidelines
   design/structures
   design/patterns
   design/wordsplitting
   design/parsing
   design/arguments
   design/options
   design/naming
   design/help
   design/types
   design/io
   design/soc
   design/summary

   references
 
