---
id: 1909
title: '6.1.5 Equações Diferenciais Ordinárias &#8212; Métodos de Runge-Kuta &#8212; Método de Runge-Kuta de Terceira Ordem'
date: 2012-10-30T13:53:30+00:00
author: SAWP
excerpt: Implementação do método de Runge-Kutta de terceira ordem utilizando os coeficientes de Ralston.
layout: post
guid: http://www.sawp.com.br/blog/?p=1909
permalink: /p=1909
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1962:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> ralston3order<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.5</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.5</span> * k1 * h<span style="color: black;">&#41;</span>
    k3 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> y - k1 * h + <span style="color: #ff4500;">2</span> * k2 * h<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> y + <span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span>. / <span style="color: #ff4500;">6</span>.<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>k1 + <span style="color: #ff4500;">4</span> * k2 + k3<span style="color: black;">&#41;</span> * h
    x1 <span style="color: #66cc66;">=</span> x + h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def ralston3order(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.5 * h, y + 0.5 * k1 * h)
    k3 = f(x + h, y - k1 * h + 2 * k2 * h)
    y1 = y + (1. / 6.) * (k1 + 4 * k2 + k3) * h
    x1 = x + h
    return (x1, y1)</p></div>
    ";}
categories:
  - Computational Methods
---
Conforme mostrado no post do método de Runge-Kuta de segunda ordem, a EDO é resolvida pela fórmula iterativa:

<center>
  $$ y_{i+1} = y_i + \phi (x_i, y_i, h) h $$
</center>


  
onde $$\phi $$ é a função incremento, que quanto mais elementos possuir, mais acurada é a aproximação:

<center>
  $$ \phi = a_1 k1 + a_2 k_2 + \cdots + a_n k_n $$
</center>


  
onde os $$a\_i $$ são constantes a serem determinadas e os termos $$k\_i $$ são combinações lineares da função diferencial a ser resolvida. Como visto naquele mesmo post, o número $$n $$ de $$k $$ &#8216;s escolhidos determina o grau do método de Runge-Kuta. 

Quando $$n=3 $$ , a dedução segue parecida com a dos métodos de segunda ordem, aumentando apenas o número de incógnitas e equações. Mais especificamente, enquanto nos métodos de ordem dois tínhamos que determinar apenas uma incógnita $$a_2 $$ , na terceira ordem temos de especificar valores para duas das oito incógnitas. Ralston e Rabinowitz[[1]](#bibitem1) fornecem os valores das incógnitas para que o erro de truncamento tenha limitante mínimo. Para isso, resolvemos iterativamente o problema com a fórmula

<center>
  $$ y_{i+1} = y_i + \dfrac{1}{6} (k_1 + 4 k_2 + k_3) h $$
</center>


  
onde

<center>
  $$ k_1 = f(x_i, y_i) $$
</center>

<center>
  $$ k_2 = f(x_i + \frac{1}{2} h, y_i + \frac{1}{2} k_1 h) $$
</center>


  
e

<center>
  $$ k_3 = f(x_i + h, y_i &#8211; k_1 h + 2 k_2 h) $$
</center>

&nbsp;

## 1. Implementação 

&nbsp;

<div>
  <pre lang="python">def ralston3order(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.5 * h, y + 0.5 * k1 * h)
    k3 = f(x + h, y - k1 * h + 2 * k2 * h)
    y1 = y + (1. / 6.) * (k1 + 4 * k2 + k3) * h
    x1 = x + h
    return (x1, y1)</pre>
</div>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/ode/runge_kuta_order_3.py" target="_blank">http://www.sawp.com.br/code/ode/runge_kuta_order_3.py</a>. 

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
