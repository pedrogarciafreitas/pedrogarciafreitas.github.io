---
id: 1930
title: 6.1.8 Equações Diferenciais Ordinárias — Métodos de Runge-Kuta — Runge-Kutta Adaptativo (Fehlberg-Cash-Karp)
date: 2013-03-04T10:04:24+00:00
author: SAWP
excerpt: Nest post é apresentado o método de Fehlberg, que é uma abordagem que permite calcular o RK de quarta e quinta ordens sem necessitar repetir todos os passos em cada uma delas, o que economiza recursos computacionais. Esse tipo de abordagem favorece, por exemplo, a seleção inteligente do tamanho do passo usado pelos métodos de Runge-Kutta. Essa "escolha inteligente" do tamanho do passo é conhecida como "adaptativa".
layout: post
guid: http://www.sawp.com.br/blog/?p=1930
permalink: p=1930
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:9800:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> fehlberg<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Solve unique step using 4th and 5th order of Fehlberg's method
    &nbsp;
    (y_5ordem, y_4ordem) = fehlberg(f, x, y, h)
    &nbsp;
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * x: local x position
    * y: partially computed y
    * h: previous partition size
    &nbsp;
    return: (y_5ordem, y_4ordem)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2013
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> compute_coeffs<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">1.0</span>/<span style="color: #ff4500;">5.0</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">1.0</span>/<span style="color: #ff4500;">5.0</span> * k1 * h<span style="color: black;">&#41;</span>
    k3 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">3.0</span>/<span style="color: #ff4500;">10.0</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">3.0</span>/<span style="color: #ff4500;">40.0</span> * k1 * h + <span style="color: #ff4500;">9.0</span>/<span style="color: #ff4500;">40.0</span> * k2 * h<span style="color: black;">&#41;</span>
    k4 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">3.0</span>/<span style="color: #ff4500;">5.0</span> * h<span style="color: #66cc66;">,</span>
    y + <span style="color: #ff4500;">3.0</span>/<span style="color: #ff4500;">10.0</span> * k1 * h - <span style="color: #ff4500;">9.0</span>/<span style="color: #ff4500;">10.0</span> * k2 * h + <span style="color: #ff4500;">6.0</span>/<span style="color: #ff4500;">5.0</span> * k3 * h<span style="color: black;">&#41;</span>
    k5 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> y - <span style="color: #ff4500;">11.0</span>/<span style="color: #ff4500;">54.0</span> * k1 * h + <span style="color: #ff4500;">5.0</span> / <span style="color: #ff4500;">2.0</span> * k2 * h -
    <span style="color: #ff4500;">70.0</span> / <span style="color: #ff4500;">27</span> * k3 * h + <span style="color: #ff4500;">35.0</span> / <span style="color: #ff4500;">27.0</span> * k4 * h<span style="color: black;">&#41;</span>
    k6 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">7.0</span> / <span style="color: #ff4500;">8.0</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">1631.0</span> / <span style="color: #ff4500;">55296</span> * k1 * h +
    <span style="color: #ff4500;">175.0</span> / <span style="color: #ff4500;">512</span> * k2 * h + <span style="color: #ff4500;">575.0</span> / <span style="color: #ff4500;">13824</span> * k3 * h +
    <span style="color: #ff4500;">44275.0</span> / <span style="color: #ff4500;">110592</span> * k4 * h + <span style="color: #ff4500;">253.0</span> / <span style="color: #ff4500;">4096</span> * k5 * h<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>k1<span style="color: #66cc66;">,</span> k2<span style="color: #66cc66;">,</span> k3<span style="color: #66cc66;">,</span> k4<span style="color: #66cc66;">,</span> k5<span style="color: #66cc66;">,</span> k6<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> fehlberg5order<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> coeffs<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>k1<span style="color: #66cc66;">,</span> k2<span style="color: #66cc66;">,</span> k3<span style="color: #66cc66;">,</span> k4<span style="color: #66cc66;">,</span> k5<span style="color: #66cc66;">,</span> k6<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> coeffs
    delta <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.102</span> * k1 + <span style="color: #ff4500;">0.384</span> * k3 + <span style="color: #ff4500;">0.244</span> * k4 + <span style="color: #ff4500;">0.019</span> * k5 + <span style="color: #ff4500;">0.25</span> * k6
    y1_5ordem <span style="color: #66cc66;">=</span> y + delta * h
    <span style="color: #ff7700;font-weight:bold;">return</span> y1_5ordem
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> fehlberg4order<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> coeffs<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>k1<span style="color: #66cc66;">,</span> k2<span style="color: #66cc66;">,</span> k3<span style="color: #66cc66;">,</span> k4<span style="color: #66cc66;">,</span> k5<span style="color: #66cc66;">,</span> k6<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> coeffs
    delta <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.097</span> * k1 + <span style="color: #ff4500;">0.402</span> * k3 + <span style="color: #ff4500;">0.210</span> * k4 + <span style="color: #ff4500;">0.289</span> * k6
    y1_4ordem <span style="color: #66cc66;">=</span> y + delta * h
    <span style="color: #ff7700;font-weight:bold;">return</span> y1_4ordem
    &nbsp;
    coeffs <span style="color: #66cc66;">=</span> compute_coeffs<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    y1_5ordem <span style="color: #66cc66;">=</span> fehlberg5order<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> coeffs<span style="color: black;">&#41;</span>
    y1_4ordem <span style="color: #66cc66;">=</span> fehlberg4order<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> coeffs<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>y1_5ordem<span style="color: #66cc66;">,</span> y1_4ordem<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def fehlberg(f, x, y, h):
    &quot;&quot;&quot;
    Solve unique step using 4th and 5th order of Fehlberg's method
    
    (y_5ordem, y_4ordem) = fehlberg(f, x, y, h)
    
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * x: local x position
    * y: partially computed y
    * h: previous partition size
    
    return: (y_5ordem, y_4ordem)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2013
    &quot;&quot;&quot;
    def compute_coeffs(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 1.0/5.0 * h, y + 1.0/5.0 * k1 * h)
    k3 = f(x + 3.0/10.0 * h, y + 3.0/40.0 * k1 * h + 9.0/40.0 * k2 * h)
    k4 = f(x + 3.0/5.0 * h,
    y + 3.0/10.0 * k1 * h - 9.0/10.0 * k2 * h + 6.0/5.0 * k3 * h)
    k5 = f(x + h, y - 11.0/54.0 * k1 * h + 5.0 / 2.0 * k2 * h -
    70.0 / 27 * k3 * h + 35.0 / 27.0 * k4 * h)
    k6 = f(x + 7.0 / 8.0 * h, y + 1631.0 / 55296 * k1 * h +
    175.0 / 512 * k2 * h + 575.0 / 13824 * k3 * h +
    44275.0 / 110592 * k4 * h + 253.0 / 4096 * k5 * h)
    return (k1, k2, k3, k4, k5, k6)
    
    def fehlberg5order(f, x, y, h, coeffs):
    (k1, k2, k3, k4, k5, k6) = coeffs
    delta = 0.102 * k1 + 0.384 * k3 + 0.244 * k4 + 0.019 * k5 + 0.25 * k6
    y1_5ordem = y + delta * h
    return y1_5ordem
    
    def fehlberg4order(f, x, y, h, coeffs):
    (k1, k2, k3, k4, k5, k6) = coeffs
    delta = 0.097 * k1 + 0.402 * k3 + 0.210 * k4 + 0.289 * k6
    y1_4ordem = y + delta * h
    return y1_4ordem
    
    coeffs = compute_coeffs(f, x, y, h)
    y1_5ordem = fehlberg5order(f, x, y, h, coeffs)
    y1_4ordem = fehlberg4order(f, x, y, h, coeffs)
    return (y1_5ordem, y1_4ordem)</p></div>
    ;i:2;s:5242:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> adapt_folberg<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1e-6</span><span style="color: #66cc66;">,</span> safety<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.5</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Solve each point and find partial y, adjusting h
    &nbsp;
    (x, y, h) = adapt_folberg(f, x, y, h, errto=1e-6, safety=0.5)
    &nbsp;
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * x: local x position
    * y: partially computed y
    * h: previous partition size
    * errto: acceptable approximation error
    * safety: control the h rescaling
    &nbsp;
    return: (x, y, h)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2013
    &quot;&quot;&quot;</span>
    err <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> err <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">1</span>:
    <span style="color: black;">&#40;</span>y1_5ordem<span style="color: #66cc66;">,</span> y1_4ordem<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> fehlberg<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    y <span style="color: #66cc66;">=</span> y1_5ordem
    yscal <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>y<span style="color: black;">&#41;</span> + <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>h * f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + <span style="color: #ff4500;">1e-30</span>
    yerr <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>y1_5ordem - y1_4ordem<span style="color: black;">&#41;</span>
    err <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>yerr / yscal / errto<span style="color: black;">&#41;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">max</span><span style="color: black;">&#40;</span><span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>safety * h * err ** <span style="color: black;">&#40;</span>-<span style="color: #ff4500;">0.25</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0.25</span> * <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>h<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> err <span style="color: #66cc66;">&gt;</span> errto:
    h <span style="color: #66cc66;">=</span> safety * h * err ** <span style="color: black;">&#40;</span>-<span style="color: #ff4500;">0.2</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    h <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">4</span> * h
    x <span style="color: #66cc66;">=</span> x + h</pre></td></tr></table><p class="theCode" style="display:none;">def adapt_folberg(f, x, y, h, errto=1e-6, safety=0.5):
    &quot;&quot;&quot;
    Solve each point and find partial y, adjusting h
    
    (x, y, h) = adapt_folberg(f, x, y, h, errto=1e-6, safety=0.5)
    
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * x: local x position
    * y: partially computed y
    * h: previous partition size
    * errto: acceptable approximation error
    * safety: control the h rescaling
    
    return: (x, y, h)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2013
    &quot;&quot;&quot;
    err = errto + 1
    while err &gt; 1:
    (y1_5ordem, y1_4ordem) = fehlberg(f, x, y, h)
    y = y1_5ordem
    yscal = abs(y) + abs(h * f(x, y)) + 1e-30
    yerr = abs(y1_5ordem - y1_4ordem)
    err = abs(yerr / yscal / errto)
    h = max(abs(safety * h * err ** (-0.25)), 0.25 * abs(h))
    if err &gt; errto:
    h = safety * h * err ** (-0.2)
    else:
    h = 4 * h
    x = x + h</p></div>
    ;i:3;s:4853:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_adapt<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> y0<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1e10</span><span style="color: #66cc66;">,</span> method<span style="color: #66cc66;">=</span>adapt_folberg<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration for solve ODE's using Runge-Kuta (adaptative)
    &nbsp;
    integral = integral_adapt(f, xi, xe, n=1e6)
    &nbsp;
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * xi: beginning of integration interval
    * xe: end of integration interval
    * y0: initial estimative for y
    * n: number of points used
    * method: method used to solve a unique step (adapt_folberg)
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2013
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> i <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> n <span style="color: #ff7700;font-weight:bold;">and</span> x <span style="color: #66cc66;">&lt;=</span> xe:
    i +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x + h <span style="color: #66cc66;">&gt;</span> xe:
    h <span style="color: #66cc66;">=</span> xe - x
    <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> adapt_folberg<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> y
    &nbsp;
    <span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>y0<span style="color: #66cc66;">,</span> xi<span style="color: black;">&#41;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    <span style="color: #ff7700;font-weight:bold;">return</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def integral_adapt(f, xi, xe, y0, n=1e10, method=adapt_folberg):
    &quot;&quot;&quot;
    Numerical integration for solve ODE's using Runge-Kuta (adaptative)
    
    integral = integral_adapt(f, xi, xe, n=1e6)
    
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * xi: beginning of integration interval
    * xe: end of integration interval
    * y0: initial estimative for y
    * n: number of points used
    * method: method used to solve a unique step (adapt_folberg)
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2013
    &quot;&quot;&quot;
    def integrator(x, y, h, n):
    i = 0
    while i &lt; = n and x &lt;= xe:
    i += 1
    if x + h &gt; xe:
    h = xe - x
    (x, y, h) = adapt_folberg(f, x, y, h)
    return y
    
    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</p></div>
    ";}
