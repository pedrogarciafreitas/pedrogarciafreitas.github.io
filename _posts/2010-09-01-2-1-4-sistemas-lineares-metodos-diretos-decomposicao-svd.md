---
id: 657
title: '2.1.4 Sistemas Lineares &#8212; Métodos Diretos &#8212; Decomposição SVD'
date: 2010-09-01T13:26:03+00:00
author: SAWP
excerpt: '    Uma das mais importantes fatorações de matrizes é a Singular Value Decomposition (SVD). Ela é utilizada em diversos problemas práticos, tais como processamento de sinais, ajuste de funções multivariadas, soluções de problemas de otimização, etc. Sua principal aplicação nestes problemas está em permitir a aproximação da pseudo-inversa da matriz decomposta. Neste artigo vamos apresentar a decomposição SVD e mostrar como ela pode ser utilizada para solução de sistemas lineares.'
layout: post
guid: http://www.sawp.com.br/blog/?p=657
permalink: /p=657
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:74229:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> SVD<span style="color: black;">&#40;</span>arg<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the (S,V,D) from Singular Values Decomposition.
    &nbsp;
    SVD(A)
    &nbsp;
    INPUT:
    * A: matrix to decompose
    &nbsp;
    return: the tuple (S,V,D)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    OBS: This is a implementation of a Modified Golub-Reinsch SVD and
    the code is adapted from the NIST Template Numerical Toolkit (TNT)
    by Roldan Pozo. see: http://math.nist.gov/tnt/
    &nbsp;
    Aug 2010
    &quot;&quot;&quot;</span>
    A <span style="color: #66cc66;">=</span> deepcopy<span style="color: black;">&#40;</span>arg<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    nu <span style="color: #66cc66;">=</span> <span style="color: #008000;">min</span><span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>numcols<span style="color: #66cc66;">,</span> numrows<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #008000;">min</span><span style="color: black;">&#40;</span>m - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">max</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">min</span><span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    S <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>nu<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>  <span style="color: #808080; font-style: italic;"># singular values</span>
    V <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">min</span><span style="color: black;">&#40;</span>m + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    D <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    e <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    sigma <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Diagonalize the original matrix in superdiagonal V</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">max</span><span style="color: black;">&#40;</span>numcols<span style="color: #66cc66;">,</span> numrows<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    km_range <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>
    kp1_range <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> k <span style="color: #66cc66;">&lt;</span> numcols:
    <span style="color: #808080; font-style: italic;"># Compute the 2-norm of k-th column for S</span>
    V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> km_range:
    V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> hypot<span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0.0</span>:
    V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> km_range:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> / V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> + <span style="color: #ff4500;">1.0</span>
    V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> kp1_range:
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>k <span style="color: #66cc66;">&lt;</span> numcols<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> km_range:
    t <span style="color: #66cc66;">=</span> t + A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    t <span style="color: #66cc66;">=</span> -t / A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> km_range:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + t * A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> k <span style="color: #66cc66;">&lt;</span> numcols:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> km_range:
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> k <span style="color: #66cc66;">&lt;</span> numrows:
    <span style="color: #808080; font-style: italic;"># Compute the 2-norm of k-th column for D</span>
    e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> kp1_range:
    e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> hypot<span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> e<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> e<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0.0</span>:
    e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> kp1_range:
    e<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> e<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> / e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> e<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #ff4500;">1.0</span>
    e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span> <span style="color: #66cc66;">&lt;</span> m<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    sigma<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> kp1_range:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    sigma<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> sigma<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> + e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> kp1_range:
    t <span style="color: #66cc66;">=</span> -e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> / e<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + t * sigma<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> kp1_range:
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> e<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># setup bidiagonal matrix</span>
    p <span style="color: #66cc66;">=</span> <span style="color: #008000;">min</span><span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> m + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> numcols <span style="color: #66cc66;">&lt;</span> n:
    V<span style="color: black;">&#91;</span>numcols<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>numcols<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>numcols<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> m <span style="color: #66cc66;">&lt;</span> p:
    V<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>numrows + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> p:
    e<span style="color: black;">&#91;</span>numrows<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>numrows<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># generate S</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>numcols<span style="color: #66cc66;">,</span> nu<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    S<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>numcols - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> nu<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> t + S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    t <span style="color: #66cc66;">=</span> -t / S<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + t * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    S<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span> + S<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    S<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># generate D</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>k <span style="color: #66cc66;">&lt;</span> numrows<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> nu<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> t + D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    t <span style="color: #66cc66;">=</span> -t / D<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + t * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    D<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># SVD</span>
    pp <span style="color: #66cc66;">=</span> p - <span style="color: #ff4500;">1</span>
    itr <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    eps <span style="color: #66cc66;">=</span> euler ** <span style="color: black;">&#40;</span>-<span style="color: #ff4500;">64</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> p <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>p - <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> k <span style="color: #66cc66;">==</span> -<span style="color: #ff4500;">1</span>:
    <span style="color: #ff7700;font-weight:bold;">break</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> eps * <span style="color: black;">&#40;</span><span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> + <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">break</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> k <span style="color: #66cc66;">==</span> <span style="color: black;">&#40;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>:
    caso <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">4</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> ks <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>p - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> k - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> ks <span style="color: #66cc66;">==</span> k:
    <span style="color: #ff7700;font-weight:bold;">break</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> ks <span style="color: #66cc66;">!=</span> p:
    t1 <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>ks<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    t1 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> ks <span style="color: #66cc66;">!=</span> <span style="color: black;">&#40;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    t2 <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>ks - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    t2 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    t <span style="color: #66cc66;">=</span> t1 + t2
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>ks<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;=</span> eps * t:
    V<span style="color: black;">&#91;</span>ks<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">break</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> ks <span style="color: #66cc66;">==</span> k:
    caso <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">3</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> ks <span style="color: #66cc66;">==</span> <span style="color: black;">&#40;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    caso <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    caso <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span>
    k <span style="color: #66cc66;">=</span> ks
    k +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> caso <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span>:
    f <span style="color: #66cc66;">=</span> e<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>p - <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> k - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> hypot<span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> f<span style="color: black;">&#41;</span>
    cs <span style="color: #66cc66;">=</span> V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> / t
    sn <span style="color: #66cc66;">=</span> f / t
    V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    <span style="color: #ff7700;font-weight:bold;">if</span> j <span style="color: #66cc66;">!=</span> k:
    f <span style="color: #66cc66;">=</span> -sn * e<span style="color: black;">&#91;</span>j - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>j - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> cs * e<span style="color: black;">&#91;</span>j - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> cs * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + sn * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -sn * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + cs * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    <span style="color: #ff7700;font-weight:bold;">elif</span> caso <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">2</span>:
    f <span style="color: #66cc66;">=</span> e<span style="color: black;">&#91;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> p<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> hypot<span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> f<span style="color: black;">&#41;</span>
    cs <span style="color: #66cc66;">=</span> V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> / t
    sn <span style="color: #66cc66;">=</span> f / t
    V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    f <span style="color: #66cc66;">=</span> -sn * e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> cs * e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> cs * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + sn * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -sn * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + cs * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    <span style="color: #ff7700;font-weight:bold;">elif</span> caso <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">3</span>:
    <span style="color: #808080; font-style: italic;"># qr-elimination</span>
    s <span style="color: #66cc66;">=</span> <span style="color: #008000;">max</span><span style="color: black;">&#40;</span><span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>e<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    s <span style="color: #66cc66;">=</span> <span style="color: #008000;">max</span><span style="color: black;">&#40;</span>s<span style="color: #66cc66;">,</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    memv <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> V<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> e<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>sp<span style="color: #66cc66;">,</span> spm1<span style="color: #66cc66;">,</span> epm1<span style="color: #66cc66;">,</span> sk<span style="color: #66cc66;">,</span> ek<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">lambda</span> x: x / s<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> memv<span style="color: black;">&#41;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>spm1 + sp<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>spm1 - sp<span style="color: black;">&#41;</span> + epm1 * epm1<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    c <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>sp * epm1<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>sp * epm1<span style="color: black;">&#41;</span>
    shift <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>b <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> <span style="color: black;">&#40;</span>c <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>:
    shift <span style="color: #66cc66;">=</span> hypot<span style="color: black;">&#40;</span>b<span style="color: #66cc66;">,</span> c<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> b <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0.0</span>:
    shift <span style="color: #66cc66;">=</span> -shift
    shift <span style="color: #66cc66;">=</span> c / <span style="color: black;">&#40;</span>b + shift<span style="color: black;">&#41;</span>
    f <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>sk + sp<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>sk - sp<span style="color: black;">&#41;</span> + shift
    g <span style="color: #66cc66;">=</span> sk * ek
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>k<span style="color: #66cc66;">,</span> p - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> hypot<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> g<span style="color: black;">&#41;</span>
    cs <span style="color: #66cc66;">=</span> f / t
    sn <span style="color: #66cc66;">=</span> g / t
    <span style="color: #ff7700;font-weight:bold;">if</span> j <span style="color: #66cc66;">!=</span> k:
    e<span style="color: black;">&#91;</span>j - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    f <span style="color: #66cc66;">=</span> cs * V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + sn * e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> cs * e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> - sn * V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    g <span style="color: #66cc66;">=</span> sn * V<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    V<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> cs * V<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> cs * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + sn * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -sn * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + cs * D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    t <span style="color: #66cc66;">=</span> hypot<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> g<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>cs<span style="color: #66cc66;">,</span> sn<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>f / t<span style="color: #66cc66;">,</span> g / t<span style="color: black;">&#41;</span>
    V<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    f <span style="color: #66cc66;">=</span> cs * e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + sn * V<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    V<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -sn * e<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + cs * V<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    g <span style="color: #66cc66;">=</span> sn * e<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> cs * e<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>j <span style="color: #66cc66;">&lt;</span> m - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    t <span style="color: #66cc66;">=</span> cs * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + sn * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -sn * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + cs * S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> t
    e<span style="color: black;">&#91;</span>p - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> f
    itr <span style="color: #66cc66;">=</span> itr + <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> caso <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&lt;=</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0.0</span>:
    V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>pp + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> -D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    <span style="color: #808080; font-style: italic;"># sort values</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: black;">&#40;</span>k <span style="color: #66cc66;">&lt;</span> pp<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&lt;</span> V<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> V<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>V<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> V<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> k <span style="color: #66cc66;">&lt;</span> n - <span style="color: #ff4500;">1</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> k <span style="color: #66cc66;">&lt;</span> m - <span style="color: #ff4500;">1</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    k +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    itr <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    p -<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>S<span style="color: #66cc66;">,</span> V<span style="color: #66cc66;">,</span> D<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def SVD(arg):
    &quot;&quot;&quot;
    Return the (S,V,D) from Singular Values Decomposition.
    
    SVD(A)
    
    INPUT:
    * A: matrix to decompose
    
    return: the tuple (S,V,D)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    OBS: This is a implementation of a Modified Golub-Reinsch SVD and
    the code is adapted from the NIST Template Numerical Toolkit (TNT)
    by Roldan Pozo. see: http://math.nist.gov/tnt/
    
    Aug 2010
    &quot;&quot;&quot;
    A = deepcopy(arg)
    (m, n) = (len(A), len(A[0]))
    nu = min(m, n)
    (numcols, numrows) = (min(m - 1, n), max(0, min(n - 2, m)))
    S = [[0.0 for i in xrange(nu)] for j in xrange(m)]  # singular values
    V = [0.0 for i in xrange(min(m + 1, n))]
    D = [[0.0 for i in xrange(n)] for j in xrange(n)]
    e = [0.0 for i in xrange(n)]
    sigma = [0.0 for i in xrange(m)]
    
    # Diagonalize the original matrix in superdiagonal V
    for k in xrange(max(numcols, numrows)):
    km_range = xrange(k, m)
    kp1_range = xrange(k + 1, n)
    if k &lt; numcols:
    # Compute the 2-norm of k-th column for S
    V[k] = 0.0
    for i in km_range:
    V[k] = hypot(V[k], A[i][k])
    if V[k] != 0.0:
    if A[k][k] &lt; 0.0:
    V[k] = -V[k]
    for i in km_range:
    A[i][k] = A[i][k] / V[k]
    A[k][k] = A[k][k] + 1.0
    V[k] = -V[k]
    for j in kp1_range:
    if (k &lt; numcols) and (V[k] != 0.0):
    t = 0.0
    for i in km_range:
    t = t + A[i][k] * A[i][j]
    t = -t / A[k][k]
    for i in km_range:
    A[i][j] = A[i][j] + t * A[i][k]
    e[j] = A[k][j]
    if k &lt; numcols:
    for i in km_range:
    S[i][k] = A[i][k]
    
    if k &lt; numrows:
    # Compute the 2-norm of k-th column for D
    e[k] = 0.0
    for i in kp1_range:
    e[k] = hypot(e[k], e[i])
    if e[k] != 0.0:
    if e[k + 1] &lt; 0.0:
    e[k] = -e[k]
    for i in kp1_range:
    e[i] = e[i] / e[k]
    e[k + 1] = e[k + 1] + 1.0
    e[k] = -e[k]
    if (k + 1 &lt; m) and (e[k] != 0.0):
    for i in xrange(k + 1, m):
    sigma[i] = 0.0
    for j in kp1_range:
    for i in xrange(k + 1, m):
    sigma[i] = sigma[i] + e[j] * A[i][j]
    for j in kp1_range:
    t = -e[j] / e[k + 1]
    for i in xrange(k + 1, m):
    A[i][j] = A[i][j] + t * sigma[i]
    for i in kp1_range:
    D[i][k] = e[i]
    
    # setup bidiagonal matrix
    p = min(n, m + 1)
    if numcols &lt; n:
    V[numcols] = A[numcols][numcols]
    if m &lt; p:
    V[p - 1] = 0.0
    if (numrows + 1) &lt; p:
    e[numrows] = A[numrows][p - 1]
    e[p - 1] = 0.0
    
    # generate S
    for j in xrange(numcols, nu):
    for i in xrange(m):
    S[i][j] = 0.0
    S[j][j] = 1.0
    for k in xrange(numcols - 1, -1, -1):
    if V[k] != 0.0:
    for j in xrange(k + 1, nu):
    t = 0.0
    for i in xrange(k, m):
    t = t + S[i][k] * S[i][j]
    t = -t / S[k][k]
    for i in xrange(k, m):
    S[i][j] = S[i][j] + t * S[i][k]
    for i in xrange(k, m):
    S[i][k] = -S[i][k]
    S[k][k] = 1.0 + S[k][k]
    for i in xrange(k - 1):
    S[i][k] = 0.0
    else:
    for i in xrange(m):
    S[i][k] = 0.0
    S[k][k] = 1.0
    
    # generate D
    for k in xrange(n - 1, -1, -1):
    if (k &lt; numrows) and (e[k] != 0.0):
    for j in xrange(k + 1, nu):
    t = 0.0
    for i in xrange(k + 1, n):
    t = t + D[i][k] * D[i][j]
    t = -t / D[k + 1][k]
    for i in xrange(k + 1, n):
    D[i][j] = D[i][j] + t * D[i][k]
    for i in xrange(n):
    D[i][k] = 0.0
    D[k][k] = 1.0
    
    # SVD
    pp = p - 1
    itr = 0
    eps = euler ** (-64)
    while p &gt; 0.0:
    for k in xrange(p - 2, -2, -1):
    if k == -1:
    break
    if abs(e[k]) &lt; = eps * (abs(V[k]) + abs(V[k + 1])):
    e[k] = 0.0
    break
    if k == (p - 2):
    caso = 4
    else:
    for ks in xrange(p - 1, k - 1, -1):
    if ks == k:
    break
    if ks != p:
    t1 = abs(e[ks])
    else:
    t1 = 0.0
    if ks != (k + 1):
    t2 = abs(e[ks - 1])
    else:
    t2 = 0.0
    t = t1 + t2
    if abs(V[ks]) &lt;= eps * t:
    V[ks] = 0.0
    break
    if ks == k:
    caso = 3
    elif ks == (p - 1):
    caso = 1
    else:
    caso = 2
    k = ks
    k += 1
    
    if caso == 1:
    f = e[p - 2]
    e[p - 2] = 0.0
    for j in xrange(p - 2, k - 1, -1):
    t = hypot(V[j], f)
    cs = V[j] / t
    sn = f / t
    V[j] = t
    if j != k:
    f = -sn * e[j - 1]
    e[j - 1] = cs * e[j - 1]
    for i in xrange(n):
    t = cs * D[i][j] + sn * D[i][p - 1]
    D[i][p - 1] = -sn * D[i][j] + cs * D[i][p - 1]
    D[i][j] = t
    elif caso == 2:
    f = e[k - 1]
    e[k - 1] = 0.0
    for j in xrange(k, p):
    t = hypot(V[j], f)
    cs = V[j] / t
    sn = f / t
    V[j] = t
    f = -sn * e[j]
    e[j] = cs * e[j]
    for i in xrange(m):
    t = cs * S[i][j] + sn * S[i][k - 1]
    S[i][k - 1] = -sn * S[i][j] + cs * S[i][k - 1]
    S[i][j] = t
    elif caso == 3:
    # qr-elimination
    s = max(abs(V[k]), abs(e[k]), abs(e[p - 2]))
    s = max(s, abs(V[p - 2]), abs(V[p - 1]))
    memv = (V[p - 1], V[p - 2], e[p - 2], V[k], e[k])
    (sp, spm1, epm1, sk, ek) = map((lambda x: x / s), memv)
    b = ((spm1 + sp) * (spm1 - sp) + epm1 * epm1) / 2.0
    c = (sp * epm1) * (sp * epm1)
    shift = 0.0
    if (b != 0.0) or (c != 0.0):
    shift = hypot(b, c)
    if b &lt; 0.0:
    shift = -shift
    shift = c / (b + shift)
    f = (sk + sp) * (sk - sp) + shift
    g = sk * ek
    for j in xrange(k, p - 1):
    t = hypot(f, g)
    cs = f / t
    sn = g / t
    if j != k:
    e[j - 1] = t
    f = cs * V[j] + sn * e[j]
    e[j] = cs * e[j] - sn * V[j]
    g = sn * V[j + 1]
    V[j + 1] = cs * V[j + 1]
    for i in xrange(n):
    t = cs * D[i][j] + sn * D[i][j + 1]
    D[i][j + 1] = -sn * D[i][j] + cs * D[i][j + 1]
    D[i][j] = t
    t = hypot(f, g)
    (cs, sn) = (f / t, g / t)
    V[j] = t
    f = cs * e[j] + sn * V[j + 1]
    V[j + 1] = -sn * e[j] + cs * V[j + 1]
    g = sn * e[j + 1]
    e[j + 1] = cs * e[j + 1]
    if (j &lt; m - 1):
    for i in xrange(m):
    t = cs * S[i][j] + sn * S[i][j + 1]
    S[i][j + 1] = -sn * S[i][j] + cs * S[i][j + 1]
    S[i][j] = t
    e[p - 2] = f
    itr = itr + 1
    elif caso == 4:
    if V[k] &lt;= 0.0:
    if V[k] &lt; 0.0:
    V[k] = -V[k]
    else:
    V[k] = 0.0
    for i in xrange(pp + 1):
    D[i][k] = -D[i][k]
    # sort values
    while (k &lt; pp) and (V[k] &lt; V[k + 1]):
    (V[k], V[k + 1]) = (V[k + 1], V[k])
    if k &lt; n - 1:
    for i in xrange(n):
    (D[i][k], D[i][k + 1]) = (D[i][k + 1], D[i][k])
    if k &lt; m - 1:
    for i in xrange(m):
    (S[i][k], S[i][k + 1]) = (S[i][k + 1], S[i][k])
    k += 1
    itr = 0
    p -= 1
    return (S, V, D)</p></div>
    ;i:2;s:13658:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> solveSVD<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    solveSVD(A, b)
    &nbsp;
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    &nbsp;
    return: a list with unknown vector 'x' of system A*x = b.
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Aug 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> transpose<span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Computes the transpose matrix of M.
    &nbsp;
    Return: M^T.
    &quot;&quot;&quot;</span>
    m <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>M<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    p <span style="color: #66cc66;">=</span> product<span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>
    MT <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> n<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> m<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> p:
    MT<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> MT
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> matmul<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> B<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Perform a matrix multiplication for two square matrices.
    &quot;&quot;&quot;</span>
    m <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>B<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #008000;">list</span>:
    C <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    C<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> C<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * B<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    C <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    C<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> C<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> + A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * B<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> C
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> singular_threshold<span style="color: black;">&#40;</span>S<span style="color: black;">&#41;</span>:
    m <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>S<span style="color: black;">&#41;</span>
    C <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    C<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span> / S<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> C
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> solve<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>u<span style="color: #66cc66;">,</span> s<span style="color: #66cc66;">,</span> v<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> SVD<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    l <span style="color: #66cc66;">=</span> singular_threshold<span style="color: black;">&#40;</span>s<span style="color: black;">&#41;</span>
    x1 <span style="color: #66cc66;">=</span> matmul<span style="color: black;">&#40;</span>v<span style="color: #66cc66;">,</span> l<span style="color: black;">&#41;</span>
    x2 <span style="color: #66cc66;">=</span> matmul<span style="color: black;">&#40;</span>transpose<span style="color: black;">&#40;</span>u<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> matmul<span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> x2<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Function's body</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> solve<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def solveSVD(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    solveSVD(A, b)
    
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    
    return: a list with unknown vector 'x' of system A*x = b.
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Aug 2010
    &quot;&quot;&quot;
    
    def transpose(M):
    &quot;&quot;&quot; Computes the transpose matrix of M.
    
    Return: M^T.
    &quot;&quot;&quot;
    m = xrange(len(M))
    n = xrange(len(M[0]))
    p = product(m, n)
    MT = [[0.0 for i in n] for j in m]
    for i in p:
    MT[i[0]][i[1]] = M[i[1]][i[0]]
    return MT
    
    def matmul(A, B):
    &quot;&quot;&quot; Perform a matrix multiplication for two square matrices.
    &quot;&quot;&quot;
    m = len(A)
    if type(B[0]) == list:
    C = [[0.0 for i in xrange(m)] for j in xrange(m)]
    for i in xrange(m):
    for j in xrange(m):
    for k in xrange(m):
    C[i][j] = C[i][j] + A[i][k] * B[k][j]
    else:
    C = [0.0 for i in xrange(m)]
    for i in xrange(m):
    for j in xrange(m):
    C[i] = C[i] + A[i][j] * B[j]
    return C
    
    def singular_threshold(S):
    m = len(S)
    C = [[0.0 for i in xrange(m)] for j in xrange(m)]
    for i in xrange(m):
    C[i][i] = 1.0 / S[i]
    return C
    
    def solve(A, b):
    (u, s, v) = SVD(A)
    l = singular_threshold(s)
    x1 = matmul(v, l)
    x2 = matmul(transpose(u), b)
    x = matmul(x1, x2)
    return x
    
    # Function's body
    return solve(A, b)</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Fatoração em Valores Singulares 

