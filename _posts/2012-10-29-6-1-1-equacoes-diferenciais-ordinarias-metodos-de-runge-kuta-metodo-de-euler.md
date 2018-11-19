---
id: 1859
title: '6.1.1 Equações Diferenciais Ordinárias &#8212; Métodos de Runge-Kuta &#8212; Método de Euler'
date: 2012-10-29T09:50:43+00:00
author: SAWP
excerpt: O método de Euler é o método mais básico de método explícito para integração numérica para equações diferenciais ordinárias.
layout: post
guid: http://www.sawp.com.br/blog/?p=1859
permalink: /p=1859
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4625:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_euler<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> y0<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1e6</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration for solve ODE's using Euler's Method
    &nbsp;
    integral = integral_euler(f, xi, xe, n=1e6)
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
    <span style="color: #ff7700;font-weight:bold;">def</span> euler<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> y + f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> * h<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> euler<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> y
    &nbsp;
    <span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>y0<span style="color: #66cc66;">,</span> xi<span style="color: black;">&#41;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    <span style="color: #ff7700;font-weight:bold;">return</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def integral_euler(f, xi, xe, y0, n=1e6):
    &quot;&quot;&quot;
    Numerical integration for solve ODE's using Euler's Method
    
    integral = integral_euler(f, xi, xe, n=1e6)
    
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
    def euler(x, y, h):
    return (x + h, y + f(x, y) * h)
    
    def integrator(x, y, h, n):
    for i in xrange(n):
    (x, y) = euler(x, y, h)
    return y
    
    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

O método de Euler é um algoritmo destinado à solução de equações diferenciais na forma
  


<center>
  $$ \dfrac{dy}{dx} = f(x,y) $$
</center>


  
onde $$y = y(x) $$ . A solução analítica da equação diferencial ordinária (EDO) é justamente encontrar a equação que expressa $$y(x) $$ . Por outro lado, quando utilizamos uma abordagem numérica, a solução retorna $$y(x) $$ avaliado em $$x$$. 

Os métodos de Runge-Kuta são iterativos sobre a estimativa das variáveis e buscam aproximar a solução $$y = y(x) $$ através de sucessivos passos. Temos que
  


<center>
  $$ y_i = y_{i-1} + \phi h $$
</center>


  
onde $$\phi $$ é a estimativa da inclinação (derivada), usada como estimadora dos novos valores ($$y\_i $$) a partir de valores prévios ($$y\_{i-1} $$) em uma distância $$h$$ (extrapolada). A figura abaixo mostra esta extrapolação. 

<a name="#fig1" href="http://www.sawp.com.br/blog/wp-content/uploads/2012/10/graph1-300x300.png"><img class="aligncenter size-full wp-image-416" title="" src="http://www.sawp.com.br/blog/wp-content/uploads/2012/10/graph1-300x300.png" alt="numerical" width="400" height="400" /></a> 

Todos os métodos de passo único possuem esta abordagem, sendo que se diferenciam pela forma em que $$\phi $$ é estimado. Assim, a forma mais ingênua consiste em utilizar a própria equação diferencial (com o $$y&#8217; $$ isolado) como inclinação da reta. Isto é, a inclinação no início do intervalo é tomada como uma inclinação média de todo intervalo. Tal abordagem simplista é utilizada no _método de Euler_. Outras abordagem são conhecidas como métodos de Runge-Kuta de ordens superior. 

&nbsp;

## 2. Método de Euler 

Conforme comentamos na seção anterior, o método de Euler utiliza a primeira derivada como estimativa direta da inclinação em $$x_i $$ . Isto é,
  


<center>
  $$ \phi = \dfrac{dy}{dx} = f(x,y) $$
</center>


  
Assim, a solução será dada por
  


<center>
  $$ y_i = y_{i-1} + f(x_{i-1}, y_{i-1}) h $$
</center>

&nbsp;

### 2.1. Exemplo 

Supondo que precisamos resolver a seguinte equação:
  


<center>
  $$ \dfrac{dy}{dx} = x + y $$
</center>


  
Sabemos que esta equação está na forma
  


<center>
  $$ \dfrac{dy}{dx} &#8211; ay = g(x) $$
</center>


  
que possui solução
  


<center>
  $$ y = e^{-ax} \int_{x_0}^{x} e^{as} g(s) ds + c e^{-at} $$
</center>


  
onde $$a=-1 $$ e $$g(x)=x $$ . Para $$x_0 = 0 $$ , temos que a solução analítica da EDO em questão será
  


<center>
  $$ y(x) = -1 -x + c e^x $$
</center>


  
Ou seja, a solução é sempre integral, por isso o método de Euler soluciona em um intervalo de integração. Assim, supondo que queremos integrar $$f(x,y)$$ no intervalo $$x \in [0,1] $$ com condições iniciais $$x=0 $$, $$y(x=0)=-1-0+ce^0=0 $$ e passo de tamanho 0.5, temos que
  


<center>
  $$ y(0.5) = y(0) + f(0, 1) 0.5 $$
</center>


  
onde $$y=1 $$ , então $$f(0.1) = 0 + 1 = 1 $$ . Portanto, a aproximação no primeiro passo será
  


<center>
  $$ y(0.5) = 1 + 1 * 0.5 = 1.5 $$
</center>


  
Novamente repetimos este processo, seguindo para $$y(0.5 + h) = y(1)$$, refinando a aproximação. Como esse processo é repetitivo e monótono, utilizamos ele no exemplo de implementação. 

&nbsp;

## 3. Implementação 

&nbsp;

<div>
  <pre lang="python">def integral_euler(f, xi, xe, y0, n=1e6):
    """
    Numerical integration for solve ODE's using Euler's Method

    integral = integral_euler(f, xi, xe, n=1e6)

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
    def euler(x, y, h):
        return (x + h, y + f(x, y) * h)

    def integrator(x, y, h, n):
        for i in xrange(n):
            (x, y) = euler(x, y, h)
        return y

    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</pre>
</div>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/ode/euler.py" target="_blank">http://www.sawp.com.br/code/ode/euler.py</a>. 

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <br /> <a name="bibitem1"><b>[1]</b>Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b>N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
