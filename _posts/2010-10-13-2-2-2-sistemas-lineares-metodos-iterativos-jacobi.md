---
id: 787
title: '2.2.2 Sistemas Lineares &#8212; Métodos Iterativos &#8212; Jacobi'
date: 2010-10-13T17:57:09+00:00
author: SAWP
excerpt: O Método de Jacobi é um algoritmo iterativo para resolução de sistemas lineares, muito semelhante ao método de Gauss-Siedel. Neste post, apresentamos características deste método e uma implementação em python do mesmo.
layout: post
guid: http://www.sawp.com.br/blog/?p=787
permalink: /p=787
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:12923:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> jacobi<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10E-10</span><span style="color: #66cc66;">,</span> maxiter<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10E5</span><span style="color: #66cc66;">,</span> SOR<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.5</span><span style="color: #66cc66;">,</span> getiters<span style="color: #66cc66;">=</span><span style="color: #008000;">False</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    jacobi(A, b)
    &nbsp;
    INPUT:
    * A: coefficients matrix
    * b: a list, vector of independent terms
    &nbsp;
    return:
    if getiters=False:
    a list with unknown vector 'x' of system A*x = b.
    else:
    the tuple (list x, integer iters)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Oct 2010
    &quot;&quot;&quot;</span>
    A <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #008000;">map</span><span style="color: black;">&#40;</span><span style="color: #008000;">float</span><span style="color: #66cc66;">,</span> i<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> A<span style="color: black;">&#93;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    errnoold <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    iters <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    sentry <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span>
    xold <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span> / <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>n + errto<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    xnew <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span> / <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>n + errto<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    diagonal <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> /<span style="color: #66cc66;">=</span> diagonal
    b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> /<span style="color: #66cc66;">=</span> diagonal
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    summ <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">!=</span> j:
    summ -<span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * xold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    xold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> summ
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #ff7700;font-weight:bold;">not</span> sentry <span style="color: #ff7700;font-weight:bold;">and</span> iters <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> maxiter:
    sentry <span style="color: #66cc66;">=</span> <span style="color: #008000;">True</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    summ <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">!=</span> j:
    summ -<span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * xold<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    xnew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> SOR * summ + <span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span> - SOR<span style="color: black;">&#41;</span> * xold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> sentry <span style="color: #ff7700;font-weight:bold;">and</span> xnew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>xnew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - xold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> / xnew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errnoold:
    newSOR <span style="color: #66cc66;">=</span> SOR - <span style="color: #ff4500;">0.1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> newSOR <span style="color: #66cc66;">&gt;=</span> errto:
    SOR <span style="color: #66cc66;">=</span> newSOR
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    newSOR <span style="color: #66cc66;">=</span> SOR + <span style="color: #ff4500;">0.1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> newSOR <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.9</span>:
    SOR <span style="color: #66cc66;">=</span> newSOR
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto:
    sentry <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span>
    xold<span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> xnew<span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span>
    errnoold <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">errno</span>
    iters +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> getiters:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>xnew<span style="color: #66cc66;">,</span> iters<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> xnew</pre></td></tr></table><p class="theCode" style="display:none;">def jacobi(A, b, errto=10E-10, maxiter=10E5, SOR=1.5, getiters=False):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    jacobi(A, b)
    
    INPUT:
    * A: coefficients matrix
    * b: a list, vector of independent terms
    
    return:
    if getiters=False:
    a list with unknown vector 'x' of system A*x = b.
    else:
    the tuple (list x, integer iters)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Oct 2010
    &quot;&quot;&quot;
    A = [map(float, i) for i in A]
    n = len(A)
    errnoold = 0.0
    errno = 0.0
    iters = 0
    sentry = False
    xold = [1.0 / float(n + errto) for i in xrange(n)]
    xnew = [1.0 / float(n + errto) for i in xrange(n)]
    
    for i in xrange(n):
    diagonal = float(A[i][i])
    for j in xrange(n):
    A[i][j] /= diagonal
    b[i] /= diagonal
    for i in xrange(n):
    summ = b[i]
    for j in xrange(n):
    if i != j:
    summ -= A[i][j] * xold[i]
    xold[i] = summ
    while not sentry and iters &lt; = maxiter:
    sentry = True
    for i in xrange(n):
    summ = b[i]
    for j in xrange(n):
    if i != j:
    summ -= A[i][j] * xold[j]
    xnew[i] = SOR * summ + (1.0 - SOR) * xold[i]
    if sentry and xnew[i] != 0:
    errno = abs((xnew[i] - xold[i]) / xnew[i])
    if errno &gt; errnoold:
    newSOR = SOR - 0.1
    if newSOR &gt;= errto:
    SOR = newSOR
    else:
    newSOR = SOR + 0.1
    if newSOR &lt; = 1.9:
    SOR = newSOR
    if errno &gt; errto:
    sentry = False
    xold[:] = xnew[:]
    errnoold = errno
    iters += 1
    if getiters:
    return (xnew, iters)
    else:
    return xnew</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. O método de Jacobi 

