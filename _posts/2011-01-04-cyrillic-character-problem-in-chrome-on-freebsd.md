---
id: 896
title: Cyrillic character problem in Chrome on FreeBSD
date: 2011-01-04T10:23:48+00:00
author: CKPYT
excerpt: Fix bad character appearing in Google Chrome
layout: post
guid: http://www.sawp.com.br/blog/?p=896
permalink: /p=896
categories:
  - FreeBSD
---
If there is bad character appearing in Google Chrome on FreeBSD, try installing the following port **x11-fonts/droid-fonts-ttf**:

<center>
  <code>cd /usr/ports/x11-fonts/droid-fonts-ttf/ && make install clean</code>
</center>
