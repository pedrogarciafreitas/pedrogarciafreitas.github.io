---
id: 473
title: '1.3.3 Raízes de Equações &#8212; Raízes de Polinômios &#8212; O Método de Bairstow'
date: 2010-03-09T21:49:39+00:00
author: SAWP
excerpt: |
  O Método de Bairstow permite encontrar todas as raízes de um polinômio de grau $n$ exigindo-se apenas seus coeficientes.
  
  Este artigo faz uma breve exposição matemática do método, seguida de duas implementações reais nas linguagens Python e Fortran 90.
layout: post
guid: http://www.sawp.com.br/blog/?p=473
permalink: p=473
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:19823:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> bairstow<span style="color: black;">&#40;</span>a<span style="color: #66cc66;">,</span> rr<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> ss<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">500</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Calculate the roots of a function (using the Bairstow Method)
    &nbsp;
    bairstow(a, polDegree, errto, rr, ss, imax)
    &nbsp;
    * a[]: list with the coeficients
    * rr: initial aprox. of &quot;r&quot; param
    * ss: initial aprox. of &quot;s&quot; param
    * errto: tolerated error
    * imax: max iterCountation allowed (not inf-loop)
    &nbsp;
    return: a list with all roots of polynom
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jan 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> filt<span style="color: black;">&#40;</span>l<span style="color: black;">&#41;</span>:
    r <span style="color: #66cc66;">=</span> l.<span style="color: black;">real</span>
    i <span style="color: #66cc66;">=</span> l.<span style="color: black;">imag</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>r<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> errto:
    r <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> errto:
    i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>r<span style="color: #66cc66;">,</span> i<span style="color: black;">&#41;</span>
    &nbsp;
    r <span style="color: #66cc66;">=</span> rr
    s <span style="color: #66cc66;">=</span> ss
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>a<span style="color: black;">&#41;</span> - <span style="color: #ff4500;">1</span>
    &nbsp;
    ea1 <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    ea2 <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    roots <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>a<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>a<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    c <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>a<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> n <span style="color: #66cc66;">&gt;=</span> <span style="color: #ff4500;">3</span> <span style="color: #ff7700;font-weight:bold;">or</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> ea1 <span style="color: #66cc66;">&gt;=</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> ea2 <span style="color: #66cc66;">&gt;=</span> errto <span style="color: #ff7700;font-weight:bold;">or</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    b<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> a<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span>
    b<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> a<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + r * b<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span>
    c<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span>
    c<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + r * c<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> a<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> + r * b<span style="color: black;">&#91;</span>i+<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + s * b<span style="color: black;">&#91;</span>i+<span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    c<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> + r * c<span style="color: black;">&#91;</span>i+<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + s * c<span style="color: black;">&#91;</span>i+<span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    &nbsp;
    det <span style="color: #66cc66;">=</span> c<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>*c<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> - c<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span>*c<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> det <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    dr <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>-b<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>*c<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> + b<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>*c<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>/det
    ds <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>-b<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>*c<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> + b<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>*c<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>/det
    r <span style="color: #66cc66;">=</span> r + dr
    s <span style="color: #66cc66;">=</span> s + ds
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> r <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    ea1 <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>dr/r<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> s <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    ea2 <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>ds/s<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    r +<span style="color: #66cc66;">=</span> errto
    s +<span style="color: #66cc66;">=</span> errto
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: black;">&#40;</span>r1<span style="color: #66cc66;">,</span> i1<span style="color: #66cc66;">,</span> r2<span style="color: #66cc66;">,</span> i2<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> quadratic_solve<span style="color: black;">&#40;</span>r<span style="color: #66cc66;">,</span> s<span style="color: black;">&#41;</span>
    roots<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>r1<span style="color: #66cc66;">,</span> i1<span style="color: black;">&#41;</span>
    roots<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>r2<span style="color: #66cc66;">,</span> i2<span style="color: black;">&#41;</span>
    n <span style="color: #66cc66;">=</span> n - <span style="color: #ff4500;">2</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    a<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i+<span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> n <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">2</span>:
    r <span style="color: #66cc66;">=</span> -a<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>/a<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    s <span style="color: #66cc66;">=</span> -a<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>/a<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    <span style="color: black;">&#40;</span>r1<span style="color: #66cc66;">,</span> i1<span style="color: #66cc66;">,</span> r2<span style="color: #66cc66;">,</span> i2<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> quadratic_solve<span style="color: black;">&#40;</span>r<span style="color: #66cc66;">,</span> s<span style="color: black;">&#41;</span>
    roots<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>r1<span style="color: #66cc66;">,</span> i1<span style="color: black;">&#41;</span>
    roots<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>r2<span style="color: #66cc66;">,</span> i2<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    roots<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>-a<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>/a<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> iterCount
    roots<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span>:<span style="color: #008000;">len</span><span style="color: black;">&#40;</span>roots<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>.<span style="color: black;">sort</span><span style="color: black;">&#40;</span>key<span style="color: #66cc66;">=</span><span style="color: #ff7700;font-weight:bold;">lambda</span> r: r.<span style="color: black;">real</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span>filt<span style="color: #66cc66;">,</span> roots<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span>:<span style="color: #008000;">len</span><span style="color: black;">&#40;</span>roots<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def bairstow(a, rr=1, ss=1, errto=0.001, imax=500):
    &quot;&quot;&quot;
    Calculate the roots of a function (using the Bairstow Method)
    
    bairstow(a, polDegree, errto, rr, ss, imax)
    
    * a[]: list with the coeficients
    * rr: initial aprox. of &quot;r&quot; param
    * ss: initial aprox. of &quot;s&quot; param
    * errto: tolerated error
    * imax: max iterCountation allowed (not inf-loop)
    
    return: a list with all roots of polynom
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jan 2010
    &quot;&quot;&quot;
    
    def filt(l):
    r = l.real
    i = l.imag
    if abs(r) &lt; errto:
    r = 0.0
    if abs(i) &lt; errto:
    i = 0.0
    return complex(r, i)
    
    r = rr
    s = ss
    n = len(a) - 1
    
    ea1 = errto + 1
    ea2 = errto + 1
    iterCount = 0
    roots = [ complex(0,0) for i in xrange(len(a)) ]
    b = [ complex(0,0) for i in xrange(len(a)) ]
    c = [ complex(0,0) for i in xrange(len(a)) ]
    
    while n &gt;= 3 or iterCount &lt; imax:
    iterCount = 0
    
    while ea1 &gt;= errto and ea2 &gt;= errto or iterCount &lt; imax:
    iterCount += 1
    b[n] = a[n]
    b[n-1] = a[n-1] + r * b[n]
    c[n] = b[n]
    c[n-1] = b[n-1] + r * c[n]
    
    for i in xrange(n-2, -1, -1):
    b[i] = a[i] + r * b[i+1] + s * b[i+2]
    c[i] = b[i] + r * c[i+1] + s * c[i+2]
    
    det = c[2]*c[2] - c[3]*c[1]
    
    if det != 0.0:
    dr = (-b[1]*c[2] + b[0]*c[3])/det
    ds = (-b[0]*c[2] + b[1]*c[1])/det
    r = r + dr
    s = s + ds
    
    if r != 0.0:
    ea1 = abs(dr/r)
    
    if s != 0.0:
    ea2 = abs(ds/s)
    else:
    r += errto
    s += errto
    iterCount = 0
    
    (r1, i1, r2, i2) = quadratic_solve(r, s)
    roots[n] = complex(r1, i1)
    roots[n-1] = complex(r2, i2)
    n = n - 2
    
    for i in xrange(n):
    a[i] = b[i+2]
    
    if n == 2:
    r = -a[1]/a[2]
    s = -a[0]/a[2]
    (r1, i1, r2, i2) = quadratic_solve(r, s)
    roots[n] = complex(r1, i1)
    roots[n-1] = complex(r2, i2)
    else:
    roots[n] = complex(-a[0]/a[1], 0.0)
    print iterCount
    roots[1:len(roots)].sort(key=lambda r: r.real)
    return map(filt, roots[1:len(roots)])</p></div>
    ;i:2;s:3478:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> quadratic_solve<span style="color: black;">&#40;</span>r<span style="color: #66cc66;">,</span> s<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Calculate the roots of a parabolic equation: a*x^2 + b*x + c = 0 (*)
    &nbsp;
    quadratic_solve(r, s)
    &nbsp;
    * r: b coeficient of (*)
    * s: a*c, coeficients of (*)
    &nbsp;
    return: a tuple with roots of (*)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http:!www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jan 2009
    &quot;&quot;&quot;</span>
    delta <span style="color: #66cc66;">=</span> r*r + <span style="color: #ff4500;">4.0</span>*s
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> delta <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    r1 <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>r + sqrt<span style="color: black;">&#40;</span>delta<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>/<span style="color: #ff4500;">2.0</span>
    r2 <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>r - sqrt<span style="color: black;">&#40;</span>delta<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>/<span style="color: #ff4500;">2.0</span>
    i1 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    i2 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    r1 <span style="color: #66cc66;">=</span> r/<span style="color: #ff4500;">2.0</span>
    r2 <span style="color: #66cc66;">=</span> r1
    i1 <span style="color: #66cc66;">=</span> sqrt<span style="color: black;">&#40;</span><span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>/<span style="color: #ff4500;">2.0</span>
    i2 <span style="color: #66cc66;">=</span> -i1
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>r1<span style="color: #66cc66;">,</span> i1<span style="color: #66cc66;">,</span> r2<span style="color: #66cc66;">,</span> i2<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def quadratic_solve(r, s):
    &quot;&quot;&quot;
    Calculate the roots of a parabolic equation: a*x^2 + b*x + c = 0 (*)
    
    quadratic_solve(r, s)
    
    * r: b coeficient of (*)
    * s: a*c, coeficients of (*)
    
    return: a tuple with roots of (*)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http:!www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jan 2009
    &quot;&quot;&quot;
    delta = r*r + 4.0*s
    
    if delta &gt; 0:
    r1 = (r + sqrt(delta))/2.0
    r2 = (r - sqrt(delta))/2.0
    i1 = 0.0
    i2 = 0.0
    else:
    r1 = r/2.0
    r2 = r1
    i1 = sqrt(abs(delta))/2.0
    i2 = -i1
    
    return (r1, i1, r2, i2)</p></div>
    ";}
