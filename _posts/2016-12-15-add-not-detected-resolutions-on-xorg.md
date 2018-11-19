---
id: 2100
title: Add not detected resolutions on Xorg
date: 2016-12-15T09:13:03+00:00
author: SAWP
layout: post
guid: http://www.sawp.com.br/blog/?p=2100
permalink: /p=2100
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4256:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> butcher<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.25</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.25</span> * k1 * h<span style="color: black;">&#41;</span>
    k3 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.25</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.125</span> * k1 * h + <span style="color: #ff4500;">0.125</span> * k2 * h<span style="color: black;">&#41;</span>
    k4 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.5</span> * h<span style="color: #66cc66;">,</span> y - <span style="color: #ff4500;">0.5</span> * k2 * h + k3 * h<span style="color: black;">&#41;</span>
    k5 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.75</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.1875</span> * k1 * h + <span style="color: #ff4500;">0.5625</span> * k4 * h<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>a1<span style="color: #66cc66;">,</span> a2<span style="color: #66cc66;">,</span> a3<span style="color: #66cc66;">,</span> a4<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>-<span style="color: #ff4500;">3.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">2.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">12.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">8.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: black;">&#41;</span>
    delta <span style="color: #66cc66;">=</span> a1 * k1 * h + a2 * k2 * h + a3 * k3 * h - a3 * k4 * h + a4 * k5 * h
    k6 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> y + delta<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> y + <span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span> / <span style="color: #ff4500;">90</span><span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">7</span> * k1 + <span style="color: #ff4500;">32</span> * k3 + <span style="color: #ff4500;">12</span> * k4 + <span style="color: #ff4500;">32</span> * k5 + <span style="color: #ff4500;">7</span> * k6<span style="color: black;">&#41;</span> * h
    x1 <span style="color: #66cc66;">=</span> x + h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def butcher(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.25 * h, y + 0.25 * k1 * h)
    k3 = f(x + 0.25 * h, y + 0.125 * k1 * h + 0.125 * k2 * h)
    k4 = f(x + 0.5 * h, y - 0.5 * k2 * h + k3 * h)
    k5 = f(x + 0.75 * h, y + 0.1875 * k1 * h + 0.5625 * k4 * h)
    (a1, a2, a3, a4) = (-3.0 / 7.0, 2.0 / 7.0, 12.0 / 7.0, 8.0 / 7.0)
    delta = a1 * k1 * h + a2 * k2 * h + a3 * k3 * h - a3 * k4 * h + a4 * k5 * h
    k6 = f(x + h, y + delta)
    y1 = y + (1.0 / 90) * (7 * k1 + 32 * k3 + 12 * k4 + 32 * k5 + 7 * k6) * h
    x1 = x + h
    return (x1, y1)</p></div>
    ";}
categories:
  - Miscellaneous
---
Supposing you are using lightdm and your monitor has support to 2560&#215;1080@75.00. If your monitor is identified by HDMI2.

First, execute:

<pre>cvt 2560 1080 75</pre>

The output will be something like that:

> Modeline &#8220;2560x1080_75.00&#8221; 294.00 2560 2744 3016 3472 1080 1083 1093 1130 -hsync +vsync

Now, copy this line without &#8220;Modeline&#8221; part. Paste this string into the following script file: **/root/addmodeset.sh**. The content of this file will be:

> #!/bin/sh
> 
> xrandr &#8211;newmode &#8220;2560x1080_75.00&#8221; 294.00 2560 2744 3016 3472 1080 1083 1093 1130 -hsync +vsync
  
> xrandr &#8211;addmode HDMI2 2560x1080_75.00 

Now, add the following line to file **/etc/lightdm/lightdm.conf**:

> display-setup-script=/root/addmodeset.sh 

Finally, make script executable:

<pre>sudo chmod +x /root/addmodeset.sh</pre>

Reboot the system and add the resolution via system preference.