Toda matriz pode ser decomposta como sendo um produto de três matrizes de propriedades específicas. Quando a matriz a ser decomposta $$A \in \mathbf{R}^{m \times n} $$ com $$m \leq n $$ (ou seja, mais linhas que colunas), a decomposição em valores singulares possui a forma
  

    


<center>
  <br /> $$ A = U ~<br /> \left[ \begin{array}{c}<br /> S \\<br /> 0<br /> \end{array} \right]<br /> ~ V^{T} $$<br />
</center>


  

    
onde $$U $$ e $$V $$ são matrizes ortogonais de dimensão $$m \times m $$ e $$n \times n $$ , respectivamente, e $$S $$ é uma matriz diagonal de ordem $$n \times n $$ com elementos $$\sigma_i $$ , $$i = 1, 2, \ldots, n $$ , que satisfaz
  

    


<center>
  <br /> $$<br /> \sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_n \geq 0<br /> $$<br />
</center>



  


Os valores $$\sigma_i \in diag(S) $$ são chamados de _valores singulares_ da matriz $$A $$ . Podemos definir a seguinte condição para a matriz não-singular $$A $$
  

    


<center>
  <br /> $$ \kappa(A) = \|A\|~\|A^{-1}\| $$<br />
</center>


    
como sendo $$\frac{\sigma\_1}{\sigma\_n} $$.

