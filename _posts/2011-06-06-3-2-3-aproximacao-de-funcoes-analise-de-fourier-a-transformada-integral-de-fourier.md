---
id: 1163
title: '3.2.3 Aproximação de Funções &#8212; Análise de Fourier &#8212; A Transformada Integral de Fourier'
date: 2011-06-06T10:13:25+00:00
author: SAWP
excerpt: A integral de Fourier é a principal ferramenta para analisar funções de ondas não-periódicas através da modelagem trigonométrica das séries de Fourier. Neste post discutiremos a versão contínua da transformada de Fourier.
layout: post
guid: http://www.sawp.com.br/blog/?p=1163
permalink: /p=1163
categories:
  - Computational Methods
---
## 1. A Transformada Integral de Fourier 

A série de Fourier &#8212; detalhada em outro post &#8212; é uma útil ferramenta de modelagem e análise do espectro de uma função periódica. Contudo, existem muitos fenômenos em que as ondas não se repetem regularmente. A alternativa para modelagem de tais fenômenos consiste em criar uma série de Fourier para ondas não-periódicas. 

A integral de Fourier é o principal recurso para criar tal modelo. Ela pode ser deduzida a partir da versão complexa da série de Fourier.

<center>
  $$ f(t) = \sum_{k=-\infty}^{\infty} c_k e^{i k \omega_0 t}$$
</center>

onde

<center>
  $$ c_k = \frac{1}{T} \int_{-T/2}^{T/2} f(t) e^{-i k \omega_0 t} dt $$
</center>

e onde $$\omega_0 = \frac{2 \pi}{T} $$ e $$k=0,1,2,\ldots$$ 

A transição de uma função periódica em outra não-periódica pode ser feita permitindo-se que o período tenda ao infinito. Isto é, quando $$T $$ se torna infinitamente grande, a função não se repete, e, assim, torna-se não-periódica. Se isso ocorre, temos que a série de Fourier se reduz a

<center>
  $$f(t) = \frac{1}{2 \pi} \int_{-\infty}^{\infty} F(i \omega_0) e^{i \omega_0 t} d\omega_0 $$
</center>

e os coeficientes se tornam uma função no contínuo da variável de frequência $$\omega_0 $$ ,

<center>
  $$F(i \omega_0) = \int_{-\infty}^{\infty} f(t) e^{-i \omega_0 t} dt$$
</center>

A função$$F(i \omega_0) $$ , definida acima, é chamada de _transformada integral de Fourier_ de$$f(t) $$ . A função$$f(t) $$ , por outro lado, é chamada de _transformada inversa de Fourier_ de $$F(i \omega_0) $$ . Esse par de funções nos permite transformarmos os espaços relativos aos domínios de tempo para o domínio de frequência e vice-versa. 

A diferença entre a transformada e a série de Fourier reside na classe de funções em que elas são aplicadas. Enquanto a série de Fourier modela bem funções periódicas, a transformada modela as formas de funções não-periódicas. Além disso, ambas se diferem na forma como se movimentam pelos espaços de tempo e frequência. A série converte uma função definida no contínuo, periódica no domínio do tempo, para **amplitudes** no domínio da frequência em **frequências discretas**. Por outro lado, a transformada de Fourier converte uma função no contínuo no domínio do tempo em uma função no domínio da frequência. Desta forma, **o espectro de frequência discreto gerado pela série de Fourier é análogo ao espectro contínuo gerado pela transformada de Fourier**. 

&nbsp;

## 2. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.

&nbsp;

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a><br /> </fieldset>