categories:
  - Computational Methods
---
<h2>1. Introdução <a name="sec1"></a> </h2>
<p>O Método de Bairstow consiste em dividir um polinômio em fatores isolados que permitam aproximar suas raízes.
</p>
<p>
  Possui a grande vantagem de conseguir extrair todas as raízes de um polinômio arbitrário sem a necessidade de percorrer todo o espaço de busca,como fariam o métodos de Muller ou Newton Raphson, que sempre convergem à aproximação mais próxima.
</p>
<p>
  Além disso, ainda possui o benefício de fornecer as raízes complexas à uma taxa de convergência quadrática utilizando-se apenas de aritmética real.
</p>
<p><h2>2. Desenvolvimento do Método <a name="sec2"></a> </h2>
</p>
<p>  Seja a função um polinômio geral:<br />
  <a name="eq1">(eq1)</a><br />
    <center><br />
    \( f_{n} = a_{0} + a_{1}x + a_{2}x^2 + \cdots + a_{n}x^n \)<br />
    </center><br />
  Se dividirmos o polinômio <a href="#eq1">1</a> pelo fator  \(x-t \) , obtemos outro polinômio de um grau a menos:<br />
  <a name="eq2">(eq2)</a><br />
    <center><br />
    \( f_{n-1} = b_{1} + b_{2}x + b_{3}x^2 + \cdots + b_{n}x^{n-1} \)<br />
    </center><br />
  Caso esta divisão não gere resto, então  \(t \)  é uma raiz do polinômio  \(f \). Mas, tomando o pior caso, onde há um resto  \(R \) . Nesse caso  \(R = b_0 \) e os coeficientes poderão ser calculados pela relação:<br />
  <a name="eq3">(eq3)</a><br />
    <center><br />
    \( b_{n} = a_{n} \)<br />
    </center><br />
   e<br />
  <a name="eq4">(eq4)</a><br />
    <center><br />
    \( b_{i} = a_{i} + b_{i+1}t \)<br />
    </center><br />
  onde  \(i=n-1, n-2, \ldots, 0 \) .
