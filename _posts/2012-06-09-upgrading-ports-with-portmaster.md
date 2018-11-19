---
id: 1571
title: Upgrading ports with portmaster
date: 2012-06-09T11:15:00+00:00
author: CKPYT
excerpt: How to updating all ports with portmaster without prompt.
layout: post
guid: http://www.sawp.com.br/blog/?p=1571
permalink: /p=1571
categories:
  - FreeBSD
---

  


### Updating all ports:
        


<center>
  <br /> <tt>portmaster -GDabw --no-confirm</tt><br />
</center>

The flags mean: 

  * <tt>G</tt>: Don&#8217;t run <tt>make config</tt>. 

  * <tt>a</tt>: Update all installed ports. 

  * <tt>b</tt>: Build a backup of the previous port. 

  * <tt>w</tt>: Save all shared libraries before removing (“deinstalling”) old port.
              
    port. 

  * <tt>--no-confirm</tt>: Don&#8217;t stop in some places to ask questions. Unfortunately, it still stops in other places. 

### Updating a single port:
        


<center>
  <br /> <tt>portmaster -DGbw --no-confirm {portname}</tt><br />
</center>
