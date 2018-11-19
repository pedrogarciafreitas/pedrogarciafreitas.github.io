---
id: 604
title: '2.1.3 Sistemas Lineares &#8212; Métodos Diretos &#8212; Decomposição de Cholesky'
date: 2010-04-08T09:12:45+00:00
author: SAWP
excerpt: |
  Este artigo apresenta o algoritmo conhecido como "Fatoração de Cholesky", onde decompõe uma matriz A tal que A = LL*, onde L será uma matriz triangular-inferior com diagonal composta apenas por elementos não negativos, enquanto L* será a matriz adjunta de L.
  
  Caso A seja uma matriz positiva, então L será única, o que permite servir como fator identificador dos dados de A, chamado de "Fator de Cholesky de A". Essa propriedade pode permitir aplicações em diversas áreas da ciência e computação.
  
  Decomposições baseadas na de Cholesky estão presentes em criptografia, geração de hashes, verificação de dados e em uma diversidade de aplicações práticas.
layout: post
guid: http://www.sawp.com.br/blog/?p=604
permalink: /p=604
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:19916:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> cholesky<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    cholesky(A, b)
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
    Apr 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> isSimetric<span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; As Cholesky factorization explore the symmetric proprierty of
    A, this function check it.
    &nbsp;
    Return: True if A is symmetric. False if not.
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> M<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">False</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">True</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> cholesky_decomposition<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Perform the Cholesky decomposition on matriz A, returning L
    (Cholesky Factor).
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    M <span style="color: #66cc66;">=</span> deepcopy<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    L <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    Lt <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>:
    soma <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> i<span style="color: black;">&#41;</span>:
    soma +<span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - soma<span style="color: black;">&#41;</span>/M<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Diagonal</span>
    soma <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>:
    soma +<span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> sqrt<span style="color: black;">&#40;</span>M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> - soma<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># This is to show the LU form of Cholesky</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    L<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span>:k+<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span>:k+<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Lt is transpose of L</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    Lt<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> L<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>L<span style="color: #66cc66;">,</span> Lt<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> solveLU<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    y <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: black;">&#40;</span>L<span style="color: #66cc66;">,</span> U<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> cholesky_decomposition<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
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
    <span style="color: #808080; font-style: italic;"># Function's body</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> isSimetric<span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> solveLU<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">False</span></pre></td></tr></table><p class="theCode" style="display:none;">def cholesky(A, b):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    cholesky(A, b)
    
    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms
    
    return: a list with unknown vector 'x' of system A*x = b.
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Apr 2010
    &quot;&quot;&quot;
    
    def isSimetric(M):
    &quot;&quot;&quot; As Cholesky factorization explore the symmetric proprierty of
    A, this function check it.
    
    Return: True if A is symmetric. False if not.
    &quot;&quot;&quot;
    n = len(M)
    for i in xrange(n):
    for j in xrange(n):
    if M[i][j] != M[j][i]:
    return False
    return True
    
    def cholesky_decomposition(A):
    &quot;&quot;&quot; Perform the Cholesky decomposition on matriz A, returning L
    (Cholesky Factor).
    &quot;&quot;&quot;
    n = len(A)
    M = deepcopy(A)
    L = [[0.0 for i in xrange(n)] for j in xrange(n)]
    Lt = [[0.0 for i in xrange(n)] for j in xrange(n)]
    
    for k in xrange(0, n):
    for i in xrange(0, k):
    soma = 0.0
    for j in xrange(0, i):
    soma += M[i][j] * M[k][j]
    M[k][i] = (M[k][i] - soma)/M[i][i]
    
    # Diagonal
    soma = 0.0
    for j in xrange(0, k):
    soma += M[k][j] * M[k][j]
    M[k][k] = sqrt(M[k][k] - soma)
    
    # This is to show the LU form of Cholesky
    for k in xrange(0, n):
    L[k][0:k+1] = M[k][0:k+1]
    
    # Lt is transpose of L
    for i in xrange(0, n):
    for j in xrange(0, n):
    Lt[i][j] = L[j][i]
    return (L, Lt)
    
    def solveLU(A, b):
    n = len(b)
    y = [0.0 for i in xrange(n)]
    x = [0.0 for i in xrange(n)]
    (L, U) = cholesky_decomposition(A)
    
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
    
    # Function's body
    if isSimetric(A):
    return solveLU(A, b)
    else:
    return False</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. A Fatoração de Cholesky </p> 

A Fatoração de Cholesky expressa uma matriz simétrica $$A $$ como o produto,de uma matriz triangular $$L $$ (chamada de Fator de Cholesky) pela sua transposta $$L* $$ , na forma:
    
<a name="eq1">(eq1)</a>
  


