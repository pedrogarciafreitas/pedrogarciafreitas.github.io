---
id: 1076
title: '[Solved] login_getclass: unknown class &#8216;default&#8217; after freebsd-update'
date: 2011-01-17T11:38:48+00:00
author: SAWP
excerpt: Fixing login error after freebsd-update
layout: post
guid: http://www.sawp.com.br/blog/?p=1076
permalink: /p=1076
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:782:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">cp</span> <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>src<span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>login.conf <span style="color: #000000; font-weight: bold;">/</span>etc
    cap_mkdb <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span>login.conf
    reboot</pre></td></tr></table><p class="theCode" style="display:none;">cp /usr/src/etc/login.conf /etc
    cap_mkdb /etc/login.conf
    reboot</p></div>
    ";}
categories:
  - FreeBSD
---
If you are experiencing the following error after <a href="http://ht.ly/3ELwV" target="_blank">updating FreeBSD</a>:

> `login_getclass: unknown class 'default'<br />
login_getclass: no default/fallback class 'default'<br />
pam_acct_mgmt: error in service module` 

Restart your system, login as root and run the following commands:

<pre lang="bash">cp /usr/src/etc/login.conf /etc
cap_mkdb /etc/login.conf 
reboot</pre>

After reboot the system again and it should be working.