Seja o sistema linear $$Ax = b $$ tal que a matriz dos coeficientes $$A $$ possa ser decomposta na seguinte forma:
    


<center>
  $$A = D + R $$
</center>


    
onde $$D $$ é uma matriz diagonal e $$R $$ é a matriz que possui diagonal nula. Desta forma, o sistema é decomposto como
    


<center>
  <br /> $$<br /> Dx + Rx = b<br /> $$<br />
</center>


    
onde podemos isolar o vetor formado pela diagonal $$Dx = b &#8211; Rx $$ . 

O passo iterativo do método consiste em sucessivas iterações para aproximar a solução através da fórmula:
    


<center>
  <br /> $$x^{(k+1)} = D^{-1} (b &#8211; Rx^{(k)}) $$<br />
</center>


    
ou em uma forma mais simples
    


<center>
  <br /> $$ x_{i}^{(k+1)} = \dfrac{\left( b_i &#8211; \sum_{j \neq i} a_{ij}x_{j}^{(k)} \right)}{a_{ii} $$<br />
</center>

&nbsp;

## 2. SOR Adaptativo 

Como apresentamos no post sobre o método de Gauss-Siedel, podemos inserir uma variável na formula iterativa para controlar o comportamento da convergência. Tal recurso é chamado de **SOR** (_Sucessive OverRelaxation_). 

Uma propriedade interessante da variável de relaxação é que ela permite transformar um processo não-convergente em outro convergente ou acelerar a taxa de convergência. Quando escolhemos um valor entre $$]0,1[ $$ , observamos o primeiro caso, enquanto que valores entre $$]1,2[ $$ favorecem o segundo. Assim, podemos dizer que, respeitando estes intervalos, quanto maior o valor para variável de relaxação, maior será a velocidade de convergência, caso o sistema seja predominantemente diagonal. 

Na nossa implementação, utilizamos um valor dinâmico para variável de relaxação. Utilizamos um valor inicial que favorece a convergência (entre 0 e 1). Caso o sistema se mantenha com uma taxa de convergência constante entre duas iterações consecutivas, aumentamos o valor da variável com o objetivo de aumentar esta taxa. Se nesta configuração detectarmos divergência, diminuímos a variável de relaxação para forçar o solução do sistema.

&nbsp;

## 3. Implementação 

<div>
  <pre lang="python">def jacobi(A, b, errto=10E-10, maxiter=10E5, SOR=1.5, getiters=False):
    """
    Return a list with the solution of linear system.

    jacobi(A, b)

    INPUT:
    * A: coefficients matrix
    * b: a list, vector of independent terms

    return:
            if getiters=False:
                a list with unknown vector 'x' of system A*x = b.
            else:
                the tuple (list x, integer iters)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Oct 2010
    """
    A = [map(float, i) for i in A]
    n = len(A)
    errnoold = 0.0
    errno = 0.0
    iters = 0
    sentry = False
    xold = [1.0 / float(n + errto) for i in xrange(n)]
    xnew = [1.0 / float(n + errto) for i in xrange(n)]

    for i in xrange(n):
        diagonal = float(A[i][i])
        for j in xrange(n):
            A[i][j] /= diagonal
        b[i] /= diagonal
    for i in xrange(n):
        summ = b[i]
        for j in xrange(n):
            if i != j:
                summ -= A[i][j] * xold[i]
        xold[i] = summ
    while not sentry and iters &lt; = maxiter:
        sentry = True
        for i in xrange(n):
            summ = b[i]
            for j in xrange(n):
                if i != j:
                    summ -= A[i][j] * xold[j]
            xnew[i] = SOR * summ + (1.0 - SOR) * xold[i]
            if sentry and xnew[i] != 0:
                errno = abs((xnew[i] - xold[i]) / xnew[i])
                if errno > errnoold:
                    newSOR = SOR - 0.1
                    if newSOR >= errto:
                        SOR = newSOR
                else:
                    newSOR = SOR + 0.1
                    if newSOR &lt; = 1.9:
                        SOR = newSOR
                if errno > errto:
                    sentry = False
        xold[:] = xnew[:]
        errnoold = errno
        iters += 1
    if getiters:
        return (xnew, iters)
    else:
        return xnew</pre>
</div>

Esta função está disponível em <a href="http://www.sawp.com.br/code/linear/jacobi.py" target="_blank">http://www.sawp.com.br/code/linear/jacobi.py</a>, assim como um exemplo de como utilizá-la. 

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 69.</a>
  </p>
  
  <p>
    </fieldset>
  </p>
