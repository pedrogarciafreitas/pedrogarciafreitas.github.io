---
id: 1758
title: '5.8 Integração Numérica &#8212; Método de Monte Carlo'
date: 2012-09-03T14:52:43+00:00
author: SAWP
excerpt: ' O Método de Monte Carlo é uma técnica heurística para avaliação ou estimação de problemas (geralmente intratáveis) usando simulação probabilística e amostragem.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1758
permalink: /p=1758
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3616:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_monte_carlo<span style="color: black;">&#40;</span>fun<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1e6</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using Tanh-sinh quadrature
    &nbsp;
    integral = integral_monte_carlo(fun, xi, xe, n=1e5)
    &nbsp;
    INPUT:
    * fun: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of points used by Monte Carlo Method
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Sep 2012
    &quot;&quot;&quot;</span>
    <span style="color: black;">&#40;</span>fmedio<span style="color: #66cc66;">,</span> i<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> i <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> n:
    x <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> * <span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span> + xi
    fmedio +<span style="color: #66cc66;">=</span> fun<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    i +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    fmedio /<span style="color: #66cc66;">=</span> n
    integral <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> * fmedio
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def integral_monte_carlo(fun, xi, xe, n=1e6):
    &quot;&quot;&quot;
    Numerical integration using Tanh-sinh quadrature
    
    integral = integral_monte_carlo(fun, xi, xe, n=1e5)
    
    INPUT:
    * fun: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of points used by Monte Carlo Method
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Sep 2012
    &quot;&quot;&quot;
    (fmedio, i, n) = (0.0, 0, int(n))
    while i &lt; = n:
    x = fabs(xe - xi) * random() + xi
    fmedio += fun(x)
    i += 1
    fmedio /= n
    integral = (xe - xi) * fmedio
    return integral</p></div>
    ";}
categories:
  - Computational Methods
---
<a name="#fig1" href="http://www.sawp.com.br/blog/wp-content/uploads/2012/09/integrate.png"><img class="aligncenter size-full wp-image-416" title="" src="http://www.sawp.com.br/blog/wp-content/uploads/2012/09/integrate.png" alt="numerical" width="576" height="360" /></a>

O Método de Monte Carlo é uma técnica heurística para avaliação ou estimação de problemas (geralmente intratáveis) usando simulação probabilística e amostragem. Um exemplo básico da utilização do Método de Monte Carlo é a integração de funções com uma variável. Isto é, a integral
  


<center>
  $$ I = \int_a^b f(x) dx $$
</center>


  
pode ser aproximada por
  


<center>
  $$ \hat{I} = \dfrac{b &#8211; a}{n} \sum_{i=1}^N f(x_i) $$
</center>


  
onde todas $$x_i $$ são observações independentes de uma distribuição uniforme no intervalo $$[a,b] $$. Assim, como a esperança $$E(\hat{I}) = I $$, temos que a precisão aumenta com o aumento no número de amostras $$n $$. 

&nbsp;

## Implementação 

&nbsp;

<pre lang="python">def integral_monte_carlo(fun, xi, xe, n=1e6):
    """
    Numerical integration using Tanh-sinh quadrature

    integral = integral_monte_carlo(fun, xi, xe, n=1e5)

    INPUT:
      * fun: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * n: number of points used by Monte Carlo Method

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Sep 2012
    """
    (fmedio, i, n) = (0.0, 0, int(n))
    while i &lt; = n:
        x = fabs(xe - xi) * random() + xi
        fmedio += fun(x)
        i += 1
    fmedio /= n
    integral = (xe - xi) * fmedio
    return integral</pre>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integral_monte_carlo.py" target="_blank">http://sawp.com.br/code/integral/integral_monte_carlo.py</a>. 

&nbsp;

## Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
