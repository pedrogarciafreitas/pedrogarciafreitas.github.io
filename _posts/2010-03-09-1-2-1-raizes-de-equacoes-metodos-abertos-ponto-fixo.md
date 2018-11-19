---
id: 435
title: '1.2.1 Raízes de Equações &#8212; Métodos Abertos &#8212; Ponto Fixo'
date: 2010-03-09T16:01:53+00:00
author: SAWP
excerpt: |
  O Método do Ponto Fixo é o primeiro e mais básico dos métodos abertos para busca de zeros em funções.
  
  Diferente dos métodos intervalares, onde exige-se um conhecimento prévio da localização da raiz para delimitação do intervalo de busca, os métodos abertos, em geral, necessitam apenas de uma estimativa inicial para convergir à raiz.
  
  Este artigo apresenta uma breve explanação sobre os métodos abertos --  cuja maioria dos métodos numéricos derivam -- e uma implementação do Método do Ponto Fixo.
layout: post
guid: http://www.sawp.com.br/blog/?p=435
permalink: p=435
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3132:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> fixedPoint<span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">,</span> imax<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    return the root of a function (using the Fixed Point Method)
    &nbsp;
    fixedPoint(fun, x0, errto, imax)
    &nbsp;
    * fun: Iteration function (used by method)
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;</span>
    &nbsp;
    x1 <span style="color: #66cc66;">=</span> G<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    x0 <span style="color: #66cc66;">=</span> x1
    x1 <span style="color: #66cc66;">=</span> G<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x1 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x1 - x0<span style="color: black;">&#41;</span> / x1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x1</pre></td></tr></table><p class="theCode" style="display:none;">def fixedPoint(G, x0, errto, imax):
    &quot;&quot;&quot;
    return the root of a function (using the Fixed Point Method)
    
    fixedPoint(fun, x0, errto, imax)
    
    * fun: Iteration function (used by method)
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;
    
    x1 = G(x0)
    errno = errto + 1
    iterCount = 0
    while errno &gt; errto and iterCount &lt; imax:
    x0 = x1
    x1 = G(x0)
    iterCount += 1
    if x1 != 0:
    errno = fabs((x1 - x0) / x1)
    return x1</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução<a name="sec1"></a>

Diferente dos Métodos da Bissecção e Regula Falsi, que são métodos onde a busca à raiz deve ser realizada dentro de um intervalo, os Métodos Abertos utilizam-se de estratégias para encontrar zeros de funções que não dependam de uma delimitação do local onde se encontra a raiz. 

Sendo assim, os métodos abertos não necessitam de um conhecimento prévio da localização da raiz, o que permite a construção de algoritmos que exijam apenas um único valor inicial de \(x \) para convergir à resposta. 

Diferente dos métodos intervalares, os métodos abertos podem divergir da raiz verdadeira ao longo da execução do programa. Contudo, quando há convergência, os métodos abertos o fazem com velocidade muito superior aos intervalares. </p> 

## 2. O Método do Ponto Fixo <a name="sec2"></a> 

Embora hajam formas mais eficientes para implementação em um programa de computador, todos os métodos abertos são variantes do Método do Ponto Fixo. Por isso, é interessante conhecê-lo para o entendimento das suas variações. 

Ele consiste em aplicar sucessivas aproximações de uma função no ponto em que ela se anula, ou seja, quando \(x \) for uma raiz. 

Sabemos que qualquer \(x \) onde \(f(x) = 0 \) será uma raiz de \(f \) . Sendo assim, a idéia por trás do Método do Ponto Fixo consiste em isolar uma variável \(x \) de forma que \(x \) fica em função de \(x \) e utiliza-se a função anterior. 

Por exemplo, vamos supor que a função \(f(x) \) seja composta por:
    
<a name="eq1">(eq1)</a> 

<center>
  \( f(x) = g(x) + x \)
</center>

como \(f(x) = 0 \) , então
    
<a name="eq2">(eq2)</a>

<center>
  \( g(x) + x = 0 \)
</center>

o que faz com que \(x \) fique em função de \(x \) , onde esta função é \(g \) :
    
<a name="eq3">(eq3)</a>

<center>
  \( x = g(x) \)
