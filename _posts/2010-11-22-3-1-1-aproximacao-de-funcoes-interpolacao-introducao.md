---
id: 850
title: '3.1.1 Aproximação de Funções &#8212; Interpolação &#8212; Introdução'
date: 2010-11-22T14:54:35+00:00
author: SAWP
excerpt: |
  Neste artigo, comentamos sobre a importância das formas mais simples de ajuste de funções: a interpolação. Nos posts seguintes, iremos detalhar as
  diversas abordagens numéricas utilizadas para transformar dados obtidos do mundo real (finitos) em funcionais (abstrações contínuas).
layout: post
guid: http://www.sawp.com.br/blog/?p=850
permalink: p=850
categories:
  - Computational Methods
---
## 1. Introdução 

Ajuste de curvas consiste na principal área de estudos de Métodos Computacionais. O motivo disso está no fato de usarmos computadores para processarmos informações a partir de entradas finitas. Ou seja, os dados de entrada em uma máquina finita são fornecidos em um conjunto finito e discreto de valores que são obtidos de um contínuo de possibilidades. Todavia, para reconstruirmos a informação do mundo real &#8212; de onde vêm este contínuo &#8212; precisamos fazer estimativas em pontos que estão entre os pontos discretos. Existem diversas técnicas para fazermos tais estimativas, que são explicadas nos artigos que se seguem. 

Assim como o ajuste de curvas é o principal tema em Métodos Computacionais, técnicas de interpolação é o assunto mais importante na aproximação de funções. Isso ocorre porque toda técnica de ajuste de curvas é uma forma de interpolação: dados um conjunto discreto de pontos que delimitam um intervalo, o método transforma estes parâmetros em uma curva contínua. Além disso, observamos que os métodos de interpolação estão fortemente relacionados com outros temas de métodos computacionais. Embora a abordagem dos livros modernos de análise numérica não relacionem tão profundamente interpolação com outras áreas, sua importância e utilidade são grandes para o entendimento de diversos métodos computacionais (tais como derivação e integração numérica). 

&nbsp;

## 2. Interpolação 

Supondo que um problema é modelado por função contínua conhecida \(f(x) \) e pudemos obter um conjunto de pontos discretos a partir de um experimento. Chamaremos estes valores amostrados de _pontos tabulares_. O objetivo da interpolação é estimar valores da função \(f(x) \) que não pertençam aos valores tabulares, mas que os utilizem para ajustar os parâmetros da função. 

Nossa abordagem nos próximos artigos será de aproximar esta função \(f(x) \) por outra \(y(x) \) que, com a utilização dos pontos tabulares, retornará os mesmos valores do modelo teórico &#8212; \(f(x) \) &#8212; adicionados de um erro numérico associado \(E(x) \) . Isto é,



<center>
  \( f(x) = \sum_{j=1}^{n} l_j(x)f(a_j) + E(x) = y(x) + E(x) \)
</center>

ou, em notação geral

<center>
  \( f(x) = \sum_{j=1}^{n}\sum_{i=0}^{m_j}A_{ij}(x) f^{(i)}(a_j) + E(x) \)
</center>

Então, nosso objetivo é encontrar funções \(y(x) \) que aproximem \(f(x) \) , minimizando o erro associado: 

<center>
  \( E(a_j) = 0 \)
</center>


   
onde \(a_j \) são os _pontos tabulares_, ou _valores conhecidos_. 

Além disso, os métodos de interpolação devem determinar \(l\_j(x) \) para que satisfaça \(E(x) \neq 0 \) com o menor erro associado para os valores não-tabulares \(x \neq a\_j, j=1,2,\ldots, n \) . 

&nbsp;

## 3. Copyright 

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
</fieldset>