categories:
  - Computational Methods
---
Todos métodos numéricos para solução de EDOs apresentados nos posts anteriores utilizam passos de tamanho constante. Conforme ilustrado nesses posts, para diversos problemas essa abordagem é satisfatória. Contudo, algumas funções podem ter taxas de variações muito diferentes ao longo do espaço em que estão definidas, o que pode limitar seriamente a escolha do tamanho do passo. 

Sendo assim, alguns algoritmos ajustam o tamanho do passo de acordo com a trajetória da solução. Dessa forma, chamam-se tais métodos de &#8220;adaptativos&#8221;, pois eles adaptam o tamanho do passo de acordo com a taxa de crescimento local da função. Portanto, a implementação dessas abordagens adaptativas requer que uma estimativa do erro de aproximação local seja obtida em cada passo, servindo de base para a estimativa do novo tamanho de passo. 

Há duas abordagens para calcular o tamanho do passo de forma adaptativa. A primeira delas calcula o erro entre duas previsões, usando um dado método de Runge-Kutta de mesma ordem, mas com tamanho de passos diferentes. A outra abordagem consiste em estimar o erro de truncamento local a partir da diferença entre duas previsões, usando métodos de Runge-Kutta de ordens diferentes. 

&nbsp;

## 1. Runge-Kutta Adaptativo 