Quando $$m \leq n $$ , isto é, quando o número de colunas é menor ou igual ao número de colunas, a decomposição terá a forma
    


<center>
  <br /> $$<br /> A = U ~ \left[ ~ S ~ ~ ~ 0 ~\right] ~ V^{T}<br /> $$<br />
</center>


    
onde, novamente, $$U $$ e $$V $$ são ortogonais e terão dimensões $$m \ times m $$ e $$n \times n $$ , respectivamente. $$S $$ agora será uma matriz singular $$m \times m $$ com a diagonal não-negativa, com elementos
    


<center>
  <br /> $$<br /> \sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_m \geq 0<br /> $$<br />
</center>

Para $$A $$ simétrica, com $$n $$ autovalores reais $$\lambda\_1, \lambda\_2, \ldots, \lambda\_n $$ , e seus autovetores associados $$q\_1, q\_2, \ldots, q\_n $$ , podemos usar a _decomposição espectral_ de $$A $$ :
    


<center>
  <br /> $$<br /> A = \sum_{i = 1}^{n} \lambda_i q_i q_i^T<br /> $$<br />
</center>


    
Assim, a decomposição pode ser reescrita, definindo-se
    


<center>
  <br /> $$<br /> \Lambda = diag(\lambda_1, \lambda_2, \ldots, \lambda_n)<br /> $$<br />
