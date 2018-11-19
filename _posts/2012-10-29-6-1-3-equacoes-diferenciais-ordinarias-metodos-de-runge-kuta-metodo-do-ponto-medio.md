---
id: 1894
title: '6.1.3 Equações Diferenciais Ordinárias &#8212; Métodos de Runge-Kuta &#8212; Método do Ponto Médio'
date: 2012-10-29T15:53:17+00:00
author: SAWP
excerpt: A modificação do método de Euler que substitui a inclinação f(x,y) pelo valor do centro do intervalo, ou seja, pela inclinação da reta tangente em f(x+h/2, y(x)). No caso, y(x) = (y1 + y0)/2, é o ponto médio.
layout: post
guid: http://www.sawp.com.br/blog/?p=1894
permalink: p=1894
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5056:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_midpoint<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> y0<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1e6</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration for solve ODE's using Midpoint Method
    &nbsp;
    integral = integral_midpoint(f, xi, xe, n=1e6)
    &nbsp;
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * xi: beginning of integration interval
    * xe: end of integration interval
    * y0: initial estimative for y
    * n: number of points used
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
    <span style="color: #ff7700;font-weight:bold;">def</span> midpoint<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    pred <span style="color: #66cc66;">=</span> y + f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> * h / <span style="color: #ff4500;">2.0</span>
    corr <span style="color: #66cc66;">=</span> y + f<span style="color: black;">&#40;</span>x + h / <span style="color: #ff4500;">2.0</span><span style="color: #66cc66;">,</span> pred<span style="color: black;">&#41;</span> * h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> corr<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> midpoint<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> y
    &nbsp;
    <span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>y0<span style="color: #66cc66;">,</span> xi<span style="color: black;">&#41;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    <span style="color: #ff7700;font-weight:bold;">return</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def integral_midpoint(f, xi, xe, y0, n=1e6):
    &quot;&quot;&quot;
    Numerical integration for solve ODE's using Midpoint Method
    
    integral = integral_midpoint(f, xi, xe, n=1e6)
    
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * xi: beginning of integration interval
    * xe: end of integration interval
    * y0: initial estimative for y
    * n: number of points used
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Sep 2012
    &quot;&quot;&quot;
    def midpoint(x, y, h):
    pred = y + f(x, y) * h / 2.0
    corr = y + f(x + h / 2.0, pred) * h
    return (x + h, corr)
    
    def integrator(x, y, h, n):
    for i in xrange(n):
    (x, y) = midpoint(x, y, h)
    return y
    
    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</p></div>
    ";}
categories:
  - Computational Methods
---
O _método do ponto médio_ é uma abordagem do tipo preditor-corretor, que utiliza o método de Euler para prever um valor \(y \) no ponto médio do intervalo. Isto é,
  


<center>
  \( y_{i+1/2} = y_i + f(x_i, y_i) \frac{h}{2} \)
</center>


  
é usado como predito para calcular a inclinação do ponto médio:
  


<center>
  \( y_{i+1/2}&#8217; = f(x_{i+1/2}, y_{i+1/2}) \)
</center>


  
que é a aproximação da inclinação média para todo intervalo. Essa inclinação é então usada para extrapolar o novo valor de \(y\),
  


<center>
  \( y_{i+1} = y_i + f(x_{i+1/2}, y_{i+1/2}) h \)
</center>


  
que é a fórmula do método do ponto médio. 

&nbsp;

## 1. Implementação 

<div>
  <pre lang="python">def integral_midpoint(f, xi, xe, y0, n=1e6):
    """
    Numerical integration for solve ODE's using Midpoint Method

    integral = integral_midpoint(f, xi, xe, n=1e6)

    INPUT:
      * f: derivative function f(x, y) = dy/dx
      * xi: beginning of integration interval
      * xe: end of integration interval
      * y0: initial estimative for y
      * n: number of points used

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Sep 2012
    """
    def midpoint(x, y, h):
        pred = y + f(x, y) * h / 2.0
        corr = y + f(x + h / 2.0, pred) * h
        return (x + h, corr)

    def integrator(x, y, h, n):
        for i in xrange(n):
            (x, y) = midpoint(x, y, h)
        return y

    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</pre>
</div>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/ode/midpoint.py" target="_blank">http://www.sawp.com.br/code/ode/midpoint.py</a>. 

&nbsp;

## 2. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <br /> <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
