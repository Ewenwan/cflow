# 静态分析C语言生成函数调用关系的利器——cflow

   cflow是一款静态分析C语言代码的工具，通过它可以生成函数的调用关系。和calltree不一样，
   cflow有独立的网页介绍它（https://www.gnu.org/software/cflow/#TOCdocumentation）。
   而且在Ubuntu系统上，我们可以不用去编译cflow的源码，而直接使用下面命令获取
   
     apt-get install cflow


GNU cflow README
Copyright (C) 2005 Sergey Poznyakoff
See the end of file for copying conditions.

* Introduction

This file contains brief information about configuring, and installing
GNU cflow. It is *not* intended as a replacement for the
documentation, instead it is provided as a brief reference only.
Please be sure to read the accompanuing documentation before using the
utility. See section `Documentation' below.

Please read *all* sections of this `README' file before starting
configuration.  Also make sure you read `INSTALL' if you are not
familiar with them already. Refer to file `ABOUT-NLS' for information
regarding internationalization.

* History

The GNU cflow was initially written in 1997, when I needed a utility
that could display the control flow in a C program. The latest updates
date back to 1999. Then, as I no longer needed the package, it fell into
oblivion.

A recent thread in gnu-devel mailing list has shown that there is a
kind of demand for that sort of utility, so I decided to resurrect
it and make a full-fledged package of it. On 2005-04-12 it was dubbed
a GNU package.

* Current Status

The package compiles and runs on GNU/Linux systems. It supports all
command line switches required by POSIX, plus a number of extended
ones. It is able to produce output two formats: default output format
(which I call GNU cflow format and which is the default) and in POSIX
format.

Currently the utility is only able to process C sources. It is the
only deviation from POSIX specs, that require the ability to process
YACC and LEX sources as well as binary object files. This support will
appear in future versions.

Emacs module cflow-mode.el works wit files in GNU cflow format (as
opposed to POSIX format). It has been tested with Emacs 21.3.

* Compilation

Please see the INSTALL file in this directory for the generic instructions
on how to use configure. There is currently only one package-specific
configuration option: --enable-debug, which compiles the package with
-g (or -ggdb if appropriate) option. Use it if you plan debugging
cflow.

* Installation

After running `./configure' and `make', run `make install'.

* Documentation

Complete user manual in texinfo format is provided. After the
installation, it will be accessible by running `info cflow'. To read it
before installing the package, run `info -f doc/cflow' from the
package source root directory.

If you don't have GNU texinfo installed, see
http://www.gnu.org/software/texinfo for information on where to obtain it.

* Bug reporting.

Send bug reports to <bug-cflow@gnu.org>.

* Copyright Information:

Copyright (C) 2005, Sergey Poznyakoff 

   Permission is granted to anyone to make or distribute verbatim copies
   of this document as received, in any medium, provided that the
   copyright notice and this permission notice are preserved,
   thus giving the recipient permission to redistribute in turn.

   Permission is granted to distribute modified versions
   of this document, or of portions of it,
   under the above conditions, provided also that they
   carry prominent notices stating who last changed them.


Local variables:
mode: outline
paragraph-separate: "[ 	]*$"
end:
