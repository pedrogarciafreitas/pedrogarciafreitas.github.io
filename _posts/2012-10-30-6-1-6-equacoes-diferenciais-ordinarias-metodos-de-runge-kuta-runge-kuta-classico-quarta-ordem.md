---
id: 1913
title: '6.1.6 Equações Diferenciais Ordinárias &#8212; Métodos de Runge-Kuta &#8212; Runge-Kuta Clássico (Quarta Ordem)'
date: 2012-10-30T14:18:31+00:00
author: SAWP
excerpt: 'Os métodos de Runge-Kuta mais utilizados são variantes do método de quarta ordem. Como nos casos apresentados nos posts sobre RK de segunda e terceira ordem, há um número infinito de métodos para  n=4 . Por isso é conhecido como "método de RK clássico".'
layout: post
guid: http://www.sawp.com.br/blog/?p=1913
permalink: p=1913
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2265:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> ralston4order<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.5</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.5</span> * k1 * h<span style="color: black;">&#41;</span>
    k3 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.5</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.5</span> * k2 * h<span style="color: black;">&#41;</span>
    k4 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> y + k3 * h<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> y + <span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span>. / <span style="color: #ff4500;">6</span>.<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>k1 + <span style="color: #ff4500;">2</span> * k2 + <span style="color: #ff4500;">2</span> * k3 + k4<span style="color: black;">&#41;</span> * h
    x1 <span style="color: #66cc66;">=</span> x + h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def ralston4order(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.5 * h, y + 0.5 * k1 * h)
    k3 = f(x + 0.5 * h, y + 0.5 * k2 * h)
    k4 = f(x + h, y + k3 * h)
    y1 = y + (1. / 6.) * (k1 + 2 * k2 + 2 * k3 + k4) * h
    x1 = x + h
    return (x1, y1)</p></div>
    ";}
categories:
  - Computational Methods
---
Os métodos de Runge-Kuta mais utilizados são variantes do método de quarta ordem. Como nos casos apresentados nos posts sobre RK de segunda e terceira ordem, há um número infinito de métodos para \(n=4 \) . Uma fórmula muito encontrada e, por isso, conhecida como &#8220;método de Runge-Kuta clássico&#8221;, é:
  


<center>
  \( y_{i+1} = y_i + \frac{1}{6} (k_1 + 2 k_2 + 2 k_3 + k_4) h \)
</center>


  
onde

<center>
  <br /> \( k_1 = f(x_1, y_1) \)<br />
</center>

<center>
  <br /> \(k_2 = f(x_i + \frac{1}{2} h, y_i + \frac{1}{2} k_1 h) \)<br />
</center>

<center>
  <br /> \(k_3 = f(x_i + \frac{1}{2} h, y_i + \frac{1}{2} k_2 h) \)<br />
</center>


  
e
  


<center>
  <br /> \(k_4 = f(x_i + h, y_i + k_3 h) \)<br />
</center>

Dessas equações, notamos que o método de Runge-Kuta de quarta ordem clássico usa a regra de Simpson, sendo uma abordagem semelhante à de Heun, uma vez que são desenvolvidas múltiplas estimativas da inclinação para se chegar a uma inclinação melhorada do intervalo. Isso é, conforme comentado no post sobre o RK de segunda ordem, cada um dos \(k \) &#8216;s representa uma inclinação, o que faz com que

<center>
  \( \phi = (k_1 + 2 k_2 + 2 k_3 + k_4) \)
</center>


  
seja uma média ponderada dessas inclinações. 

&nbsp;

## 1. Implementação 

&nbsp;

<div>
  <pre lang="python">def ralston4order(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.5 * h, y + 0.5 * k1 * h)
    k3 = f(x + 0.5 * h, y + 0.5 * k2 * h)
    k4 = f(x + h, y + k3 * h)
    y1 = y + (1. / 6.) * (k1 + 2 * k2 + 2 * k3 + k4) * h
    x1 = x + h
    return (x1, y1)</pre>
</div>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/ode/runge_kuta_order_4.py" target="_blank">http://www.sawp.com.br/code/ode/runge_kuta_order_4.py</a>. 

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
