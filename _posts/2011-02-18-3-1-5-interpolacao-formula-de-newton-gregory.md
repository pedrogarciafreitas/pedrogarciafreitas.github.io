---
id: 1111
title: '3.1.5 Aproximação de Funções &#8212; Interpolação &#8212; Fórmula de Newton-Gregory'
date: 2011-02-18T09:37:10+00:00
author: SAWP
excerpt: Um caso especial de interpolação polinomial se dá quando temos dados obtidos em uma amostragem igualmente espaçada. Neste post veremos a Interpolação com Dados Igualmente Espaçados, que cumina em uma equação conhecida como Fórmula de Newton-Gregory.
layout: post
guid: http://www.sawp.com.br/blog/?p=1111
permalink: /p=1111
categories:
  - Computational Methods
---
## 1. A Fórmula de Newton-Gregory 

Se os dados amostrados forem igualmente espaçados e estiverem em ordem crescente, então a variável independente assume os valores
    


<center>
  $$ x_1 = x_0 + h $$<br /> $$ x_2 = x_0 + 2h $$<br /> $$ \vdots $$<br /> $$ x_n = x_0 + nh $$
</center>


  
onde $$h $$ é o intervalo entre os dados. Com base nisso, as diferenças divididas podem ser expressas. Isto é, a segunda diferença dividida progressiva é
    


<center>
  $$ f(x_0,x_1,x_2) = \dfrac{\frac{f(x_2) &#8211; f(x_1)}{x_2 &#8211; x_1} &#8211; \frac{f(x_1) &#8211; f(x_0)}{x_1 &#8211; x_0}{x_2 &#8211; x_0} $$
</center>


  
Esta fórmula pode ser simplificada na seguinte expressão:
    


<center>
  $$ f(x_0,x_1,x_2) = \dfrac{f(x_2) &#8211; 2f(x_1) + f(x_0)}{2h^2} $$
</center>


  
pois $$x\_1 &#8211; x\_0 = x\_2 &#8211; x\_1 = \frac{x\_2 &#8211; x\_0}{2} = h $$ . Sabemos que as diferenças finitas de derivadas superiores produzem uma fórmula muito semelhante à esta, sendo:
    


<center>
  $$ f&#8221;(x_i) = \dfrac{f(x_i) &#8211; 2f(x_{i-1}) + f(x_{i-2})}{h^2} + O(h) $$
</center>


  
Ou seja, a segunda diferença progressiva é igual à
    


<center>
  $$ \Delta^2f(x_0) = f(x_2) &#8211; 2f(x_1) + f(x_0) $$
</center>


  
Portanto, a equação que recebe os parâmetros $$x\_0, x\_1, x_2 $$ fica
    


<center>
  $$ f(x_0,x_1,x_2) = \dfrac{\Delta^2f(x_0)}{2!h^2} $$
</center>


  
Generalizando esta fórmula para $$n $$ parâmetros (amostras), temos
    


<center>
  $$ f(x_0,x_1,\ldots,x_n) = \dfrac{\Delta^n f(x_0)}{n! h^n} $$
</center>

Podemos utilizar a última equação acima para expressar o polinômio interpolador para casos em que a amostragem nos fornece dados igualmente espaçados. No caso geral, temos
    


<center>
  $$ f_n(x) = f(x_0) + \dfrac{\Delta f(x_0)}{h}(x-x_0) + \dfrac{\Delta^2 f(x_0)}{2!h^2}(x-x_0)(x-x_0-h) + \cdots + \dfrac{\Delta^n f(x_0)}{n!h^n}(x-x_0)(x-x_0-h)\cdots[x-x_0-(n-1)h] + R_n $$
</center>


  
onde o resto $$R_n $$ é
    


<center>
  $$ R_n = \dfrac{f^{(n+1)}(\xi)}{(n+1)!} (x_{i+1} &#8211; x_i)^{n+1} = \dfrac{f^{(n+1)}(\xi)}{(n+1)!} (x-x_0)(x-x_1)\cdots(x-x_n) $$
</center>

Essa equação é conhecida como _Fórmula de Newton-Gregory_. Ela pode ser simplificada ainda mais ao definirmos uma nova variável de relaxação $$\alpha $$ :
    


<center>
  $$<br /> \alpha = \dfrac{x-x_0}{h}<br /> $$
</center>

Essa definição pode ser usada para deduzir as seguintes expressões simplificadas para os termos na fórmula:
    


<center>
  <br /> $$x &#8211; x_0 = \alpha h $$<br /> $$x &#8211; x_0 &#8211; h = \alpha h &#8211; h $$<br /> $$\vdots $$<br /> $$x &#8211; x_0 &#8211; (n &#8211; 1)h = \alpha h &#8211; (n &#8211; 1) h = h (\alpha &#8211; n + 1) $$<br />
</center>


    
Ou seja, a Fórmula de Newton-Gregory fica:
    


<center>
  $$ f_n(x) = f(x_0) + \Delta f(x_0) \alpha + \dfrac{\Delta^2 f(x_0)}{2!} \alpha (\alpha + 1) + \cdots + \dfrac{\Delta^n f(x_0)}{n!} \alpha (\alpha &#8211; 1) \cdots (\alpha &#8211; n + 1) + R_n $$
</center>

Embora a implementação deste método seja equivalente à regressão polinomial simples, esta notação é relevante para dedução e análise de erro de diversas fórmulas de integração numérica. 

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
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</p> 
    
    <p>
      </a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006).</p> 
      
      <p>
        </a>
      </p></fieldset>
