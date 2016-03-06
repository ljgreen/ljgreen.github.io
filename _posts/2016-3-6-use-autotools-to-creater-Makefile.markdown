--- 
layout: posts
categories: kernel
title: How to use autotools to create Makefile
---
##Study something new every day!

<ol>
<li>
在当前目录下运行autoscan,生成configure.scan文件；
</li>
<li>

修改configure.scan文件，
AC_INIT([main], [1.0], [your email])
AC_CONFIG_SRCDIR([queue.c])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([main], [1.0])

AC_PROG_CC
CFLAGS="-g -O2" 

AC_OUTPUT(Makefile)

将configure.scan重命名为configure.ac文件；
</li>
<li>
aclocal
</li>
<li>
autoconf
</li>
<li>
autoheader
</li>
<li>
automake -a
</li>
<li>
创建Makefile.am文件:
bin_PROGRAMS=main
main_SOURCES=producer_consumer.c queue.c
LIBS=-lpthread
</li>
<li>
automake 
</li>
<li>
./configure
</li>
</ol>
