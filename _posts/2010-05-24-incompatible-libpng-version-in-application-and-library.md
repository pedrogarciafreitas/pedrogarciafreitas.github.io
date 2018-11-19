---
id: 628
title: Incompatible libpng version in application and library
date: 2010-05-24T12:51:25+00:00
author: SAWP
excerpt: 'Fixing Fatal error in PNG image file: Incompatible libpng version in application and library'
layout: post
guid: http://www.sawp.com.br/blog/?p=628
permalink: /p=628
categories:
  - FreeBSD
---
Gnome showing the following error?
  
**Fatal error in PNG image file: Incompatible libpng version in application and library**

Try:
  


<center>
  <br /> <code>&lt;br />
sudo ln -s /usr/local/lib/libpng.so.6 /usr/local/lib/libpng.so.5&lt;br />
</code><br />
</center>

That solved at Gnome 2.30 on FreeBSD 8.
