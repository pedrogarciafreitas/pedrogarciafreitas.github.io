---
id: 586
title: '2.1.2 Sistemas Lineares &#8212; Métodos Diretos &#8212; Decomposição LU'
date: 2010-03-16T13:08:03+00:00
author: SAWP
excerpt: '    Este artigo trata de uma classe de algoritmos de eliminação -- tais como da Eliminação de Gauss -- que utilizam decomposição de uma matriz para obtenção das incógnitas do sistema. A principal vantagem da decomposição LU é que ela otimiza o tempo gasto na eliminação, sendo adaptativo às situações nas quais o vetor dos termos independentes são calculados para um único conjunto de coeficientes do sistema. Além disso, este artigo desenvolve o método da decomposição LU como uma implementação da eliminação de Gauss.'
layout: post
guid: http://www.sawp.com.br/blog/?p=586
permalink: /p=586
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:20278:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> LU<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    LU(A, b)
    &nbsp;
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    &nbsp;
    return: a list with all unknown variables of system.
    &nbsp;
    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> pivot<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>:
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
    <span style="color: #ff7700;font-weight:bold;">return</span> A
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> crout_decomposition<span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Perform the Crout-based algorithm for decomposition the matriz
    A in two L and U using the Croud's Method.
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>
    L <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    U <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    U<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>/U<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #808080; font-style: italic;"># Calculate L</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i+<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>j<span style="color: black;">&#41;</span>:
    suma +<span style="color: #66cc66;">=</span> L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * U<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> - suma
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Calculate U</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span>:
    suma +<span style="color: #66cc66;">=</span> L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * U<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    U<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> - suma<span style="color: black;">&#41;</span>/L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>L<span style="color: #66cc66;">,</span> U<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> solveLU<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    y <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: black;">&#40;</span>L<span style="color: #66cc66;">,</span> U<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> crout_decomposition<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Step 1: Solve the L system: L * y = b</span>
    y<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>/L<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span>:
    suma +<span style="color: #66cc66;">=</span> L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * y<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    y<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - suma<span style="color: black;">&#41;</span>/L<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Step 2: Solve the U system: U * x = y (regressive replacement)</span>
    x<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>/U<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> y<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>i+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    suma <span style="color: #66cc66;">=</span> suma - U<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> suma/U<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Function body</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> solveLU<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def LU(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    LU(A, b)
    
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    
    return: a list with all unknown variables of system.
    
    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2010
    &quot;&quot;&quot;
    
    def pivot(A, k):
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
    return A
    
    def crout_decomposition(M):
    &quot;&quot;&quot; Perform the Crout-based algorithm for decomposition the matriz
    A in two L and U using the Croud's Method.
    &quot;&quot;&quot;
    n = len(M)
    L = [[0.0 for i in xrange(n)] for j in xrange(n)]
    U = [[0.0 for i in xrange(n)] for j in xrange(n)]
    
    for j in xrange(n):
    U[0][j] = M[0][j]
    for i in xrange(n):
    L[i][0] = M[i][0]/U[0][0]
    
    for i in xrange(n):
    # Calculate L
    for j in xrange(i+1):
    suma = 0.0
    for k in xrange(j):
    suma += L[i][k] * U[k][j]
    L[i][j] = M[i][j] - suma
    
    # Calculate U
    for j in xrange(i, n):
    suma = 0.0
    for k in xrange(i):
    suma += L[i][k] * U[k][j]
    U[i][j] = (M[i][j] - suma)/L[i][i]
    return (L, U)
    
    def solveLU(A, b):
    n = len(b)
    y = [0.0 for i in xrange(n)]
    x = [0.0 for i in xrange(n)]
    (L, U) = crout_decomposition(A)
    
    # Step 1: Solve the L system: L * y = b
    y[0] = b[0]/L[0][0]
    for i in xrange(1, n):
    suma = 0.0
    for j in xrange(i):
    suma += L[i][j] * y[j]
    y[i] = (b[i] - suma)/L[i][i]
    
    # Step 2: Solve the U system: U * x = y (regressive replacement)
    x[n-1] = y[n-1]/U[n-1][n-1]
    for i in xrange(n-1, -1, -1):
    suma = y[i]
    for j in xrange(i+1, n):
    suma = suma - U[i][j] * x[j]
    x[i] = suma/U[i][i]
    return x
    
    # Function body
    return solveLU(A, b)</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução </p> 

Um sistema linear do tipo
       
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ a_{11}x_1 + a_{12}x_2 + \cdots + a_{1n}x_n = b_1 $$<br />
</center>


       
<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ a_{21}x_1 + a_{22}x_2 + \cdots + a_{2n}x_n = b_2 $$<br />
</center>


       


<center>
  $$\vdots $$
</center>


       
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ a_{n1}x_1 + a_{n2}x_2 + \cdots + a_{nn}x_n = b_n $$<br />
</center>


    
pode ser representado na seguinte forma matricial:
      


<center>
  <br /> $$AX = B $$<br />
</center>


    
onde $$A$$ é a matriz formada pelos coeficientes $$a\_{11}, a\_{12}, \ldots, a\_{nn} $$, $$X $$ é o vetor formado pelas variáveis a serem determinadas $$x\_1, x\_2, \ldots, x\_n $$ e $$B$$ é o vetor dos termos independentes. 

Para determinação das incógnitas, o método da eliminação de Gauss desenvolve duas fases: a primeira é a _eliminação progressiva_, onde reduz o número de variáveis ao longo da execução para, então, aplicar a segunda fase, chamada de _substituição regressiva_, onde utiliza o resultado da primeira para determinar a solução geral do sistema. 

Dois dois passos descritos, o primeiro é o que consome mais tempo de cálculo, uma vez que é nesta fase que consiste o maior número de operações aritméticas e de trocas de dados. Por isso, encontrar um método que minimize esta fase crítica, implica em aumentar o desempenho para realizar a tarefa de resolução de sistemas lineares. 

Os métodos de decomposição LU consistem em separar a fase de eliminação da matriz dos coeficientes $$A $$ , que consomem maior tempo, das manipulações envolvidas com o vetor dos termos independentes, $$B $$ . Portanto, devemos deixar claro que, ao contrário da eliminação de Gauss, uma decomposição de LU é uma estratégia de melhoria na resolução de sistemas lineares. Sendo assim, não existe &#8220;o método&#8221; de decomposição LU, mas sim algumas abordagens a serem tomadas que permitem decompor o sistema. Uma implicação interessante disso é que a própria eliminação de Gauss pode ser descrita como uma decomposição LU. Ralson e Rabinowitz utilizam essa abordagem ao tratar os métodos diretos em seu livro _A First Course in Numerical Analysis_[[rabinowitz]](#bibitemrabinowitz), desenvolvendo os principais algoritmos de decomposição &#8212; Crout, Doolittle e Cholesky &#8212; como técnicas de resolução direta de sistemas lineares. 



## 2. Desenvolvimento do método da decomposição LU </p> 

A equação
    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ AX = B $$<br />
</center>


    
pode ser reescrita como
   
<a name="eq5">(eq5)</a>
      


<center>
  <br /> $$ AX &#8211; B = 0 $$<br />
</center>

Aplicando a eliminação de Gauss, sabemos que este sistema pode ser reescrito como uma matriz triangular superior na forma:
    


<center>
  <br /> $$\left[ \begin{array}{ccc} u_{11} & u_{12} & u_{13} \\ 0 & u_{22} & u_{23} \\ 0 & 0 & u_{33} \end{array} \right]$$ $$\left[ \begin{array}{c} x_1 \\ x_2 \\ x_3 \end{array} \right] = $$ $$\left[ \begin{array}{c} d_1 \\ d_2 \\ d_3 \\ \end{array} \right]$$<br />
</center>


    
Esta notação matricial também pode ser usada da seguinte maneira:
    
<a name="eq6">(eq6)</a>
      


<center>
  <br /> $$ UX &#8211; D = 0 $$<br />
</center>

Agora, vamos supor que existe uma matriz composta apenas pela formula triangular inferior, tal que
    


<center>
  <br /> $$L = \left[ \begin{array}{ccc} 1 & 0 & 0 \\ l_{21} & 1 & 0 \\ l_{31} & l_{32} & 1 \end{array} \right]$$<br />
</center>

O processo de decomposição LU consiste justamente de em decompor a matriz dos coeficientes $$A $$ em duas matrizes, onde a primeira está na forma triangular inferior (_Low_), enquanto a outra está na forma triangula superior (_Upper_). Sendo assim, para $$L $$ e $$U $$ , comparadascom a Equação [5](#eq5), temos que
    
<a name="eq7">(eq7)</a>
      


<center>
  <br /> $$ L[UX &#8211; D] = AX &#8211; B = 0 $$<br />
</center>

Agora, isolamos os termos dependentes de $$X $$ , temos que
    
<a name="eq8">(eq8)</a>
      


<center>
  <br /> $$ LU = A $$<br />
</center>


    
e
    
<a name="eq9">(eq9)</a>
      


<center>
  <br /> $$ LD = B $$<br />
</center>


    
desta forma, isolamos a dependência dos termos independentes $$B $$ da matriz dos coeficientes $$A $$ . Desta forma, também livramos as operações efetuadas sobre $$A $$ (agora $$LU $$ ) de serem feitas em $$B $$ , diminuindo a demanda de recursos para resolução deste sistema. 



### 2.1. Eliminação de Gauss como uma Decomposição LU </p> 

Como dito na seção anterior, a matriz $$U $$ possui uma forma muito semelhante àquela gerada pelo processo de _eliminação progressiva_, estágio da eliminação de Gauss. Neste estágio, a matriz dos coeficientes $$A $$ é reduzida para a forma
    


<center>
  <br /> $$\left[ \begin{array}{ccc} a_{11} & a_{12} & a_{13} \\ 0 & a&#8217;_{22} & a&#8217;_{23} \\ 0 & 0 & a&#8221;_{33} \end{array} \right]$$<br />
</center>


    
que é a forma triangular superior procurada. Desta forma, os termos retirados são aqueles que formam a matriz $$L $$ . Podemos ver isso ao agruparmos em uma mesma matriz os elementos obtidos da eliminação progressiva, e os retirados pelo processo. Isto é, para o sistema original
    


<center>
  <br /> $$\left[ \begin{array}{ccc} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{array} \right] \left[ \begin{array}{c} x_1 \\ x_2 \\ x_3 \end{array} \right] = \left[ \begin{array}{c} b_1 \\ b_2 \\ b_3 \\ \end{array} \right] $$<br />
</center>


    
a primeira etapa na eliminação de Gauss é multiplicar a primeira linha pelo fator de normalização
    


<center>
  <br /> $$\phi_{21} = \dfrac{a_{21}{a_{11} $$<br />
</center>


    
e subtrair este resultado da próxima linha, a fim de eliminar o termo $$a_{21} $$ . Da mesma forma, o próximo passo se dá em multiplicar a primeira linha por
    


<center>
  <br /> $$\phi_{31} = \dfrac{a_{31}{a_{11} $$<br />
</center>


    
e o resultado é subtraído da terceira linha para eliminar $$a_{31} $$ . Por fim, multiplicamos a segunda linha por
    


<center>
  <br /> $$\phi_{32} = \dfrac{a&#8217;_{31}{a&#8217;_{22} $$<br />
</center>


    
e subtraímos o resultado da terceira linha para eliminarmos $$a&#8217;\_{32} $$. Como a ideia neste processo é gerar zeros em $$a\_{21} $$ , $$a\_{31} $$ e $$a\_{32} $$ . Assim, após a eliminação, $$A $$ pode ser escrita na forma:
    


<center>
  <br /> $$\left[ \begin{array}{ccc} a_{11} & a_{12} & a_{13} \\ \phi_{21} & a&#8217;_{22} & a&#8217;_{23} \\ \phi_{31} & \phi_{32} & a&#8221;_{33} \end{array} \right]$$<br />
</center>


    
Essa matriz, de fato, representa uma decomposição $$LU $$ de $$A $$ :
    
<a name="eq10">(eq10)</a>
      


<center>
  <br /> $$ A = LU $$<br />
</center>


    
pois
    


<center>
  <br /> $$U = \left[ \begin{array}{ccc} a_{11} & a_{12} & a_{13} \\ 0 & a&#8217;_{22} & a&#8217;_{23} \\ 0 & 0 & a&#8221;_{33} \end{array} \right]$$<br />
</center>


    
e
    


<center>
  <br /> $$L = \left[ \begin{array}{ccc} 1 & 0 & 0 \\ \phi_{21} & 1 & 0 \\ \phi_{31} & \phi_{32} & 1 \end{array} \right]$$<br />
</center>

### 2.2. O algoritmo de Crout 

O algoritmo de Crout decompõe as matrizes $$U $$ e $$L $$ de forma não-singular da matriz quadrada $$A $$ , sendo a fatoração de $$A $$ nos produtos da matriz $$L $$ (_Lower_) e $$U $$ (_Upper_), cuja diagonal principal é formada por valores unitários. O processo de decomposição é feito a partir das seguintes fórmulas (Obtidas de Ralson e Rabinowitz _A First Course in Numerical Analysis_[[rabinowitz]](#bibitemrabinowitz), páginas 422 e 423):
    
<a name="eq10">(eq10)</a>
      


<center>
  <br /> $$ l_{i1} = a_{i1} $$<br />
</center>


     
para $$i = 1,2,\ldots, n $$ .
    
<a name="eq11">(eq11)</a>
      


<center>
  <br /> $$ u_{1k} = \dfrac{a_{1k}{l_{11} $$<br />
</center>


    
para $$k = 2, 3, \ldots, n $$. Para $$j = 2, 3, \ldots, n-1 $$ , temos:
    
<a name="eq12">(eq12)</a>
      


<center>
  <br /> $$ l_{ij} = a_{ij} &#8211; \sum^{j-1}_{k=1} l_{ik}u_{kj} $$<br />
</center>


    
onde $$i = j, j+1, j+2, \ldots, n $$ e também
    
<a name="eq13">(eq13)</a>
      


<center>
  <br /> $$ u_{ji} = \dfrac{a_{ji} &#8211; \sum^{j-1}_{k=1} l_{jk}u_{ki}{l_{ii} $$<br />
</center>


    
onde $$i = j + 1, j + 2, \ldots, n $$ , e
    
<a name="eq14">(eq14)</a>
      


<center>
  <br /> $$ l_{nn} = a_{nn} &#8211; \sum^{n-1}_{k=1} l_{nk}u_{kn} $$<br />
</center>



## 3. Implementação </p> 

Uma implementação eficiente para decomposição $$LU $$ segue abaixo:

<div>
  <pre lang="python">def LU(A, b):
    """
    Return a list with the solution of linear system.

    LU(A, b)

    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms

    return: a list with all unknown variables of system.

    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2010
    """

    def pivot(A, k):
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
        return A

    def crout_decomposition(M):
        """ Perform the Crout-based algorithm for decomposition the matriz
        A in two L and U using the Croud's Method.
        """
        n = len(M)
        L = [[0.0 for i in xrange(n)] for j in xrange(n)]
        U = [[0.0 for i in xrange(n)] for j in xrange(n)]

        for j in xrange(n):
            U[0][j] = M[0][j]
        for i in xrange(n):
            L[i][0] = M[i][0]/U[0][0]

        for i in xrange(n):
            # Calculate L
            for j in xrange(i+1):
                suma = 0.0
                for k in xrange(j):
                    suma += L[i][k] * U[k][j]
                L[i][j] = M[i][j] - suma

            # Calculate U
            for j in xrange(i, n):
                suma = 0.0
                for k in xrange(i):
                    suma += L[i][k] * U[k][j]
                U[i][j] = (M[i][j] - suma)/L[i][i]
        return (L, U)

    def solveLU(A, b):
        n = len(b)
        y = [0.0 for i in xrange(n)]
        x = [0.0 for i in xrange(n)]
        (L, U) = crout_decomposition(A)

        # Step 1: Solve the L system: L * y = b
        y[0] = b[0]/L[0][0]
        for i in xrange(1, n):
            suma = 0.0
            for j in xrange(i):
                suma += L[i][j] * y[j]
            y[i] = (b[i] - suma)/L[i][i]

        # Step 2: Solve the U system: U * x = y (regressive replacement)
        x[n-1] = y[n-1]/U[n-1][n-1]
        for i in xrange(n-1, -1, -1):
            suma = y[i]
            for j in xrange(i+1, n):
                suma = suma - U[i][j] * x[j]
            x[i] = suma/U[i][i]
        return x

    # Function body
    return solveLU(A, b)</pre>
</div>

Esta função está disponível em <a href="http://www.sawp.com.br/code/linear/LU.py" target="_blank">http://www.sawp.com.br/code/linear/LU.py</a>, assim como um exemplo de como utilizá-la. </p> 

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitemrabinowitz"><b>[rabinowitz]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.)</cite> McGraw-Hill and Dover, (2001), 425.</a>
  </p>
</fieldset>
