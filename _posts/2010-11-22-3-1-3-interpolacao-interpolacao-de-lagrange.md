---
id: 868
title: '3.1.3 Aproximação de Funções &#8212; Interpolação &#8212; Interpolação de Lagrange'
date: 2010-11-22T15:58:49+00:00
author: SAWP
excerpt: ' O polinômio interpolador de Lagrange é uma das formulas mais simples para obtenção do polinômio interpolador. Neste post apresentamos e discutimos o método, além de disponibilizar um código que ilustra o algoritmo.'
layout: post
guid: http://www.sawp.com.br/blog/?p=868
permalink: p=868
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:6398:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> interpolation_lagrange<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> x_j<span style="color: #66cc66;">,</span> f_j<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return x evaluated in Lagrangian interpolation function.
    &nbsp;
    interpolation_lagrange(x, x_j, f_j)
    &nbsp;
    INPUT:
    * x: evalue at this point
    * x_j: LIST, tabular points
    * f_j: LIST, tabular points (must be same size of x_j)
    * n: polynom degree (optional)
    &nbsp;
    return:
    * y(x): interpolated and evaluated x value
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Oct 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>f_j<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Error: wrong type parameters&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;NaN&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>f_j<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Error: the tabular points must have same size&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;NaN&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> n <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    n <span style="color: #66cc66;">=</span> n + <span style="color: #ff4500;">1</span>
    &nbsp;
    p <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    li <span style="color: #66cc66;">=</span> f_j<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    xi <span style="color: #66cc66;">=</span> x_j<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    xj <span style="color: #66cc66;">=</span> x_j<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">!=</span> j:
    li <span style="color: #66cc66;">=</span> li * <span style="color: black;">&#40;</span>x - xj<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span>xi - xj<span style="color: black;">&#41;</span>
    p +<span style="color: #66cc66;">=</span> li
    <span style="color: #ff7700;font-weight:bold;">return</span> p</pre></td></tr></table><p class="theCode" style="display:none;">def interpolation_lagrange(x, x_j, f_j, n=0):
    &quot;&quot;&quot;
    Return x evaluated in Lagrangian interpolation function.
    
    interpolation_lagrange(x, x_j, f_j)
    
    INPUT:
    * x: evalue at this point
    * x_j: LIST, tabular points
    * f_j: LIST, tabular points (must be same size of x_j)
    * n: polynom degree (optional)
    
    return:
    * y(x): interpolated and evaluated x value
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Oct 2010
    &quot;&quot;&quot;
    
    if type(x_j) != type(f_j) or type(x_j) != type([]):
    print &quot;Error: wrong type parameters&quot;
    return float(&quot;NaN&quot;)
    
    if len(x_j) != len(f_j):
    print &quot;Error: the tabular points must have same size&quot;
    return float(&quot;NaN&quot;)
    
    if n &lt; = 0:
    n = len(x_j)
    else:
    n = n + 1
    
    p = 0.0
    for i in xrange(n):
    li = f_j[i]
    xi = x_j[i]
    for j in xrange(n):
    xj = x_j[j]
    if i != j:
    li = li * (x - xj) / (xi - xj)
    p += li
    return p</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Interpolação Lagrangiana 

Seja a função que desejamos aproximar

<center>
  \(f(x) = \sum_{j=1}^{n} l_j(x)f(a_j) + E(x) = y(x) + E(x) \)
</center>

tal que mantemos as restrições que mantém o erro dos pontos tabulares nulos e que seja independente de \(f(x) \) . Tomamos

<center>
  \(l_j(a_k) = \delta_{ij} \hspace{50pt} (j,k) = 1,\ldots,n \)
</center>

onde \(\delta\_{jk} \) é o Delta de Kronecker. Como \(l\_j(x) \) é um polinômio, isto implica que terá o fator

