---
id: 704
title: '2.1.6 Sistemas Lineares &#8212; Métodos Diretos &#8212; Decomposição LDL'
date: 2010-09-06T11:09:36+00:00
author: SAWP
excerpt: ' Um aspecto da decomposição de Cholesky que insere um custo adicional na computação das matrizes decompostas está na necessidade de calcular a raiz quadrada durante a resolução do problema. Contudo, o cálculo da raiz quadrada é um processo caro, sujeito à propagações de erros maiores do que aqueles obtidos com a utilização de operações simples de ponto flutuante, tais como adição e multiplicação. Neste artigo mostraremos uma modificação na decomposição de Cholesky que elimina necessidade do cálculo da raiz quadrada, sendo mais eficiente e propagando menos erros.'
layout: post
guid: http://www.sawp.com.br/blog/?p=704
permalink: /p=704
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:27156:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> LDL<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    LDL(A, b)
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
    Sep 2010
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
    m <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>B<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #008000;">list</span>:
    C <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> m<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> m<span style="color: black;">&#93;</span>
    p <span style="color: #66cc66;">=</span> product<span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> m<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> p:
    C<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> C<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> + A<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> * B<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    C <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> m<span style="color: black;">&#93;</span>
    p <span style="color: #66cc66;">=</span> product<span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> p:
    C<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> C<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> + A<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> * B<span style="color: black;">&#91;</span>i<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> C
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> isSimetric<span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; As Cholesky factorization explore the symmetric proprierty of
    A, this function check it.
    &nbsp;
    Return: True if A is symmetric. False if not.
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> n:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> n:
    <span style="color: #ff7700;font-weight:bold;">if</span> M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> M<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">False</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">True</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> LDL_decomposition<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Perform the LDL decomposition on matriz A, returning L
    (Cholesky Factor).
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    M <span style="color: #66cc66;">=</span> deepcopy<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    L <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> n<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> n<span style="color: black;">&#93;</span>
    Lt <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> n<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> n<span style="color: black;">&#93;</span>
    D <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> n<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Calcule L and Lt</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> n:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> n:
    suma <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span>M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * M<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * D<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>j<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> - suma<span style="color: black;">&#41;</span> / D<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #808080; font-style: italic;"># Update diagonal</span>
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span>M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * D<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># L</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> n:
    L<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span>:k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span>:k<span style="color: black;">&#93;</span>
    L<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Lt is transpose of L</span>
    Lt <span style="color: #66cc66;">=</span> transpose<span style="color: black;">&#40;</span>L<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>L<span style="color: #66cc66;">,</span> D<span style="color: #66cc66;">,</span> Lt<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> solveLDL<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    rn <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> rn<span style="color: black;">&#93;</span>
    y <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> rn<span style="color: black;">&#93;</span>
    <span style="color: black;">&#40;</span>L<span style="color: #66cc66;">,</span> D<span style="color: #66cc66;">,</span> Lt<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> LDL_decomposition<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Step 1: Solve the L system: L * y = b</span>
    y<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> / L<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span>:
    suma +<span style="color: #66cc66;">=</span> L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * y<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    y<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - suma<span style="color: black;">&#41;</span> / L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Step 2: Solve the U system: U * x = y (regressive replacement)</span>
    x<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / Lt<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> y<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> suma - Lt<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> suma / Lt<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Function's body</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> isSimetric<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> solveLDL<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">False</span></pre></td></tr></table><p class="theCode" style="display:none;">def LDL(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    LDL(A, b)
    
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    
    return: a list with unknown vector 'x' of system A*x = b.
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Sep 2010
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
    m = xrange(len(A))
    if type(B[0]) == list:
    C = [[0.0 for i in m] for j in m]
    p = product(m, m, m)
    for i in p:
    C[i[0]][i[1]] = C[i[0]][i[1]] + A[i[0]][i[2]] * B[i[2]][i[1]]
    else:
    C = [0.0 for i in m]
    p = product(m, m)
    for i in p:
    C[i[0]] = C[i[0]] + A[i[0]][i[1]] * B[i[1]]
    return C
    
    def isSimetric(M):
    &quot;&quot;&quot; As Cholesky factorization explore the symmetric proprierty of
    A, this function check it.
    
    Return: True if A is symmetric. False if not.
    &quot;&quot;&quot;
    n = xrange(len(M))
    for i in n:
    for j in n:
    if M[i][j] != M[j][i]:
    return False
    return True
    
    def LDL_decomposition(A):
    &quot;&quot;&quot; Perform the LDL decomposition on matriz A, returning L
    (Cholesky Factor).
    &quot;&quot;&quot;
    n = xrange(len(A))
    M = deepcopy(A)
    L = [[0.0 for i in n] for j in n]
    Lt = [[0.0 for i in n] for j in n]
    D = [1.0 for i in n]
    
    # Calcule L and Lt
    for i in n:
    for j in n:
    suma = sum([M[i][k] * M[j][k] * D[k] for k in xrange(j)])
    M[i][j] = (A[i][j] - suma) / D[j]
    # Update diagonal
    D[i] = A[i][i] - sum([M[i][k] * M[i][k] * D[k] for k in xrange(i)])
    
    # L
    for k in n:
    L[k][0:k] = M[k][0:k]
    L[k][k] = 1.0
    
    # Lt is transpose of L
    Lt = transpose(L)
    
    return (L, D, Lt)
    
    def solveLDL(A, b):
    n = len(b)
    rn = xrange(n)
    x = [0.0 for i in rn]
    y = [0.0 for i in rn]
    (L, D, Lt) = LDL_decomposition(A)
    
    # Step 1: Solve the L system: L * y = b
    y[0] = b[0] / L[0][0]
    for i in xrange(1, n):
    suma = 0.0
    for j in xrange(i):
    suma += L[i][j] * y[j]
    y[i] = (b[i] - suma) / L[i][i]
    
    # Step 2: Solve the U system: U * x = y (regressive replacement)
    x[n - 1] = y[n - 1] / Lt[n - 1][n - 1]
    for i in xrange(n - 1, -1, -1):
    suma = y[i]
    for j in xrange(i + 1, n):
    suma = suma - Lt[i][j] * x[j]
    x[i] = suma / Lt[i][i]
    
    return x
    
    # Function's body
    if isSimetric(A):
    return solveLDL(A, b)
    else:
    return False</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. A Fatoração LDL 

