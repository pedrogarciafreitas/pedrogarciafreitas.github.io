---
id: 700
title: Freebsd Cython Compile Error
date: 2010-09-03T21:02:00+00:00
author: SAWP
excerpt: Fixing pth.h when compiling Cython on FreeBSD.
layout: post
guid: http://www.sawp.com.br/blog/?p=700
permalink: p=700
categories:
  - FreeBSD
---
If you had an error like this when compiling the port lang /cython :

> `<br />
building 'Cython.Plex.Scanners' extension<br />
creating build/temp.freebsd-8.0-RELEASE-i386-2.6<br />
creating build/temp.freebsd-8.0-RELEASE-i386-2.6/Cython<br />
creating build/temp.freebsd-8.0-RELEASE-i386-2.6/Cython/Plex<br />
cc -DNDEBUG -O2 -pipe -D__wchar_t=wchar_t -DTHREAD_STACK_SIZE=0x100000 -fno-strict-aliasing -O2 -pipe -fno-strict-aliasing -fPIC -I/usr/local/include/python2.6 -c Cython/Plex/Scanners.c -o build/temp.freebsd-8.0-RELEASE-i386-2.6/Cython/Plex/Scanners.o<br />
In file included from Cython/Plex/Scanners.c:4:<br />
/usr/local/include/python2.6/Python.h:168:17: error: pth.h: No such file or directory<br />
error: command 'cc' failed with exit status 1<br />
*** Error code 1<br />
` 

try:

> `<br />
# ln -s /usr/local/include/pth/pth.h /usr/local/include/python2.6/<br />
# ln -s /usr/local/include/pth/pthread.h /usr/local/include/python2.6/<br />
` 

and recompile. It should work.
