---
id: 577
title: '2.1.1 Sistemas Lineares &#8212; Métodos Diretos &#8212; Eliminação de Gauss'
date: 2010-03-15T17:11:26+00:00
author: SAWP
excerpt: O método conhecido como "Eliminação de Gauss" consiste em combinar as equações de forma ir eliminando as variáveis até convergir à uma solução. Embora este seja um dos métodos mais antigos, e também um dos menos eficientes, serve como fundamento para compreendermos as demais técnicas relativas à resolução de sistemas lineares.
layout: post
guid: http://www.sawp.com.br/blog/?p=577
permalink: p=577
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:8447:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> gauss<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    gauss(A, b)
    &nbsp;
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    &nbsp;
    return: a list with all unknown variables of system.
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> progressive_elimination<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    factor <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>/A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> - factor * A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - factor * b<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> regressive_replace<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>/A<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> suma - A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> suma/A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> progressive_elimination<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> regressive_replace<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def gauss(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    gauss(A, b)
    
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    
    return: a list with all unknown variables of system.
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2010
    &quot;&quot;&quot;
    
    def progressive_elimination(A, b):
    n = len(b)
    for k in xrange(n-1):
    for i in xrange(k+1, n):
    factor = A[i][k]/A[k][k]
    for j in xrange(k+1, n):
    A[i][j] = A[i][j] - factor * A[k][j]
    b[i] = b[i] - factor * b[k]
    return (A, b)
    
    def regressive_replace(A, b):
    n = len(b)
    x = [0.0 for i in xrange(n)]
    x[n-1] = b[n-1]/A[n-1][n-1]
    for i in xrange(n-1, -1, -1):
    suma = b[i]
    for j in xrange(i+1, n):
    suma = suma - A[i][j] * x[j]
    x[i] = suma/A[i][i]
    return x
    
    (A, b) = progressive_elimination(A, b)
    return regressive_replace(A, b)</p></div>
    ;i:2;s:3441:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> remove_null_pivot<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    checked <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> i <span style="color: #66cc66;">&lt;</span> n <span style="color: #ff7700;font-weight:bold;">and</span> checked <span style="color: #66cc66;">&lt;</span> n:
    <span style="color: #ff7700;font-weight:bold;">if</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> i + <span style="color: #ff4500;">1</span> <span style="color: #66cc66;">==</span> n-<span style="color: #ff4500;">1</span>:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i+<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i+<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    checked +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def remove_null_pivot(A, b):
    n = len(b)
    checked = 0
    i = 0
    while i &lt; n and checked &lt; n:
    if A[i][i] == 0.0:
    if i + 1 == n-1:
    A[i] = A[i-1]
    b[i] = b[i-1]
    else:
    A[i] = A[i+1]
    b[i] = b[i+1]
    i = 0
    checked += 1
    return (A, b)</p></div>
    ;i:3;s:4286:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> pivot<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    p <span style="color: #66cc66;">=</span> k
    bigger <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    sentinel <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>sentinel <span style="color: #66cc66;">&gt;</span> bigger<span style="color: black;">&#41;</span>:
    bigger <span style="color: #66cc66;">=</span> sentinel
    p <span style="color: #66cc66;">=</span> i
    <span style="color: #ff7700;font-weight:bold;">if</span> p <span style="color: #66cc66;">!=</span> k:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> A<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>b<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> b<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>b<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> b<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def pivot(A, b, k):
    n = len(b)
    p = k
    bigger = abs(A[k][k])
    for i in xrange(k+1, n):
    sentinel = abs(A[i][k])
    if (sentinel &gt; bigger):
    bigger = sentinel
    p = i
    if p != k:
    for i in xrange(k, n):
    (A[p][i], A[k][i]) = (A[k][i], A[p][i])
    (b[p], b[k]) = (b[k], b[p])</p></div>
    ;i:4;s:13262:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> gauss_robust<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    gauss_robust(A, b)
    &nbsp;
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    &nbsp;
    return: a list with all unknown variables of system.
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> pivot<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    p <span style="color: #66cc66;">=</span> k
    bigger <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    sentinel <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>sentinel <span style="color: #66cc66;">&gt;</span> bigger<span style="color: black;">&#41;</span>:
    bigger <span style="color: #66cc66;">=</span> sentinel
    p <span style="color: #66cc66;">=</span> i
    <span style="color: #ff7700;font-weight:bold;">if</span> p <span style="color: #66cc66;">!=</span> k:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> A<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>b<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> b<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>b<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> b<span style="color: black;">&#91;</span>p<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> progressive_elimination<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> pivot<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    factor <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>/A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> - factor * A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - factor * b<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> regressive_replace<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>/A<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> suma - A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> suma/A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> progressive_elimination<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> regressive_replace<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def gauss_robust(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    gauss_robust(A, b)
    
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    
    return: a list with all unknown variables of system.
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2010
    &quot;&quot;&quot;
    
    def pivot(A, b, k):
    n = len(b)
    p = k
    bigger = abs(A[k][k])
    for i in xrange(k+1, n):
    sentinel = abs(A[i][k])
    if (sentinel &gt; bigger):
    bigger = sentinel
    p = i
    if p != k:
    for i in xrange(k, n):
    (A[p][i], A[k][i]) = (A[k][i], A[p][i])
    (b[p], b[k]) = (b[k], b[p])
    return (A, b)
    
    def progressive_elimination(A, b):
    n = len(b)
    for k in xrange(n-1):
    (A, b) = pivot(A, b, k)
    for i in xrange(k+1, n):
    factor = A[i][k]/A[k][k]
    for j in xrange(k+1, n):
    A[i][j] = A[i][j] - factor * A[k][j]
    b[i] = b[i] - factor * b[k]
    return (A, b)
    
    def regressive_replace(A, b):
    n = len(b)
    x = [0.0 for i in xrange(n)]
    x[n-1] = b[n-1]/A[n-1][n-1]
    for i in xrange(n-1, -1, -1):
    suma = b[i]
    for j in xrange(i+1, n):
    suma = suma - A[i][j] * x[j]
    x[i] = suma/A[i][i]
    return x
    
    (A, b) = progressive_elimination(A, b)
    return regressive_replace(A, b)</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Em um sistema linear formado por um par de equações, o processo para obtenção se descobrir as duas incógnitas consiste em isolar uma delas e substituir na outra equação, eliminando assim, uma das incógnitas.

Para um sistema maior, podemos estender a abordagem para um número maior de equações através do algoritmo conhecido como &#8220;Eliminação de Gauss&#8221;, que basicamente manipula algumas variáveis, a fim de gerar uma eliminação ao longo da execução, ao tempo que vai substituindo regressivamente nas equações originais, a fim de obter a solução final. 

Sendo assim, o sistema geral que iremos estudar é formado por um conjunto arbitrário de \(n \) equações tais que:
       
<a name="eq1">(eq1)</a>
      


<center>
  <br /> \( a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n = b_1 \)<br />
</center>


       
<a name="eq2">(eq2)</a>
      


<center>
  <br /> \( a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n = b_2 \)<br />
</center>


       


<center>
  \(\vdots \) \(\vdots \)
</center>


      
<a name="eq3">(eq3)</a>
      


<center>
  <br /> \( a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n = b_n \)<br />
</center>

Entre os métodos computacionais temos que o processo de diagonalização de matrizes é uma técnica-chave para solução de sistemas lineares. Sendo assim, a primeira fase da eliminação de Gauss está em reduzir a matriz dos coeficientes para uma matriz triangular-superior, eliminando da primeira variável em todas as equações diferentes de \(1 \) . 

Para isso, vamos multiplicar a Equação [1](#eq1) por \(\frac{a\_{21}}{a\_{11}} \) . Com isso, obtemos
    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> \( a_{21}x_1 + \dfrac{a_{21}}{a_{11}}a_{12}x_2 + \cdots + \dfrac{a_{21}}{a_{11}}a_{1n}x_n = \dfrac{a_{21}}{a_{11}}b_{1} \)<br />
</center>

Agora, subtraímos a Equação [4](#eq4) da Equação [2](#eq2), o que nos permite obter
    
<a name="eq5">(eq5)</a>
      


<center>
  <br /> \( \left(a_{22} &#8211; \dfrac{a_{21}}{a_{11}}a_{12}\right)x_2 + \cdots + \left(a_{2n} &#8211; \dfrac{a_{21}}{a_{11}}a_{1n}\right)x_n = b_2 &#8211; \dfrac{a_{21}}{a_{11}}b_1 \)<br />
</center>


    
substituindo cada termo dentro dos parênteses por um novo \(a&#8217;_{2i} \) , onde \(i=2 \ldots n \) , temos que a Equação [5](#eq5) pode ser escrita como
     
<a name="eq6">(eq6)</a>
      


<center>
  <br /> \( a&#8217;_{22}x_2 + \cdots + a&#8217;_{2n}x_n = b&#8217;_2 \)<br />
</center>


    
onde \(a&#8217;\_{2i} = \left( a\_{2i} &#8211; \dfrac{a\_{21}}{a\_{11}}a_{1n} \right) \) . 

Assim como fizemos com a segunda linha do sistema, repetimos o processo para as demais \(n \) equações. Ou seja, multiplicamos \(\frac{a\_{31}}{a\_{11}} \) pela Equação [1](#eq1) e subtraímos o resultado da equação [3](#eq3), e continuamos o processo até a última equação. 

No processo de eliminação, o termo \(a\_{11} \) é conhecido como &#8220;pivô&#8221;, e a multiplicação de cada linha pelo elemento \(\frac{a\_{2i}}{a_{11}} \) é denominada &#8220;normalização&#8221;. Portanto, podemos notar que o pivô nulo é um problema no processo de normalização, já que provoca uma divisão por zero. Por isso, em implementações reais, devemos utilizar algumas técnicas de &#8220;re-normalização&#8221; para eliminarmos o pivô nulo do processo. 

Após a primeira eliminação, a qual estamos descrevendo até aqui, o sistema linear modificado ficará:
     
<a name="eq7">(eq7)</a>
      


<center>
  <br /> \( a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n = b_1 \)<br />
</center>


     
<a name="eq8">(eq8)</a>
      


<center>
  <br /> \( \hspace{35pt} a&#8217;_{22}x_2 + \cdots + a&#8217;_{2n}x_n = b&#8217;_2 \)<br />
</center>


       


<center>
  \(\vdots \) \(\vdots \)
</center>


     
<a name="eq9">(eq9)</a>
      


<center>
  <br /> \( \hspace{35pt} a&#8217;_{n2}x_2 + \cdots + a&#8217;_{nn}x_n = b&#8217;_n \)<br />
</center>


    
agora, repetimos o mesmo processo de eliminação, mas tomando como coeficiente de normalização como sendo \(\dfrac{a&#8217;\_{32}}{a&#8217;\_{22}} \) , aplicando-o à todas equações a partir da terceira. Este processo deve continuar usando os pivôs obtidos nas equações remanescentes. Ou seja, repetimos o pivotamento e normalização descritas para até a equação \((n-1) \) , eliminando até o termo \(x_{n-1} \) da \(n-esima \) equação. Com isso, obteremos o sistema triangular a seguir:
     
<a name="eq10">(eq10)</a>
      


<center>
  <br /> \( a_{11}x_1 + a_{12}x_2 + a_{13}x_3 + \cdots + a_{1n}x_n = b_1 \)<br />
</center>


     
<a name="eq11">(eq11)</a>
      


<center>
  <br /> \( \hspace{35pt} a&#8217;_{22}x_2 + a&#8217;_{23}x_3 + \cdots + a&#8217;_{2n}x_n = b&#8217;_2 \)<br />
</center>


     
<a name="eq12">(eq12)</a>
      


<center>
  <br /> \( \hspace{70pt} a&#8221;_{33}x_3 + \cdots + a&#8221;_{3n}x_n = b&#8221;_3 \)<br />
</center>


      


<center>
  \(\hspace{50pt} \vdots \)
</center>


     
<a name="eq13">(eq13)</a>
      


<center>
  <br /> \( \hspace{110pt} a^{(n-1)}_{nn}x_n = b^{(n-1)}_n \)<br />
</center>

A partir do sistema triangular, a solução é facilmente obtida, a começar por \(x_n \) :
      
<a name="eq14">(eq14)</a>
      


<center>
  <br /> \( x_n = \dfrac{b^{n-1}_n}{a^{n-1}_{nn}} \)<br />
</center>


    
substituindo esse resultado na equação anterior, isto é, na equação \((n-1) \), cuja dependência está apenas nas variáveis \(x\_{n-1} \) e \(x\_n\), podemos determinar também \(x_{n-1}\). Esse processo de ir substituindo as incógnitas já encontradas nas equações anteriores chamaremos de _backtrack_. A partir dele, encontramos todos \(x_i\) pela da fórmula:
    
<a name="eq15">(eq15)</a>
      


<center>
  <br /> \( x_i = \dfrac{ b^{(i-1)}_{i} &#8211; \sum^{n}_{j=i+1} a^{(i-1)}_{ij}x_j }{a^{i-1}_{ii}} \)<br />
</center>


    
para \(i = (n-1), (n-2), \ldots, 1 \) 



## 2. Implementação </p> 

A implementação da forma mais simples do processo de eliminação progressiva, seguida da substituição regressiva segue abaixo. 

<div>
  <pre lang="python">def gauss(A, b):
    """
    Return a list with the solution of linear system.

    gauss(A, b)

    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms

    return: a list with all unknown variables of system.

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2010
    """

    def progressive_elimination(A, b):
        n = len(b)
        for k in xrange(n-1):
            for i in xrange(k+1, n):
                factor = A[i][k]/A[k][k]
                for j in xrange(k+1, n):
                    A[i][j] = A[i][j] - factor * A[k][j]
                b[i] = b[i] - factor * b[k]
        return (A, b)

    def regressive_replace(A, b):
        n = len(b)
        x = [0.0 for i in xrange(n)]
        x[n-1] = b[n-1]/A[n-1][n-1]
        for i in xrange(n-1, -1, -1):
            suma = b[i]
            for j in xrange(i+1, n):
                suma = suma - A[i][j] * x[j]
            x[i] = suma/A[i][i]
        return x

    (A, b) = progressive_elimination(A, b)
    return regressive_replace(A, b)</pre>
</div>

Embora este código funciona bem para uma série de equações ele produzirá um erro cada vez que o pivô for um elemento nulo, pois isso implicará em divisão por zero. 

Como os pivôs são formados apenas pelos elementos da diagonal principal, antes do programa executar a eliminação progressiva, ele pode verificar a existência de nulidade dos pivôs. Caso haja, basta que a linha nula seja trocada por outra, já que isso não afeta o resultado final. Esta função pode ser, por exemplo:

<div>
  <pre lang="python">def remove_null_pivot(A, b):
        n = len(b)
        checked = 0
        i = 0
        while i &lt; n and checked &lt; n:
            if A[i][i] == 0.0:
                if i + 1 == n-1:
                    A[i] = A[i-1]
                    b[i] = b[i-1]
                else:
                    A[i] = A[i+1]
                    b[i] = b[i+1]
                i = 0
            checked += 1
        return (A, b)</pre>
</div>

A implementação destas funções, bem como um exemplo de como utilizá-la está disponível em <a href="http://www.sawp.com.br/code/linear/gauss.py" target="_blank">http://www.sawp.com.br/code/linear/gauss.py</a>. 



## 3. Refinando a Implementação </p> 

Ainda que muitos sistemas de equações possam ser resolvidos com a última implementação apresentada, há algumas peculiaridades de casos em que ela não é eficiente. Para ser usado em um programa robusto, devemos fazer com que o algoritmo preveja as seguintes situações de erro:

  * **Divisão por zero:** quando o pivô é nulo, o programa mostrado anteriormente acabará gerando uma divisão por zero, o que implicará em uma possível falha de todo o sistema. Para evitar este tipo de problema, um tratamento sobre os dados deve ser feito. Esse tratamento consiste em uma técnica chamada _pivotamento_. 
      * **Roundoff Error:** &#8220;Erros de arrendondamento.&#8221; Um problema muito comum no tratamento de números reais por computadores. O problema de arrendondamento é um fator inerente às máquinas reais. Isso ocorre porque os computadores possuem um número finito de algarismos significativos, implicando em limites na expressão de números reais através da notação de ponto flutuante. 
        O problema de arrendondamento pode ser propagando em um grande número de iterações ou, como é o caso da Eliminação de Gauss, que é um método de solução direta, na manipulação de um grande número de equações. Como erros de arrendondamento induzem mudanças nos coeficientes dessas equações, essas mudanças podem levar a erros grandes nas soluções de sistemas sem balanceamento. 
        
        Um fator importante para evitar a propagação de erros, a fim de se obter um resultado com certa precisão desejada, consiste em utilizar técnicas de arrendondamento. Ralson e Rabinowitz[[rabinowitz]](#bibitemrabinowitz) fazem uma excelente discussão formal de tratamento de erros de arrendondamento, que vale a pena ser consultada. 
        
          * **Mal condicionamento:** Sistemas &#8220;mal condicionados&#8221;, como o próprio nome sugere, são aqueles que por sua própria formação estão sob condições ruins. Isto é, eles estão desbalanceados, de forma que a realização de operações entre seus coeficientes geram resultados ruins, normalmente associados à propagação de erros de arrendondamento. 
            A primeira implicação de problemas mal condicionados é que pequenas mudanças nos seus coeficientes implicam em grande divergência na solução correta. Assim, haveria uma quantidade grande de respostas que serviriam como aproximação da solução do sistema, o que é uma coisa indesejável, uma vez que sistemas lineares possuem solução única. </p> 

Sendo assim, com o intuito de contornar esses erros, intrínsecos à precisão computacional, as técnicas para tornar o nosso programa mais robusto são:

  * **Aumentar o número de algarismos significativos:** Com mais casas disponíveis para manipulação dos dados, os problemas do mal condicionamento e da propagação do erro são minimizados ao longo de uma série muito grande de cálculos. Por isso, o ideal é sempre usarmos a maior palavra disponível para manipulação de ponto flutuante disponível para nosso sistema (em geral, sempre que precisarmos de valores de até \(16 \) casas de precisão (equivalente ao tipo _float_ em C), devemos prefirir usar o tipo _double_. As arquiteturas mais atuais possuem tecnologias avançadas de tratamento de ponto flutuante, tais como _SSE_, que contém registradores de até \(128 \) _bits_, o que permite uma precisão muito superior, e que deve ser explorada). 
      * **Pivoteamento:** Para solucionar o problema do pivô nulo (ou muito menor que o elemento da normalização), podemos balancear o sistema, a fim de gerar uma pré-normalização, a fim de evitar uma disparidade muito grande entre os operandos. 
        Assim, antes que cada linha seja normalizada, o programa deve determinar o maior coeficiente disponível na coluna logo abaixo do pivô. Em seguida, as linhas devem ser trocadas para que o maior elemento dado seja o pivô. Após este re-pivotamento parcial, buscamos o maior elemento nas colunas, a fim de encontrar também o maior elemento dentre as colunas, refinando assim o melhor pivô a ser usado. 
        
        O pivotamento, além de resolver o problema do pivô nulo, também auxilia na diminuição da propagação do erro de arrendondamento, sendo uma solução eficiente e altamente recomendada para implementações reais. 
        
        Um pivotamento pode ser realizado pela seguinte função:
        
        <div>
          <pre lang="python">def pivot(A, b, k):
    n = len(b)
    p = k
    bigger = abs(A[k][k])
    for i in xrange(k+1, n):
        sentinel = abs(A[i][k])
        if (sentinel > bigger):
            bigger = sentinel
            p = i
    if p != k:
        for i in xrange(k, n):
            (A[p][i], A[k][i]) = (A[k][i], A[p][i])
        (b[p], b[k]) = (b[k], b[p])</pre>
        </div>
        
        Este função é projetada para ser chamada antes de cada nova normalização do sistema. Isso é, como cada eliminação progressiva é feita em cada linha, \((n-1) \) pivôs serão gerados, como já discutimos anteriormente. Sendo assim, para cada um deles, devemos chamar a função _pivot_ para permitir o balanceamento do sistema. 
        
        Da função _pivot_, temos que a linha \(3 \) captura inicialmente a posição do primeiro pivô, enquanto que a linha \(4 \) coloca na variável _bigger_, o seu valor. O laço de repetição definido da linha \(5 \) à \(9 \) é que realiza a busca na matriz dos coeficientes. Caso haja um valor maior que o pivô inicial, seu valor e posição são atualizados nas variáveis _bigger_ e _p_. As linhas que seguem servem para verificar se a posição do maior pivô foi alterado. Caso isso tenha ocorrido, o sistema é rearranjado para a forma pivotada, conforme descrevemos anteriormente. 

## 4. Implementação da Eliminação de Gauss </p> 

A implementação completa da eliminação de Gauss, considerando o pivotamento segue abaixo:

<div>
  <pre lang="python">def gauss_robust(A, b):
    """
    Return a list with the solution of linear system.

    gauss_robust(A, b)

    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms

    return: a list with all unknown variables of system.

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2010
    """

    def pivot(A, b, k):
        n = len(b)
        p = k
        bigger = abs(A[k][k])
        for i in xrange(k+1, n):
            sentinel = abs(A[i][k])
            if (sentinel > bigger):
                bigger = sentinel
                p = i
        if p != k:
            for i in xrange(k, n):
                (A[p][i], A[k][i]) = (A[k][i], A[p][i])
            (b[p], b[k]) = (b[k], b[p])
        return (A, b)

    def progressive_elimination(A, b):
        n = len(b)
        for k in xrange(n-1):
            (A, b) = pivot(A, b, k)
            for i in xrange(k+1, n):
                factor = A[i][k]/A[k][k]
                for j in xrange(k+1, n):
                    A[i][j] = A[i][j] - factor * A[k][j]
                b[i] = b[i] - factor * b[k]
        return (A, b)

    def regressive_replace(A, b):
        n = len(b)
        x = [0.0 for i in xrange(n)]
        x[n-1] = b[n-1]/A[n-1][n-1]
        for i in xrange(n-1, -1, -1):
            suma = b[i]
            for j in xrange(i+1, n):
                suma = suma - A[i][j] * x[j]
            x[i] = suma/A[i][i]
        return x

    (A, b) = progressive_elimination(A, b)
    return regressive_replace(A, b)</pre>
</div>

Note que pouca alteração foi necessária em relação à forma mais ingênua do algoritmo. Este código está disponível em <a href="http://www.sawp.com.br/code/linear/gauss_robust.py" target="_blank">http://www.sawp.com.br/code/linear/gauss_robust.py</a>, bem como um exemplo de como utilizá-lo.

## 5. Copyright </p> 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.
  


<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitemrabinowitz"><b>[rabinowitz]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.)</cite> McGraw-Hill and Dover, (2001), 425.</a>
  </p>
  
  <p>
    <a name="all"><b>[2]</b> David Goldberg,<cite> <em>What Every Computer Scientist Should Know About Floating-Point Arithmetic</em></cite>http://docs.sun.com/source/806-3568/ncg_goldberg.html</a><br /> </fieldset>
  </p>
