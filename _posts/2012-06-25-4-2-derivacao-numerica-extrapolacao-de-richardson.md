---
id: 1618
title: '4.2 Derivação Numérica &#8212; Extrapolação de Richardson'
date: 2012-06-25T13:05:13+00:00
author: SAWP
excerpt: 'A extrapolação de Richardson é um método para aceleração de convergência em processos iterativos de interpolação, derivação numérica e integração numérica. '
layout: post
guid: http://www.sawp.com.br/blog/?p=1618
permalink: /p=1618
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3134:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> richard_extrapolation<span style="color: black;">&#40;</span>diff<span style="color: #66cc66;">,</span> f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> h1<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.1</span><span style="color: #66cc66;">,</span> h2<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.05</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Increase the accuracy of numerical derivative (diff).
    &nbsp;
    diff_f_xi = richard_extrapolation(diff, f, x, h1=0.001, h2=0.0005)
    &nbsp;
    INPUT:
    * diff: the numerical differentiation function (diff1, diff2, ...)
    * f: function to derivate
    * x: evaluation point
    * h: step size
    &nbsp;
    return: f^(i)(X=x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jun 2012
    &quot;&quot;&quot;</span>
    Dh2 <span style="color: #66cc66;">=</span> diff<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> h2<span style="color: black;">&#41;</span>
    Dh1 <span style="color: #66cc66;">=</span> diff<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> h1<span style="color: black;">&#41;</span>
    extrapolation <span style="color: #66cc66;">=</span> Dh2 + <span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span> / <span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>h1 / h2<span style="color: black;">&#41;</span> ** <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span> - <span style="color: #ff4500;">1.0</span><span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>Dh2 - Dh1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> extrapolation</pre></td></tr></table><p class="theCode" style="display:none;">def richard_extrapolation(diff, f, x, h1=0.1, h2=0.05):
    &quot;&quot;&quot;
    Increase the accuracy of numerical derivative (diff).
    
    diff_f_xi = richard_extrapolation(diff, f, x, h1=0.001, h2=0.0005)
    
    INPUT:
    * diff: the numerical differentiation function (diff1, diff2, ...)
    * f: function to derivate
    * x: evaluation point
    * h: step size
    
    return: f^(i)(X=x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jun 2012
    &quot;&quot;&quot;
    Dh2 = diff(f, x, h2)
    Dh1 = diff(f, x, h1)
    extrapolation = Dh2 + (1.0 / ((h1 / h2) ** 2) - 1.0) * (Dh2 - Dh1)
    return extrapolation</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

No post anterior, mostramos que as estimativas das derivadas podem ser melhoradas ao diminuir o passo $$h $$ ou ao usar mais pontos através de sucessivas substituições na fórmula de Taylor. Além disso, na seção de implementação, comentamos que a escolha de $$h $$ pode acarretar em problemas, uma vez que o computador possui precisão limita. Uma abordagem para se melhorar a estimativa da derivada consiste na utilização da extrapolação de Richardson. 

No caso geral da extrapolação de Richardson, temos um procedimento para aproximar um funcional $$\phi = \phi(f) $$ de uma dada função $$f$$ por uma sequência, dependente do tamanho de $$h $$ , em que, como $$h \rightarrow 0 $$ , o erro possui a seguinte forma assintótica

<center>
  $$ E = \sum_{j=1}^{\infty} a_j h^{\gamma_j} $$
</center>


  
onde $$\gamma\_1 \lt \gamma\_2 \lt \cdots $$ , os $$a\_j $$ são constantes que podem depender da função $$f $$ mas não dependem de $$h $$ . Tais constantes $$a\_j $$ nos são desconhecidas, mas assumimos conhecer $$\gamma\_j $$ . Se a computação é gerada para dois valores distintos de $$h $$ , $$h\_1 $$ e $$h\_2 $$ , tal que $$h\_1 \gt h\_2 $$ , então há duas aproximações distintas $$\phi\_1 $$ e $$\phi_2 $$ , que se relacionam com o valor verdadeiro de $$\phi $$ pela fórmula

<center>
  $$ \phi = \phi_i + \sum_{j=1}^{\infty} a_j h_i^{\gamma_j} $$
</center>


  
para $$i=1,2 $$ . Multiplicando essa equação para quando $$i=1 $$ por $$h\_2^{\gamma\_1} $$ e por $$i=2 $$ por $$h\_1^{\gamma\_1} $$ , e subtraindo, temos que $$\phi $$ é dado por

<center>
  $$ \phi = \frac{1}{h_1^{\gamma_1} &#8211; h_2^{\gamma_1} (h_1^{\gamma_1} \phi_2 + h_2^{\gamma_1} \phi_1) + \sum_{j=2}^{\infty} a_j \frac{h_1^{\gamma_1} h_2^{\gamma_j} &#8211; h_2^{\gamma_1} h_1^{\gamma_j} {h_1^{\gamma_1} &#8211; h_2^{\gamma_1} $$
</center>


  
Escolhendo-se $$h\_2 = \rho h\_1 $$ , $$\rho > 1 $$ , na equação acima, temos

<center>
  $$ \phi = \frac{\phi_2 &#8211; \rho^{\gamma_1}\phi_1}{1 &#8211; \rho^{\gamma_1} + \sum_{j=2}^{\infty} \frac{\rho^{\gamma_j} &#8211; \rho^{\gamma_1}{1 &#8211; \rho^{\gamma_1} a_j h_1^{\gamma_j} = \phi_{12} + \sum_{j=2}^{\infty} b_j h_1^{\gamma_j} $$
</center>


  
Se desejarmos eliminar p termo com $$j=2 $$ nessa equação, devemos computar $$\phi\_3 $$ com $$h\_3 = \rho h\_2 $$ e computar $$\phi\_{23}f$$ de forma simular para, então, calcular $$\phi\_{123} $$ a partir de $$\phi\_{12} $$ e $$\phi_{23}$$. 

Formalmente, denotamos $$\phi\_i $$ por $$T\_0^i $$ e geramos um vetor triangular de aproximantes $$T_m^i $$ pela fórmula

<center>
  $$ T_m^i = \frac{T_{m-1}^{i+1} &#8211; \rho^{\gamma_m}T_{m-1}^i}{1 &#8211; \rho^{\gamma_m} = T_{m-1}^{i+1} + \frac{T_{m-1}^{i+1} &#8211; T_{m-1}^i}{\rho^{-\gamma_m} &#8211; 1} $$
</center>


  
onde o elemento $$T\_{m-1}^1 $$ corresponde a $$\phi\_{12 \cdots m}$$. 

Em alguns casos, um crescimento geométrico de $$\frac{1}{h}$$ pelo fator $$\frac{1}{\rho}$$ não é desejável ou possível, e nós estamos interessados em uma sequência geral $${h\_i} $$ . Neste caso, podemos gerar uma tabela $$T\_m^i$$ por um simples algoritmo apenas se $$\gamma\_j $$ tem uma estrutura especial, $$y\_j = j \gamma + \delta $$ . Para o caso usual $$\delta=0 $$ , temos que

<center>
  $$ T_m^i = \frac{h_j^{\gamma} T_{m-1}^{i+1} &#8211; h_{i+m}^{\gamma} T_{m-1}^i}{h_i^{\gamma} &#8211; h_{i+m}^{\gamma}= T_{m-1}^{i+1} + \frac{T_{m-1}^{i+1} &#8211; T_{m-1}^{i} {(h_i/h_{i+m}^{\gamma}) &#8211; 1} $$
</center>

&nbsp;

## 2. Extrapolação de Richardson 

A derivada numérica $$D $$ de uma função pode ser descrita como função do passo $$h$$ das fórmulas apresentadas no post anterior na forma

<center>
  $$ D = D(h) + E(h) $$
</center>


  
em que $$D $$ é o valor exato da derivada (analítica), $$E(h) $$ é o resíduo que aparece do truncamento da série de Taylor e $$D(h) $$ é a derivada aproximada. Se fizermos duas estimativas independentes usando passos distintos, $$h\_1 $$ e $$h\_2 $$, teremos que
  


<center>
  $$ D = D(h_1) + E(h_1) $$
</center>


  
e
  


<center>
  $$ D = D(h_2) + E(h_2) $$
</center>


  
portanto
  


<center>
  $$ D(h_1) + E(h_1) = D(h_2) + E(h_2) $$
</center>

Supondo que as fórmulas usadas na diferenciação numérica sejam aquelas com erros $$O(h^2) $$ , temos que
  


<center>
  $$ E(h_1) \approx E(h_2) \approx h^2 $$
</center>


  
logo, a razão entre os dois erros será

<center>
  $$ \frac{E(h_2)}{E(h_1)} \approx \frac{h_2^2}{h_1^2} $$
</center>


  
Com isso, temos a seguinte relação entre os erros

<center>
  $$ E(h_1) \approx E(h_2) \left( \frac{h_1}{h_2} \right)^2 $$
</center>


  
que podemos substituir na equação da igualdade das derivadas numéricas

<center>
  $$ D(h_1) + E(h_2) \left( \frac{h_1}{h_2} \right)^2 \approx D(h_2) + E(h_2) $$
</center>


  
isolando o erro, temos

<center>
  $$ E(h_2) \approx \frac{D(h_1) &#8211; D(h_2)}{1 &#8211; (h1/h2)^2} $$
</center>


  
Com isso, podemos obter a estimativa para o erro de truncamento em termos da relação dos tamanhos dos passos. Essa estimativa pode ser substituída em

<center>
  $$ D = D(h_2) + E(h_2) $$
</center>


  
o que permite fornecer uma estimativa melhorada da derivada

<center>
  $$ D \approx D(h_2) + \frac{1}{(h1/h2)^2 &#8211; 1} \left( D(h_2) &#8211; D(h_1) \right) $$
</center>

&nbsp;

## 3. Implementação 

<pre lang="python">def richard_extrapolation(diff, f, x, h1=0.1, h2=0.05):
    """
    Increase the accuracy of numerical derivative (diff).

    diff_f_xi = richard_extrapolation(diff, f, x, h1=0.001, h2=0.0005)

    INPUT:
      * diff: the numerical differentiation function (diff1, diff2, ...)
      * f: function to derivate
      * x: evaluation point
      * h: step size

    return: f^(i)(X=x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jun 2012
    """
    Dh2 = diff(f, x, h2)
    Dh1 = diff(f, x, h1)
    extrapolation = Dh2 + (1.0 / ((h1 / h2) ** 2) - 1.0) * (Dh2 - Dh1)
    return extrapolation</pre>

Um exemplo de utilização dessa função pode ser obtido em  <a href="http://www.sawp.com.br/code/derivatives/derivative_richard_extrapolation.py" target="_blank">http://www.sawp.com.br/code/derivatives/derivative_richard_extrapolation.py </a>. 

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a><br /> </fieldset>
  </p>
