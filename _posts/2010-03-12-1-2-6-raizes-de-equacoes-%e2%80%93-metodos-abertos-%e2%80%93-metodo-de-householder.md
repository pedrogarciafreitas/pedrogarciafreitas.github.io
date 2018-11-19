---
id: 549
title: 1.2.6 Raízes de Equações – Métodos Abertos – Método de Householder
date: 2010-03-12T13:54:17+00:00
author: SAWP
excerpt: 'Assim como o Método de Newton exige a derivada de primeira ordem e apresenta uma taxa de convergência quadrática; o Método de Halley leva a primeira e segunda derivada e possui convergência cúbica; o Método de Householder é um algoritmo de busca de raízes que permite que as iterações convirjam a uma taxa  d+1 , uma vez que sejam utilizadas  d derivadas, onde d é a ordem do método.'
layout: post
guid: http://www.sawp.com.br/blog/?p=549
permalink: p=549
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

Assim como o Método de Newton exige a derivada de primeira ordem e apresenta uma taxa de convergência quadrática; o Método de Halley leva a primeira e segunda derivada e possui convergência cúbica; o Método de Householder é um algoritmo de busca de raízes que permite que as iterações convirjam a uma taxa \(d+1 \) , uma vez que sejam utilizadas \(d \) derivadas, onde \(d \) é a ordem do método. 

Por isso, dizemos que o Método de Householder é uma generalização do Método de Newton. Desta forma, esse utiliza a função de iteração de Householder de ordem um, enquanto o Método de Halley utiliza a de ordem dois.

O algoritmo de Householder é muito importante, uma vez que nos fornece um recurso para construirmos funções de iteração com velocidades de aproximação arbitrárias, adaptadas para cada caso necessário. Além disso, a partir desse método é possível criar técnicas cujas raízes sempre serão encontradas, pois as múltiplas derivadas favorecem a convergência absoluta, independente da aproximação inicial.

&nbsp;

## 2. Desenvolvimento do Método <a name="sec2"></a> 

Seja a aproximação de Padé de ordem \((m,n) \) da função \(f \left( x \right) \) no ponto \(\alpha \) dada pela função racional: 

<a name="eq1">(eq1)</a>
      