</p>
<p>
  O Método de Bairstow segue um procedimento semelhante ao descrito acima, contudo, ao invés de dividir  \(f \)  por um fator  \(x-t \) , ele divide o polinômio pelo fator  \(x*x &#8211; r*x &#8211; s \) . A introdução deste fator quadrático serve para permitir a determinação de raízes complexas, enquanto que o fator linear permitiria apenas aproximações reais.
</p>
<p>
  Ao dividirmos o polinômio pelo fator de segunda ordem, obtemos:<br />
  <a name="eq5">(eq5)</a><br />
    <center><br />
        \(f_{n-2} = b_{2} + b_{3} x + b_{4} x^2 + \cdots + b_{n-1} x^{n-3} + b_{n} x^{n-2}\)<br />
    </center><br />
  isso gera uma expressão para o resto que é:<br />
  <a name="eq6">(eq6)</a><br />
    <center><br />
    \( R = b_{1} \left(x -r \right) + b_{0} \)<br />
    </center>
</p>
<p>
  Aplicando o algoritmo de Briot-Ruffine com   \(x*x &#8211; r*x &#8211; s \)  como divisor, obtemos a seguinte relação de recorrência:<br />
  <a name="eq7">(eq7)</a><br />
    <center><br />
        \( b_{n} = a_{n} \)<br />
    </center></p>
<p>  <center><br />
    \(\Downarrow \)<br />
  </center><br />
  <a name="eq8">(eq8)</a><br />
    <center><br />
        \( b_{n-1} = a_{n-1} + r b_{n} \)<br />
    </center></p>
<p>  <center><br />
    \(\Downarrow \)<br />
  </center><br />
  <a name="eq9">(eq9)</a></p>
<p>    <center><br />
        \( b_j = a_{j} + r b_{j+1} + s b_{j+2} \)<br />
    </center><br />
  onde  \(j = n-2, n-1, \ldots, 0 \) .
</p>
<p>
  Com isso, o Método de Bairstow se resume a determinar os valores de  \(r \)  e \(s \)  que tornam o fator quadrático  \((x*x &#8211; r*x &#8211; s) \)   exato. Ou seja, ele utiliza uma estratégia para encontrar os valores de  \(r \)  e  \(s \)  para qual \(R \)  é zero. Quando  \(R=0 \) ,  \(r \)  será uma raiz do polinômio.
</p>
<p>
  Da equação do resto (Equação <a href="#eq6">6</a>) é possível notar que quando  \(R \)  é nulo,  \(b_{0} \)  e  \(b_{1} \)  são nulos. A técnica usada por Bairstow segue o desenvolvimento do Método de Newton, expandindo  \(b_{0} \)  e  \(b_{1} \)  em expressões que os aproximem de zero. Como  \(b_{0} \)  e  \(b_{1} \)  são funções de \(r \)  e  \(s \) , é possível expandir  \(R \)  por Série de Taylor para duas variáveis. Bairstow utiliza uma expansão de até a primeira ordem, gerando:</p>
<p>  <a name="eq10">(eq10)</a></p>
<p>   <center><br />
    \( b_{1}(r+\Delta r, s+\Delta s) = b_{1} + \left( \dfrac{\partial}{\partial r} b_{1} \right) \Delta r + \left( \dfrac{\partial}{\partial s} b_{1} \right) \Delta s \)<br />
    </center></p>
<p>
  <a name="eq11">(eq11)</a></p>
<p>    <center><br />
        \( b_{0}(r+\Delta r, s+\Delta s) = b_{0} + \left( \dfrac{\partial}{\partial r} b_{0} \right) \Delta r + \left( \dfrac{\partial}{\partial s} b_{0} \right) \Delta s \)<br />
    </center></p>
<p>  Como  \(b_{0} \)  e  \(b_{1} \)  serão nulos quando  \(R=0 \) , então é possível reescrever as equações acimas como:<br />
  <a name="eq12">(eq12)</a><br />
    <center><br />
        \( -b_{1} = \left( \dfrac{\partial}{\partial r} b_{1} \right) \Delta r + \left( \dfrac{\partial}{\partial s} b_{1} \right) \Delta s \)<br />
    </center>
</p>
<p>
  <a name="eq13">(eq13)</a><br />
    <center><br />
        \( -b_{0} =  \left( \dfrac{\partial}{\partial r} b_{0} \right) \Delta r + \left( \dfrac{\partial}{\partial s} b_{0} \right) \Delta s \)<br />
    </center>
</p>
<p>
  A partir das duas últimas equações, podemos obter os  valores de  \(b_{0} \)  e \(b_{1} \) . O problema agora está nas derivadas parciais de  \(b \)  em relação a \(r \)  e  \(s \) . Se elas forem determinadas o problema é reduzido à um sistema de duas equações lineares com apenas duas incógnitas:  \(\Delta r\)  e  \(\Delta s \).
</p>
<p>
  Tomando as derivadas como constantes, renomeamos elas em termos de um vetor \(c \) , tal que:<br />
  <a name="eq14">(eq14)</a><br />
    <center><br />
        \( \dfrac{\partial}{\partial r} b_{0} = c_{1} \)<br />
    </center>
</p>
<p>
  <a name="eq15">(eq15)</a><br />
    <center><br />
    \( \dfrac{\partial}{\partial s} b_{0} = c_{2} \)<br />
    </center>
</p>
<p>
  <a name="eq16">(eq16)</a><br />
    <center><br />
    \( \dfrac{\partial}{\partial r} b_{1} = c_{2} \)<br />
    </center>
</p>
<p>
  <a name="eq17">(eq17)</a><br />
    <center><br />
    \( \dfrac{\partial}{\partial s} b_{1} = c_{3} \)<br />
    </center>
</p>
<p>
  A partir das suposições acimas, o sistema de equações pode ser reescrito com suas derivadas parciais substituídas pela variável  \(c \) , tal que<br />
  <a name="eq18">(eq18)</a><br />
    <center><br />
        \( c_{2} \Delta r + c_{3} \Delta s = -b_{1} \)<br />
    </center>
</p>
<p>
  <a name="eq19">(eq19)</a><br />
    <center> \( c_{1} \Delta r + c_{2} \Delta s = -b_{0} \) </center>
</p>
<p>
  O Método de Bairstow utiliza este sistema de equações lineares para ajustar variáveis complexas da mesma forma que as reais. As derivadas parciais, obtidas pela divisão sintética de \(b \), são:<br />
  <a name="eq20">(eq20)</a><br />
    <center> \( c_{n} = b_{n} \) </center>
</p>
<p>
  <a name="eq21">(eq21)</a><br />
    <center> \( c_{n-1} = b_{n-1} + r c_{n} \) </center><br />
  portanto, generalizando para todos termos,<br />
  <a name="eq22">(eq22)</a><br />
    <center> \( c_{i} = b_{i} + r~c_{i+1} + s~c_{i+2} \) </center><br />
  onde  \(i = n-1, n-2, \ldots, 1 \) .
</p>
<p>
  Com este conjunto de equações é possível determinar  \(\Delta r \)  e  \(\Delta s \), necessários para as aproximações de  \(r \)  e  \(s \) , sendo o processo de cálculo do erro relativo de cada iteração é obtido pelas expressões:<br />
  <a name="eq23">(eq23)</a><br />
    <center> \( \left| err(r)  \right| = \left| \dfrac{\Delta r}{r} \right| \)</center><br />
   e<br />
  <a name="eq24">(eq24)</a><br />
    <center> \( \left| err(s)  \right| = \left| \dfrac{\Delta s}{s} \right| \) </center>
</p>
<p>
  Quando ambos erros estiverem abaixo do máximo tolerado,  \(r \)  e  \(s \)  estarão aproximados de forma que as raízes  \(x \)  serão determinadas por
</p>
<ol>
<li> Pela expressão abaixo, caso o polinômio que deseja-se encontrar a raiz seja quadrático:<br />
          <a name="eq25">(eq25)</a><br />
            <center><br />
                \( x = \dfrac{1}{2}r + \dfrac{1}{2} \sqrt{r^2 + 4s} \)<br />
            </center></p>
<p><li> Pela expressão abaixo, caso o polinômio seja de grau um:<br />
          <a name="eq26">(eq26)</a><br />
            <center><br />
                \( x = &#8211; \dfrac{s}{r} \)<br />
            </center></p>
<li> Caso o polinômio seja de grau maior ou igual a três, o Método de Bairstow será aplicado ao quociente para o cálculo de novos valores \(r \)  e  \(s \) usando a função abaixo. Os valores de  \(r \)  e  \(s \)  calculados anteriormente servem como parâmetro inicial para a próxima iteração.
</p>
</li>
</li>
</li>
</ol>
</p>
<p>
<!--  IMPLEMENTACAO --></p>
</p>
<p><h2>3. Implementação <a name="sec3"></a> </h2>
</p>
<p>
  Implementação em Python:</p>
<div>
<pre lang="python">def bairstow(a, rr=1, ss=1, errto=0.001, imax=500):
    """
    Calculate the roots of a function (using the Bairstow Method)

    bairstow(a, polDegree, errto, rr, ss, imax)

    * a[]: list with the coeficients
    * rr: initial aprox. of "r" param
    * ss: initial aprox. of "s" param
    * errto: tolerated error
    * imax: max iterCountation allowed (not inf-loop)

    return: a list with all roots of polynom

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
         http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jan 2010
    """

    def filt(l):
        r = l.real
        i = l.imag
        if abs(r) < errto:
            r = 0.0
        if abs(i) < errto:
            i = 0.0
        return complex(r, i)

    r = rr
    s = ss
    n = len(a) - 1

    ea1 = errto + 1
    ea2 = errto + 1
    iterCount = 0
    roots = [ complex(0,0) for i in xrange(len(a)) ]
    b = [ complex(0,0) for i in xrange(len(a)) ]
    c = [ complex(0,0) for i in xrange(len(a)) ]

    while n >= 3 or iterCount < imax:
        iterCount = 0

        while ea1 >= errto and ea2 >= errto or iterCount < imax:
            iterCount += 1
            b[n] = a[n]
            b[n-1] = a[n-1] + r * b[n]
            c[n] = b[n]
            c[n-1] = b[n-1] + r * c[n]

            for i in xrange(n-2, -1, -1):
                 b[i] = a[i] + r * b[i+1] + s * b[i+2]
                 c[i] = b[i] + r * c[i+1] + s * c[i+2]

            det = c[2]*c[2] - c[3]*c[1]

            if det != 0.0:
                dr = (-b[1]*c[2] + b[0]*c[3])/det
                ds = (-b[0]*c[2] + b[1]*c[1])/det
                r = r + dr
                s = s + ds

                if r != 0.0:
                    ea1 = abs(dr/r)

                if s != 0.0:
                    ea2 = abs(ds/s)
            else:
                r += errto
                s += errto
                iterCount = 0

        (r1, i1, r2, i2) = quadratic_solve(r, s)
        roots[n] = complex(r1, i1)
        roots[n-1] = complex(r2, i2)
        n = n - 2

        for i in xrange(n):
            a[i] = b[i+2]

    if n == 2:
        r = -a[1]/a[2]
        s = -a[0]/a[2]
        (r1, i1, r2, i2) = quadratic_solve(r, s)
        roots[n] = complex(r1, i1)
        roots[n-1] = complex(r2, i2)
    else:
        roots[n] = complex(-a[0]/a[1], 0.0)
    print iterCount
    roots[1:len(roots)].sort(key=lambda r: r.real)
    return map(filt, roots[1:len(roots)])</pre>
</div>
<p>
    Note que a função <i>quadratic\_solve</i> foi incluída para deixar explícita a resolução da fórmula quadrática. A implementação desta função é:</p>
<div>
<pre lang="python">def quadratic_solve(r, s):
    """
    Calculate the roots of a parabolic equation: a*x^2 + b*x + c = 0 (*)

    quadratic_solve(r, s)

    * r: b coeficient of (*)
    * s: a*c, coeficients of (*)

    return: a tuple with roots of (*)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http:!www.sawp.com.br

    License: Creative Commons
         http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jan 2009
    """
    delta = r*r + 4.0*s

    if delta > 0:
        r1 = (r + sqrt(delta))/2.0
        r2 = (r - sqrt(delta))/2.0
        i1 = 0.0
        i2 = 0.0
    else:
        r1 = r/2.0
        r2 = r1
        i1 = sqrt(abs(delta))/2.0
        i2 = -i1

    return (r1, i1, r2, i2) </pre>
</div>
<p>
  Observe que o programa altera os valores de  \(r \)  e  \(s \)  com algum incremento aleatório e repete o procedimento da resolução das equações quando a determinante é nula, forçando o programa a convergir à uma aproximação melhor.
</p>
<p>
  Um exemplo da utilização desta sub-rotina pode ser encontrado em: <a href="http://www.sawp.com.br/code/rootfind/bairstow.py" target="_blank">http://www.sawp.com.br/code/rootfind/bairstow.py</a>
</p>
<p>
  A utilização desta função não é tão simples, pois exige como parâmetro de entrada um vetor com os coeficientes do polinômio. Embora a utilização de listas para representar um polinômio seja algo comum para muitos programadores, certamente é uma abordagem menos intuitiva que passar uma função como referência.
</p>
<p>
  Também há disponível uma outra implementação deste algoritmo em Fortran 90 no endereço <a href="http://www.sawp.com.br/code/rootfind/bairstow.f90" target="_blank">http://www.sawp.com.br/code/rootfind/bairstow.f90</a>
</p>
</p>
</p>
<p><h2>4. Copyright </h2>
</p>
<p>
  Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.
</p>
<p></p>
<fieldset>
<legend>
<h2>References</h2>
</legend>
<p><a></a><br />
<a name="bibitem1"><b>[1]</b> </a><a href="http://mathworld.wolfram.com/BairstowsMethod.html" target="_blank">http://mathworld.wolfram.com/BairstowsMethod.html</a><br />
<a name="bibitem2"><b>[2]</b>  <cite>http://en.wikipedia.org/wiki/Bairstow&#8217;s_method</cite></a><br />
<a name="bibitem3"><b>[3]</b>  Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 374.</a><br />
<a name="bibitem4"><b>[4]</b>  N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 99.</a><br />
</fieldset></p>
