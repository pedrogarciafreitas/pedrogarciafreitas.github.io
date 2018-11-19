---
id: 573
title: '1.3.7 Raízes de Equações &#8212; Raízes de Polinômios &#8212; O Método de Jenkins-Traub'
date: 2010-03-12T15:23:38+00:00
author: SAWP
excerpt: O Método de Jenkins-Traub é um algoritmo para busca dos zeros de uma função polinomial que utiliza três estágios de estimativas para aproximar as raízes.
layout: post
guid: http://www.sawp.com.br/blog/?p=573
permalink: /p=573
categories:
  - Computational Methods
---
## 1. Introdução </p> 

O Método de Jenkins-Traub é um algoritmo para busca dos zeros de uma função polinomial que utiliza três estágios de estimativas para aproximar as raízes. 

É um método de convergência rápida, uma vez que utiliza o Método de Newton implicitamente no terceiro estágio de aproximação. Sendo assim, é considerado praticamente um padrão na busca de raízes de polinômios[1]. Por ser um algoritmo já projetado para ser implementado computacionalmente, produz soluções gerais, não importando se elas sejam de natureza complexa ou real. 

Este algoritmo inicia a busca checando a existência de raízes muito pequenas. Após encontrá-las, tende à buscar raízes muito grandes. Isto cria um intervalo onde as demais raízes provavelmente estarão. 

No segundo estágio, o algoritmo reajusta as aproximações das raízes complexas reescalando as variáveis. Nesta fase de execução, as raízes são refinadas uma por vez, e então esta aproximação é aplicada na função polinomial dividida por um fator linear. Desta forma, a fatoração que observaríamos do polinômio em fatores lineares, dividido pela aproximação linear, já produz uma segunda aproximação. Este processo é semelhante ao desenvolvido no Método de Durand-Kerner. </p> 

## 2. Desenvolvimento do Método de Jenkins-Traub 

Considere o polinômio
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ P(z) = z^n + a_{n-1}z^{n-1} + \cdots + a_1z + a_0 = \prod_{j=1}^p (z = \alpha_j)^{m_j} $$<br />
</center>


    
onde os termos $$a\_i $$ são números complexos com $$a\_0 \neq 0 $$ e onde a raiz $$\alpha\_j $$ de $$P(z) $$ têm multiplicidade $$m\_j $$ , com $$j=1,\ldots, p $$ , então temos que $$\sum_{j=1}^p = n $$ . Assim, teremos que
    
<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ P'(z) = \sum_{j=1}^{p} m_j P_j(z) $$<br />
</center>


    
onde
    
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ P_j(z) = \dfrac{P(z)}{z-\alpha_j} $$<br />
</center>


    
onde $$j $$ , sabemos que itera sobre o intervalo $$[1,p] $$ . 

O algoritmo de Jenkins-Traub gera uma sequência de polinômios $$H^{(\lambda)}(z) $$ iniciando com $$H^{(0)}(z) = P'(z) $$ , onde cada outro polinômio para $$\lambda > 0 $$ , tendo a forma
    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ H^{(\lambda)}(z) = \sum_{j=1}^{p} c_j^{(\lambda)} P_j(z) $$<br />
</center>


    
com $$c\_j^{(0)} = m\_j $$ . Se escolhermos uma sequência tal que $$H^{(\lambda)}(z) \rightarrow c\_1^{\lambda} P\_1(z) $$ , isto é, que possua as taxas
    
<a name="eq5">(eq5)</a>
      


<center>
  <br /> $$ d_j^{(\lambda)} = \dfrac{c_j^{(\lambda)}{c_1^{(\lambda)} $$<br />
</center>


    
com $$j=2,\ldots,p $$ , então poderemos encontrar a sequência $$t\_{\lambda} $$ das aproximações de $$\alpha\_1 $$ , utilizando a fórmula
    
<a name="eq6">(eq6)</a>
      


<center>
  <br /> $$ t_{\lambda + 1} = s_{\lambda} &#8211; \dfrac{P(s_{\lambda})}{U^{(\lambda+1)}(s_{\lambda} $$<br />
</center>


    
onde $$U $$ é uma normalização de $$H $$ do tipo
    
<a name="eq7">(eq7)</a>
      


<center>
  <br /> $$ U^{(\lambda)} = \dfrac{H^{(\lambda)}(z)}{\sum_{j=1}^{p}c_j^{(\lambda)} $$<br />
</center>

A partir dessas funções, o algoritmo utiliza três estágios de aproximação de novos polinômios para aplicar à interação de Newton. </p> 

### 2.1. Primeiro estágio: processo sem deslocamento 

Para $$\lambda &#8211; 0, 1, \ldots, M-1 $$ , utilizamos $$s_{\lambda} = 0 $$ . No caso, $$M $$ é uma variável escolhida como um polinômio de grau de aproximação
    
razoável. 

### 2.2. Segundo estágio: processo com deslocamento fixo 

Esta etapa da execução que determina as aproximações gerais das menores raízes dos polinômios. Isto é é feito, estimando-se $$s $$ aleatoriamente dentro de um círculo com centro no zero do plano complexo. Ou seja,
    
<a name="eq8">(eq8)</a>
      


<center>
  <br /> $$ s = e^{i\theta}\beta $$<br />
</center>


    
onde $$\beta $$ é o raio que espera-se conter as menores raízes do polinômio. Esta etapa, normalmente é escolhida entre para o intervalo $$M, \ldots, L &#8211; 1 $$ . </p> 

### 2.3. Terceiro estágio: processo com deslocamento variável (adaptativo) 

O polinômio $$H^{(\lambda + 1)}(x) $$ agora é gerado utilizando-se a variável de deslocamento $$s_{\lambda} $$ para os demais polinômios e será obtido utilizando-se a Equação [6](#eq6). </p> 

## 3. Implementação 

O algoritmo de Jenkins-Traub, pela sua complexidade, possui um código um pouco mais elaborado, além de ser extenso demais para ser publicado neste artigo. Por questão de conveniência, ele não está presente aqui, estando disponível em
  


<center>
  <br /> <a href="http://www.sawp.com.br/code/rootfind/jenkinstraub.tar.gz" target="_blank">http://www.sawp.com.br/code/rootfind/jenkinstraub.tar.gz</a>.<br />
</center>

&nbsp;</p> 

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a></a><br /> <a name="bibitem1"><b>[1]</b> </a><a href="http://en.wikipedia.org/wiki/Jenkins-Traub_algorithm" target="_blank">http://en.wikipedia.org/wiki/Jenkins-Traub_algorithm</a><br /> <a name="bibitem2"><b>[2]</b> Jenkins, M. A. and Traub, J. F. <cite> <em>A Three-Stage Variables-Shift Iteration for Polynomial Zeros and Its Relation to Generalized Rayleigh Iteration. </em> </cite> http://www.springerlink.com/content/q6w17w30035r2152/p=ae17d723839045be82d270b45363625f&pi=1 (1970), number. 14, 252-263.</a><br /> <a name="bibitem3"><b>[3]</b> Jenkins, M. A. and Traub, J. F. <cite> <em>A Three-Stage Algorithm for Real Polynomials Using Quadratic Iteration.</em> </cite>SIAM Journal, Vol 7, Num 4 (1970), 545-566.</a><br /> <a name="bibitem4"><b>[4]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 380.</a>
  </p>
</fieldset>
