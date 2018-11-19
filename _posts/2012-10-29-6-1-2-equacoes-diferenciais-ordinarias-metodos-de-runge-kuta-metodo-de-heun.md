---
id: 1875
title: '6.1.2 Equações Diferenciais Ordinárias &#8212; Métodos de Runge-Kuta &#8212; Método de Heun'
date: 2012-10-29T11:06:19+00:00
author: SAWP
excerpt: O método de Heun é um melhoramento do método de Euler, que utiliza um processo preditor-corretor para resolver equações diferenciais ordinárias.
layout: post
guid: http://www.sawp.com.br/blog/?p=1875
permalink: p=1875
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:6282:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_heun<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> y0<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1e6</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration for solve ODE's using Heun's Method
    &nbsp;
    integral = integral_heun(f, xi, xe, n=1e6)
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
    <span style="color: #ff7700;font-weight:bold;">def</span> predictor<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> y + f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> * h
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> corrector<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    pred <span style="color: #66cc66;">=</span> predictor<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    corr <span style="color: #66cc66;">=</span> y + <span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> + f<span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> pred<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span> * h
    <span style="color: #ff7700;font-weight:bold;">return</span> corr
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> heun<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> corrector<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> heun<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> y
    &nbsp;
    <span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>y0<span style="color: #66cc66;">,</span> xi<span style="color: black;">&#41;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    <span style="color: #ff7700;font-weight:bold;">return</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def integral_heun(f, xi, xe, y0, n=1e6):
    &quot;&quot;&quot;
    Numerical integration for solve ODE's using Heun's Method
    
    integral = integral_heun(f, xi, xe, n=1e6)
    
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
    def predictor(x, y, h):
    return y + f(x, y) * h
    
    def corrector(x, y, h):
    pred = predictor(x, y, h)
    corr = y + (f(x, y) + f(x + h, pred)) / 2.0 * h
    return corr
    
    def heun(x, y, h):
    return (x + h, corrector(x, y, h))
    
    def integrator(x, y, h, n):
    for i in xrange(n):
    (x, y) = heun(x, y, h)
    return y
    
    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</p></div>
    ";}
categories:
  - Computational Methods
---
O método de Euler possui uma velocidade de convergência baixa porque utiliza a derivada do início do intervalo como média para o intervalo todo. Para melhorar a estimativa da inclinação, o método de Heun determina duas derivadas para o intervalo. A primeira derivada é tomada no início do intervalo e equivale àquela usada no método de Euler. A segunda é tomada no ponto final do intervalo. A partir dessas duas derivadas, tomamos a média delas para obter uma estimativa melhorada da inclinação no intervalo. 

Do método de Euler, tínhamos que
  


<center>
  \( y&#8217;_i = \dfrac{dy}{dx} = f(x_i, y_i) \)
</center>


  
era a inclinação do início do intervalo. Essa mesma equação pode ser usada para extrapolar a solução
  


<center>
  \( y_{i+1}^0 = y_i + f(x_i, y_i) h \)
</center>

No método de Euler, essa equação é a usada para solucionar o problema das EDOs. Contudo, no método de Heun, esta estimativa é usada como aproximação inicial do valor, chamado de &#8220;predita&#8221;. Assim, essa equação é chamada de _equação preditora_, pois ela fornece uma estimativa de \(y\_{i+1}\) que permite o cálculo da inclinação na extremidade final do intervalo. A figura abaixo mostra graficamente o valor predito (\(y\_{i+1}^0\)) e o corrigido (\(y_{i+1}\)). 

<a name="#fig1" href="http://www.sawp.com.br/blog/wp-content/uploads/2012/10/graph11.png"><img class="aligncenter size-full wp-image-416" title="" src="http://www.sawp.com.br/blog/wp-content/uploads/2012/10/graph11.png" alt="numerical" width="400" height="400" /></a> 

As duas inclinações podem ser combinadas para obter uma inclinação média do intervalo:
  


<center>
  \( \bar{y}&#8217; = \dfrac{y_i&#8217; + y_{i+1}&#8217;}{2} = \dfrac{f(x_i, y_i) + f(x_{i+1}, y_{i+1}^0)}{2} \)
</center>


  
Essa inclinação média é então usada para extrapolar a fórmula de Euler:
  


<center>
  \( y_{i+1} = y_i + \dfrac{f(x_i, y_i) + f(x_{i+1}, y_{i+1}^0)}{2} h \)
</center>

Esta abordagem de Heun é chamada do tipo _preditor-corretor_. Todos os métodos de passo múltiplos são dessa categoria. Uma característica interessante dessa abordagem é a capacidade de se acelerar a convergência das aproximações sucessivas. A figura abaixo ilustra a redução do erro de acordo com o número de divisões do intervalo de integração. Note que para o mesmo \(n\), o método de Heun decai o erro mais velozmente. 

<a name="#fig2" href="http://www.sawp.com.br/blog/wp-content/uploads/2012/10/graph2.gif"><img class="aligncenter size-full wp-image-416" title="" src="http://www.sawp.com.br/blog/wp-content/uploads/2012/10/graph2.gif" alt="numerical" width="588" height="400" /></a> 

&nbsp;

## 1. Implementação 

&nbsp;

<div>
  <pre lang="python">def integral_heun(f, xi, xe, y0, n=1e6):
    """
    Numerical integration for solve ODE's using Heun's Method

    integral = integral_heun(f, xi, xe, n=1e6)

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
    def predictor(x, y, h):
        return y + f(x, y) * h

    def corrector(x, y, h):
        pred = predictor(x, y, h)
        corr = y + (f(x, y) + f(x + h, pred)) / 2.0 * h
        return corr

    def heun(x, y, h):
        return (x + h, corrector(x, y, h))

    def integrator(x, y, h, n):
        for i in xrange(n):
            (x, y) = heun(x, y, h)
        return y

    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</pre>
</div>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/ode/heun.py" target="_blank">http://www.sawp.com.br/code/ode/heun.py</a>. 

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
