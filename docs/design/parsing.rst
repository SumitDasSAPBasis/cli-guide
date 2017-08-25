####################################################
Parsing: Arguments/Options and the 5 Types of Dashes
####################################################

It's important to understanding how dashes are parsed in POSIX compliant
command-line parsers since they can be interpreted in multiple ways.

How-To Interpret Dashes
-----------------------

1. Argument Separator
    word == '--'

2. Long-Option
    word.startswith('--') + len(word) > 2

3. Short-Option
    word.startswith('-') + len(word) > 1

4. Argument (operand)


Arguments
---------
* Arguments can be:
  1. Required (default)
  2. Optional.

* Arguments can also be:
  1. A Single Argument (default)
  2. An Argument List of unknown length

Note: Although 



Option-Arguments

Packed Options
--------------

- Short-option flags can be packed, meaning that a single-dash can beLieter
  followed by one or more short-option flag characters.
- The last option in the packed options can be a short-option argument.
- A space between a short-option character and the option's argument is
  optional.
- Long options can include an equal sign between the option and the option-argument.

Utility Syntax Guidelines (POSIX.1-2008)
----------------------------------------
*The follow POSIX guidelines are related to the dash character.*  [Open16]_

POSIX.1-2008 Guideline 4:
    "All options should be preceded by the `'-'` delimiter character."

POSIX.1-2008 Guideline 5:
    "One or more options without option-arguments, followed by at most one option
    that takes an option-argument, should be accepted when grouped behind one
    `'-'` delimiter."

POSIX.1-2008 Guideline 10:
    "The first -- argument that is not an option-argument should be accepted as a
    delimiter indicating the end of options. Any following arguments should be
    treated as operands, even if they begin with the `'-'` character.""

POSIX.1-2008 Guideline 13:
    "For utilities that use operands to represent files to be opened for either
    reading or writing, the '-' operand should be used to mean only standard
    input (or standard output when it is clear from context that an output file
    is being specified) or a file named `'-'`."


Examples
---------
.. rubric:: dashes.py

.. literalinclude:: ../../examples/dashes.py

Argument Separators
-------------------
The double-dashes in the following example are interpreted as an argument
separator; note that the arg1 is not set to '--'::

    $ python dashes.py --
    Usage: dashes.py [OPTIONS] ARG1 [ARG2] [ARG3] [ARG3]

    Error: Missing argument "arg1".

The three dashes in the following example are interpeted as a long option
where the long option string equals a dash character::

    $ python dashes.py ---
    Error: no such option: ---

If an argument literally starts with a dash use an argument-separator::

    $ python dashes.py -- -argstartswithdash
    arg1:  -argstartswithdash
    arg2:  None
    arg3:  None
    flag1:  False
    flag2:  False
    opt: None

Otherwise it treats it as packed options::

    $ python dashes.py -argstartwithdash
    Error: no such option: -a

Similar type problem with double-dashes::

    $ python dashes.py --argstartswithdoubledashes
    Error: no such option: --argstartswithdoubledashes

Again use an argument-separator::

    $ dashes.py -- --argstartswithdoubledashes
    arg1:  --argstartswithdoubledashes
    arg2:  None
    arg3:  None
    flag1:  False
    flag2:  False
    opt: None

.. rubric:: Still Confused?

If this still sounds confusing it might be helpful to take a look at the
answer `here
<https://unix.stackexchange.com/questions/146913/is-used-only-with-cd/146917>`_
describing how `cd -` is parsed in UNIX\ :sup:`®`.

Single-Dashes for Stdin/Stdout
------------------------------
Since the first argument is not a File type, the following example passes
in a single dash::

    $ python dashes.py -
    arg1:  -
    arg2:  None
    arg3:  None
    flag1:  False
    flag2:  False
    opt: None

If the single stand-alone dash is passed into a non-writable File the input
data is read from STDIN::

    $ python dashes.py test -
    arg1:  test
    arg2:  <_io.TextIOWrapper name='<stdin>' mode='r' encoding='UTF-8'>
    arg3:  None
    flag1:  False
    flag2:  False
    opt: None

On Windows\ :sup:`®` it may look a little different::

    > python dashes.py test -
    arg1:  test
    arg2:  <ConsoleStream name='<stdin>' encoding='utf-16-le'>
    arg3:  None
    flag1:  False
    flag2:  False
    opt: None

If the single stand-alone dash is passed into a writable File the output
will be written to STDOUT::

    $ python dashes.py test - -
    arg1: test
    arg2: <_io.TextIOWrapper name='<stdin>' encoding='UTF-8'>
    arg3: <_io.TextIOWrapper name='<stdout>' encoding='UTF-8'>
    flag1: False
    flag2: False
    opt:None    

Packed Options
--------------
Flag options can be specified individually::

    $ python dashes.py -f -F test
    arg1: test
    arg2: None
    arg3: None
    arg3: None
    flag1: True
    flag2: True
    opt:None

Or the flag options can be packed::

    $ python dashes.py -fF test
    arg1: test
    arg2: None
    arg3: None
    arg3: None
    flag1: True
    flag2: True
    opt:None

Packed option flags can be followed by an option argument::

    $ python dashes.py -fFo optionargtext test
    arg1: test
    arg2: None
    arg3: None
    arg3: None
    flag1: True
    flag2: True
    opt:optionargtext

The space between short options and the argument is optional::

    $ python dashes.py -fFooptionargtext test
    arg1: test
    arg2: None
    arg3: None
    arg3: None
    flag1: True
    flag2: True
    opt:optionargtext

Long options can't be packed and the space is required for long-option
arguments::

    $ python dashes.py --flag2ooptionargtext test
    Error: no such option: --flag2ooptionargtext

.. rubric:: References:

.. [Open16] The IEEE and The Open Group.
    The Open Group Base Specifications Issue 7.
    IEEE Std 1003.1-2008, 2016 Edition.
    Utility Conventions. Retreived from
    http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html

.. rubric:: Registered Trademarks:

* *UNIX® is a registered trademark of The Open Group.*
* *POSIX® is a registered trademark of the Institute of Electrical and Electronic Engineers (IEEE).*
* *Windows® is a registered trademark of the Microsoft® Corporation.