---
id: 528
title: 1.2.7 Raízes de Equações – Métodos Abertos – Interpolação Quadrática Inversa
date: 2010-03-12T11:10:18+00:00
author: SAWP
excerpt: Interpolação Quadrática Inversa é uma técnica usada para obtermos zeros de equações não-lineares na forma f(x) = 0. Ele é raramente implementado em aplicações como único método de busca de raízes, sendo usado como fator acelerador da convergência.
layout: post
guid: http://www.sawp.com.br/blog/?p=528
permalink: /p=528
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:11716:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> IQI<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function (Inverse quadratic interpolation)
    &nbsp;
    IQI(f, x0=1.0, errto=0.001, imax=100)
    &nbsp;
    * f: Function where find roots
    * x0: next point (estimative)
    * errto: tolerated error ( for aprox. )
    * imax: max of iterations allowed
    &nbsp;
    return: root next x0
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &nbsp;
    Jan 2009
    &quot;&quot;&quot;</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    y0 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> fabs<span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>x0 + y0<span style="color: black;">&#41;</span> - y0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    x1 <span style="color: #66cc66;">=</span> x0 - y0*y0/<span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>x0 + y0<span style="color: black;">&#41;</span> - y0<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    x3 <span style="color: #66cc66;">=</span> x0
    <span style="color: #ff7700;font-weight:bold;">break</span>
    &nbsp;
    y1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> y0 <span style="color: #66cc66;">!=</span> y1:
    x2 <span style="color: #66cc66;">=</span> x1 - y1*<span style="color: black;">&#40;</span>x0 - x1<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>y0 - y1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    x3 <span style="color: #66cc66;">=</span> x1
    <span style="color: #ff7700;font-weight:bold;">break</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># try Aitkens optimization</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>x2 - <span style="color: #ff4500;">2</span>*x1 + x0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    alpha <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>x0*x2 - x1*x1<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>x2 - <span style="color: #ff4500;">2</span>*x1 + x0<span style="color: black;">&#41;</span>
    C1 <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>alpha - x1<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>alpha - x0<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    C2 <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>alpha - x2<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>alpha - x1<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>C1 <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: black;">&#40;</span>C2 <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    x2 <span style="color: #66cc66;">=</span> alpha
    &nbsp;
    y2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x2<span style="color: black;">&#41;</span>
    delta <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">7</span>*<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y0 - y1
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y0 - y2
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y1 - y0
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y1 - y2
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y2 - y0
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">6</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y2 - y1
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> disturb<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span><span style="color: black;">&#40;</span>x <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> errto
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    delta <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span>disturb<span style="color: #66cc66;">,</span> delta<span style="color: black;">&#41;</span>
    &nbsp;
    x3 <span style="color: #66cc66;">=</span> y1*y2*x0/<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + \
    y0*y2*x1/<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + \
    y0*y1*x2/<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">6</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> x3 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x3-x0<span style="color: black;">&#41;</span>/x3<span style="color: black;">&#41;</span>
    &nbsp;
    x0 <span style="color: #66cc66;">=</span> x3
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> x3</pre></td></tr></table><p class="theCode" style="display:none;">def IQI(f, x0=1.0, errto=0.001, imax=100):
    &quot;&quot;&quot;
    Return the root of a function (Inverse quadratic interpolation)
    
    IQI(f, x0=1.0, errto=0.001, imax=100)
    
    * f: Function where find roots
    * x0: next point (estimative)
    * errto: tolerated error ( for aprox. )
    * imax: max of iterations allowed
    
    return: root next x0
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    
    Jan 2009
    &quot;&quot;&quot;
    errno = errto + 1
    iterCount = 0
    
    while errno &gt; errto and iterCount &lt; imax:
    y0 = f(x0)
    if fabs(f(x0 + y0) - y0) != 0:
    x1 = x0 - y0*y0/(f(x0 + y0) - y0)
    else:
    x3 = x0
    break
    
    y1 = f(x1)
    if y0 != y1:
    x2 = x1 - y1*(x0 - x1)/(y0 - y1)
    else:
    x3 = x1
    break
    
    # try Aitkens optimization
    if (x2 - 2*x1 + x0) != 0:
    alpha = (x0*x2 - x1*x1)/(x2 - 2*x1 + x0)
    C1 = fabs((alpha - x1)/(alpha - x0))
    C2 = fabs((alpha - x2)/(alpha - x1))
    
    if (C1 &lt; 1) and (C2 &lt; 1):
    x2 = alpha
    
    y2 = f(x2)
    delta = 7*[0]
    delta[1] = y0 - y1
    delta[2] = y0 - y2
    delta[3] = y1 - y0
    delta[4] = y1 - y2
    delta[5] = y2 - y0
    delta[6] = y2 - y1
    
    def disturb(x):
    if(x == 0):
    return errto
    else:
    return x
    
    delta = map(disturb, delta)
    
    x3 = y1*y2*x0/((delta[1])*(delta[2])) + \
    y0*y2*x1/((delta[3])*(delta[4])) + \
    y0*y1*x2/((delta[5])*(delta[6]))
    
    iterCount += 1
    
    if x3 != 0:
    errno = fabs((x3-x0)/x3)
    
    x0 = x3
    
    return x3</p></div>
    ;i:2;s:9804:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> IQI2<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function (Inverse quadratic interpolation)
    &nbsp;
    IQI2(f, x0=1.0, errto=0.001, imax=100)
    &nbsp;
    * f: Function where find roots
    * x0: next point (estimative)
    * errto: tolerate error ( for aprox. )
    * imax: max of iterations allowed
    &nbsp;
    return: root next x0
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &nbsp;
    Jan 2009
    &quot;&quot;&quot;</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    y0 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> fabs<span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>x0 + y0<span style="color: black;">&#41;</span> - y0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    x1 <span style="color: #66cc66;">=</span> x0 - y0*y0/<span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>x0 + y0<span style="color: black;">&#41;</span> - y0<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    x1 <span style="color: #66cc66;">=</span> errto
    &nbsp;
    y1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> y0 <span style="color: #66cc66;">!=</span> y1:
    x2 <span style="color: #66cc66;">=</span> x1 - y1*<span style="color: black;">&#40;</span>x0 - x1<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>y0 - y1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    x2 <span style="color: #66cc66;">=</span> errto
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    y0 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span>
    y2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x2<span style="color: black;">&#41;</span>
    delta <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">7</span>*<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y0 - y1
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y0 - y2
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y1 - y0
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y1 - y2
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y2 - y0
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">6</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y2 - y1
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> disturb<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span><span style="color: black;">&#40;</span>x <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> errto
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    delta <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span>disturb<span style="color: #66cc66;">,</span> delta<span style="color: black;">&#41;</span>
    &nbsp;
    x3 <span style="color: #66cc66;">=</span> y1*y2*x0/<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + \
    y0*y2*x1/<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + \
    y0*y1*x2/<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">6</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> x3 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x3-x0<span style="color: black;">&#41;</span>/x3<span style="color: black;">&#41;</span>
    &nbsp;
    x0 <span style="color: #66cc66;">=</span> x1
    x1 <span style="color: #66cc66;">=</span> x2
    x2 <span style="color: #66cc66;">=</span> x3
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> x3</pre></td></tr></table><p class="theCode" style="display:none;">def IQI2(f, x0=1.0, errto=0.001, imax=100):
    &quot;&quot;&quot;
    Return the root of a function (Inverse quadratic interpolation)
    
    IQI2(f, x0=1.0, errto=0.001, imax=100)
    
    * f: Function where find roots
    * x0: next point (estimative)
    * errto: tolerate error ( for aprox. )
    * imax: max of iterations allowed
    
    return: root next x0
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    
    Jan 2009
    &quot;&quot;&quot;
    errno = errto + 1
    iterCount = 0
    
    y0 = f(x0)
    if fabs(f(x0 + y0) - y0) != 0:
    x1 = x0 - y0*y0/(f(x0 + y0) - y0)
    else:
    x1 = errto
    
    y1 = f(x1)
    if y0 != y1:
    x2 = x1 - y1*(x0 - x1)/(y0 - y1)
    else:
    x2 = errto
    
    while errno &gt; errto and iterCount &lt; imax:
    y0 = f(x0)
    y1 = f(x1)
    y2 = f(x2)
    delta = 7*[0]
    delta[1] = y0 - y1
    delta[2] = y0 - y2
    delta[3] = y1 - y0
    delta[4] = y1 - y2
    delta[5] = y2 - y0
    delta[6] = y2 - y1
    
    def disturb(x):
    if(x == 0):
    return errto
    else:
    return x
    
    delta = map(disturb, delta)
    
    x3 = y1*y2*x0/((delta[1])*(delta[2])) + \
    y0*y2*x1/((delta[3])*(delta[4])) + \
    y0*y1*x2/((delta[5])*(delta[6]))
    
    iterCount += 1
    
    if x3 != 0:
    errno = fabs((x3-x0)/x3)
    
    x0 = x1
    x1 = x2
    x2 = x3
    
    return x3</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

