---
id: 1142
title: '3.2.2 Aproximação de Funções &#8212; Análise de Fourier &#8212; A Série de Fourier'
date: 2011-02-24T15:57:15+00:00
author: SAWP
excerpt: 'Neste post veremos a aproximação de uma função qualquer em termo de funções trigonométricas através da série de Fourier. '
layout: post
guid: http://www.sawp.com.br/blog/?p=1142
permalink: p=1142
categories:
  - Computational Methods
---
## 1. A Série de Fourier </p> 

Fourier desenvolveu uma técnica para aproximação de funções periódicas quaisquer através de uma série infinita de funções trigonométricas com frequências harmonicamente relacionadas. Para uma função de período \(T \), a chamada _série de Fourier_ é
    


<center>
  <br /> \(f(t) = a_0 + a_1 cos(\omega_0 t) + b_1 sin(\omega_0 t) + a_2 cos(2 \omega_0 t) + b_2 sin(2 \omega_0 t) + \cdots \)<br />
</center>


    
ou, em termos gerais
    


<center>
  <br /> \(f(t) = a_0 + \sum_{k=1}^{\infty}[a_k cos(k \omega_0 t) + b_k sin(k \omega_0 t)] \)<br />
</center>


    
onde \(\omega_0 = \frac{2 \pi}{T} \) é denominada _frequência fundamental_ e os seus múltiplos \(\omega\_1 \) , \(\omega\_2 \) , \(\ldots \) , são denominados _harmônicos_. Portanto, a série de fourier nada mais é do que uma combinação linear de base \(1, cos(\omega\_0 t), sin(\omega\_0 t), cos(2 \omega\_0 t), sin(2 \omega\_0 t), \cdots \) 

Para determinar os coeficientes das bases, vamos integrar a série de Fourier dentro do período de oscilação \(T \) . Assim, temos
    


<center>
  <br /> \(\int_0^T f(t) dt = \int_0^T a_0 dt + \int_0^T \sum_{k=1}^{\infty}[a_k cos(k \omega_0 t) + b_k sin(k \omega_0 t)] dt \)<br />
</center>

Como todos os termos da somatória acima estão na forma de senos e cossenos apenas, e sabendo que
    


<center>
  <br /> \(\int_0^T sin(k \omega_0 t) dt = \int_0^T cos(k \omega_0 t) dt = 0 \)<br />
</center>


    
a equação se torna apenas
    


<center>
  <br /> \(\int_0^T f(t) dt = a_0 T \)<br />
</center>


    
que nos fornece como resolução o valor do coeficiente \(a_0 \)
    


<center>
  <br /> \(a_0 = \dfrac{\int_0^T f(t) dt}{T} \)<br />
</center>


    
Ou seja, \(a_0 \) é o valor médio da função sobre o período. 

Para calcularmos os coeficientes do cossenos, multiplicamos a série de Fourier por \(cos(k \omega_0 t) \) e integramos, como no processo acima:
    


<center>
  <br /> \(\int_0^T f(t) cos(k \omega_0 t) dt = \int_0^T a_0 cos(k \omega_0 t) dt + \int_0^T \sum_{k=1}^{\infty}[a_k cos(k \omega_0 t) + b_k sin(k \omega_0 t)] cos(k \omega_0 t) dt \)<br />
</center>


    
Esta integral nos fornece a expressão geral para determinarmos os coeficientes das bases em cosseno:
    


<center>
  <br /> \(a_k = \dfrac{2}{T} \int_0^T f(t) cos(k \omega_0 t) dt \)<br />
</center>


    
onde \(k=1,2,\ldots \) . 

De forma análoga, podemos calcular os coeficientes das bases em seno como
    
sendo:
    


<center>
  <br /> \(b_k = \dfrac{2}{T} \int_0^T f(t) sin(k \omega_0 t) dt \)<br />
</center>

### 1.1. A Série de Fourier na Forma Complexa 

Como a série de Fourier é composta por senos e cossenos, é possível colocá-la na forma de exponenciais complexas. Isto é,
    


<center>
  <br /> \(f(t) = \sum_{k=-\infty}^{\infty} c_k e^{i k \omega_0 t} \)<br />
</center>


    
onde \(i \) é o número imaginário e \(c_k \) é
    


<center>
  <br /> \(c_k = \dfrac{1}{T} \int_{-T/2}^{T/2} f(t) e^{-i k \omega_0 t} dt \)<br />
</center>

## 2. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
