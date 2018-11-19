---
id: 858
title: '3.1.2 Aproximação de Funções &#8212; Interpolação &#8212; Polinômios de Interpolação'
date: 2010-11-22T15:40:49+00:00
author: SAWP
excerpt: |
  Frequentemente precisamos fazer estimativas de valores intermediários àqueles obtidos a partir de amostras. A forma mais comum para fazer estas
  estimativas está no uso de interpolações polinomiais. Neste artigo, discutiremos sobre a teoria comum à todas técnicas numéricas que utilizam polinômios interpoladores, tais como as funções de Lagrange e de Hermite.
layout: post
guid: http://www.sawp.com.br/blog/?p=858
permalink: /p=858
categories:
  - Computational Methods
---
## 1. Polinômios Interpoladores 

O problema geral da interpolação polinomial consiste em, dados $$n+1 $$ _pontos tabulares_ distintos $$(x\_0, f(x\_0)), (x\_1, f(x\_1)), \ldots, (x\_n, f(x\_n)) $$, determinar um polinômio de grau $$n $$ tal que $$y = P_n(x) $$ que obedeça

<center>
  $$ P_n(x_0) = f(x_0), P_n(x_1) = f(x_1), \ldots, P_n(x_n) = f(x_n) $$
</center>

e que seja único para todos pontos $$x_j $$ distintos. 

Chamamos de _polinômio interpolador_ de uma função $$f(x) = y $$ sobre um conjunto de pontos distintos $$x\_0,x\_1,\ldots,x\_n $$ ao polinômio de grau $$n $$ que coincide com $$f(x) $$ em $$x\_0,x\_1,\ldots, x\_n $$ . Tal polinômio será denotado por $$P_n(x) $$ . 

Uma propriedade fundamental para formação de um polinômio interpolador caracteriza qual será a relação entre o grau do polinômio gerado &#8212; e, eventualmente, a precisão da aproximação &#8212; e o número de pontos tabulares disponíveis. Para isso, dados $$n + 1 $$ pontos distintos $$x\_0, x\_1,\ldots,x\_n $$ e $$x\_{n+1} $$ valores de uma função $$y = f(x) $$ sobre esses pontos, existe um único polinômio $$P\_n(x) $$ de grau máximo $$n $$ tal que $$P\_n(x\_k) = f(x\_k) $$ , $$k=0,1,\ldots,n $$. 

**Prova:** Para $$P\_n(x) = a\_0 + a\_1x + \ldots + a\_nx^n $$ polinômio de grau $$n $$ , com $$n+1 $$ coeficientes $$a\_0,a\_1,\ldots,a\_n $$ a serem determinados. Sabemos que $$P\_n(x\_j) = y\_j = f(x\_j) $$ . Portanto, para cada $$x\_j $$ valores tabulares, teremos uma equação associada, gerando um total de $$n+1 $$ equações, uma vez que $$j=0,1,\ldots,n $$ : 

<center>
  $$ a_0 + a_1 x_0 + \ldots + a_n x_0^n = y_0 = f(x_0) $$<br /> $$ a_0 + a_1 x_1 + \ldots + a_n x_1^n = y_1 = f(x_1) $$<br /> $$ \vdots \hspace{50pt} \vdots $$<br /> $$ a_0 + a_1 x_n + \ldots + a_n x_n^n = y_n = f(x_n) $$
</center>

