---
id: 2117
title: Fixing libssl.so.1.0.0 Android SDK cmake error on CentOS
date: 2017-03-07T08:44:04+00:00
author: SAWP
excerpt: |
  CMake support is broken due to a missing dependency on libssl.so.1.0.0 and libcrypto.so.1.0.0 of the bundled cmake binary.
layout: post
guid: http://www.sawp.com.br/blog/?p=2117
permalink: p=2117
categories:
  - Programming Internals
---
<pre>cd /usr/src/
wget https://www.openssl.org/source/old/1.0.0/openssl-1.0.0k.tar.gz
tar -zxf openssl-1.0.0k.tar.gz 
cd openssl-1.0.0k
./config shared zlib-dynamic
make
cp ./lib*.so.1.0.0 /usr/lib64/</pre>
