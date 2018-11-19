---
id: 2092
title: 'luarocks install [package] does not work'
date: 2016-04-29T16:43:43+00:00
author: SAWP
excerpt: Error on torch package installation.
layout: post
guid: http://www.sawp.com.br/blog/?p=2092
permalink: p=2092
categories:
  - Quick Tips For Networking
---
Edit your 

> /path/to/torch/install/share/lua/5.1/luarocks/fetch/git.lua

changing 

> rockspec.source.url

to 

> rockspec.source.url:gsub(&#8220;^git://&#8221;, &#8220;https://&#8221;)
