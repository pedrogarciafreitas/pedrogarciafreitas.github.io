---
id: 620
title: Compiling and installing Eclipse on FreeBSD
date: 2010-05-18T15:41:26+00:00
author: SAWP
excerpt: How to install Eclipse.
layout: post
guid: http://www.sawp.com.br/blog/?p=620
permalink: p=620
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:786:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>ports<span style="color: #000000; font-weight: bold;">/</span>x11-toolkits<span style="color: #000000; font-weight: bold;">/</span>open-motif <span style="color: #000000; font-weight: bold;">&amp;&amp;</span> <span style="color: #c20cb9; font-weight: bold;">make</span> <span style="color: #c20cb9; font-weight: bold;">install</span> clean</pre></td></tr></table><p class="theCode" style="display:none;">cd /usr/ports/x11-toolkits/open-motif &amp;&amp; make install clean</p></div>
    ;i:2;s:762:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"> <span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>ports<span style="color: #000000; font-weight: bold;">/</span>java<span style="color: #000000; font-weight: bold;">/</span>jdk15 <span style="color: #000000; font-weight: bold;">&amp;&amp;</span> <span style="color: #c20cb9; font-weight: bold;">make</span> <span style="color: #c20cb9; font-weight: bold;">install</span> clean</pre></td></tr></table><p class="theCode" style="display:none;"> cd /usr/ports/java/jdk15 &amp;&amp; make install clean</p></div>
    ;i:3;s:762:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"> <span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>ports<span style="color: #000000; font-weight: bold;">/</span>java<span style="color: #000000; font-weight: bold;">/</span>jdk16 <span style="color: #000000; font-weight: bold;">&amp;&amp;</span> <span style="color: #c20cb9; font-weight: bold;">make</span> <span style="color: #c20cb9; font-weight: bold;">install</span> clean</pre></td></tr></table><p class="theCode" style="display:none;"> cd /usr/ports/java/jdk16 &amp;&amp; make install clean</p></div>
    ;i:4;s:702:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>ports<span style="color: #000000; font-weight: bold;">/</span>java<span style="color: #000000; font-weight: bold;">/</span>eclipse <span style="color: #000000; font-weight: bold;">&amp;&amp;</span> <span style="color: #c20cb9; font-weight: bold;">make</span> <span style="color: #c20cb9; font-weight: bold;">install</span> clean</pre></td></tr></table><p class="theCode" style="display:none;">/usr/ports/java/eclipse &amp;&amp; make install clean</p></div>
    ";}
categories:
  - FreeBSD
---
<pre lang="bash">cd /usr/ports/x11-toolkits/open-motif && make install clean</pre>

<pre lang="bash">cd /usr/ports/java/jdk15 && make install clean</pre>

<pre lang="bash">cd /usr/ports/java/jdk16 && make install clean</pre>

<pre lang="bash">/usr/ports/java/eclipse && make install clean</pre>

following these commands: [http://blogs.sun.com/meena/entry/open\_web\_server\_on\_freebsd](http://blogs.sun.com/meena/entry/open_web_server_on_freebsd)

or

Mail me with logs errors if this not work: sawp@sawp.com.br