<center>
  \((x &#8211; a_1)(x &#8211; a_2) \ldots (x &#8211; a_{j-1}) (x &#8211; a_{j+1}) \ldots (x &#8211; a_n) \)
</center>

e como \(l\_j(a\_j) = 1 \) , podemos escrever para os termos gerais:

<center>
  \(l_j(x) = \dfrac{(x-a_1)\ldots(x-a_{j-1})(x-a_{j+1})\ldots(x-a_n)}{(a_j-a1)\ldots(a_j-a_{j-1})(a_j-a_{j+1})\ldots(a_j-a_n)}\)
</center>

Note que há outras possíveis representações para o polinômio \(l\_j(x) \), mas apenas a equação acima será um polinômio de grau \(n-1 \) . Isto torna conveniente escrever \(l\_j(x) \) como

<center>
  \(l_j(x) = \dfrac{p_n(x)}{(x-a_j)p&#8217;_n(a_j)} \)
</center>

onde \(p&#8217;\_n(x) = \frac{dp\_n}{dx} \) e \(p\_n(x) = \prod\_{i=1}^{n}(x-a_i) \). 

Para fazermos uma análise do erro de aproximação associado, devemos obter expressão \(E(x) \) , considerando a função

<center>
  \(F(z) = f(z) &#8211; y(z) &#8211; [f(x) &#8211; y(x)]\frac{p_n(z)}{p_n(x)} \)
</center>

com \(y(x) \) sendo a função ajustada da original. A função \(F(z) \) como uma função de \(z \) com \(n+1 \) raízes nos pontos \(a\_0,a\_1,\ldots,a_n \) e assumindo \(x \) sempre diferente dos pontos tabulares. Assim, ao aplicarmos o teorema de Rolle \(n \) vezes, teremos que

<center>
  \(F^{(n)}(z) = f^{(n)}(z) &#8211; y^{(n)}(z) &#8211; [f(x) &#8211; y(x)]\frac{n!}{p_n(x)} \)
</center>

terá ao menos um zero no intervalo determinado por \([a\_1,a\_n] \) . Chamando este zero de \(z = \xi \) e notando que \(y^{(n)}(z) = 0 \) , teremos

<center>
  \(0 = F^{(n)}(\xi) = f^{(n)}(\xi) &#8211; [f(x) &#8211; y(x)] \frac{n!}{p_n(x)} \)
</center>

que pode ser utilizado no cálculo do erro como

<center>
  \(E(x) = \frac{p_n(x)}{n!}f^{(n)}(\xi) \)
</center>

Utilizando a equação

<center>
  \(f(x) = \sum_{j=1}^{n} l_j(x)f(a_j) + E(x) = y(x) + E(x) \)
</center>

e agora de posse das funções \(l_j(x) \) e \(E(x) \) , podemos obter a formula para a interpolação de Lagrange:

<center>
  \(y(x) = \sum_{j=0}^{n} P_j(x)f(x_j) \)
</center>

onde

<center>
  \(P_j(x) = \prod_{i=0}^{n} \dfrac{x-x_i}{x_j-x_i} \)
</center>

Da expressão acima, podemos notar que diferentes graus de polinômios podem ser gerados. Por exemplo:

  * Polinômios de primeiro grau (interpolação linear):
           
    <center>
      \(y(x) = f_1(x) = \frac{x-x_1}{x_0 &#8211; x_1}f(x_0) + \frac{x-x_0}{x_1-x_0}f(x_1) \)
    </center>

  * Polinômios de segundo grau (interpolação quadrática):
            
    <center>
      \(y(x) = f_2(x) = \frac{(x-x_1)(x-x_2)}{(x_0-x_1)(x_0-x_2)}f(x_0) + \frac{(x-x0)(x-x2)}{(x_1-x_0)(x_1-x_2)}f(x_1) + \frac{(x-x_0)(x-x_1)}{(x_2-x_0)(x_2-x_1)}f(x_2) \)
    </center>

&nbsp;

## 2. Implementação 

<div>
  <pre lang="python">def interpolation_lagrange(x, x_j, f_j, n=0):
    """
    Return x evaluated in Lagrangian interpolation function.

    interpolation_lagrange(x, x_j, f_j)

    INPUT:
      * x: evalue at this point
      * x_j: LIST, tabular points
      * f_j: LIST, tabular points (must be same size of x_j)
      * n: polynom degree (optional)

    return:
      * y(x): interpolated and evaluated x value

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Oct 2010
    """

    if type(x_j) != type(f_j) or type(x_j) != type([]):
        print "Error: wrong type parameters"
        return float("NaN")

    if len(x_j) != len(f_j):
        print "Error: the tabular points must have same size"
        return float("NaN")

    if n &lt; = 0:
        n = len(x_j)
    else:
        n = n + 1

    p = 0.0
    for i in xrange(n):
        li = f_j[i]
        xi = x_j[i]
        for j in xrange(n):
            xj = x_j[j]
            if i != j:
                li = li * (x - xj) / (xi - xj)
        p += li
    return p</pre>
</div>

Esta função está disponível em <a href="http://www.sawp.com.br/code/interpolation/interpolation_lagrange.py" target="_blank">http://www.sawp.com.br/code/interpolation/interpolation_lagrange.py</a> assim como um exemplo de como utilizá-la. 

&nbsp;

## 3. Copyright 

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
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 69.</a>
  </p>
  
  <p>
    <a name="bibitem3" href='http://en.wikipedia.org/wiki/Rolle's_theorem'><b>[3]</b> http://en.wikipedia.org/wiki/Rolle&#8217;s_theorem </a>
  </p>
</fieldset>