</center>

A equação acima fornece uma fórmula para prever um novo valor de \(x \) em função de um valor prévio de \(x \) . Portanto, o algoritmo só necessita de uma estimativa inicial \(x\_{i} \) para aproximar à raiz em \(x\_{i+1} \) . Repetindo-se este processo sucessivas vezes, é possível convergir às raízes de uma função. 

Logo, na forma iterativa, temos:
    
<a name="eq4">(eq4)</a> 

<center>
  \( x_{i+1} = g(x_{i}) \)
</center></p> 

### 2.1. Critério de Parada 

Como nos métodos intervalares, no Ponto Fixo as sucessivas substituições são feitas até que a aproximação para a solução esteja dentro de um erro de tolerância aceito, dado pela fórmula:
    
<a name="eq5">(eq5)</a> 

<center>
  \( errno = \dfrac{ x_{new} &#8211; x_{old} }{ x_{old} } \)
</center>



### 2.2. Exemplo 



Seja encontrar a raíz da função não-linear \( f(x) = \dfrac{1}{e^x} &#8211; x^2 \). Como isto significa \(f(x) = 0 \) , isolando \(x \) , temos:
    
<a name="eq6">(eq6)</a> 

<center>
  \( x^2 = \dfrac{1}{e^x} \)
</center>

<center>
  <br /> \(\Downarrow \)<br />
</center>


    
<a name="eq7">(eq7)</a>

<center>
  \( \sqrt{x^2} = \sqrt{ \dfrac{1}{e^x} } \)
</center>

<center>
  <br /> \(\Downarrow \)<br />
</center>


    
<a name="eq8">(eq8)</a>

<center>
  \( x = \sqrt{ \dfrac{1}{e^x} }\)
</center>

ou seja,
    
<a name="eq9">(eq9)</a>

<center>
  \( x = \sqrt{e^{-x}} = e^{ &#8211; \frac{1}{2} x }\)
</center>

Substituindo sucessivas vezes a Equação [9](#eq9), temos que o seguinte processo iterativo pode ser encontrado:
    
<a name="eq10">(eq10)</a> 

<center>
  \( x_{i+1} = e^{ &#8211; \frac{1}{2} x_{i} }\)
</center></p> 

## 3. Convergência do Método do Ponto Fixo 

A convergência de uma aproximação numérica está intimamente relacionada com o comportamento do erro. Um método que busca uma raiz está convergindo para ela se o erro relativo diminui ao longo das iterações. Portanto, para saber se a solução será encontrada, deve-se ver como o erro está diminuindo com o aumento do número de iterações. 

No caso do Método do Ponto Fixo, a _i-ésima_ iteração é dada por \(x\_{i+1} = g(x\_{i}) \) e supondo que a solução seja dada por \(x\_{sol} = g(x\_{sol}) \) , podemos tomar a diferença destas duas equações tal que
    
<a name="eq11">(eq11)</a> 

<center>
  \( x_{sol} &#8211; x_{i+1} = g(x_{sol}) &#8211; g(x_{i})\)
</center>

Pelo Teorema do Valor Médio, se a função \(g(x) \) e sua primeira derivada forem contínuas em \( \left[ x\_l,x\_r \right] \) , então existe ao menos um valor de e \(x \) tal que \(x = M \) , onde
    
<a name="eq12">(eq12)</a> 

<center>
  \( \dfrac{d}{dx} g(M) = \dfrac{ g(x_{r}) &#8211; g(x_{l}) }{ x_{r} &#8211; x_{l} }\)
</center>

Assim, para \(x\_{l} = x\_{i} \) e \(x\_{r} = x\_{sol} \) , a Equação [12](#eq12) pode ser reescrita como
    
<a name="eq13">(eq13)</a>

<center>
  \( \dfrac{d}{dx} g(M) = \dfrac{ g(x_{sol}) &#8211; g(x_{i}) }{ x_{sol} &#8211; x_{i} }\)
</center>

Isolando \(\Delta g(x) = g(x\_{sol}) &#8211; g(x\_{i}) \) no caso acima,
    
<a name="eq14">(eq14)</a>

<center>
  \( \left( \dfrac{d}{dx} g(M) \right) \left( x_{sol} &#8211; x_{i} \right)<br /> = g(x_{sol}) &#8211; g(x_{i})\)
</center>

onde \(M \) pertence ao intervalo \(\left[ x\_i, x\_{sol} \right] \) . Substituindo a Equação [14](#eq14) na Equação [11](#eq11), podemos obter a relação entre \(x\_{sol} \) , \(x\_{i+1} \) e \(x_{i} \):
    
<a name="eq15">(eq15)</a>

<center>
  \( x_{sol} &#8211; x_{i+1} = \left( \dfrac{d}{dx} g(M) \right)<br /> \left( x_{sol} &#8211; x_{i} \right)\)
</center>

O erro absoluto é dado pela diferença entre a _i-ésima_ aproximação e a solução real \(x\_{sol} \) , então o erro \(E\_{i} \) é dado por
    
<a name="eq16">(eq16)</a> 

<center>
  \( E_{i} = x_{sol} &#8211; x{i}\)
</center>

da mesma forma o erro da próxima iteração \((i+1) \) é:
    
<a name="eq17">(eq17)</a>

<center>
  \( E_{i+1} = x_{sol} &#8211; x_{i+1}\)
</center>

Portanto, a relação entre os erros da iteração \(i \) e \((i+1) \) será:
    
<a name="eq18">(eq18)</a>

<center>
  \( E_{i+1} = \left( \dfrac{d}{dx} g(M) \right) E_{i}\)
</center>

Os erros de uma iteração em relação à sua anterior é uma proporção fixa, \(g'(x) \) por isso o Método do Ponto Fixo é dito &#8220;Linearmente Convergente&#8221;, ou seja, o erro em \((i+1) \) é uma equação linear em função da iteração anterior, \(i \) . Logo, se o coeficiente angular \(g'(x) \) for menor que um, o erro \((i+1) \) será menor que \(i \) , diminuindo ao longo das iterações. Com \(g'(x) \) maior que um, têm-se que o erro de \((i+1) \) é crescente em relação ao erro em \(i \) , o que caracteriza a divergência. </p> 

## 4. Considerações sobre o Método do Ponto Fixo 

Dada a possibilidade de divergência, devemos ter cuidado ao implementar o Método do Ponto Fixo. Diferente dos Métodos Intervalares &#8212; que dependem apenas do intervalo dado e da função que deseja se buscar a raiz &#8212; o Método do Ponto Fixo é menos generalizável, pois depende da implementação de quem desenvolve o código na escolha de cada função \(g(x) \) . 

Ao selecionar a função de iteração \(g(x) \) , o programador deve procurar isolar \(x \) na forma que minimize \(g'(x) \) , pois quão menor for esta taxa, maior será a velocidade de convergência da função. 

Por fim, a escolha dos Métodos Abertos deve ser feita quando aplicados à problemas onde as funções que se deseja buscar os zeros tenham propriedades conhecidas. </p> 

## 5. Implementação <a name="sec3"></a> 

Embora o código abaixo tenha como parâmetro de entrada um ponteiro para função, a implementação não é geral. A função que deve ser passada deve ser a de iteração \(g \) &#8212; obtida a partir do isolamento de uma variável \(x \) &#8212; e não a função \(f \) , cuja raiz queremos encontrar.

<div>
  <pre lang="python">def fixedPoint(G, x0, errto, imax):
    """
    return the root of a function (using the Fixed Point Method)

    fixedPoint(fun, x0, errto, imax)

    * fun: Iteration function (used by method)
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed

    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>
    """

    x1 = G(x0)
    errno = errto + 1
    iterCount = 0
    while errno > errto and iterCount &lt; imax:
        x0 = x1
        x1 = G(x0)
        iterCount += 1
        if x1 != 0:
            errno = fabs((x1 - x0) / x1)
    return x1</pre>
</div>

Um exemplo de utilização desta implementação está disponível em: <a href="http://www.sawp.com.br/code/rootfind/fixedpoint.py" target="_blank">http://www.sawp.com.br/code/rootfind/fixedpoint.py</a> 



## 6. Copyright 

Este documento está disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 69.</a>
  </p>
</fieldset>
