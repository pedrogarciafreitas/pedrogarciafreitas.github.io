---
id: 1130
title: '3.1.7 Aproximação de Funções &#8212; Interpolação &#8212; Splines'
date: 2011-02-24T15:06:58+00:00
author: SAWP
excerpt: '    Neste post, usamos funções lineares simples para introduzir alguns conceitos básicos e problemas relacionados à splines. Então, desenvolvemos um algoritmo para ajuste de valores aos dados. Finalmente, discutimos sobre splines cúbicos, que possuem maior aplicabilidade em problemas reais.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1130
permalink: /p=1130
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:16876:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> spline<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> x_j<span style="color: #66cc66;">,</span> f_j<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return x evaluated in Spline interpolation function.
    &nbsp;
    spline(x, x_j, f_j, n=3)
    &nbsp;
    INPUT:
    * x: float, evalue at this point
    * x_j: LIST, tabular points
    * f_j: LIST, tabular points (must be same size of x_j)
    * n: spline degree (1=linear,2=quadratic,3=cubic(default),4= quartic)
    &nbsp;
    return:
    * f(x): interpolated and evaluated x value
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Feb 2011
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> cubic_spline<span style="color: black;">&#40;</span>xi<span style="color: #66cc66;">,</span> fi<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Fit a curve using a cubic spline&quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>xi<span style="color: black;">&#41;</span> - <span style="color: #ff4500;">1</span>
    h <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    g <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    d <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    c <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    <span style="color: #808080; font-style: italic;"># diferences between points</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    hi <span style="color: #66cc66;">=</span> xi<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> - xi<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    gi <span style="color: #66cc66;">=</span> fi<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> - fi<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    h.<span style="color: black;">append</span><span style="color: black;">&#40;</span>hi<span style="color: black;">&#41;</span>
    g.<span style="color: black;">append</span><span style="color: black;">&#40;</span>gi<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># generate 3-diagonal matrix</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    di <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span> * <span style="color: black;">&#40;</span>h<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + h<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    bi <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">6</span> * <span style="color: black;">&#40;</span>g<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / h<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> - g<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> / h<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    ci <span style="color: #66cc66;">=</span> h<span style="color: black;">&#91;</span>i + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    d.<span style="color: black;">append</span><span style="color: black;">&#40;</span>di<span style="color: black;">&#41;</span>
    b.<span style="color: black;">append</span><span style="color: black;">&#40;</span>bi<span style="color: black;">&#41;</span>
    c.<span style="color: black;">append</span><span style="color: black;">&#40;</span>ci<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># solve the tridiagonal system</span>
    g <span style="color: #66cc66;">=</span> tridiagonal_solve<span style="color: black;">&#40;</span>d<span style="color: #66cc66;">,</span> c<span style="color: #66cc66;">,</span> c<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># solution</span>
    pol <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    pol<span style="color: black;">&#91;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    pol<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> g<span style="color: black;">&#91;</span>i-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> pol
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>f_j<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Error: wrong type parameters&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;NaN&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>f_j<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Error: the tabular points must have same size&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;NaN&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> n <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span>:
    <span style="color: #808080; font-style: italic;"># TODO</span>
    <span style="color: #ff7700;font-weight:bold;">pass</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> n <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">2</span>:
    <span style="color: #808080; font-style: italic;"># TODO</span>
    <span style="color: #ff7700;font-weight:bold;">pass</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> n <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span>:
    <span style="color: #808080; font-style: italic;"># TODO</span>
    <span style="color: #ff7700;font-weight:bold;">pass</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    polinomial <span style="color: #66cc66;">=</span> cubic_spline<span style="color: black;">&#40;</span>x_j<span style="color: #66cc66;">,</span> f_j<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># this is just to assure convergence</span>
    m <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">100</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    k <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    dx <span style="color: #66cc66;">=</span> x - x_j<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> dx <span style="color: #66cc66;">&gt;=</span> <span style="color: #ff4500;">0</span>:
    k <span style="color: #66cc66;">=</span> k + <span style="color: #ff4500;">1</span>
    dx <span style="color: #66cc66;">=</span> x - x_j<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    k <span style="color: #66cc66;">=</span> k - <span style="color: #ff4500;">1</span>
    <span style="color: #808080; font-style: italic;"># encontra um valor para a funcao f(x)</span>
    dx <span style="color: #66cc66;">=</span> x_j<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> - x_j<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    alpha <span style="color: #66cc66;">=</span> polinomial<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">6</span> * dx<span style="color: black;">&#41;</span>
    beta <span style="color: #66cc66;">=</span> - polinomial<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">6</span> * dx<span style="color: black;">&#41;</span>
    gamma <span style="color: #66cc66;">=</span> f_j<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / dx - dx * polinomial<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> / <span style="color: #ff4500;">6</span>
    ro <span style="color: #66cc66;">=</span> dx * polinomial<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> / <span style="color: #ff4500;">6</span> - f_j<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> / dx
    f <span style="color: #66cc66;">=</span> alpha * <span style="color: black;">&#40;</span>x - x_j<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> ** <span style="color: #ff4500;">3</span> + \
    beta * <span style="color: black;">&#40;</span>x - x_j<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> ** <span style="color: #ff4500;">3</span> + \
    gamma * <span style="color: black;">&#40;</span>x - x_j<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> + \
    ro * <span style="color: black;">&#40;</span>x - x_j<span style="color: black;">&#91;</span>k + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> f</pre></td></tr></table><p class="theCode" style="display:none;">def spline(x, x_j, f_j, n=3):
    &quot;&quot;&quot;
    Return x evaluated in Spline interpolation function.
    
    spline(x, x_j, f_j, n=3)
    
    INPUT:
    * x: float, evalue at this point
    * x_j: LIST, tabular points
    * f_j: LIST, tabular points (must be same size of x_j)
    * n: spline degree (1=linear,2=quadratic,3=cubic(default),4= quartic)
    
    return:
    * f(x): interpolated and evaluated x value
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Feb 2011
    &quot;&quot;&quot;
    
    def cubic_spline(xi, fi):
    &quot;&quot;&quot; Fit a curve using a cubic spline&quot;&quot;&quot;
    n = len(xi) - 1
    h = []
    g = []
    d = []
    b = []
    c = []
    # diferences between points
    for i in xrange(n):
    hi = xi[i + 1] - xi[i]
    gi = fi[i + 1] - fi[i]
    h.append(hi)
    g.append(gi)
    # generate 3-diagonal matrix
    for i in xrange(n-1):
    di = 2 * (h[i + 1] + h[i])
    bi = 6 * (g[i + 1] / h[i + 1] - g[i] / h[i])
    ci = h[i + 1]
    d.append(di)
    b.append(bi)
    c.append(ci)
    # solve the tridiagonal system
    g = tridiagonal_solve(d, c, c, b)
    # solution
    pol = [0.0 for i in xrange(n)]
    pol[n-1] = 0.0
    for i in xrange(1, n):
    pol[i] = g[i-1]
    return pol
    
    if type(x_j) != type(f_j) or type(x_j) != type([]):
    print &quot;Error: wrong type parameters&quot;
    return float(&quot;NaN&quot;)
    
    if len(x_j) != len(f_j):
    print &quot;Error: the tabular points must have same size&quot;
    return float(&quot;NaN&quot;)
    
    if n == 1:
    # TODO
    pass
    elif n == 2:
    # TODO
    pass
    elif n == 4:
    # TODO
    pass
    else:
    polinomial = cubic_spline(x_j, f_j)
    
    # this is just to assure convergence
    m = 100
    for i in xrange(m):
    k = 1
    dx = x - x_j[0]
    while dx &gt;= 0:
    k = k + 1
    dx = x - x_j[k]
    k = k - 1
    # encontra um valor para a funcao f(x)
    dx = x_j[k + 1] - x_j[k]
    alpha = polinomial[k + 1] / (6 * dx)
    beta = - polinomial[k] / (6 * dx)
    gamma = f_j[k + 1] / dx - dx * polinomial[k + 1] / 6
    ro = dx * polinomial[k] / 6 - f_j[k] / dx
    f = alpha * (x - x_j[k]) ** 3 + \
    beta * (x - x_j[k + 1]) ** 3 + \
    gamma * (x - x_j[k]) + \
    ro * (x - x_j[k + 1])
    return f</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Interpolação por Splines 

