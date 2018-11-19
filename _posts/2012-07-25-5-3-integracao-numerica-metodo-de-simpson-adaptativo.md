---
id: 1658
title: '5.3 Integração Numérica &#8212; Método de Simpson Adaptativo'
date: 2012-07-25T18:39:38+00:00
author: SAWP
excerpt: ' A regra de Simpson adaptativa é um algoritmo recursivo de integração numérica que usa uma estimativa do erro para calcular uma integral definida através de múltiplas aplicações do método de Simpson. Como em muitas abordagens numéricas, se o erro estimado ultrapassa um erro tolerado, o algoritmo divide o intervalo de integração em dois sub-intervalos e reaplica o método de Simpson nesses intervalos de forma independente, somando os resultados. Essa técnica acaba por ser mais eficiente que outros métodos de integração por convergir quadraticamente ao resultado.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1658
permalink: /p=1658
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8090:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> adaptative_simpson<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10e-10</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using the Adaptative Simpson's Rule.
    &nbsp;
    integral = adaptative_simpson(f, xi, xe, errto=10e-10)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * errto: numerical error tolerated in the integration
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> simpson_rule<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    middle_point <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>a + b<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>a - b<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">6.0</span>
    n <span style="color: #66cc66;">=</span> g<span style="color: black;">&#40;</span>a<span style="color: black;">&#41;</span> + <span style="color: #ff4500;">4.0</span> * g<span style="color: black;">&#40;</span>middle_point<span style="color: black;">&#41;</span> + g<span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    integral <span style="color: #66cc66;">=</span> h * n
    <span style="color: #ff7700;font-weight:bold;">return</span> integral
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> apply_simpson_rule<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    middle_point <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>a + b<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    left <span style="color: #66cc66;">=</span> simpson_rule<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> middle_point<span style="color: black;">&#41;</span>
    right <span style="color: #66cc66;">=</span> simpson_rule<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> middle_point<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>left<span style="color: #66cc66;">,</span> middle_point<span style="color: #66cc66;">,</span> right<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> recursion<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> <span style="color: #dc143c;">errno</span><span style="color: #66cc66;">,</span> integral<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>left<span style="color: #66cc66;">,</span> middle<span style="color: #66cc66;">,</span> right<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> apply_simpson_rule<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    adap <span style="color: #66cc66;">=</span> left + right - integral
    err <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>adap<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">15.0</span>
    rec <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> z: recursion<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> <span style="color: #dc143c;">errno</span> / <span style="color: #ff4500;">2.0</span><span style="color: #66cc66;">,</span> z<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> err <span style="color: #66cc66;">&lt;</span> <span style="color: #dc143c;">errno</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> left + right + adap / <span style="color: #ff4500;">15.0</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> rec<span style="color: black;">&#40;</span>a<span style="color: #66cc66;">,</span> middle<span style="color: #66cc66;">,</span> left<span style="color: black;">&#41;</span> + rec<span style="color: black;">&#40;</span>middle<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> right<span style="color: black;">&#41;</span>
    integral <span style="color: #66cc66;">=</span> recursion<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">,</span> simpson_rule<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def adaptative_simpson(f, xi, xe, errto=10e-10):
    &quot;&quot;&quot;
    Numerical integration using the Adaptative Simpson's Rule.
    
    integral = adaptative_simpson(f, xi, xe, errto=10e-10)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * errto: numerical error tolerated in the integration
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    def simpson_rule(g, a, b):
    middle_point = (a + b) / 2.0
    h = abs(a - b) / 6.0
    n = g(a) + 4.0 * g(middle_point) + g(b)
    integral = h * n
    return integral
    
    def apply_simpson_rule(g, a, b):
    middle_point = (a + b) / 2.0
    left = simpson_rule(g, a, middle_point)
    right = simpson_rule(g, middle_point, b)
    return (left, middle_point, right)
    
    def recursion(g, a, b, errno, integral):
    (left, middle, right) = apply_simpson_rule(g, a, b)
    adap = left + right - integral
    err = abs(adap) / 15.0
    rec = lambda x, y, z: recursion(g, x, y, errno / 2.0, z)
    if err &lt; errno:
    return left + right + adap / 15.0
    else:
    return rec(a, middle, left) + rec(middle, b, right)
    integral = recursion(f, xi, xe, errto, simpson_rule(f, xi, xe))
    return integral</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

A regra de Simpson adaptativa é um algoritmo recursivo de integração numérica que usa uma estimativa do erro para calcular uma integral definida através de múltiplas aplicações do método de Simpson. Como em muitas abordagens numéricas, se o erro estimado ultrapassa um erro tolerado, o algoritmo divide o intervalo de integração em dois sub-intervalos e reaplica o método de Simpson nesses intervalos de forma independente, somando os resultados. Essa técnica acaba por ser mais eficiente que outros métodos de integração por convergir quadraticamente ao resultado. 

&nbsp;

## 2. O Método 

Seja $$S(a,b) $$ o resultado da aproximação da integral utilizando a regra de Simpson &#8212; $$1/3 $$ ou $$3/4 $$ &#8212; no intervalo $$[a,b] $$ . Assim,
  


<center>
  $$ I = S(a,b) = \int_{a}^{b} f(x) dx \approx \int_a^b f_2(x) dx $$
</center>


  
O critério de parada da sub-divisão dos intervalos é calculado pela seguinte equação 

<center>
  $$ \dfrac{S(a,m) + S(m, b) &#8211; S(a,b)}{15} < \epsilon [/latex]
</center>


  
com
  
</center>

<center>
  [latex] m = \dfrac{b-a}{2} $$
</center>


  
onde $$m $$ é o ponto médio do intervalo $$[a,b]$$ e $$\epsilon$$ é o erro tolerado para o intervalo. 

&nbsp;

## 3. Implementação 

A implementação utilizando as fórmulas indutivas é

<pre lang="python">def adaptative_simpson(f, xi, xe, errto=10e-10):
    """
    Numerical integration using the Adaptative Simpson's Rule.

    integral = adaptative_simpson(f, xi, xe, errto=10e-10)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * errto: numerical error tolerated in the integration

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    def simpson_rule(g, a, b):
        middle_point = (a + b) / 2.0
        h = abs(a - b) / 6.0
        n = g(a) + 4.0 * g(middle_point) + g(b)
        integral = h * n
        return integral

    def apply_simpson_rule(g, a, b):
        middle_point = (a + b) / 2.0
        left = simpson_rule(g, a, middle_point)
        right = simpson_rule(g, middle_point, b)
        return (left, middle_point, right)

    def recursion(g, a, b, errno, integral):
        (left, middle, right) = apply_simpson_rule(g, a, b)
        adap = left + right - integral
        err = abs(adap) / 15.0
        rec = lambda x, y, z: recursion(g, x, y, errno / 2.0, z)
        if err &lt; errno:
            return left + right + adap / 15.0
        else:
            return rec(a, middle, left) + rec(middle, b, right)
    integral = recursion(f, xi, xe, errto, simpson_rule(f, xi, xe))
    return integral  </pre>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integral_adaptative_simpson.py" target="_blank">http://www.sawp.com.br/code/integral/integral_adaptative_simpson.py</a>. 

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a>
  </p></p> 
  
  <p>
    <a name="bibitem3"><b>[2]</b> Guy F. Kuncir,<cite> <em>Algorithm 103: Simpson's rule integrator</em>,</cite> Communications of the ACM 5 (6): 347.</a>
  </p></p> 
  
  <p>
    <a name="bibitem2"><b>[3]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p></p>
</fieldset>