O método de RK adaptativo consiste em fazer cada passo duas vezes, uma com um passo completo e outra com dois meio-passos. A diferença dos dois resultados fornece uma estimativa do erro local. Assim, sendo \(y\_1 \) a previsão de passo único e \(y\_2 \) a previsão a partir de dois meio-passos, o erro \(\Delta\) é obtido como a diferença simples entre essas previsões,
  


<center>
  <br /> \(\Delta = y_2 &#8211; y_1\) .<br />
</center>


  
Além de fornecer um critério para o controle do tamanho do passo, a equação acima também é usada para correção na previsão de \(y\_2 \) . Em outras palavras, para métodos de Runge-Kutta de até quinta ordem, \(y\_2 \) pode ser corrigida por
  


<center>
  <br /> \(y2 = y2 + \dfrac{\Delta}{15} \) .<br />
</center>

&nbsp;

## 2. Runge-Kutta-Fehlberg 

Uma outra abordagem para obter a estimativa do erro consiste em calcular duas previsões, usando métodos de Runge-Kutta de ordens diferentes. Os resultados podem então ser subtraídos para obtenção do erro local. 

Como em cada passo deve-se utilizar um método de RK duas vezes (duas ordens diferentes), essa abordagem tem como desvantagem o alto consumo de recursos computacionais. Utilizando, por exemplo, o método de Butcher como RK de quinta ordem e o método de Ralston como RK de quarta ordem, as previsões equivaleriam a um cálculo de dez valores de função por passo, o que representa um significante gasto computacional. 

O método de Fehlberg contorna esse problema, uma vez que os coeficientes calculados na interpolação da função de ajuste desse método podem ser aproveitados tanto na versão de quinta ordem quanto na versão de quarta ordem. Assim, a abordagem de Fehlberg fornece uma estimativa do erro de truncamento com apenas seis cálculos de função. 

Dessa forma, o método de Fehlberg estima \(y \) a partir da seguinte RK de quarta ordem
  


<center>
  <br /> \(y_{i+1} = y_i + \left(\frac{37}{378} k_1 + \frac{250}{621} k_3 + \frac{125}{594} k_4 + \frac{512}{1771} k_6 \right) h \) ,<br />
</center>


  
junto com a RK de quinta ordem
  


<center>
  <br /> \(y_{i+1} = y_i + \left( \frac{2825}{27648} k_1 + \frac{18575}{48384} k_3 + \frac{13525}{55296} k_4 + \frac{255}{14336} k_5 + \frac{1}{4} k_6 \right) h \) ,<br />
</center>


  
onde,
  


<center>
  <br /> \(k_1 = f(x_i, y_i) \)<br />
</center>

<center>
  <br /> \(k_2 = f\left(x_i + \frac{1}{5} h, y_i + \frac{1}{5} k_1 h \right) \)<br />
</center>

<center>
  <br /> \(k_3 = f\left( x_i + \frac{3}{10} h, y_i + \frac{3}{40} k_1 h + \frac{9}{40} k_2 h \right) \)<br />
</center>

<center>
  <br /> \(k_4 = f\left( x_i + \frac{3}{5} h, y_i + \frac{3}{10} k_1 h &#8211; \frac{9}{10} k_2 h + \frac{6}{5} k_3 h \right) \)<br />
</center>

<center>
  <br /> \(k_5 = f\left( x_i + h, y_i &#8211; \frac{11}{54} k_1 h + \frac{5}{2} k_2 h &#8211; \frac{70}{27} k_3 h + \frac{35}{27} k_4 h \right) \)<br />
</center>

<center>
  <br /> \(k_6 = f\left( x_i + \frac{7}{8} h, y_i + \frac{1631}{55296} k1 h + \frac{175}{512} k2 h + \frac{575}{13824} k3 h + \frac{44275}{110592} k4 h + \frac{253}{4096} k5 h \right) \) .<br />
</center>


  
Assim, a estimativa de erro pode ser obtida a partir da diferença das equações de quarta e quinta ordens. Além disso, esses coeficientes \(k_i \) foram obtidos por Cash e Karp, o que faz com que esse método seja também conhecido como Runge-Kutta de Cash-Karp. 

&nbsp;

### 2.1. Ajuste do Tamanho do Passo 

Após determinado o erro de truncamento local, ele pode ser utilizado no ajuste do tamanho do passo. A ideia é aumentar o tamanho do passo se o erro for menor que um valor tolerável ou diminuir o tamanho do passo se o erro for maior que esse valor. Press _et. al_ (1992), sugerem o seguinte critério de ajuste do passo:
  


<center>
  <br /> \(h_{i+1} = h_i \left| \dfrac{\Delta_{i+1}}{\Delta_i} \right|^\alpha \) ,<br />
</center>


  
onde \(h\_{i+1} \) e \(h\_i \) são o tamanho dos passos na iteração atual e ajustado, respectivamente, \(\Delta\_{i} \) é a acurácia atual e \(\Delta\_{i+1}\) é a acurácia
  
desejada, e \(\alpha \) é uma potência constante que é igual a \(0.2 \) quando o tamanho do passo aumenta ( \(\Delta\_{i} \leq \Delta\_{i+1} \) ) e igual a \(0.25 \) quando o tamanho do passo diminui ( \(\Delta\_{i} > \Delta\_{i+1}\)). 

Assim, o parâmetro-chave na estimativa do tamanho do novo passo é \(\Delta\_{i+1} \) . Para isso, relaciona-se \(\Delta\_{i+1} \) a um erro relativo. Isso irá funcionar bem para valores positivos, embora cause alguns problemas em soluções que passem pelo valor zero, o que requer que um pequeno ajuste de segurança seja tomado nessa situação. Assim, a forma proposta por Press _et al._ para determinar \(\Delta_{i+1}\) é
  


<center>
  <br /> \(\Delta_{i+1} = \epsilon y_{c} \) ,<br />
</center>


  
onde \(\epsilon \) é um erro tolerável, \(y_c \) é definido como
  


<center>
  <br /> \(y_c = \left| y \right| + \left| h \dfrac{dy}{dx} \right| \) .<br />
</center>

&nbsp;

## 3. Implementação 

Os códigos abaixo implementam o método de Runge-Kutta-Fehlberg utilizando os coeficientes propostos por Cash-Karp. A primeira função (<tt>fehlberg</tt>) computa a solução local utilizando o método de Runge-Kutta de quarta e quinta ordem pela abordagem de Fehlberg. O retorno dessa função é justamente a solução numérica na EDO no instante \(x \) , aproximada conforme essas duas ordens. 

A função <tt>integral_adapt</tt> delineia a função principal que resolve o problema, utilizando a adaptação do tamanho dos passos calculadas pela função <tt>adapt_folberg</tt>. 

Um exemplo de utilização dessas funções pode ser obtido em <a href="http://www.sawp.com.br/code/ode/fehlberg_adaptativo.py" target="_blank">http://www.sawp.com.br/code/ode/fehlberg_adaptativo.py</a>. 

<pre lang="python">def fehlberg(f, x, y, h):
    """
    Solve unique step using 4th and 5th order of Fehlberg's method

    (y_5ordem, y_4ordem) = fehlberg(f, x, y, h)

    INPUT:
      * f: derivative function f(x, y) = dy/dx
      * x: local x position
      * y: partially computed y
      * h: previous partition size

    return: (y_5ordem, y_4ordem)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2013
    """
    def compute_coeffs(f, x, y, h):
        k1 = f(x, y)
        k2 = f(x + 1.0/5.0 * h, y + 1.0/5.0 * k1 * h)
        k3 = f(x + 3.0/10.0 * h, y + 3.0/40.0 * k1 * h + 9.0/40.0 * k2 * h)
        k4 = f(x + 3.0/5.0 * h,
               y + 3.0/10.0 * k1 * h - 9.0/10.0 * k2 * h + 6.0/5.0 * k3 * h)
        k5 = f(x + h, y - 11.0/54.0 * k1 * h + 5.0 / 2.0 * k2 * h -
               70.0 / 27 * k3 * h + 35.0 / 27.0 * k4 * h)
        k6 = f(x + 7.0 / 8.0 * h, y + 1631.0 / 55296 * k1 * h +
               175.0 / 512 * k2 * h + 575.0 / 13824 * k3 * h +
               44275.0 / 110592 * k4 * h + 253.0 / 4096 * k5 * h)
        return (k1, k2, k3, k4, k5, k6)

    def fehlberg5order(f, x, y, h, coeffs):
        (k1, k2, k3, k4, k5, k6) = coeffs
        delta = 0.102 * k1 + 0.384 * k3 + 0.244 * k4 + 0.019 * k5 + 0.25 * k6
        y1_5ordem = y + delta * h
        return y1_5ordem

    def fehlberg4order(f, x, y, h, coeffs):
        (k1, k2, k3, k4, k5, k6) = coeffs
        delta = 0.097 * k1 + 0.402 * k3 + 0.210 * k4 + 0.289 * k6
        y1_4ordem = y + delta * h
        return y1_4ordem

    coeffs = compute_coeffs(f, x, y, h)
    y1_5ordem = fehlberg5order(f, x, y, h, coeffs)
    y1_4ordem = fehlberg4order(f, x, y, h, coeffs)
    return (y1_5ordem, y1_4ordem)</pre>

<pre lang="python">def adapt_folberg(f, x, y, h, errto=1e-6, safety=0.5):
    """
    Solve each point and find partial y, adjusting h

    (x, y, h) = adapt_folberg(f, x, y, h, errto=1e-6, safety=0.5)

    INPUT:
      * f: derivative function f(x, y) = dy/dx
      * x: local x position
      * y: partially computed y
      * h: previous partition size
      * errto: acceptable approximation error
      * safety: control the h rescaling

    return: (x, y, h)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2013
    """
    err = errto + 1
    while err > 1:
        (y1_5ordem, y1_4ordem) = fehlberg(f, x, y, h)
        y = y1_5ordem
        yscal = abs(y) + abs(h * f(x, y)) + 1e-30
        yerr = abs(y1_5ordem - y1_4ordem)
        err = abs(yerr / yscal / errto)
        h = max(abs(safety * h * err ** (-0.25)), 0.25 * abs(h))
    if err > errto:
        h = safety * h * err ** (-0.2)
    else:
        h = 4 * h
    x = x + h</pre>

<pre lang="python">def integral_adapt(f, xi, xe, y0, n=1e10, method=adapt_folberg):
    """
    Numerical integration for solve ODE's using Runge-Kuta (adaptative)

    integral = integral_adapt(f, xi, xe, n=1e6)

    INPUT:
      * f: derivative function f(x, y) = dy/dx
      * xi: beginning of integration interval
      * xe: end of integration interval
      * y0: initial estimative for y
      * n: number of points used
      * method: method used to solve a unique step (adapt_folberg)

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2013
    """
    def integrator(x, y, h, n):
        i = 0
        while i &lt; = n and x &lt;= xe:
            i += 1
            if x + h > xe:
                h = xe - x
            (x, y, h) = adapt_folberg(f, x, y, h)
        return y

    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</pre>

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    Referências
  </h2></legend> 
  
  <p>
    <br /> <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006).</a><br /> <a name="bibitem3"><b>[3]</b> J.R Cash and A. H. Karp,<cite> <em>Transactions on Mathematical Software</em>,</cite> v.16, p. 201-222, (1990).</a><br /> <a name="bibitem4"><b>[4]</b> W. H. Press,<cite> <em>Numerical Recipes</em>,</cite> Cambridge University Press, (1992).</a>
  </p>
</fieldset>
