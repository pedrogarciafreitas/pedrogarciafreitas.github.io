---
id: 689
title: '2.1.5. Sistemas Lineares &#8212; Métodos Diretos &#8212; Decomposição QR'
date: 2010-09-03T17:45:56+00:00
author: SAWP
excerpt: '    Neste post apresentaremos um método para decomposição de matrizes conhecido como Fatoração QR. Esta técnica consiste em decompor  uma matriz A como sendo um produto de uma matriz ortogonal com outra matriz  triangular. Em problemas práticos, este método é consideravelmente mais útil que outras técnicas (tais como LU ou Cholesky).'
layout: post
guid: http://www.sawp.com.br/blog/?p=689
permalink: /p=689
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:15763:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> QR<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the (Q,R) from QR Decomposition.
    &nbsp;
    QR(A)
    &nbsp;
    INPUT:
    * A: matrix to decompose
    &nbsp;
    return: the tuple (Q, R)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    OBS: This is a implementation of a QR with Householder transformation and
    the code is adapted from the NIST Template Numerical Toolkit (TNT)
    by Roldan Pozo. see: http://math.nist.gov/tnt/
    &nbsp;
    Sep 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    QR <span style="color: #66cc66;">=</span> deepcopy<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    nrange <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    mrange <span style="color: #66cc66;">=</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>
    minor <span style="color: #66cc66;">=</span> <span style="color: #008000;">min</span><span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>
    Rdiag <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> nrange<span style="color: black;">&#93;</span>
    Q <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> nrange<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> mrange<span style="color: black;">&#93;</span>
    R <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> nrange<span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> nrange<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> least <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>minor<span style="color: black;">&#41;</span>:
    norm <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>least<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    norm +<span style="color: #66cc66;">=</span> QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> * QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span>
    a <span style="color: #66cc66;">=</span> sqrt<span style="color: black;">&#40;</span>norm<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> QR<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    a <span style="color: #66cc66;">=</span> -a
    Rdiag<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> a
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> a <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    QR<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> -<span style="color: #66cc66;">=</span> a
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>least + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    phi <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>least<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    phi -<span style="color: #66cc66;">=</span> QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> * QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span>
    phi /<span style="color: #66cc66;">=</span> a * QR<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>least<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> -<span style="color: #66cc66;">=</span> phi * QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># get R</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>minor - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    R<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> Rdiag<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    R<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># get Q</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> least <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> minor - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    Q<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> least <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>minor - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    Q<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> QR<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>least<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    phi <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>least<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    phi -<span style="color: #66cc66;">=</span> Q<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> * QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span>
    phi /<span style="color: #66cc66;">=</span> Rdiag<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span> * QR<span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>least<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    Q<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> -<span style="color: #66cc66;">=</span> phi * QR<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>least<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>Q<span style="color: #66cc66;">,</span> R<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def QR(A):
    &quot;&quot;&quot;
    Return the (Q,R) from QR Decomposition.
    
    QR(A)
    
    INPUT:
    * A: matrix to decompose
    
    return: the tuple (Q, R)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    OBS: This is a implementation of a QR with Householder transformation and
    the code is adapted from the NIST Template Numerical Toolkit (TNT)
    by Roldan Pozo. see: http://math.nist.gov/tnt/
    
    Sep 2010
    &quot;&quot;&quot;
    
    (m, n) = (len(A), len(A[0]))
    QR = deepcopy(A)
    nrange = xrange(n)
    mrange = xrange(m)
    minor = min(m, n)
    Rdiag = [0.0 for i in nrange]
    Q = [[0.0 for i in nrange] for j in mrange]
    R = [[0.0 for i in nrange] for j in nrange]
    
    for least in xrange(minor):
    norm = 0.0
    for row in xrange(least, m):
    norm += QR[row][least] * QR[row][least]
    a = sqrt(norm)
    if QR[least][least] &gt; 0:
    a = -a
    Rdiag[least] = a
    
    if a != 0.0:
    QR[least][least] -= a
    for col in xrange(least + 1, n):
    phi = 0.0
    for row in xrange(least, m):
    phi -= QR[row][col] * QR[row][least]
    phi /= a * QR[least][least]
    for row in xrange(least, m):
    QR[row][col] -= phi * QR[row][least]
    
    # get R
    for row in xrange(minor - 1, -1, -1):
    R[row][row] = Rdiag[row]
    for col in xrange(row + 1, n):
    R[row][col] = QR[row][col]
    
    # get Q
    for least in xrange(m - 1, minor - 1, -1):
    Q[least][least] = 1.0
    for least in xrange(minor - 1, -1, -1):
    Q[least][least] = 1.0
    if QR[least][least] != 0.0:
    for col in xrange(least, m):
    phi = 0.0
    for row in xrange(least, m):
    phi -= Q[row][col] * QR[row][least]
    phi /= Rdiag[least] * QR[least][least]
    for row in xrange(least, m):
    Q[row][col] -= phi * QR[row][least]
    return (Q, R)</p></div>
    ;i:2;s:16591:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> solveQR<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    solveQR(A, b)
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
    <span style="color: #ff7700;font-weight:bold;">def</span> solve<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Solution by QR decomposition R x = Q^T b.
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: black;">&#40;</span>Q<span style="color: #66cc66;">,</span> R<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> QR<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># Step 1: Solve the system: y = Q^T b</span>
    y <span style="color: #66cc66;">=</span> matmul<span style="color: black;">&#40;</span>transpose<span style="color: black;">&#40;</span>Q<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># Step 2: Solve the R system: Rx = y (regressive replacement)</span>
    x<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / R<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>y<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> - R<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span>R<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">3</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">sum</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>j + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #008000;">sum</span> +<span style="color: #66cc66;">=</span> R<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>y<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> - <span style="color: #008000;">sum</span><span style="color: black;">&#41;</span> / R<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Function's body</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> solve<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def solveQR(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    solveQR(A, b)
    
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
    
    def solve(A, b):
    &quot;&quot;&quot; Solution by QR decomposition R x = Q^T b.
    &quot;&quot;&quot;
    n = len(b)
    x = [0.0 for i in xrange(n)]
    (Q, R) = QR(A)
    # Step 1: Solve the system: y = Q^T b
    y = matmul(transpose(Q), b)
    # Step 2: Solve the R system: Rx = y (regressive replacement)
    x[n - 1] = y[n - 1] / R[n - 1][n - 1]
    x[n - 2] = (y[n - 2] - R[n - 2][n - 1] * x[n - 1]) / (R[n - 2][n - 2])
    for j in xrange(n - 3, -1, -1):
    sum = 0.0
    for k in xrange(j + 1, n):
    sum += R[j][k] * x[k]
    x[j] = (y[j] - sum) / R[j][j]
    return x
    
    # Function's body
    return solve(A, b)</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Decomposição QR 

