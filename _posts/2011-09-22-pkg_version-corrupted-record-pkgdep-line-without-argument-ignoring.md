---
id: 1338
title: 'pkg_version: corrupted record (pkgdep line without argument), ignoring'
date: 2011-09-22T10:37:52+00:00
author: CKPYT
excerpt: 'Fixing "pkg_version: corrupted record (pkgdep line without argument), ignoring" error on FreeBSD ports.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1338
permalink: /p=1338
categories:
  - FreeBSD
---
`<br />
#portmaster --check-depends<br />
#portmaster --check-port-dbdir<br />
#pkgdb -Fu<br />
#portmaster -a<br />
`
