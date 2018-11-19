---
id: 711
title: '2.1.7 Sistemas Lineares &#8212; Métodos Diretos &#8212; O Algoritmo de Thomas'
date: 2010-09-06T11:16:53+00:00
author: SAWP
excerpt: '    Neste post veremos o algoritmo para resolução de sistemas com matrizes tri-diagonais (TDMA - Tridiagonal Matrix Algorithm), conhecido como "Algoritmo de Thomas", que é uma forma simplificada da Eliminação de Gauss. Este algoritmo é um dos mais eficientes métodos para resolução de problemas reduzidos à sistemas lineares e também possui grande simplicidade, o que favorece a implementação.'
layout: post
guid: http://www.sawp.com.br/blog/?p=711
permalink: p=711
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8125:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> thomas<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    thomas(A, b)
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
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    terms <span style="color: #66cc66;">=</span> deepcopy<span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    d <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    upper <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    lower <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    d.<span style="color: black;">append</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    x.<span style="color: black;">append</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>
    upper.<span style="color: black;">append</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>
    lower.<span style="color: black;">append</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    upper<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    lower<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    d<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> d<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - lower<span style="color: black;">&#91;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> * upper<span style="color: black;">&#91;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / d<span style="color: black;">&#91;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    terms<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> terms<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - lower<span style="color: black;">&#91;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> * terms<span style="color: black;">&#91;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / d<span style="color: black;">&#91;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> terms<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / d<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># (regressive replacement)</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>terms<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - upper<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> / d<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def thomas(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    thomas(A, b)
    
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
    n = len(b)
    terms = deepcopy(b)
    x = []
    d = []
    upper = []
    lower = []
    
    for i in xrange(n):
    d.append(A[i][i])
    x.append(0.0)
    upper.append(0.0)
    lower.append(0.0)
    for i in xrange(n - 1):
    upper[i] = A[i][i + 1]
    lower[i] = A[i + 1][i]
    
    for i in xrange(1, n):
    d[i] = d[i] - lower[i - 1] * upper[i - 1] / d[i - 1]
    terms[i] = terms[i] - lower[i - 1] * terms[i - 1] / d[i - 1]
    x[n - 1] = terms[n - 1] / d[n - 1]
    
    # (regressive replacement)
    for i in xrange(n - 2, -1, -1):
    x[i] = (terms[i] - upper[i] * x[i + 1]) / d[i]
    return x</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. O algoritmo de Thomas 

Seja um sistema tri-diagonal de \(n \) incógnitas que pode ser escrito como
    


<center>
  <br /> \( a_i x_{i-1} + b_i x_i + c_i x_{i+1} = d_i \)<br />
</center>


    
onde \(a\_1 = 0 \) e \(c\_n = 0 \) . Na forma matricial, este sistema é escrito como
    


<center>
  <br /> \( \left[<br /> \begin{array}{cccccc}<br /> b_1 & c_1 & 0 & 0 & \cdots & 0 \\<br /> a_2 & b_2 & c_2 & 0 & \cdots & 0 \\<br /> 0 & a_3 & b_3 & \ddots & ~ & ~ \\<br /> \vdots & ~ & \ddots & ~ & \ddots & c_{n-1} \\<br /> 0 & ~ & ~ & ~ & a_n & b_n<br /> \end{array}<br /> \right] \)<br />
</center>

Para a resolução de tal sistema, definimos
    


<center>
  <br /> \( c_i&#8217; = \left\{ \begin{array}{ll}<br /> \dfrac{c_1}{b_1} & \textrm{para i = 1 }\\<br /> ~ \\<br /> \dfrac{c_i}{b_i &#8211; c_{i-1}&#8217; a_i} & \textrm{para i = 2, 3, &#8230; , n-1}\\<br /> \end{array} \right. \)<br />
</center>


    
e
    


<center>
  <br /> \( d_i&#8217; = \left\{ \begin{array}{ll}<br /> \dfrac{d_1}{b_1} & \textrm{para i = 1 }\\<br /> ~ \\<br /> \dfrac{d_i &#8211; d_{i-1}&#8217; a_i}{b_i &#8211; c_{i-1}&#8217; a_i} & \textrm{para i = 2, 3, &#8230; , n-1 }\\<br /> \end{array} \right. \)<br />
</center>


    
a solução \(x \) deste sistema será
    


<center>
  <br /> \( x_i = \left\{ \begin{array}{ll}<br /> d_n&#8217; & \textrm{para i = n }\\<br /> ~ \\<br /> d_i&#8217; &#8211; c_i&#8217; x_{i+1} & \textrm{para i = n-1, n-2, &#8230; , 1 }\\<br /> \end{array} \right. \)<br />
</center>

## 2. Implementação 

<div>
  <pre lang="python">
def thomas(A, b):
    """
    Return a list with the solution of linear system.

    thomas(A, b)

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
    n = len(b)
    terms = deepcopy(b)
    x = []
    d = []
    upper = []
    lower = []

    for i in xrange(n):
        d.append(A[i][i])
        x.append(0.0)
        upper.append(0.0)
        lower.append(0.0)
    for i in xrange(n - 1):
        upper[i] = A[i][i + 1]
        lower[i] = A[i + 1][i]

    for i in xrange(1, n):
        d[i] = d[i] - lower[i - 1] * upper[i - 1] / d[i - 1]
        terms[i] = terms[i] - lower[i - 1] * terms[i - 1] / d[i - 1]
    x[n - 1] = terms[n - 1] / d[n - 1]

    # (regressive replacement)
    for i in xrange(n - 2, -1, -1):
        x[i] = (terms[i] - upper[i] * x[i + 1]) / d[i]
    return x
   </pre>
</div>

Estas funções estão disponíveis em <a href="http://www.sawp.com.br/code/linear/thomas.py" target="_blank">http://www.sawp.com.br/code/linear/thomas.py</a>, assim como um exemplo de como utilizá-las. 

&nbsp; 

## 3. Copyright </p> 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a><br /> <a name="bibitem2"><b>[2]</b> Lars Elden,<cite> <em>Numerical Linear Algebra and Applications in Data Mining</em> (Preliminary version),</cite> http://www.mai.liu.se/~ laeld/, (2005)</a><br /> <a name="bibitem3"><b>[3]</b> </a><a href="http://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm" target="_blank">http://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm</a>
  </p>
</fieldset>
