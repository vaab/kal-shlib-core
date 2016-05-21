What is kal-shlib ?
--------------------

These shell components contains the core libraries that ease a lot of
common tasks encountered when scripting in bash.

The shell libs are divided into several sub-packages providing code
for various needs. An exception is ``kal-shlib-core`` which contains
the central library inclusion mecanism. As a consequence, it is a
dependence of all ``kal-shlib-*`` packages.


What is kal-shlib-core ?
------------------------

This package only provide the library inclusion mecanism. Please note that it
provides also the ``shlib`` executable that allows to inline bash code from the
library into any shell script using shlib facilities. This allows you to use
the shell script on system without the ``kal-shlib-core`` package installed.

You can compare this with statically compiled C code, and dynamically linked
library. ``shlib`` allows you to go back and forth between these 2 states.


Do I need shlibs ?
------------------

If you take time shell-scripting, this might be of interest, some
function have actually saved me lot of time.

If you have found an utility for other component of the kal packages, you can
save place by making all binaries dynamically linked to these libraries. This
is especially useful if you have installed more than one kal package.

I use ``shlib`` executable for many of my other publicly distributed shell script
program.


Where can I find docs ?
-----------------------

Sorry, there are very few docs at the moment. Best of all is to look at libraries
source code.


How can I install it ?
----------------------

Consider this release as alpha software. Use at your own risk. It may or may
not upgrade to a more user friendly version in future, depending on my spare
time.


From source
===========

You might have to consider running ``./autogen.sh`` if you got
source from ``git``.

If you got the source code thanks to downloading the ``tar.gz``,
running ``./autogen.sh`` shouldn't be necessary.

This package support GNU install quite well so a simple::

  # ./configure && make && make install

Should work (and has been tested and is currently used).

Note: you can specify a ``--prefix=/your/location``


From debian package
===================

This method works with any Debian distrib or Ubuntu version and
derivatives.

A debian package repository is available at::

  deb http://deb.kalysto.org no-dist kal-alpha

You should include this repository to your apt system and then::

  # apt-get update && apt-get install kal-shlib-core


What do this package contains ?
-------------------------------

- directory ``$prefix/lib/shlib/`` where library will be loaded
- an executable ``shlib`` installed in $prefix/bin
- an executable ``bash-shlib`` installed in $prefix/bin
- a config file ``shlib`` installed in $prefix/etc

The debian package version will install to these location (and ``$prefix``
is set to ``/``)


How can I use the libraries in one of my scripts ?
--------------------------------------------------

You just have to source ``/etc/shlib`` in your bash script or use
``bash-shlib`` as a replacement shebang interpreter. Either of these
this will give you access to an ``include`` function allowing you to
source any library found in ``/usr/lib/shlib/lib*.sh``.

So you need some libraries in ``/usr/lib/shlib/lib*.sh`` to go forward,
you can write them or install some provided like ``kal-shlib-common`` and
others...

Example::

  #!/bin/bash

  . /etc/shlib

  include common

  die "Argl!"      ## function 'die' comes from 'common'


These can be installed manually, or thanks to debian packages of
various ``kal-shlib-*``.

As an alternative, you can use the shebang loading ``bash-shlib`` that
will then source for you the ``/etc/shlib``. This is shorter,
example::

  #!/usr/bin/bash-shlib

  include common

  die "Argl!"


Special autoloaded code ?
-------------------------

With version 0.5, you can now put source code into
``/usr/lib/shlib/autoload/*.sh``, and they will be autoloaded to any
shlib using code.

DO NOT ABUSE of this. This is used mainly to add new features to
``shlib`` code, from external package, as shell decorators.


How to use the executable linker ``shld`` ?
-------------------------------------------

Depending on the method you use to load the shell lib (aka, using the ``bash-shlib``
interpreter or sourcing ``/etc/shlib``).

Using the sourcing method, these lines of code should be inserted at
the beginning of your shell script, before any other shell code, but
after the shebang::

  #!- shlib loader
  . /etc/shlib  ## shlib call
  #!-

Note that there two ``#!-`` at the beginning of line. You can put any comment
after. These 2 lines will mark the beginning and ending of the ``shlib
call``.

Using the ``bash-shlib`` interpreter, you have nothing special to do.

Then, for both method, what follows applies::

  # shlib d <filename>

..

  will *erase* and write a *dynamical* version of the shlib caller. This means
  that your shell script will look for the libraries at each call.

::

  # shlib s <filename>

..

  will *erase* and write a *statical* version of the shlib caller. It makes a
  snapshot of your current libraries and feeds it *in* your script.