Interpolação Quadrática Inversa é uma técnica usada para obtermos zeros de equações não-lineares na forma $$f(x) = 0 $$ . Ele é raramente implementado em aplicações como único método de busca de raízes, sendo usado como fator acelerador da convergência. 

## 2. Desenvolvimento do Método 

Seja a fórmula obtida a partir do Teorema de Expansão de Lagrange:
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ x=y+\sum _{k=1}^{\infty }{\dfrac {a}^{k}{\dfrac {d^{d-1}{d{x}^{d-1}} \left( \left( g \left( x \right) \right) ^{k}\right) }{k!} $$<br />
</center>

Onde $$x = x(y) $$ . A partir desta expressão, podemos obter uma fórmula iterativa se tomarmos $$y=f \left( x \right) $$ . Por questão de conveniência, expressamos na Equação [1](#eq1) $$y\_{i} = f\_{i} = f \left( x_{i} \right) $$, $$a = -1 $$ e alteramos o índice $$k$$ para um intervalo finito tal que $$ k = 1 \ldots m+1 $$ . Desta forma, a Equação [1](#eq1) fica na forma: 

<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ x_{i+1}=x_{i}+\sum _{j=1}^{m+1}{\dfrac { \left( -1 \right) ^{j}{\dfrac {\partial ^{j-1}{\partial {x}^{j-1}} \left( \left( g \left( x_{i}\right) \right) ^{j} \right) }{j!} $$<br />
</center>


    
onde
    
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ {\dfrac {\partial ^{j-1}{\partial {x^{j-1}}g \left( x_{j} \right)} = {\dfrac {\partial ^{j-1}{\partial {x^{j-1}} {\dfrac {1}{f(x_{i})}} $$<br />
</center>

Desenvolvendo o somatório até $$m = 1 $$ , obtemos:
    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ x_{i+1}=x_{i}-{\dfrac {f \left( x_{i} \right) }{\dfrac {d}{dx}f \left( x_{i} \right) } &#8211; \dfrac {1}{2}\,{\dfrac { \left( f \left( x_{i}\right) \right) ^{2}{\dfrac {d^{2}{d{x}^{2}}f \left( x_{i}\right) }{ \left( {\dfrac {d}{dx}f \left( x_{i} \right) \right) ^{3}} $$<br />
</center>

Aproximando a função por ela mesmo através da Interpolação de Lagrange por dois pontos $$x\_{i} $$ e $$x\_{i-1} $$, temos:
      
<a name="eq5">(eq5)</a>
      


<center>
  <br /> $$ f \left( x \right) ={\frac { \left( x-x_{i} \right) f \left( x_{i-1} \right) }{x_{i-1}-x_{i}}+{\frac { \left( x-x_{i-1} \right) f \left( x_{i} \right) }{x_{i}-x_{i-1}} $$<br />
</center>


    
Igualmente para a primeira derivada e segunda derivada:
      
<a name="eq6">(eq6)</a>
      


<center>
  <br /> $$ {\dfrac {d}{dx}f \left( x_{i} \right) ={\dfrac {f \left( x_{i-1} \right) -f \left( x_{i} \right) }{x_{i-1}-x_{i}} $$<br />
</center>

<a name="eq7">(eq7)</a>
      


<center>
  <br /> $$ {\dfrac {d^{2}{d{x}^{2}}f \left( x_{i} \right) =-6\,{\dfrac {f \left( x_{i} \right) -f \left( x_{i-1} \right) }{ \left( x_{i} &#8211; x_{i-1} \right) ^{2}}+2\,{\dfrac {2\,{\dfrac {d}{dx}f \left( x_{i} \right) +{\dfrac {d}{dx}f \left( x_{i-1} \right) }{x_{i}-x_{i-1} }} $$<br />
</center>

Levando as Expressões [5](#eq5), [6](#eq6) e [7](#eq7) na Equação [2](#eq2), obteremos:
     
<a name="eq8">(eq8)</a>
      


<center>
  <br /> $$ x_{i+1}={\frac {f \left( x_{i-1} \right) f \left( x_{i} \right) x_{i-2}}{ \left( f \left( x_{i-2} \right) -f \left( x_{i-1} \right) \right) \left( f \left( x_{i-2} \right) -f \left( x_{i} \right) \right) }+{\frac {f \left( x_{i-2} \right) f \left( x_{i} \right) x_{i-1}}{ \left( f \left( x_{i-1} \right) -f \left( x_{i-2} \right) \right) \left( f \left( x_{i-1} \right) -f \left( x _{i} \right) \right) }+{\frac {f \left( x_{i-2} \right) f \left( x_{i-1} \right) x_{i}}{ \left( f \left( x_{i} \right) -f \left( x_{i-2} \right) \right) \left( f \left( x_{i} \right) -f \left( x_{i-1} \right) \right) } $$<br />
</center>

Para melhor melhorar a notação, tomemos $$y\_{k} = f(x\_{k}) $$ . Desta forma, a fórmula [8](#eq8) fica expressa como:

<a name="eq9">(eq9)</a>
      


<center>
  <br /> $$ x_{i+1}={\frac {y_{i-1}y_{i}x_{i-2}}{ \left( y_{i-2}-y_{i-1} \right) \left( y_{i-2}-y_{i} \right) }+{\frac {y_{i-2}y_{i}x_{i-1}}{ \left( y_{i-1}-y_{i-2} \right) \left( y_{i-1}-y_{i} \right) }+{\frac {y_{i-2}y_{i-1}x_{i}}{ \left( y_{i}-y_{i-2} \right) \left( y_{i}-y_{i-1} \right) }$$<br />
</center>

## 3. Critérios usados na implementação 

Nas implementações apresentadas a seguir, utilizamos o Método de Steffensen para obtermos a primeira aproximação e o Método da Secante para a segunda, para que de posse dessas, pudéssemos refinar a aproximação utilizando a Interpolação Quadrática Inversa. 

Desta forma, na derivada:
    
<a name="eq10">(eq10)</a>
      


<center>
  <br /> $$ {\frac {d}{dx}f \left( x \right) ={\frac {f \left( x+h \right) -f \left( x \right) }{h}$$<br />
</center>


    
aplicamos o critério de Steffensen &#8212; $$h=f \left( x \right) $$ &#8212; na primeira aproximação. Ou seja,
    
<a name="eq11">(eq11)</a>
      


<center>
  <br /> $$ h=f \left( x_{i-2} \right) $$<br />
</center>


    
o que nos permite obter a aproximação seguinte:
      


<center>
  <br /> $$ x_{i-1}=x_{i-2}-{\frac {h}^{2}{f \left( x_{i-2}+h \right) -h} $$<br />
</center>

Para próxima aproximação, aplicamos o Método da Secante:
    
<a name="eq12">(eq12)</a>
      


<center>
  <br /> $$x_{i}=x_{i-1}-{\frac {f \left( x_{i-1} \right) \left( x_{i-2} -x_{i-1} \right) }{f \left( x_{i-2} \right) -f \left( x_{i-1}\right) }$$<br />
</center>

Por questão de conveniência, renomeamos as variáveis,
    


<center>
  <br /> $$x_{0}=x_{i-2} $$<br /> <br /> $$x_{1}=x_{i-1} $$<br /> <br /> $$x_{2}=x_{i} $$<br /> <br /> $$x_{3}=x_{i+1} $$<br /> <br /> $$y_{0}=y_{i-2} $$<br /> <br /> $$y_{1}=y_{i-1} $$<br /> <br /> $$y_{2}=y_{i} $$<br />
</center>


    
o que gera o conjunto de expressões utilizados no programa:
    
<a name="eq13">(eq13)</a>
      


<center>
  <br /> $$ x_{1}=x_{0}-{\frac {y_{0}}^{2}{f \left( x_{0}+y_{0}\right) -y_{0}} $$<br />
</center>

<a name="eq14">(eq14)</a>
      


<center>
  <br /> $$ x_{2}=x_{1}-{\frac {y_{1} \left( x_{0}-x_{1} \right) }{y_{0}-y_{1}} $$<br />
</center>

<a name="eq15">(eq15)</a>
      


<center>
  <br /> $$ x_{3}={\frac {y_{1}y_{2}x_{0}}{ \left( y_{0}-y_{1} \right) \left( y_{0}-y_{2} \right) }+{\frac {y_{0}y_{2}x_{1}}{ \left( y_{1}-y_{0} \right) \left( y_{1}-y_{2} \right) }+{\frac {y_{0}y_{1}x_{2}}{ \left( y_{2}-y_{0} \right) \left( y_{2}-y_{1} \right) } $$<br />
</center>

<!--  IMPLEMENTACAO  --></p> 

## 4. Implementação <a name="sec4"></a> 

A primeira implementação apresentada a seguir consiste em aplicar os critérios apresentados na seção anterior a cada iteração, enquanto que a segunda utiliza tais critérios apenas para inicialização das variáveis, aplicando apenas a Fórmula [8](#eq8) ao longo da execução. 

Após algumas simulações, a primeira abordagem pareceu convergir mais rápido, desde que fosse dada uma boa aproximação inicial. Por outro lado, a implementação que utiliza somente a Interpolação Quadrática Inversa convergiu, independendo da aproximação inicial dada, ainda que sendo mais lenta. 

Segue as implementações destas funções abaixo: 

<div>
  <pre lang="python">def IQI(f, x0=1.0, errto=0.001, imax=100):
    """
    Return the root of a function (Inverse quadratic interpolation)

     IQI(f, x0=1.0, errto=0.001, imax=100)

    * f: Function where find roots
    * x0: next point (estimative)
    * errto: tolerated error ( for aprox. )
    * imax: max of iterations allowed

    return: root next x0

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>

    Jan 2009
    """
    errno = errto + 1
    iterCount = 0

    while errno > errto and iterCount &lt; imax:
        y0 = f(x0)
        if fabs(f(x0 + y0) - y0) != 0:
            x1 = x0 - y0*y0/(f(x0 + y0) - y0)
        else:
            x3 = x0
            break

        y1 = f(x1)
        if y0 != y1:
            x2 = x1 - y1*(x0 - x1)/(y0 - y1)
        else:
            x3 = x1
            break

        # try Aitkens optimization
        if (x2 - 2*x1 + x0) != 0:
            alpha = (x0*x2 - x1*x1)/(x2 - 2*x1 + x0)
            C1 = fabs((alpha - x1)/(alpha - x0))
            C2 = fabs((alpha - x2)/(alpha - x1))

            if (C1 &lt; 1) and (C2 &lt; 1):
                x2 = alpha

        y2 = f(x2)
        delta = 7*[0] 
        delta[1] = y0 - y1
        delta[2] = y0 - y2
        delta[3] = y1 - y0
        delta[4] = y1 - y2
        delta[5] = y2 - y0
        delta[6] = y2 - y1

        def disturb(x):            
            if(x == 0):
                return errto
            else:
                return x

        delta = map(disturb, delta)

        x3 = y1*y2*x0/((delta[1])*(delta[2])) + \
            y0*y2*x1/((delta[3])*(delta[4])) + \
            y0*y1*x2/((delta[5])*(delta[6]))

        iterCount += 1

        if x3 != 0:
            errno = fabs((x3-x0)/x3)

        x0 = x3

    return x3</pre>
</div>

A segunda forma:

<div>
  <pre lang="python">def IQI2(f, x0=1.0, errto=0.001, imax=100):
    """
    Return the root of a function (Inverse quadratic interpolation)

     IQI2(f, x0=1.0, errto=0.001, imax=100)

    * f: Function where find roots
    * x0: next point (estimative)
    * errto: tolerate error ( for aprox. )
    * imax: max of iterations allowed

    return: root next x0

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>

    Jan 2009
    """
    errno = errto + 1
    iterCount = 0

    y0 = f(x0)
    if fabs(f(x0 + y0) - y0) != 0:
        x1 = x0 - y0*y0/(f(x0 + y0) - y0)
    else:
        x1 = errto

    y1 = f(x1)
    if y0 != y1:
        x2 = x1 - y1*(x0 - x1)/(y0 - y1)
    else:
        x2 = errto

    while errno > errto and iterCount &lt; imax:
        y0 = f(x0)
        y1 = f(x1)
        y2 = f(x2)
        delta = 7*[0] 
        delta[1] = y0 - y1
        delta[2] = y0 - y2
        delta[3] = y1 - y0
        delta[4] = y1 - y2
        delta[5] = y2 - y0
        delta[6] = y2 - y1

        def disturb(x):            
            if(x == 0):
                return errto
            else:
                return x

        delta = map(disturb, delta)

        x3 = y1*y2*x0/((delta[1])*(delta[2])) + \
            y0*y2*x1/((delta[3])*(delta[4])) + \
            y0*y1*x2/((delta[5])*(delta[6]))

        iterCount += 1

        if x3 != 0:
            errno = fabs((x3-x0)/x3)

        x0 = x1
        x1 = x2
        x2 = x3        

    return x3</pre>
</div>

Nos arquivos <a href="http://www.sawp.com.br/code/rootfind/IQI.py" target="_blank">http://www.sawp.com.br/code/rootfind/IQI.py</a> e <a href="http://www.sawp.com.br/code/rootfind/IQI2.py" target="_blank">http://www.sawp.com.br/code/rootfind/IQI2.py</a> apresento exemplos onde o uso do primeiro caso não converge, enquanto que o segundo
    
converge rapidamente. Nos mesmos arquivos, podemos ver outro exemplo onde a raiz é encontrada para ambas implementações. Nesse caso, podemos ver que o primeiro encontra o zero da função utilizando menos iterações. </p> </p> 

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a></a><br /> <a name="bibitem1"><b>[1]</b> <cite><a href="http://en.wikipedia.org/wiki/Inverse_quadratic_interpolation" target="_blank">http://en.wikipedia.org/wiki/Inverse_quadratic_interpolation</a></cite></a><br /> <a name="bibitem2"><b>[2]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 358&#8211;359.</a>
  </p>
</fieldset>
