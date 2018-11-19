---
id: 1511
title: Creating a HTTP Server to Share Files Using Just Two Command Lines
date: 2012-05-04T01:57:13+00:00
author: CKPYT
excerpt: Files transfer using python.
layout: post
guid: http://www.sawp.com.br/blog/?p=1511
permalink: /p=1511
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:336:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">cd</span> ~<span style="color: #000000; font-weight: bold;">/</span>share</pre></td></tr></table><p class="theCode" style="display:none;">cd ~/share</p></div>
    ;i:2;s:544:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">SimpleHTTPServer</span>
    <span style="color: #dc143c;">SimpleHTTPServer</span>.<span style="color: #dc143c;">test</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">import SimpleHTTPServer
    SimpleHTTPServer.test()</p></div>
    ;i:3;s:469:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">http:<span style="color: #000000; font-weight: bold;">//</span><span style="color: #7a0874; font-weight: bold;">&#91;</span>your-ip-here<span style="color: #7a0874; font-weight: bold;">&#93;</span>:<span style="color: #000000;">8000</span></pre></td></tr></table><p class="theCode" style="display:none;">http://[your-ip-here]:8000</p></div>
    ";}
categories:
  - Quick Tips For Networking
---
Suppose you want to share the files located in the &#8220;~/share&#8221; folder. In terminal, type:

<pre lang="bash">cd ~/share</pre>



Now, open the python terminal and write:

<pre lang="python">import SimpleHTTPServer
SimpleHTTPServer.test()</pre>



Find out your ip using this site:

<center>
  <a href="http://www.whatismyip.com/" target="_blank">http://www.whatismyip.com/</a>
</center>

Note that the server is running on port 8000. So when you share your IP, go as follows:

<pre lang="bash">http://[your-ip-here]:8000</pre></p>