Se assumirmos que é possível decompor uma matriz real $$A $$ em um produto de matrizes $$QR $$ , onde $$Q $$ seja ortogonal e $$R $$ é uma matriz triangular-superior de diagonal não-nula, então quando $$A $$ for uma matriz não-singular, esta decomposição é única e sempre existe. 

Para obter esta decomposição, aplicamos em $$A $$ a sequência $$P_k $$ de transformações de Holseholder, garantindo que os elementos da diagonal de cada estágio (_Rdiag_) sejam não-negativos. Isto é possível, uma vez que cada transformação é determinada pela mudança de sinal. Assim, teremos que
    


<center>
  <br /> $$ P_{n-1} P_{n-2} \cdots P_{1} A = R $$<br />
</center>


    
Como cada $$P_j $$ é ortogonal, temos que $$A = Q R $$ , onde
    


<center>
  <br /> $$ Q = \left[ ~ P_{n-1} ~ P_{n-2} ~ \ldots ~ P_1 ~ \right]^T $$<br />
</center>


    
Como cada $$P\_j $$ é unicamente determinado pela condição de não-negatividade, se o elemento da diagonal $$a\_{jj}^{(j)} $$ é não-nulo quando $$P_j $$ é aplicado, então a decomposição é única para $$A $$ não-singular. 

Como o produto de matrizes triangulares é triangular, assim como o produto de matrizes ortogonais é ortogonal, quando temos que $$E\_k $$ é triangular-inferior ou é um fator ortogonal da $$k-esima $$ transformação da original $$A\_1 $$ . Disso, a convergência do processo $$QR $$ é determinado pelo comportamento da sequência $$E\_k $$ , desde que $$A\_{k+1} = E\_{k}^{-1} A\_1 E_k $$ . </p> 

&nbsp;

### 1.1. Resolvendo sistemas lineares com decomposição QR </p> 

A matriz $$A $$ de dimensões $$(m,n) $$ pode ser decomposta em termos de duas matrizes $$Q $$ e $$R $$ como
    


<center>
  $$ A = Q \left[ \begin{array}{c}<br /> R \\<br /> 0<br /> \end{array} \right] $$<br />
</center>


    
com a matriz $$R $$ sendo quadrada e triangular-superior $$R $$ de dimensão $$(n,n) $$ . 

Para o problema que tem $$A $$ como matriz de coeficientes na forma
    


<center>
  $$ A x = b $$
</center>


    
podemos utilizar a decomposição QR para resolvê-lo com o sistema triangular $$R $$ na forma
    