<center>
  <br /> \( \left| f \left( x \right) -{\frac {A_{n} \left( x \right) }{B_{m} \left( x \right) } \right| =O \left( \left( x-\alpha \right) ^{v} \right) \)<br />
</center>


    
onde v é tão grande quanto possível. Neste caso, as funções \(A\_{n}(x) \) e \(B\_{n}(x) \) são polinômios de ordem n e m que também aproximam \(f \left( x \right) \) . Esta é a fórmula de Padé, e que nos permite refinar a aproximação de \(f \left( x \right) \) por polinômios de Taylor sempre que \(v \gneq n \) e \(v \geq n + m + 1 \) . 

Representando a função \(f \left( x \right) \) através de uma aproximação de Padé de ordem \((d+1) \) , cujos polinômios \(A\_{n}(x) \) e \(B\_{n}(x) \) são tais que o numerador seja uma função linear, enquanto o denominador seja um polinômio de Taylor de ordem \((d-1) \) . Desta forma, temos a seguinte relação: 

<a name="eq2">(eq2)</a>
      


<center>
  <br /> \( f \left( x+h \right) ={\frac {a_{0}+h}{b_{0}+b_{1}h+ \cdots + b_{d-1}{h}^{d-1}}+O \left( {h}^{d+1} \right) \)<br />
</center>

Note que a função racional tem um zero trivial quando \(h = -a_{0} \) . 

Para um polinômio de Taylor que possua \((d+1) \) coeficientes dependentes de \(f \left( x \right) \) , também temos a aproximação de Padé com \((d+1) \) coeficientes dependentes de \(f \left( x \right) \) e suas derivadas, com \(b_{d} = 0 \) . 

Agora vamos aproximar uma função \(g \left( x \right) \) tal que por polinômios de Taylor, tal que $g \left( x \right) = \left( f \left( x \right) \right) ^{-1}$. Com isso, obteremos a seguinte aproximação: 

<a name="eq3">(eq3)</a>
      


<center>
  <br /> \( g \left( x+h \right) =g \left( x \right) + \left( {\frac {d}{dx}g \left( x \right) \right) h + \ldots + {\dfrac { \left( {\frac {d^{d-1}{d{x}^{d-1}}g \left( x \right) \right) {h}^{d-1}{ \left( d-1 \right) !}+{\dfrac { \left( {\frac {d^{d}{d{x}^{d}}g \left( x \right) \right) {h}^{d}{d!}+O \left( {h}^{d+1}\right)\)<br />
</center>

Multiplicando [3](#eq3) por \(a_{0} + h \) , e dividindo tudo por \(h^d \) após substituir o erro \(O(d^{d+1}) \) da série de Taylor na aproximação de Padé, obteremos: 

<a name="eq4">(eq4)</a>
      


<center>
  <br /> \( b_{d}={\dfrac {a_{0}{\dfrac {d^{d}{d{x}^{d}}g \left( x \right) }{d!} + {\dfrac {\dfrac {d^{d-1}{d{x}^{d-1}}g \left( x \right) }{ \left( d-1\right)!}\)<br />
</center>

Resolvendo a Equação [4](#eq4) para \(h = -a_{0} \) , temos: 

<a name="eq5">(eq5)</a>
      


<center>
  <br /> \( h={\frac {d! {\dfrac {d^{d-1}{d{x}^{d-1}}g \left( x \right)}{ \left( d-1 \right) !\,{\dfrac {d^{d}{d{x}^{d}}g \left( x \right) } = {d \frac {\dfrac {d^{d-1}{d{x}^{d-1}}g \left( x \right) }{\dfrac {d^{d}{d{x}^{d}}g \left( x \right) } \)<br />
</center>

A Equação [5](#eq5) implica na fórmula iterativa: 

<a name="eq6">(eq6)</a>
      


<center>
  <br /> \( x_{n+1}=x_{n}+{d \dfrac {\dfrac {d^{d-1}{d{x}^{d-1}}g \left( x \right) }{\dfrac {d^{d}{d{x}^{d}}g \left( x \right) } \)<br />
</center>

Como tomamos \(g \left( x \right) = \left( f \left( x \right) \right) ^{-1} \) , a Equação [6](#eq6) reescrita em termos da função cuja raiz queremos
    
encontrar fica: 

<a name="eq7">(eq7)</a>
      


<center>
  <br /> \( x_{n+1}=x_{n}+{d \dfrac {\dfrac {d^{d-1}{d{x}^{d-1}} \left( \dfrac{1}{f(x)}\right) }{\dfrac {d^{d}{d{x}^{d}}\left( \dfrac{1}{f(x)} \right) } \)<br />
</center>

A Equação [7](#eq7) é a expressão do Método de Householder que gera as funções de iteração para busca de zeros da função \(f(x) \) , convergindo com taxa \(\left(d+1\right)\). </p> 

## 3. Implicações do Método de Householder 

Para as ordens mais baixas do Método de Householder, observamos que as fórmulas iterativas obtidas implicam em expressões de alguns métodos bem conhecidos. 

Por exemplo, para a fórmula de Householder de primeira ordem , ou seja, \(d = 1 \) , temos: 

<a name="eq8">(eq8)</a>
      


<center>
  <br /> \( x_{n+1}=x_{n}+{\dfrac {1}{f \left( x \right) {\dfrac {d}{dx} \left( \left( f \left( x \right) \right) ^{-1} \right) } = x_{n}-{\frac {f \left( x \right) }{\dfrac {d}{dx}f \left( x \right) } \)<br />
</center>

A Expressão [8](#eq8) é exatamente aquela obtida pelo Método de Newton, por isso ele é considerado o Método de Householder de primeira ordem. 

Aplicando uma ordem a mais de derivação em ([7](#eq7)), temos que \(d=2 \) nos fornece: 

<a name="eq9">(eq9)</a>
      


<center>
  <br /> \( x_{n+1}=x_{n}+2\,{\frac {\dfrac {d}{dx} \left( \left( f \left( x \right) \right) ^{-1} \right) }{\dfrac {d^{2}{d{x}^{2}} \left( \left( f \left( x \right) \right) ^{-1} \right) } \)<br />
</center>


    
que é exatamente a função de iteração utilizada pelo Método de Halley: 

<a name="eq10">(eq10)</a>
      


<center>
  <br /> \( x_{n+1}=x_{n}+2\,{\frac {f \left( x \right) {\dfrac {d}{dx}f \left( x \right) }{-2\, \left( {\dfrac {d}{dx}f \left( x \right) \right) ^{2}+ \left( {\dfrac {d^{2}{d{x}^{2}}f \left( x \right) \right) f \left( x \right) } \)<br />
</center>

Para ordens mais altas, obtemos expressões mais complexas, muitas vezes de difícil implementação prática, sendo que o método discutido neste trabalho costuma fornecer maior auxílio no desenvolvimento teórico de outros métodos. 

A complexidade das expressões geradas para ordens elevadas do Método de Householder pode ser visualizada já a partir do terceiro grau de derivação. Alguns exemplos:
    
Ordem3
  


<center>
  <br /> \( x_{n+1}=x_{n}+3\,{\dfrac { \left( -2\, \left( {\dfrac {d}{dx}f \left( x \right) \right) ^{2}+ \left( {\dfrac {d^{2}{d{x}^{2}}f \left( x \right) \right) f \left( x \right) \right) f \left( x \right) }{6\, \left( {\dfrac {d}{dx}f \left( x \right) \right) ^{3}- 6\, \left( {\dfrac {d}{dx}f \left( x \right) \right) \left( {\dfrac { d^{2}{d{x}^{2}}f \left( x \right) \right) f \left( x \right) + \left( {\dfrac {d^{3}{d{x}^{3}}f \left( x \right) \right) \left( f \left( x \right) \right) ^{2}} \)<br />
</center>

&nbsp;

## 4. Detalhes de Implementação 

A natureza do Método de Householder o torna difícil de ser generalizado em uma implementação real, uma vez que obter uma derivada de ordem arbitrária numericamente não é uma tarefa trivial. 

Uma abordagem que pode ser usada consiste em utilizar artifícios que aproximem numericamente as derivadas através de interpolações e outras técnicas numéricas. Todavia, este tratamento, na maioria das vezes, não produz um resultado satisfatório. Sendo assim, neste artigo não será apresentado nenhuma implementação deste método. </p> 

&nbsp;

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> <cite>http://mathworld.wolfram.com/HouseholdersMethod.html</cite></a>
  </p>
</fieldset>
