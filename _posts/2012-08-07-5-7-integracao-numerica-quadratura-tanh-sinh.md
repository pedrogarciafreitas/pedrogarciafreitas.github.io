---
id: 1745
title: '5.7 Integração Numérica &#8212; Quadratura tanh-sinh'
date: 2012-08-07T20:23:13+00:00
author: SAWP
excerpt: 'Quadratura de tanh-sinh  é um método para a integração numérica introduzido por Hidetosi Takahasi e Mori Masatake em 1974.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1745
permalink: p=1745
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8754:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_tanhsinh_quadrature<span style="color: black;">&#40;</span>fun<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">12</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using Tanh-sinh quadrature
    &nbsp;
    integral = integral_tanhsinh_quadrature(fun, xi, xe, n=12)
    &nbsp;
    INPUT:
    * fun: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of points used in quadrature
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
    <span style="color: #ff7700;font-weight:bold;">def</span> convert_intervals<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    frac <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    xd <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> x: <span style="color: black;">&#40;</span>xe + xi + <span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> * x<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    f <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> x: fun<span style="color: black;">&#40;</span>xd<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * frac
    <span style="color: #ff7700;font-weight:bold;">return</span> f
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> compute_quadrature_weights<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    w_num <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> k: <span style="color: #ff4500;">0.5</span> * h * pi * cosh<span style="color: black;">&#40;</span>k * h<span style="color: black;">&#41;</span>
    w_den <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> k: cosh<span style="color: black;">&#40;</span><span style="color: #ff4500;">0.5</span> * pi * sinh<span style="color: black;">&#40;</span>k * h<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> ** <span style="color: #ff4500;">2</span>
    w <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> k: w_num<span style="color: black;">&#40;</span>k<span style="color: black;">&#41;</span> / w_den<span style="color: black;">&#40;</span>k<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#91;</span>w<span style="color: black;">&#40;</span>k<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>-n<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> compute_abcissas<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    x <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> k: tanh<span style="color: black;">&#40;</span><span style="color: #ff4500;">0.5</span> * pi * sinh<span style="color: black;">&#40;</span>k * h<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#91;</span>x<span style="color: black;">&#40;</span>k<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>-n<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> compute_quadrature<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    s <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span> ** n
    h <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">4.0</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span> ** n<span style="color: black;">&#41;</span>
    f <span style="color: #66cc66;">=</span> convert_intervals<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    w <span style="color: #66cc66;">=</span> compute_quadrature_weights<span style="color: black;">&#40;</span>s<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> compute_abcissas<span style="color: black;">&#40;</span>s<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    quad <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>w<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * f<span style="color: black;">&#40;</span>x<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span>quad<span style="color: black;">&#41;</span>
    &nbsp;
    integral <span style="color: #66cc66;">=</span> compute_quadrature<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def integral_tanhsinh_quadrature(fun, xi, xe, n=12):
    &quot;&quot;&quot;
    Numerical integration using Tanh-sinh quadrature
    
    integral = integral_tanhsinh_quadrature(fun, xi, xe, n=12)
    
    INPUT:
    * fun: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of points used in quadrature
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    def convert_intervals():
    frac = (xe - xi) / 2.0
    xd = lambda x: (xe + xi + (xe - xi) * x) / 2.0
    f = lambda x: fun(xd(x)) * frac
    return f
    
    def compute_quadrature_weights(n, h):
    w_num = lambda k: 0.5 * h * pi * cosh(k * h)
    w_den = lambda k: cosh(0.5 * pi * sinh(k * h)) ** 2
    w = lambda k: w_num(k) / w_den(k)
    return [w(k) for k in xrange(-n, n)]
    
    def compute_abcissas(n, h):
    x = lambda k: tanh(0.5 * pi * sinh(k * h))
    return [x(k) for k in xrange(-n, n)]
    
    def compute_quadrature(n):
    s = 2 ** n
    h = 4.0 / (2 ** n)
    f = convert_intervals()
    w = compute_quadrature_weights(s, h)
    x = compute_abcissas(s, h)
    quad = [w[k] * f(x[k]) for k in xrange(len(x))]
    return sum(quad)
    
    integral = compute_quadrature(n)
    return integral</p></div>
    ";}
categories:
  - Computational Methods
---
A quadratura _tanh-sinh_ é um método de integração numérica que utiliza a seguinte mudança de variáveis para transformar uma integral definida no intervalo \([-1,1] \) em um somatório infinito:
  


<center>
  \( x = tanh \left(\frac{1}{2}~\pi~sinh~t \right) \)
</center>


  
Após essa transformação, os integrandos decaem com uma proporção exponencial. Para um dado passo de tamanho \(h \) , a integral pode ser aproximada por
  


<center>
  \( \int_{-1}^1 f(x) dx \approx \sum_{k=-\infty}^{\infty} H_k f(a_k) \)
</center>


  
com as abcissas
  


<center>
  \( a_k = tanh\left(\frac{1}{2} \pi ~ sinh(k h) \right) \)
</center>


  
e pesos
  


<center>
  \( H_k = \dfrac{\frac{1}{2} h \pi ~ cosh(k h)}{cosh^2 \left(\frac{1}{2} \pi ~ sinh(k h) \right)} \)
</center>

Assim como na quadratura gaussiana, a quadratura _tanh-sinh_ é adequada para integração de funções quaisquer. A convergência dessa fórmula é exponencial em base dois (em relação ao número de divisões). Ou seja, duplicando-se \(n \) temos que o número de dígitos corretos dobra também, sendo o método de quadratura que possui a maior velocidade de convergência conhecido. 

&nbsp;

### Escolha do tamanho do passo de discretização (h) 

Há uma relação entre o número de pontos usados na soma ( \(n \) ) e o tamanho do passo que deve ser preservada. O \(h \) deve ser escolhido da seguinte forma
  


<center>
  \( h = \frac{4}{2^n} \)
</center>

&nbsp;

## Implementação 

<pre lang="python">def integral_tanhsinh_quadrature(fun, xi, xe, n=12):
    """
    Numerical integration using Tanh-sinh quadrature

    integral = integral_tanhsinh_quadrature(fun, xi, xe, n=12)

    INPUT:
      * fun: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * n: number of points used in quadrature

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    def convert_intervals():
        frac = (xe - xi) / 2.0
        xd = lambda x: (xe + xi + (xe - xi) * x) / 2.0
        f = lambda x: fun(xd(x)) * frac
        return f

    def compute_quadrature_weights(n, h):
        w_num = lambda k: 0.5 * h * pi * cosh(k * h)
        w_den = lambda k: cosh(0.5 * pi * sinh(k * h)) ** 2
        w = lambda k: w_num(k) / w_den(k)
        return [w(k) for k in xrange(-n, n)]

    def compute_abcissas(n, h):
        x = lambda k: tanh(0.5 * pi * sinh(k * h))
        return [x(k) for k in xrange(-n, n)]

    def compute_quadrature(n):
        s = 2 ** n
        h = 4.0 / (2 ** n)
        f = convert_intervals()
        w = compute_quadrature_weights(s, h)
        x = compute_abcissas(s, h)
        quad = [w[k] * f(x[k]) for k in xrange(len(x))]
        return sum(quad)

    integral = compute_quadrature(n)
    return integral</pre>

Um exemplo de utilização dessas funções pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integral_tan_sinh_quadrature.py" target="_blank">http://www.sawp.com.br/code/integral/integral_tan_sinh_quadrature.py</a>. 

&nbsp;

## 2. Copyright 

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