Neste caso, queremos determinar os coeficientes $$a\_0,a\_1,\ldots,a\_n $$ , e não temos dependência em $$x $$ nas incógnitas. Assim, podemos tratar este sistema como sendo um sistema linear para os coeficientes $$a\_j $$ , caracterizado pelo determinante de Vandermonde[[3]](#bibitem3):

<center>
  $$ V = V(x_0,x_1,\ldots,x_n) =<br /> \left[ \begin{array}{cccc}<br /> 1 & x_0 & \ldots & x_0^n \\<br /> 1 & x_1 & \ldots & x_1^n \\<br /> \vdots & \ldots & \ddots & \vdots \\<br /> 1 & x_n & \ldots & x_n^n \end{array}<br /> \right] $$<br />
</center>


    
Para calcularmos $$V $$ , consideraremos este determinando uma função dependente de $$x $$ definida por:

<center>
  $$ V(x) = V(x_0,x_1,\ldots,x_{n-1}, x) =<br /> \left[ \begin{array}{cccc}<br /> 1 & x_0 & \ldots & x_0^n \\<br /> 1 & x_1 & \ldots & x_1^n \\<br /> \vdots & \ldots & \ddots & \vdots \\<br /> 1 & x_{n-1} & \ldots & x_{n-1}^n \\<br /> 1 & x & \ldots & x^n \end{array}<br /> \right] $$<br />
</center>

A função $$V(x) $$ é um polinômio de grau menor que $$n $$ , que se anula em todos pontos $$x\_0, x\_1, \ldots, x_{n-1} $$ . Desta maneira, podemos escrever $$V $$ como um polinômio:

<center>
  $$ V(x_0,x_1,\ldots,x_{n-1},x) = A (x-x_0) (x-x_1) \ldots (x-x_{n-1}) $$
</center>

onde $$A $$ é o coeficiente do termo de **maior grau**, que depende das variáveis $$x_j $$ . Para determinarmos $$A $$ , desenvolvemos o sistema que caracteriza $$V(x) $$ , substituindo a última linha, permitindo que a última equação seja reescria como:

<center>
  $$ V(x_0,x_1,\ldots,x_{n-1},x) = V(x_0,x_1,\ldots,x_{n-1})(x-x_0)\ldots(x-x_{n-1}) $$
</center>

Substituindo $$x $$ por $$x_n $$ , conseguimos a fórmula de recorrência:

<center>
  $$ V(x_0,x_1,\ldots,x_{n-1},x_n) = V(x_0,x_1,\ldots,x_{n-1})(x_n-x_0)\ldots(x_n-x_{n-1}) $$
</center>


  
onde $$V(x\_0,x\_1) = x\_1 &#8211; x\_0 $$ . Utilizando isto, temos que

<center>
  $$ V(x_0,x_1,x_2) = (x_1 &#8211; x_0)(x_2 &#8211; x_0)(x2 &#8211; x_1) $$
</center>

pela recorrência, aplicamos sucessivas substituições para obtermos

<center>
  $$ V(x_0,x_1,\ldots,x_n) = \prod_{i>j} (x_i &#8211; x_j) $$
</center>

Por hipótese, os pontos $$x\_0,x\_1,\ldots,x_n $$ são distintos. Portanto, $$V \neq 0 $$ , levando o sistema a ter uma solução única. 

As figuras abaixo ilustram alguns exemplos de interpolação. Note que os pontos denotados são os valores tabulares (obtidos de uma amostragem real), enquanto que as linhas são as funções ajustadas. Note que na interpolação polinomial, devemos ter ao menos uma unidade a mais que o grau do polinômio interpolador. 

<center>
  <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/11/interpolation.gif"><img class="aligncenter size-full wp-image-860" title="interpolation" src="http://www.sawp.com.br/blog/wp-content/uploads/2010/11/interpolation.gif" alt="" width="800" height="266" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/11/interpolation.gif 800w, http://www.sawp.com.br/blog/wp-content/uploads/2010/11/interpolation-300x99.gif 300w" sizes="(max-width: 800px) 100vw, 800px" /></a>
</center>

&nbsp;

## 2. Copyright </p> 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a>
  </p>
  
  <p>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 69.</a>
  </p>
  
  <p>
    <a name="bibitem3"><b>[3]</b> </a><a href="http://www.proofwiki.org/wiki/Vandermonde_Determinant" target="_blank">http://www.proofwiki.org/wiki/Vandermonde_Determinant</a>
  </p>
</fieldset>
