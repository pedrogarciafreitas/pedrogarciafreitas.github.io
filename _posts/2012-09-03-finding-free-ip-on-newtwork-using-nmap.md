---
id: 1752
title: Finding Free IPs on Newtwork Using nmap
date: 2012-09-03T11:30:30+00:00
author: SAWP
excerpt: Do you need to find a free IP in a address range?
layout: post
guid: http://www.sawp.com.br/blog/?p=1752
permalink: p=1752
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:440:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">nmap</span> <span style="color: #660033;">-sP</span> 172.24.17.1-<span style="color: #000000;">255</span><span style="color: #000000; font-weight: bold;">/</span></pre></td></tr></table><p class="theCode" style="display:none;">nmap -sP 172.24.17.1-255/</p></div>
    ";}
categories:
  - Quick Tips For Networking
---
Do you need to find a free IP in a address range? Use NMAP:

<pre lang="bash">nmap -sP 172.24.17.1-255/</pre>