</center>


    

    


<center>
  <br /> $$<br /> Q = \left[ \begin{array}{c}<br /> q_1 \\<br /> q_2 \\<br /> \cdots \\<br /> q_n<br /> \end{array} \right]<br /> $$<br />
</center>


    
e reescrevendo $$A $$ como
    


<center>
  <br /> $$<br /> A = Q ~ \Lambda ~ Q^T<br /> $$<br />
</center>

Esta decomposição é idêntica à SVD quando definimos $$U = V = Q $$ e $$S = \Lambda $$ . Note que os valores singulares $$\sigma\_i $$ e os autovalores $$\lambda\_i $$ coincidem neste caso. 

No caso da norma euclidiana para matrizes
    


<center>
  <br /> $$<br /> \|A\|_2 = ~\text{maior autovalor de } \sqrt{\left( A^T ~ A \right)}<br /> $$<br />
</center>


    
temos que
    


<center>
  <br /> $$<br /> \|A\| = \sigma_1(A) = \text{ maior autovalor de } A<br /> $$<br />
</center>


    


<center>
  <br /> $$<br /> \|A^{-1}\| = \sigma_n(A) = \text{ inverso do menor autovalor de } A<br /> $$<br />
</center>


    
desta forma, temos que para todo $$x \in \mathbf{R}^n $$,
    


