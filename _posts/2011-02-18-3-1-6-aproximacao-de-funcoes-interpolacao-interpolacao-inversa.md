---
id: 1119
title: '3.1.6 Aproximação de Funções &#8212; Interpolação &#8212; Interpolação Inversa'
date: 2011-02-18T09:45:11+00:00
author: SAWP
excerpt: "Na maioria dos casos de interpolação os valores de f(x) e x são as variáveis dependente e independente, respectivamente. Como tal, os valores dos x's são uniformemente espaçados. Contudo, supondo que precisemos utilizar os mesmos dados amostrados para determinar x a partir de  f(x). Tal problema é chamado de interpolação inversa."
layout: post
guid: http://www.sawp.com.br/blog/?p=1119
permalink: p=1119
categories:
  - Computational Methods
---
## 1. Interpolação Inversa 

Na maioria dos casos de interpolação, os valores de f(x) e x são as variáveis dependente e independente, respectivamente. O problema da _interpolação inversa_ consiste em utilizar os mesmos dados amostrados para determinar x a partir de f(x). 

Nos primeiros tópicos sobre métodos computacionais, apresentamos e discutimos diversos métodos numéricos para solução de equações não-lineares \(f(x) = 0 \) . Uma das aplicações destas técnicas consiste na interpolação inversa. 

A abordagem para encontrarmos algum valor de \(x\_i \) para um dado \(f(x\_i) \) , portanto, consiste em dois passos. O primeiro deles seria utilizar os valores \((n + 1) \) tabelados para interpolarmos um polinômio de grau \(n \) . Com isso, teremos uma função aproximada \(f(x) \) tal que nos permita construir a função \(g(x) \) tal que \(g(x) = f(x) &#8211; f(x_i) \) . O segundo passo consiste em utilizar algum método numérico de busca de raízes para encontrar \(x \) tal que \(g(x)=0 \) . 

Por exemplo, supondo que obtemos os três pontos da amostra: \((2, 0.50), (3, 0.33), (4, 0.25) \) . Utilizando interpolação polinomial, podemos ajustar estes dados ao seguinte polinômio:

<center>
  \( f_2(x) = 0.04 x^2 &#8211; 0.37x + 1.08 \)
</center>

Agora presumindo que desejamos obter o valor de \(x \) quando \(f(x) = 0.30 \) . Neste caso temos que

<center>
  \( 0.30 = 0.04 x^2 &#8211; 0.37x + 1.08 \)
</center>

subtraindo ambos lados por \(f(x_i) = 0.3 \) , teremos \(g(x) \) tal que

<center>
  \( g(x) = f(x) &#8211; f(x_i) = (0.04 x^2 &#8211; 0.37x + 1.08) &#8211; 0.3 = 0.04 x^2 &#8211; 0.37x + 0.78 \)
</center>

Ao utilizarmos um método numérico para encontrarmos \(g(x) = 0 \) , obtemos que \(x \approx 3.296 \) , que é o valor da interpolação inversa. 

&nbsp;

## 2. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006).</a><br /> </fieldset>