O conceito de spline foi originado de uma técnica de desenho arquitetônico em que usa-se um barbante flexível &#8212; chamado _spline_ &#8212; para desenhar uma curva lisa passando por um conjunto de pontos. Nessa técnica, o desenhista coloca papel sobre uma base fixa e prega pequenos pinos ao papel sobre os pontos dados. Uma curva contínua é usada para intercalar estes pontos afixados, podendo ser reta (linear), quadrática ou cúbica. 

Esta ideia foi utilizada em análise numérica para ajuste de funções. Neste caso, utilizamos polinômios de pequeno grau para união dos pontos consecutivos da amostragem. 

&nbsp;

### 1.1. Splines Lineares 

O ajuste mais simples que podemos fazer com dois pontos é uni-los por uma reta. Os splines de primeiro grau para um conjunto de pontos amostrados podem ser definidos como um conjunto de funções lineares, tais que
    


<center>
  <br /> $$f(x) = f(x_0) + m_0 (x &#8211; x_0) $$ , para $$x_0 \leq x \leq x_1 $$ <br /> $$f(x) = f(x_1) + m_1 (x &#8211; x_1) $$ , para $$x_1 \leq x \leq x_2 $$ <br /> $$\vdots $$ <br /> $$f(x) = f(x_{n-1}) + m_{n-1}(x &#8211; x_{m-1}) $$ , para $$x_{n-1} \leq x \leq x_n $$<br />
</center>


    
onde $$m_i $$ é o coeficiente angular da reta que liga os pontos:
    


<center>
  <br /> $$m_i = \frac{f(x_{i+1}) &#8211; f(x_i)}{x_{i+1} &#8211; x_i} $$<br />
</center>

Essas equações podem ser utilizadas para calcular a função em qualquer ponto entre $$x\_0 $$ e $$x\_n $$ . Notamos que este método é idêntico à interpolação linear. 

&nbsp;

### 1.2. Splines Quadráticos 

Este método é obviamente idêntico à interpolação por splines lineares. A única diferença está na função de união dos pontos, que deve ser quadrática. Para isso, o objetivo dos splines quadráticos é determinar um polinômio de segundo grau para cada intervalo entre os pontos dados. Esse polinômio é representado pela função
    


<center>
  <br /> $$f_i(x) = a_i x ^ 2 + b_i x + c_i $$<br />
</center>


    
Para $$n+1 $$ pontos dados $$(i=0,1,2,3,\ldots,n) $$ , existem $$n $$ intervalos e, portanto, $$3n $$ constantes indeterminadas para calcularmos: $$a\_i $$ , $$b\_i $$ e $$c_i $$ . Portanto, criamos $$3n $$ equações para calcular estas incógnitas. São elas:

  1. Dos valores da função e dos polinômios adjacentes que devem ser iguais aos pontos interiores. Estas equações são:
           
    <center>
      <br /> $$a_{i-1} x_{i-1}^2 + b_{i-1} x_{i-1} + c_{i-1} = f(x_{i-1}) $$ <br /> $$a_i x_{i-1}^2 + b_i x_{i-1} + c_i = f(x_{i-1}) $$<br />
    </center>
    
    
          
    para $$i = 2 \cdots n $$ . Como apenas os pontos internos amostrados foram usados, as equações acima fornecem cada uma $$n-1 $$ equações para um total de $$2n &#8211; 2 $$ equações.</p> 
  2. A primeira e a última função deve passar pelos pontos extremos. Com isso, temos duas equações adicionais:
           
    <center>
      <br /> $$a_i x_0 ^ 2 + b_1 x_0 + c_1 = f(x_0) $$ <br /> $$a_n x_n ^ 2 + b_n x_n + c_n = f(x_n) $$<br />
    </center></p> 

  3. As primeiras derivadas nos pontos interiores devem sempre ser iguais. Isto é, como a função de ajuste é de segundo grau, sua derivada terá a forma
           
    <center>
      <br /> $$f'(x) = 2 a x + b $$<br />
    </center>
    
    
           
    Portanto, a condição geral será
           
    <center>
      <br /> $$2 a_{i-1} x_{i-1} + b_{i-1} = 2 a_i x_{i-1} + b_i $$<br />
    </center>
    
    
           
    para $$i = 2, \cdots , n $$ . Isso fornece outras $$n-1 $$ equações para um total de $$3 n &#8211; 1 $$.</p> 
  4. A última condição supõe que a segunda derivada seja nula no primeiro ponto. Isto é
           
    <center>
      <br /> $$a_1 = 0 $$<br />
    </center>

&nbsp;

### 1.3. Splines Cúbicos 

O objetivo nos splines cúbicos é determinar um polinômio de terceiro grau para cada intervalo entre os pontos amostrados. Ou seja, a aproximação de pontos consecutivos obedece à função
    


<center>
  <br /> $$f_i(x) = a_i x ^ 3 + b_i x + c_i x + d_i $$<br />
</center>


    
Logo, para $$n+1 $$ pontos dados $$(i=0,1,2,\ldots,n) $$ , existem $$n $$ intervalos e, consequentemente, $$4n $$ constantes indeterminadas. 

Para dedução dos splines cúbicos, nos baseamos na observação de que, como cada par de pontos amostrados é ligado por um polinômio cúbico, a segunda derivada no interior de cada intervalo é uma reta. A equação acima pode ser derivada duas vezes para verificar esta observação. Com base nisso, as segundas derivadas podem ser representadas por um polinômio interpolador de Lagrange de primeiro grau:
    


<center>
  <br /> $$f_i&#8221;(x) = f_i&#8221;(x_{i-1}) \frac{x &#8211; x_i}{x_{i-1} &#8211; x_i} + f_i&#8221;(x_i) \frac{x &#8211; x_{i-1}{x_i &#8211; x_{i-1} $$<br />
</center>


    
onde $$f\_i&#8221;(x) $$ é o valor da segunda derivada em um ponto qualquer $$x $$ no $$i-esimo $$ intervalo. Portanto, essa equação é uma reta ligando a segunda derivada no primeiro ponto $$f&#8221;(x\_{i-1}) $$ com a segunda derivada no segundo ponto $$f&#8221;(x_i) $$ . 

Integrando a última equação acima duas vezes, obtemos uma expressão para $$f\_i(x) $$ . Entretanto, essa expressão irá conter duas constantes de integração indeterminadas. Tais constantes podem ser determinadas invocando-se a condição de igualdade das funções. Isto é, $$f\_i(x) = f(x\_{i-1}) $$ em $$x\_{i-1} $$ e $$f\_i(x) $$ deve ser igual a $$f\_i(x\_i) $$ em $$x\_i $$ . A partir desses cálculos, obteremos a seguinte equação cúbica
    


<center>
  <br /> $$ f_i(x) = \frac{f_i&#8221;(x_{i-1})}{6 (x_i &#8211; x_{i-1})}(x_i &#8211; x)^3 +<br /> \frac{f_i&#8221;(x_i)}{6 (x_i &#8211; x_{i-1})} (x &#8211; x_{i-1})^3 +<br /> \left[ \frac{f(x_{i-1})}{x_i &#8211; x_{i-1} &#8211; \frac{f&#8221;(x_{i-1})(x_i &#8211; x_{i-1})}{6} \right] (x_i &#8211; x) +<br /> \left[ \frac{f(x_i)}{x_i &#8211; x_{i-1} &#8211; \frac{f&#8221;(x_i) (x_i &#8211; x_{i-1})}{6} \right] (x &#8211; x_{i-1})$$<br />
</center>


    
Observe que esta equação possui apenas dois coeficientes indeterminados: as segundas derivadas $$f&#8221;(x\_{i-1}) $$ e $$f&#8221;(x\_i) $$ . Estas segundas derivadas podem ser calculadas usando-se a condição de que as primeiras derivadas nos pontos amostrados são contínuas. Isto é:
    


<center>
  <br /> $$f_i'(x_i) = f_{i+1}'(x_i) $$<br />
</center>

Derivando a equação de $$f_i(x) $$ , encontramos uma expressão para a primeira derivada. Se isso for feito para os $$i-esimos $$ e $$(i-1)-esimos $$ intervalos e se os dois resultados forem igualados de acordo com a essa função, obtemos a seguinte relação:
    


<center>
  <br /> $$(x_i &#8211; x_{i-1}) f&#8221;(x_{i-1}) + 2(x_{i+1} &#8211; x_{i-1}) f&#8221;(x_i) + (x_{i+1} &#8211; x_i) f&#8221;(x_{i+1}) = \frac{6}{x_{i+1} &#8211; x_i} [f(x_{i+1}) &#8211; f(x_i)] + \frac{6}{x_i &#8211; x_{i-1} [f(x_{i-1}) &#8211; f(x_i)] $$<br />
</center>

Se esta última equação for escrita para todos os pontos interiores amostrados, temos $$(n-1) $$ equações simultâneas com $$n+1 $$ segundas derivadas. Contudo, como esse é um spline cúbico, as segundas derivadas nos extremos são nulas e o problema se reduz a $$(n-1) $$ equações com $$(n-1) $$ incógnitas. Além disso, se observamos a relação entre as variáveis, temos apenas a relação entre $$(i-1) $$ , $$i $$ e $$(i+1) $$ , o que caracteriza um sistema tridiagonal. Com isso, temos uma implementação extremamente simples e rápida de se resolver. 

&nbsp;

## 2. Implementação 

<div>
  <pre lang="python">def spline(x, x_j, f_j, n=3):
    """
    Return x evaluated in Spline interpolation function.

    spline(x, x_j, f_j, n=3)

    INPUT:
      * x: float, evalue at this point
      * x_j: LIST, tabular points
      * f_j: LIST, tabular points (must be same size of x_j)
      * n: spline degree (1=linear,2=quadratic,3=cubic(default),4= quartic)

    return:
      * f(x): interpolated and evaluated x value

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Feb 2011
    """

    def cubic_spline(xi, fi):
        """ Fit a curve using a cubic spline"""
        n = len(xi) - 1
        h = []
        g = []
        d = []
        b = []
        c = []
        # diferences between points
        for i in xrange(n):
            hi = xi[i + 1] - xi[i]
            gi = fi[i + 1] - fi[i]
            h.append(hi)
            g.append(gi)
        # generate 3-diagonal matrix
        for i in xrange(n-1):
            di = 2 * (h[i + 1] + h[i])
            bi = 6 * (g[i + 1] / h[i + 1] - g[i] / h[i])
            ci = h[i + 1]
            d.append(di)
            b.append(bi)
            c.append(ci)
        # solve the tridiagonal system
        g = tridiagonal_solve(d, c, c, b)
        # solution
        pol = [0.0 for i in xrange(n)]
        pol[n-1] = 0.0
        for i in xrange(1, n):
            pol[i] = g[i-1]
        return pol

    if type(x_j) != type(f_j) or type(x_j) != type([]):
        print "Error: wrong type parameters"
        return float("NaN")

    if len(x_j) != len(f_j):
        print "Error: the tabular points must have same size"
        return float("NaN")

    if n == 1:
        # TODO
        pass
    elif n == 2:
        # TODO
        pass
    elif n == 4:
        # TODO
        pass
    else:
        polinomial = cubic_spline(x_j, f_j)

    # this is just to assure convergence
    m = 100
    for i in xrange(m):
        k = 1
        dx = x - x_j[0]
        while dx >= 0:
            k = k + 1
            dx = x - x_j[k]
        k = k - 1
        # encontra um valor para a funcao f(x)
        dx = x_j[k + 1] - x_j[k]
        alpha = polinomial[k + 1] / (6 * dx)
        beta = - polinomial[k] / (6 * dx)
        gamma = f_j[k + 1] / dx - dx * polinomial[k + 1] / 6
        ro = dx * polinomial[k] / 6 - f_j[k] / dx
        f = alpha * (x - x_j[k]) ** 3 + \
            beta * (x - x_j[k + 1]) ** 3 + \
            gamma * (x - x_j[k]) + \
            ro * (x - x_j[k + 1])
    return f</pre>
</div>

Esta função está disponível em <a href="http://www.sawp.com.br/code/interpolation/splines.py" target="_blank">http://www.sawp.com.br/code/interpolation/splines.py</a> assim como um exemplo de como utilizá-la. 

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
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
