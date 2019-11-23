# 静态分析C语言生成函数调用关系的利器——cflow

   cflow是一款静态分析C语言代码的工具，通过它可以生成函数的调用关系。和calltree不一样，
   cflow有独立的网页介绍它（https://www.gnu.org/software/cflow/#TOCdocumentation）。
   而且在Ubuntu系统上，我们可以不用去编译cflow的源码，而直接使用下面命令获取
   
     apt-get install cflow

# cflow的使用

        -T输出函数调用树状图
        -m指定需要分析的函数名
        -n输出函数所在行号
        -r输出调用的反向关系图
        --cpp预处理，这个还是很重要的
        
## 文本输出       

最简单的使用方法是以ASCII文本的方式输出结果，
比如

    cflow -T -m main -n timer.c        

其结果是一个包含文件名和函数所在代码行号的调用关系图
```C
+-main() <int main (void) at timer.c:13>
  +-ev_timer_init()
  +-timeout_cb() <void timeout_cb (EV_P_ ev_timer *w, int revents) at timer.c:7>
  | +-puts()
  | \-ev_break()
  +-ev_timer_start()
  \-ev_run()       
  
```

  然而，对于有一定代码量的项目，我们不会使用ASCII文本的方式去查看函数调用关系，因为调用是相当复杂的，
  而文本图并不适合人去理解。于是我们希望能cflow能产出一个可供其他软件转换成图片的格式的文件。
  可惜cflow并不支持，好在网上有开发者做了一个工具，可将其结果转换成dot格式。
  
  wget -c https://github.com/tinyclub/linux-0.11-lab/raw/master/tools/tree2dotx
  
     下载完tree2dotx后，
     可对其做个软链便于使用
     
     cd /usr/bin
     ln -s 【Your Path】/tree2dotx tree2dotx   

具体的转换方法是

     cflow -T -m main -n timer.c > main.txt
     cat main.txt | tree2dotx > main.dot
     
## dot文件生成图片 

 我们需要借助graphviz（没有安装的可以使用apt-get install graphviz先安装）生成图片，指令是
        
     dot -Tgif main.dot -o main.gif  



        
        
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
