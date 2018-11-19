---
id: 725
title: Text color in FreeBSD gnome-terminal (bash)
date: 2010-09-10T18:21:31+00:00
author: SAWP
excerpt: Text color in FreeBSD terminal...
layout: post
guid: http://www.sawp.com.br/blog/?p=725
permalink: p=725
categories:
  - FreeBSD
---
The easiest way is append to file **_~/.bashrc_** the commands:

> `<br />
export force_color_prompt=yes<br />
alias ls='ls -G'<br />
export TERM=xterm-color`

and restart the console.