<center>
  <br /> $$ A = LL* $$<br />
</center>

onde $$L $$ será triangular superior. 

Sabendo-se que $$A $$ é simétrica quando seus elementos obedecem à uma formação $$a\_{ij} = a\_{ji} $$ para toda linha $$i $$ e coluna $$j $$ . Desta forma, a matriz $$A $$ será idêntica à sua transposta: $$A = A^{T} $$ . Matrizes com este tipo de formação fornece algumas vantagens computacionais, pois favorecem a eficiência na solução de sistemas lineares, quando usados métodos adequados. Além disso, essa identidade permite a criação de algoritmos simples de criptografia e verificação de dados. 

Uma vez que se identifica que uma matriz $$A $$ é simétrica, podemos utilizar a Equação [1](#eq1) para gerar $$L $$ e $$L* $$ a partir de $$A $$ . Ou seja, ao multiplicarmos e igualarmos seus termos, obtemos as seguintes relações:
    
<a name="eq2">(eq2)</a>
  


<center>
  <br /> $$ l_{ki} = \frac{ a_{ki} &#8211; \sum_{j=1}^{i-1} l_{ij}~l_{kj} }{ l_{ii} } $$<br />
</center>

onde $$i = 1, 2, \ldots, k-1 $$ . Além disso, o elemento da diagonal será obtido por
    
<a name="eq3">(eq3)</a>
  


<center>
  <br /> $$ l_{kk} = \sqrt{a_{kk} &#8211; \sum_{k-1}^{j=1} l_{kj}^{2} } $$<br />
</center>

As expressões acima são obtidas como uma especificação da decomposição LU para o caso da matriz decomposta ser simétrica. Tais equações são desenvolvidas em _A First Course in Numerical Analysis_ [[1]](#bibitem1). </p> 

## 2. Implementação 

<div>
  <pre lang="python">def cholesky(A, b):
    """
    Return a list with the solution of linear system.

    cholesky(A, b)

    INPUT:
    * A: a matrix of coefficients
    * b: a list, relative a vector of independent terms

    return: a list with unknown vector 'x' of system A*x = b.

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Apr 2010
    """

    def isSimetric(M):
        """ As Cholesky factorization explore the symmetric proprierty of
        A, this function check it.

        Return: True if A is symmetric. False if not.
        """
        n = len(M)
        for i in xrange(n):
            for j in xrange(n):
                if M[i][j] != M[j][i]:
                    return False
        return True

    def cholesky_decomposition(A):
        """ Perform the Cholesky decomposition on matriz A, returning L
        (Cholesky Factor).
        """
        n = len(A)
        M = deepcopy(A)
        L = [[0.0 for i in xrange(n)] for j in xrange(n)]
        Lt = [[0.0 for i in xrange(n)] for j in xrange(n)]

        for k in xrange(0, n):
            for i in xrange(0, k):
                soma = 0.0
                for j in xrange(0, i):
                    soma += M[i][j] * M[k][j]
                M[k][i] = (M[k][i] - soma)/M[i][i]

            # Diagonal
            soma = 0.0
            for j in xrange(0, k):
                soma += M[k][j] * M[k][j]
            M[k][k] = sqrt(M[k][k] - soma)

        # This is to show the LU form of Cholesky
        for k in xrange(0, n):
            L[k][0:k+1] = M[k][0:k+1]

        # Lt is transpose of L
        for i in xrange(0, n):
            for j in xrange(0, n):
                Lt[i][j] = L[j][i]
        return (L, Lt)

    def solveLU(A, b):
        n = len(b)
        y = [0.0 for i in xrange(n)]
        x = [0.0 for i in xrange(n)]
        (L, U) = cholesky_decomposition(A)

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

    # Function's body
    if isSimetric(A):
        return solveLU(A, b)
    else:
        return False</pre>
</div></p> 

A partir deste código, podemos verificar que a única diferença que ele possui em relação ao algoritmo apresentado no artigo sobre decomposição LU está em utilizar a função _cholesky_decomposition_ ao invés do método de Crout. Isto porque a fatoração de Cholesky, assim como muitos algoritmos de solução direta, é um método de decomposição LU. Ainda pelo código, é possível notar que o fator de Cholesky é a própria matriz $$L $$, enquanto que sua transposta é $$U $$. 

Esta função está disponível em <a href="http://www.sawp.com.br/code/linear/cholesky.py" target="_blank">http://www.sawp.com.br/code/linear/cholesky.py</a>, assim como um exemplo de como utilizá-la. </p> </p> 

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a><br /> <br /> <a name="bibitem2"><b>[2]</b> Neide Bertoldi Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), ISBN 85-7605-087-0, pag. 141-145.</a><br /> </fieldset>
  </p>