<center>
  <br /> $$<br /> \sigma_n(A)~\|x\|^2 = \dfrac{\|x\|^2}{A^{-1} \leq x^T ~ Ax \leq<br /> \|A\| ~ \|x\|^2 = \sigma_1(A) ~ \|x\|^2<br /> $$<br />
</center>

Para a matriz ortogonal $$Q $$ , temos que a norma euclidiana
    


<center>
  <br /> $$<br /> \|Qx\| = \|x\|<br /> $$<br />
</center>


    
e que todos os valores singulares desta matriz será igual à 1. 

&nbsp; 

### 1.1. Matriz pseudo-inversa de Moore </p> 

Decompondo a matriz A em três matrizes $$U $$ , $$S $$ e $$V $$
    


<center>
  <br /> $$<br /> A = U \times S \times V<br /> $$<br />
</center>


    
podemos encontrar a inversa de $$A $$ com SVD através da seguinte formula
    


<center>
  <br /> $$<br /> A^{-1} = (U ~ S ~ V)^{-1} = V^{-1} ~ S^{-1} ~ U^{-1} = V^T ~ S^{-1} ~ U^T<br /> $$<br />
</center>


    
onde $$L = \frac{1}{S} \rightarrow L\_i = \frac{1}{S\_i} $$ , $$U^{-1} = U^T $$ e $$V^{-1} = V^T $$ . Desta forma, podemos obter facilmente a matriz inversa de $$A $$ via SVD.

&nbsp; 

### 1.2. Resolvendo sistemas lineares com SVD </p> 

Para resolver um sistema linear, basta multiplicarmos a matriz inversa com o vetor de elementos independentes. Isto é, para o sistema linear
    


<center>
  <br /> $$<br /> AX = B<br /> $$<br />
</center>


    
temos que
    


<center>
  <br /> $$<br /> X = A^{-1} B<br /> $$<br />
</center>


    
onde $$A^{-1} $$ obtemos via SVD. Assim, o vetor das soluções é
    


<center>
  <br /> $$<br /> X = V L U^T B<br /> $$<br />
</center></p> 

&nbsp; 

## 2. Implementação 

Existem diversos algoritmos para computação das matrizes decompostas e o vetor de valores singulares. A seguir, apresentamos o código de uma implementação simples e eficiente da fatoração em valores singulares. 

<div>
  <pre lang="python">
def SVD(arg):
    """
    Return the (S,V,D) from Singular Values Decomposition.

    SVD(A)

    INPUT:
    * A: matrix to decompose

    return: the tuple (S,V,D)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    OBS: This is a implementation of a Modified Golub-Reinsch SVD and
         the code is adapted from the NIST Template Numerical Toolkit (TNT)
         by Roldan Pozo. see: http://math.nist.gov/tnt/

    Aug 2010
    """
    A = deepcopy(arg)
    (m, n) = (len(A), len(A[0]))
    nu = min(m, n)
    (numcols, numrows) = (min(m - 1, n), max(0, min(n - 2, m)))
    S = [[0.0 for i in xrange(nu)] for j in xrange(m)]  # singular values
    V = [0.0 for i in xrange(min(m + 1, n))]
    D = [[0.0 for i in xrange(n)] for j in xrange(n)]
    e = [0.0 for i in xrange(n)]
    sigma = [0.0 for i in xrange(m)]

    # Diagonalize the original matrix in superdiagonal V
    for k in xrange(max(numcols, numrows)):
        km_range = xrange(k, m)
        kp1_range = xrange(k + 1, n)
        if k &lt; numcols:
            # Compute the 2-norm of k-th column for S
            V[k] = 0.0
            for i in km_range:
                V[k] = hypot(V[k], A[i][k])
            if V[k] != 0.0:
                if A[k][k] &lt; 0.0:
                    V[k] = -V[k]
                for i in km_range:
                    A[i][k] = A[i][k] / V[k]
                A[k][k] = A[k][k] + 1.0
            V[k] = -V[k]
        for j in kp1_range:
            if (k &lt; numcols) and (V[k] != 0.0):
                t = 0.0
                for i in km_range:
                    t = t + A[i][k] * A[i][j]
                t = -t / A[k][k]
                for i in km_range:
                    A[i][j] = A[i][j] + t * A[i][k]
                e[j] = A[k][j]
        if k &lt; numcols:
            for i in km_range:
                S[i][k] = A[i][k]

        if k &lt; numrows:
            # Compute the 2-norm of k-th column for D
            e[k] = 0.0
            for i in kp1_range:
                e[k] = hypot(e[k], e[i])
            if e[k] != 0.0:
                if e[k + 1] &lt; 0.0:
                    e[k] = -e[k]
                for i in kp1_range:
                    e[i] = e[i] / e[k]
                e[k + 1] = e[k + 1] + 1.0
            e[k] = -e[k]
            if (k + 1 &lt; m) and (e[k] != 0.0):
                for i in xrange(k + 1, m):
                    sigma[i] = 0.0
                for j in kp1_range:
                    for i in xrange(k + 1, m):
                        sigma[i] = sigma[i] + e[j] * A[i][j]
                for j in kp1_range:
                    t = -e[j] / e[k + 1]
                    for i in xrange(k + 1, m):
                        A[i][j] = A[i][j] + t * sigma[i]
            for i in kp1_range:
                D[i][k] = e[i]

    # setup bidiagonal matrix
    p = min(n, m + 1)
    if numcols &lt; n:
        V[numcols] = A[numcols][numcols]
    if m &lt; p:
        V[p - 1] = 0.0
    if (numrows + 1) &lt; p:
        e[numrows] = A[numrows][p - 1]
    e[p - 1] = 0.0

    # generate S
    for j in xrange(numcols, nu):
        for i in xrange(m):
            S[i][j] = 0.0
        S[j][j] = 1.0
    for k in xrange(numcols - 1, -1, -1):
        if V[k] != 0.0:
            for j in xrange(k + 1, nu):
                t = 0.0
                for i in xrange(k, m):
                    t = t + S[i][k] * S[i][j]
                t = -t / S[k][k]
                for i in xrange(k, m):
                    S[i][j] = S[i][j] + t * S[i][k]
            for i in xrange(k, m):
                S[i][k] = -S[i][k]
            S[k][k] = 1.0 + S[k][k]
            for i in xrange(k - 1):
                S[i][k] = 0.0
        else:
            for i in xrange(m):
                S[i][k] = 0.0
            S[k][k] = 1.0

    # generate D
    for k in xrange(n - 1, -1, -1):
        if (k &lt; numrows) and (e[k] != 0.0):
            for j in xrange(k + 1, nu):
                t = 0.0
                for i in xrange(k + 1, n):
                    t = t + D[i][k] * D[i][j]
                t = -t / D[k + 1][k]
                for i in xrange(k + 1, n):
                    D[i][j] = D[i][j] + t * D[i][k]
        for i in xrange(n):
            D[i][k] = 0.0
        D[k][k] = 1.0

    # SVD
    pp = p - 1
    itr = 0
    eps = euler ** (-64)
    while p > 0.0:
        for k in xrange(p - 2, -2, -1):
            if k == -1:
                break
            if abs(e[k]) &lt; = eps * (abs(V[k]) + abs(V[k + 1])):
                e[k] = 0.0
                break
        if k == (p - 2):
            caso = 4
        else:
            for ks in xrange(p - 1, k - 1, -1):
                if ks == k:
                    break
                if ks != p:
                    t1 = abs(e[ks])
                else:
                    t1 = 0.0
                if ks != (k + 1):
                    t2 = abs(e[ks - 1])
                else:
                    t2 = 0.0
                t = t1 + t2
                if abs(V[ks]) &lt;= eps * t:
                    V[ks] = 0.0
                    break
            if ks == k:
                caso = 3
            elif ks == (p - 1):
                caso = 1
            else:
                caso = 2
                k = ks
        k += 1

        if caso == 1:
            f = e[p - 2]
            e[p - 2] = 0.0
            for j in xrange(p - 2, k - 1, -1):
                t = hypot(V[j], f)
                cs = V[j] / t
                sn = f / t
                V[j] = t
                if j != k:
                    f = -sn * e[j - 1]
                    e[j - 1] = cs * e[j - 1]
                for i in xrange(n):
                    t = cs * D[i][j] + sn * D[i][p - 1]
                    D[i][p - 1] = -sn * D[i][j] + cs * D[i][p - 1]
                    D[i][j] = t
        elif caso == 2:
            f = e[k - 1]
            e[k - 1] = 0.0
            for j in xrange(k, p):
                t = hypot(V[j], f)
                cs = V[j] / t
                sn = f / t
                V[j] = t
                f = -sn * e[j]
                e[j] = cs * e[j]
                for i in xrange(m):
                    t = cs * S[i][j] + sn * S[i][k - 1]
                    S[i][k - 1] = -sn * S[i][j] + cs * S[i][k - 1]
                    S[i][j] = t
        elif caso == 3:
            # qr-elimination
            s = max(abs(V[k]), abs(e[k]), abs(e[p - 2]))
            s = max(s, abs(V[p - 2]), abs(V[p - 1]))
            memv = (V[p - 1], V[p - 2], e[p - 2], V[k], e[k])
            (sp, spm1, epm1, sk, ek) = map((lambda x: x / s), memv)
            b = ((spm1 + sp) * (spm1 - sp) + epm1 * epm1) / 2.0
            c = (sp * epm1) * (sp * epm1)
            shift = 0.0
            if (b != 0.0) or (c != 0.0):
                shift = hypot(b, c)
                if b &lt; 0.0:
                    shift = -shift
                shift = c / (b + shift)
            f = (sk + sp) * (sk - sp) + shift
            g = sk * ek
            for j in xrange(k, p - 1):
                t = hypot(f, g)
                cs = f / t
                sn = g / t
                if j != k:
                    e[j - 1] = t
                f = cs * V[j] + sn * e[j]
                e[j] = cs * e[j] - sn * V[j]
                g = sn * V[j + 1]
                V[j + 1] = cs * V[j + 1]
                for i in xrange(n):
                    t = cs * D[i][j] + sn * D[i][j + 1]
                    D[i][j + 1] = -sn * D[i][j] + cs * D[i][j + 1]
                    D[i][j] = t
                t = hypot(f, g)
                (cs, sn) = (f / t, g / t)
                V[j] = t
                f = cs * e[j] + sn * V[j + 1]
                V[j + 1] = -sn * e[j] + cs * V[j + 1]
                g = sn * e[j + 1]
                e[j + 1] = cs * e[j + 1]
                if (j &lt; m - 1):
                    for i in xrange(m):
                        t = cs * S[i][j] + sn * S[i][j + 1]
                        S[i][j + 1] = -sn * S[i][j] + cs * S[i][j + 1]
                        S[i][j] = t
            e[p - 2] = f
            itr = itr + 1
        elif caso == 4:
            if V[k] &lt;= 0.0:
                if V[k] &lt; 0.0:
                    V[k] = -V[k]
                else:
                    V[k] = 0.0
                for i in xrange(pp + 1):
                    D[i][k] = -D[i][k]
            # sort values
            while (k &lt; pp) and (V[k] &lt; V[k + 1]):
                (V[k], V[k + 1]) = (V[k + 1], V[k])
                if k &lt; n - 1:
                    for i in xrange(n):
                        (D[i][k], D[i][k + 1]) = (D[i][k + 1], D[i][k])
                if k &lt; m - 1:
                    for i in xrange(m):
                        (S[i][k], S[i][k + 1]) = (S[i][k + 1], S[i][k])
                k += 1
            itr = 0
            p -= 1
    return (S, V, D)
   </pre>
</div>

&nbsp; 

### 2.1. Utilizando a decomposição para resolver sistemas lineares </p> 

<div>
  <pre lang="python">
def solveSVD(A, b):
    """
    Return a list with the solution of linear system.

    solveSVD(A, b)

    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms

    return: a list with unknown vector 'x' of system A*x = b.

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Aug 2010
    """

    def transpose(M):
        """ Computes the transpose matrix of M.

        Return: M^T.
        """
        m = xrange(len(M))
        n = xrange(len(M[0]))
        p = product(m, n)
        MT = [[0.0 for i in n] for j in m]
        for i in p:
            MT[i[0]][i[1]] = M[i[1]][i[0]]
        return MT

    def matmul(A, B):
        """ Perform a matrix multiplication for two square matrices.
        """
        m = len(A)
        if type(B[0]) == list:
            C = [[0.0 for i in xrange(m)] for j in xrange(m)]
            for i in xrange(m):
                for j in xrange(m):
                    for k in xrange(m):
                        C[i][j] = C[i][j] + A[i][k] * B[k][j]
        else:
            C = [0.0 for i in xrange(m)]
            for i in xrange(m):
                for j in xrange(m):
                        C[i] = C[i] + A[i][j] * B[j]
        return C

    def singular_threshold(S):
        m = len(S)
        C = [[0.0 for i in xrange(m)] for j in xrange(m)]
        for i in xrange(m):
            C[i][i] = 1.0 / S[i]
        return C

    def solve(A, b):
        (u, s, v) = SVD(A)
        l = singular_threshold(s)
        x1 = matmul(v, l)
        x2 = matmul(transpose(u), b)
        x = matmul(x1, x2)
        return x

    # Function's body
    return solve(A, b)
</pre>
</div>

Estas funções estão disponíveis em <a href="http://www.sawp.com.br/code/linear/SVD.py" target="_blank">http://www.sawp.com.br/code/linear/SVD.py</a>, assim como um exemplo de como utilizá-las. </p> </p> 

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a><br /> <a name="bibitem2"><b>[2]</b> Lars Elden,<cite> <em>Numerical Linear Algebra and Applications in Data Mining</em> (Preliminary version),</cite> http://www.mai.liu.se/~ laeld/, (2005).</a>
  </p>
</fieldset>
