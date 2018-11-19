---
id: 1918
title: '6.1.7 Equações Diferenciais Ordinárias &#8212; Métodos de Runge-Kuta &#8212; Método de Butcher (Quinta Ordem)'
date: 2012-10-30T14:38:10+00:00
author: SAWP
excerpt: "O método apresentado nesse post é o método de Butcher de quinta ordem, que consiste em um método de Runge-Kutta para aproximação da solução de y'(x) = f(x,y);  y(x0) = y0, onde f(x,y) é avaliado seis vezes por passo."
layout: post
guid: http://www.sawp.com.br/blog/?p=1918
permalink: /p=1918
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4256:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> butcher<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.25</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.25</span> * k1 * h<span style="color: black;">&#41;</span>
    k3 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.25</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.125</span> * k1 * h + <span style="color: #ff4500;">0.125</span> * k2 * h<span style="color: black;">&#41;</span>
    k4 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.5</span> * h<span style="color: #66cc66;">,</span> y - <span style="color: #ff4500;">0.5</span> * k2 * h + k3 * h<span style="color: black;">&#41;</span>
    k5 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.75</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.1875</span> * k1 * h + <span style="color: #ff4500;">0.5625</span> * k4 * h<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>a1<span style="color: #66cc66;">,</span> a2<span style="color: #66cc66;">,</span> a3<span style="color: #66cc66;">,</span> a4<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>-<span style="color: #ff4500;">3.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">2.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">12.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">8.0</span> / <span style="color: #ff4500;">7.0</span><span style="color: black;">&#41;</span>
    delta <span style="color: #66cc66;">=</span> a1 * k1 * h + a2 * k2 * h + a3 * k3 * h - a3 * k4 * h + a4 * k5 * h
    k6 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> y + delta<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> y + <span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span> / <span style="color: #ff4500;">90</span><span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">7</span> * k1 + <span style="color: #ff4500;">32</span> * k3 + <span style="color: #ff4500;">12</span> * k4 + <span style="color: #ff4500;">32</span> * k5 + <span style="color: #ff4500;">7</span> * k6<span style="color: black;">&#41;</span> * h
    x1 <span style="color: #66cc66;">=</span> x + h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def butcher(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.25 * h, y + 0.25 * k1 * h)
    k3 = f(x + 0.25 * h, y + 0.125 * k1 * h + 0.125 * k2 * h)
    k4 = f(x + 0.5 * h, y - 0.5 * k2 * h + k3 * h)
    k5 = f(x + 0.75 * h, y + 0.1875 * k1 * h + 0.5625 * k4 * h)
    (a1, a2, a3, a4) = (-3.0 / 7.0, 2.0 / 7.0, 12.0 / 7.0, 8.0 / 7.0)
    delta = a1 * k1 * h + a2 * k2 * h + a3 * k3 * h - a3 * k4 * h + a4 * k5 * h
    k6 = f(x + h, y + delta)
    y1 = y + (1.0 / 90) * (7 * k1 + 32 * k3 + 12 * k4 + 32 * k5 + 7 * k6) * h
    x1 = x + h
    return (x1, y1)</p></div>
    ";}
categories:
  - Computational Methods
---
Assim como nas ordens menores, o método de Butcher consiste em utilizar ordens superiores para resolver a EDO numericamente. Uma fórmula a ser utilizada é:

<center>
  $$ y_{i+1} = y_i + \frac{1}{90} (7 k_1 + 32 k_3 + 12 k_4 + 32 k_5 + 7 k_6) h $$
</center>

onde
  


<center>
  <br /> $$k_1 = f(x_i, y_i) $$<br />
</center>

<center>
  <br /> $$k_2 = f(x_i + \frac{1}{4} h, y_i + \frac{1}{4} k_1 h) $$<br />
</center>

<center>
  <br /> $$k_3 = f(x_i + \frac{1}{4} h, y_i + \frac{1}{8} k_1 h + \frac{1}{8} k_2 h) $$<br />
</center>

<center>
  <br /> $$k_4 = f(x_i + \frac{1}{2} h, y_i &#8211; \frac{1}{2} k_2 h + k_3 h) $$<br />
</center>

<center>
  <br /> $$k_5 = f(x_i + \frac{3}{4} h, y_i + \frac{3}{16} k_1 h + \frac{9}{16} k_4 h) $$<br />
</center>


  
e

<center>
  <br /> $$k_6 = f(x_i + h, y_i &#8211; \frac{3}{7} k_1 h + \frac{2}{7} k_2 h + \frac{12}{7} k_3 h &#8211; \frac{12}{7} k_4 h + \frac{8}{7} k_5 h)$$<br />
</center>

Se voltarmos ao post onde discutimos sobre a Regra de Boole, notaremos a similaridade daquela fórmula com o método de Butcher. Fórmulas como essa, que utilizam $$n \ge 4$$ são menos comuns porque o ganho de acurácia começa a ser mínimo, enquanto o custo computacional tende a aumentar. 

&nbsp;

## 1. Implementação 

&nbsp;

<div>
  <pre lang="python">def butcher(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.25 * h, y + 0.25 * k1 * h)
    k3 = f(x + 0.25 * h, y + 0.125 * k1 * h + 0.125 * k2 * h)
    k4 = f(x + 0.5 * h, y - 0.5 * k2 * h + k3 * h)
    k5 = f(x + 0.75 * h, y + 0.1875 * k1 * h + 0.5625 * k4 * h)
    (a1, a2, a3, a4) = (-3.0 / 7.0, 2.0 / 7.0, 12.0 / 7.0, 8.0 / 7.0)
    delta = a1 * k1 * h + a2 * k2 * h + a3 * k3 * h - a3 * k4 * h + a4 * k5 * h
    k6 = f(x + h, y + delta)
    y1 = y + (1.0 / 90) * (7 * k1 + 32 * k3 + 12 * k4 + 32 * k5 + 7 * k6) * h
    x1 = x + h
    return (x1, y1)</pre>
</div>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/ode/runge_kuta_order_5.py" target="_blank">http://www.sawp.com.br/code/ode/runge_kuta_order_5.py</a>. 

&nbsp;

## 2. Copyright 

Este documento está disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <br /> <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