A Fatoração de Cholesky expressa uma matriz simétrica $$A $$ como o produto de uma matriz triangular $$L $$ (chamada de Fator de Cholesky) pela sua transposta $$L^T $$ , na forma:
    
 <a name="eq1">(eq1)</a>

<center>
  $$ A = LL^T $$
</center>


    
onde $$L $$ será triangular superior. 

Uma vez que se identifica que uma matriz $$A $$ é hermitiana, podemos utilizar a Equação [1](#eq1) para gerar $$L $$ e $$L^T $$ a partir de $$A $$ . Ou seja, ao multiplicarmos e igualarmos seus termos, obtemos as seguintes relações:
    
<a name="eq2">(eq2)</a>

<center>
  <br /> $$ l_{ki} = \frac{ a_{ki} &#8211; \sum_{j=1}^{i-1} l_{ij}~l_{kj} }{ l_{ii} } $$<br />
</center>


    
onde $$i = 1, 2, \ldots, k-1 $$ . Além disso, o elemento da diagonal será
    
obtido por
    
<a name="eq3">(eq3)</a>

<center>
  <br /> $$ l_{kk} = \sqrt{a_{kk} &#8211; \sum_{k-1}^{j=1} l_{kj}^{2} } $$<br />
</center>

Todavia, podemos evitar o cálculo da raiz quadrada na última expressão, caso encontremos uma decomposição $$A = L D L^T $$ tal que
    


<center>
  <br /> $$ A = \left[<br /> \begin{array}{cc}<br /> \alpha & v^T \\<br /> v & C<br /> \end{array}<br /> \right] =<br /> \left[<br /> \begin{array}{cc}<br /> 1 & 0 \\<br /> \frac{v}{\alpha} & I<br /> \end{array}<br /> \right]<br /> \left[<br /> \begin{array}{cc}<br /> \alpha & 0 \\<br /> 0 & C &#8211; \frac{v v^T}{\alpha}<br /> \end{array}<br /> \right]<br /> \left[<br /> \begin{array}{cc}<br /> 1 & \frac{v^T}{\alpha} \\<br /> 0 & I<br /> \end{array}<br /> \right] $$<br />
</center>


    
Por exemplo, a expressão acima para um problema $$3 \times 3 $$
    

    


<center>
  $$\tiny A = \left[<br /> \begin{array}{ccc}<br /> 1 & 0 & 0 \\<br /> L_{21} & 1 & 0 \\<br /> L_{31} & L_{32} & 1<br /> \end{array}<br /> \right]<br /> \left[<br /> \begin{array}{ccc}<br /> D_1 & 0 & 0 \\<br /> 0 & D_2 & 0 \\<br /> 0 & 0 & D_3<br /> \end{array}<br /> \right]<br /> \left[<br /> \begin{array}{ccc}<br /> 1 & L_{21} & L_{31}\\<br /> 0 & 1 & L_{32} \\<br /> 0 & 0 & 1<br /> \end{array}<br /> \right] =<br /> \left[<br /> \begin{array}{ccc}<br /> D_1 & ~ & ~ \\<br /> L_{21} D_1 & L_{21}^{2}D_1 + D_2 & ~ \\<br /> L_{31} D_1 & L_{31} L_{21} D_1 + L_{32} D_2 & L_{31}^2 D_1 + L_{32}^{2} D_2 + D_3<br /> \end{array}<br /> \right] $$<br />
</center>

Portanto, podemos fazer a decomposição de Cholesky sem a necessidade da raiz quadrada através das relações
    


<center>
  <br /> $$ l_{ij} = \dfrac{\left( a_{ij} &#8211; \sum_{k=1}^{j-1} l_{ik} l_{jk} d_k \right)}{d_j} $$<br />
</center>


    
e
    


<center>
  <br /> $$ d_i = a_{ii} &#8211; \sum_{k=1}^{i-1} l_{ik}^2 d_k $$<br />
</center>


    
A partir destas funções, teremos as matrizes decompostas $$L = L $$ e $$U = L^T $$, que podem ser resolvidas por substituição regressiva os demais passos utilizados para resolução via decomposições LU. 

&nbsp;

## 2. Implementação 

<div>
  <pre lang="python">def LDL(A, b):
    """
    Return a list with the solution of linear system.

    LDL(A, b)

    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms

    return: a list with unknown vector 'x' of system A*x = b.

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Sep 2010
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
        m = xrange(len(A))
        if type(B[0]) == list:
            C = [[0.0 for i in m] for j in m]
            p = product(m, m, m)
            for i in p:
                C[i[0]][i[1]] = C[i[0]][i[1]] + A[i[0]][i[2]] * B[i[2]][i[1]]
        else:
            C = [0.0 for i in m]
            p = product(m, m)
            for i in p:
                C[i[0]] = C[i[0]] + A[i[0]][i[1]] * B[i[1]]
        return C

    def isSimetric(M):
        """ As Cholesky factorization explore the symmetric proprierty of
        A, this function check it.

        Return: True if A is symmetric. False if not.
        """
        n = xrange(len(M))
        for i in n:
            for j in n:
                if M[i][j] != M[j][i]:
                    return False
        return True

    def LDL_decomposition(A):
        """ Perform the LDL decomposition on matriz A, returning L
        (Cholesky Factor).
        """
        n = xrange(len(A))
        M = deepcopy(A)
        L = [[0.0 for i in n] for j in n]
        Lt = [[0.0 for i in n] for j in n]
        D = [1.0 for i in n]

        # Calcule L and Lt
        for i in n:
            for j in n:
                suma = sum([M[i][k] * M[j][k] * D[k] for k in xrange(j)])
                M[i][j] = (A[i][j] - suma) / D[j]
            # Update diagonal
            D[i] = A[i][i] - sum([M[i][k] * M[i][k] * D[k] for k in xrange(i)])

        # L
        for k in n:
            L[k][0:k] = M[k][0:k]
            L[k][k] = 1.0

        # Lt is transpose of L
        Lt = transpose(L)

        return (L, D, Lt)

    def solveLDL(A, b):
        n = len(b)
        rn = xrange(n)
        x = [0.0 for i in rn]
        y = [0.0 for i in rn]
        (L, D, Lt) = LDL_decomposition(A)

       # Step 1: Solve the L system: L * y = b
        y[0] = b[0] / L[0][0]
        for i in xrange(1, n):
            suma = 0.0
            for j in xrange(i):
                suma += L[i][j] * y[j]
            y[i] = (b[i] - suma) / L[i][i]

        # Step 2: Solve the U system: U * x = y (regressive replacement)
        x[n - 1] = y[n - 1] / Lt[n - 1][n - 1]
        for i in xrange(n - 1, -1, -1):
            suma = y[i]
            for j in xrange(i + 1, n):
                suma = suma - Lt[i][j] * x[j]
            x[i] = suma / Lt[i][i]

        return x

    # Function's body
    if isSimetric(A):
        return solveLDL(A, b)
    else:
        return False </pre>
</div>

Estas funções estão disponíveis em <a href="http://www.sawp.com.br/code/linear/LDL.py" target="_blank">http://www.sawp.com.br/code/linear/LDL.py</a>, assim como um exemplo de como utilizá-las. 

&nbsp;

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



&nbsp;

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a>
  </p>
  
  <p>
    <a name="bibitem3"><b>[3]</b> </a><a href="http://en.wikipedia.org/wiki/Cholesky_decomposition#Avoiding_taking_square_roots" target="_blank">http://en.wikipedia.org/wiki/Cholesky_decomposition#Avoiding_taking_square_roots</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> Lars Elden,<cite> <em>Numerical Linear Algebra and Applications in Data Mining</em> (Preliminary version),</cite> http://www.mai.liu.se/~ laeld/, (2005).</a>
  </p>
</fieldset>
