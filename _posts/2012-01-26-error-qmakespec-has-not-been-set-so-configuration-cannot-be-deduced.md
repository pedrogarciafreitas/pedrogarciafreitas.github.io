---
id: 1486
title: '[Solved] Compiling yuvplayer in FreeBSD'
date: 2012-01-26T10:26:00+00:00
author: CKPYT
excerpt: |
  If you got the error when trying to compile a C++ QT project:  QMAKESPEC has not been set, so configuration cannot be deduced.
  Error processing project file: *.pro
  
  Then it means you forgot to set environment variable QMAKESPE
layout: post
guid: http://www.sawp.com.br/blog/?p=1486
permalink: /p=1486
categories:
  - FreeBSD
---
`<br />
# wget http://www.tnt.uni-hannover.de/~vatis/yuvplayer/yuvplayer.tar.gz<br />
# csh<br />
% setenv QMAKESPEC freebsd-g++<br />
% qmake-qt4 -project<br />
% qmake-qt4 yuvplayer.pro<br />
% make<br />
`