<center>
  $$ R x = Q^T b $$
</center>


    
Isto é, a solução
    


<center>
  $$ x = \left( A^T A \right)^{-1} A^T b $$
</center>


    
vêm de
    


<center>
  $$ x = \left( R^T Q^T Q R \right)^{-1} R^T Q^T b =<br /> (R^T R)^{-1} R^T Q^T b = = R^{-1} Q^T b $$
</center>


    
portanto
   


<center>
  $$ R x = Q^T b $$
</center>


    
Separando este problemas, podemos solucionar $$x $$ em dois passos:

>   1. **Passo 1:** Calcular $$y = Q^T b $$ 
>   2. **Passo 2:** Resolver o sistema $$R x = y $$ 

&nbsp;

## 2. Implementação 

<div>
  <pre lang="python">
def QR(A):
    """
    Return the (Q,R) from QR Decomposition.

    QR(A)

    INPUT:
    * A: matrix to decompose

    return: the tuple (Q, R)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    OBS: This is a implementation of a QR with Householder transformation and
         the code is adapted from the NIST Template Numerical Toolkit (TNT)
         by Roldan Pozo. see: http://math.nist.gov/tnt/

    Sep 2010
    """

    (m, n) = (len(A), len(A[0]))
    QR = deepcopy(A)
    nrange = xrange(n)
    mrange = xrange(m)
    minor = min(m, n)
    Rdiag = [0.0 for i in nrange]
    Q = [[0.0 for i in nrange] for j in mrange]
    R = [[0.0 for i in nrange] for j in nrange]

    for least in xrange(minor):
        norm = 0.0
        for row in xrange(least, m):
            norm += QR[row][least] * QR[row][least]
        a = sqrt(norm)
        if QR[least][least] > 0:
            a = -a
        Rdiag[least] = a

        if a != 0.0:
            QR[least][least] -= a
            for col in xrange(least + 1, n):
                phi = 0.0
                for row in xrange(least, m):
                    phi -= QR[row][col] * QR[row][least]
                phi /= a * QR[least][least]
                for row in xrange(least, m):
                    QR[row][col] -= phi * QR[row][least]

    # get R
    for row in xrange(minor - 1, -1, -1):
        R[row][row] = Rdiag[row]
        for col in xrange(row + 1, n):
            R[row][col] = QR[row][col]

    # get Q
    for least in xrange(m - 1, minor - 1, -1):
        Q[least][least] = 1.0
    for least in xrange(minor - 1, -1, -1):
        Q[least][least] = 1.0
        if QR[least][least] != 0.0:
            for col in xrange(least, m):
                phi = 0.0
                for row in xrange(least, m):
                    phi -= Q[row][col] * QR[row][least]
                phi /= Rdiag[least] * QR[least][least]
                for row in xrange(least, m):
                    Q[row][col] -= phi * QR[row][least]
    return (Q, R)
   </pre>
</div>

&nbsp;

### 2.1. Utilizando a decomposição para resolver sistemas lineares 

<div>
  <pre lang="python">
def solveQR(A, b):
    """
    Return a list with the solution of linear system.

    solveQR(A, b)

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

    def solve(A, b):
        """ Solution by QR decomposition R x = Q^T b.
        """
        n = len(b)
        x = [0.0 for i in xrange(n)]
        (Q, R) = QR(A)
        # Step 1: Solve the system: y = Q^T b
        y = matmul(transpose(Q), b)
        # Step 2: Solve the R system: Rx = y (regressive replacement)
        x[n - 1] = y[n - 1] / R[n - 1][n - 1]
        x[n - 2] = (y[n - 2] - R[n - 2][n - 1] * x[n - 1]) / (R[n - 2][n - 2])
        for j in xrange(n - 3, -1, -1):
            sum = 0.0
            for k in xrange(j + 1, n):
                sum += R[j][k] * x[k]
            x[j] = (y[j] - sum) / R[j][j]
        return x

    # Function's body
    return solve(A, b)
</pre>
</div>

Estas funções estão disponíveis em <a href="http://www.sawp.com.br/code/linear/QR.py" target="_blank">http://www.sawp.com.br/code/linear/QR.py</a>, assim como um exemplo de como utilizá-las. 

&nbsp;

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em
    
<a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



&nbsp;

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b>Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a>
  </p>
  
  <p>
    <a name="bibitem3"><b>[3]</b> </a><a href="http://en.wikipedia.org/wiki/Householder_transformation" target="_blank">http://en.wikipedia.org/wiki/Householder_transformation</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> Lars Elden,<cite> <em>Numerical Linear Algebra and Applications in Data Mining</em> (Preliminary version),</cite> http://www.mai.liu.se/~ laeld/, (2005).</a>
  </p>
</fieldset>
