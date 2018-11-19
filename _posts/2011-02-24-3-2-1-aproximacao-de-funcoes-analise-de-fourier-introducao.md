---
id: 1137
title: '3.2.1 Aproximação de Funções &#8212; Análise de Fourier &#8212; Introdução'
date: 2011-02-24T15:38:23+00:00
author: SAWP
excerpt: 'Nos posts anteriores, apresentamos a interpolação baseada em aproximações baseadas em funções polinomiais. Agora, neste post, apresentamos uma nova classe de funções de aproximação que têm enorme importância em problemas que utilizam métodos computacionais: as funções trigonométricas.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1137
permalink: p=1137
categories:
  - Computational Methods
---
## 1. Aproximação de Fourier 

Cientistas de diversas áreas trabalham com modelos de sistemas oscilatórios. Nesses contextos, as funções trigonométricas desempenham um papel fundamental na modelagem matemática. A aproximação de Fourier consiste em um esquema sistemático para usar séries trigonométricas com esse propósito. A análise de Fourier é desenvolvida nos espaços vetoriais conhecidos como _domínio de frequência_ e _domínio de tempo_ (ou _espaço_). 

&nbsp;

## 2. Ajuste de Curvas por Funções Trigonométricas 

Uma função periódica \(f(t) \) é descrita como
    


<center>
  <br /> \(f(t) = f(t + T) \)<br />
</center>


    
onde \(T \) é uma constante chamada _período_, que é o menor valor para o qual a Equação acima vale. Em geral, uma função periódica tem a seguinte forma trigonométrica:
    


<center>
  <br /> \(f(t) = A_0 + C_1 cos(\omega_0 t + \theta) \)<br />
</center>

Logo, existem quatro parâmetros que caracterizam a senoide:

  * O **valor médio \(A_0 \)** , que determina a altura da abscissa; 
  * A **amplitude \(C_1 \)** , que especifica a altura da oscilação; 
  * A **frequência angular \(\omega_0 \)** , que caracteriza a frequência do ciclo do fenômeno periódico; 
  * O **ângulo de fase \(\theta \)** , que parametriza a extensão da curva horizontalmente. 

A frequência angular, em radianos/tempo, está relacionada com a frequência \(f \), em ciclos/tempo, pela seguinte proporção:
    


<center>
  <br /> \(\omega_0 = 2 \pi f \)<br />
</center>


    
e a frequência está relacionada com o período \(T \) por
    


<center>
  <br /> \(f = \dfrac{1}{T} \)<br />
</center>

Embora a equação \(f(t) = A\_0 + C\_1 cos(\omega_0 t + \theta) \) seja uma caracterização adequada para um movimento oscilatório, trabalhar com esta forma pode ser difícil devido ao deslocamento angular \(\theta \) . Para simplificar esta forma, utilizamos a seguinte identidade trigonométrica:
    


<center>
  <br /> \(C_1 cos(\omega_0 t + \theta) = C_1 [cos(\omega_0 t) cos(\theta) &#8211; sin(\omega_0 t) sin(\theta)] \)<br />
</center>


    
Ou seja, \(f(t) \) é aproximada por
    


<center>
  <br /> \(f(t) = A_0 + A_1 cos(\omega_0 t) + B_1 sin(\omega_0 t) \)<br />
</center>


    
onde \(A\_1 = C\_1 cos(\theta) \) e \(B\_1 = -C\_1 sin(\theta) \) . Portanto,
    


<center>
  <br /> \(\theta = arctg\left( &#8211; \frac{B_1}{A_1} \right) \)<br />
</center>


    
Elevando ao quadrado e somando a relação entre \(A\_1 \) e \(B\_1 \) , temos que
    


<center>
  <br /> \(C_1 = \sqrt{A_1^2 + B_1^2} \)<br />
</center>

Assim, a Equação
    


<center>
  <br /> \(C_1 cos(\omega_0 t + \theta) = C_1 [cos(\omega_0 t) cos(\theta) &#8211; sin(\omega_0 t) sin(\theta)] \)<br />
</center>


    
representa uma formulação alternativa geral em uma forma linear. Esta forma é interessante porque pode ser utilizada em diversas técnicas de ajustes de dados, tais como mínimos quadrados. 

&nbsp;

## 3. Copyright 

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
