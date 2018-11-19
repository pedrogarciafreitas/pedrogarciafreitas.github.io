---
id: 403
title: '1.1.2 Raízes de Equações &#8212; Métodos Intervalares &#8212; Regula Falsi'
date: 2010-03-09T13:15:36+00:00
author: SAWP
excerpt: |
  O método conhecido como Regula Falsi, ou "da Falsa Posição" é uma técnica que busca de raízes de funções dentro de um intervalo pré-definido, diferindo-se do Método da Bisecção por avaliar a intersecção entre o eixo abicisso e um segmento de reta produzido através de dois intervalos consecutivos, nos pontos [xi, f(xi)]  e [xi+1, f(x_i+1)].
  
  Para algumas funções, este método possui convergência mais veloz que o Método da Bisecção, servindo no refinamento de algumas outras técnicas compostas.
  
  Este artigo faz uma apresentação do método e segue com uma discussão sobre a implementação e as possíveis melhorias computacionais que podem ser aplicadas à ele.
layout: post
guid: http://www.sawp.com.br/blog/?p=403
permalink: /p=403
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:4982:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> RegulaFalsi<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.01</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1000</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function using Regula Falsi
    &nbsp;
    RegulaFalsi(fun, xl, xr, imax, errto)
    &nbsp;
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &nbsp;
    &quot;&quot;&quot;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> &amp;gt<span style="color: #66cc66;">;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount &amp;lt<span style="color: #66cc66;">;</span> imax:
    xold <span style="color: #66cc66;">=</span> x
    iterCount <span style="color: #66cc66;">=</span> iterCount + <span style="color: #ff4500;">1</span>
    fr <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> xr - fr * <span style="color: black;">&#40;</span>xl - xr<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span><span style="color: #dc143c;">fl</span> - fr<span style="color: black;">&#41;</span>
    fx <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x - xold<span style="color: black;">&#41;</span> / x<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> * fx
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xr <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> x
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> fx
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def RegulaFalsi(F, xl, xr, errto=0.01, imax=1000):
    &quot;&quot;&quot;
    Return the root of a function using Regula Falsi
    
    RegulaFalsi(fun, xl, xr, imax, errto)
    
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    
    &quot;&quot;&quot;
    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl)
    while errno &amp;gt; errto and iterCount &amp;lt; imax:
    xold = x
    iterCount = iterCount + 1
    fr = F(xr)
    x = xr - fr * (xl - xr) / (fl - fr)
    fx = F(x)
    if x != 0:
    errno = fabs((x - xold) / x)
    test = fl * fx
    if test &lt; 0:
    xr = x
    elif test &gt; 0:
    xl = x
    fl = fx
    else:
    errno = 0
    return x</p></div>
    ;i:2;s:7654:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> RegulaFalsi_O2<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.01</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1000</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function using Regula Falsi
    &nbsp;
    RegulaFalsi_O2(fun, xl, xr, imax, errto)
    &nbsp;
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &nbsp;
    &quot;&quot;&quot;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span>
    leftCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span> <span style="color: #808080; font-style: italic;"># O2</span>
    rightCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span> <span style="color: #808080; font-style: italic;"># O2</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;=</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> imax:
    xold <span style="color: #66cc66;">=</span> x
    iterCount <span style="color: #66cc66;">=</span> iterCount + <span style="color: #ff4500;">1</span>
    fr <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># x = (xl+xr)/2.l ponto onde modifica a Bisseccao</span>
    x <span style="color: #66cc66;">=</span> xr - fr * <span style="color: black;">&#40;</span>xl - xr<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span><span style="color: #dc143c;">fl</span> - fr<span style="color: black;">&#41;</span>
    fx <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x - xold<span style="color: black;">&#41;</span> / x<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> * fx
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xr <span style="color: #66cc66;">=</span> x
    fr <span style="color: #66cc66;">=</span> fx <span style="color: #808080; font-style: italic;"># O2</span>
    rightCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span> <span style="color: #808080; font-style: italic;"># O2</span>
    leftCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span> <span style="color: #808080; font-style: italic;"># O2</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> leftCount <span style="color: #66cc66;">&gt;=</span> <span style="color: #ff4500;">2</span>:
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> / <span style="color: #ff4500;">2</span> <span style="color: #808080; font-style: italic;"># O2</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> x
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> fx
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># O2</span>
    leftCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span> <span style="color: #808080; font-style: italic;"># O2</span>
    rightCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span> <span style="color: #808080; font-style: italic;">#O2</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> rightCount <span style="color: #66cc66;">&gt;=</span> <span style="color: #ff4500;">2</span>:
    fr <span style="color: #66cc66;">=</span> fr / <span style="color: #ff4500;">2</span> <span style="color: #808080; font-style: italic;"># O2</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def RegulaFalsi_O2(F, xl, xr, errto=0.01, imax=1000):
    &quot;&quot;&quot;
    Return the root of a function using Regula Falsi
    
    RegulaFalsi_O2(fun, xl, xr, imax, errto)
    
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    
    &quot;&quot;&quot;
    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl)
    leftCount = 0 # O2
    rightCount = 0 # O2
    while errno &gt;= errto and iterCount &lt; = imax:
    xold = x
    iterCount = iterCount + 1
    fr = F(xr)
    # x = (xl+xr)/2.l ponto onde modifica a Bisseccao
    x = xr - fr * (xl - xr) / (fl - fr)
    fx = F(x)
    if x != 0:
    errno = fabs((x - xold) / x)
    test = fl * fx
    if test &lt; 0:
    xr = x
    fr = fx # O2
    rightCount = 0 # O2
    leftCount += 1 # O2
    if leftCount &gt;= 2:
    fl = fl / 2 # O2
    elif test &gt; 0:
    xl = x
    fl = fx
    fl = F(xl) # O2
    leftCount = 0 # O2
    rightCount += 1 #O2
    if rightCount &gt;= 2:
    fr = fr / 2 # O2
    else:
    errno = 0
    return x</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a>

Semelhante ao Método da Bissecção, a técnica Regula Falsi é um Método Intervalar usado para buscar raízes de funções, aproximando um intervalo $$\left[ x\_{l}, x\_{r} \right] $$ e $$ \left[ F(x\_{l}), F(x\_{r}) \right] $$ por uma reta. A interseção da reta com o eixo das abcissas consiste em uma aproximação da raiz.

Esta técnica apresenta, em alguns casos, alguma melhoria na eficiência da busca pela raiz, pois é um método inteligente na seleção dos limites dos subintervalos, diferentemente do Método da Bissecção, que utiliza de uma abordagem de força bruta para convergir ao resultado.

A deficiência no Método da Bissecção, contornada pelo Regula Falsi, está na divisão do intervalo em dois subintervalos iguais, sem levar em conta os valores de $$F(x\_{l}) $$ e $$F(x\_{r}) $$ . Sendo assim, o algoritmo da Bissecção não considera a probabilidade de que se uma imagem $$F(x\_{r}) $$ está mais próxima de zero do que outra imagem $$F(x\_{l}) $$ , provavelmente $$x\_{r} $$ está mais próxima da raiz que $$x\_{l} $$ , e vice-versa. Para esse método, a distância da raiz $$x $$ até $$x\_{r} $$ e $$x\_{l} $$ têm a mesma probabilidade de ocorrer, o que em muitos casos não é verdade.

## 2. Desenvolvimento do Método <a name="sec2"></a>

O método consiste em aproximar uma curva por uma reta até que esta intercepte o eixo $$x $$ , permitindo estimar o valor da raiz. O valor tomado como sendo a aproximação da raiz vêm da interceptação por esta reta, que não pertence a curva. Daí o nome &#8220;Regula Falsi&#8221;, ou &#8220;Falsa Posição&#8221;. Este processo pode ser visualizado na Figura [1](#fig1).

<center>
  <br /> <a name="#fig1"></a><br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig141.png"><img class="aligncenter size-full wp-image-416" title="Aproximação da raiz por uma reta." src="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig141.png" alt="fig141" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig141.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig141-300x300.png 300w" sizes="(max-width: 400px) 100vw, 400px" /></a><br />
</center>

Podemos criar dois triângulos a partir dos pontos usados na geração da reta usada na aproximação, conforme ilustrado na Figura [2](#fig2). Por essa imagem, observamos que os triângulos serão sempre semelhantes, uma vez que estarão sempre separados pelo vértice formado pela raiz aproximada.

<center>
  <br /> <a name="#fig2"></a><br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig142.png"><img class="aligncenter size-full wp-image-417" title="Aproximação do método Regula Falsi" src="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig142.png" alt="fig142" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig142.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig142-300x300.png 300w" sizes="(max-width: 400px) 100vw, 400px" /></a><br />
</center>

Usando as propriedades de semelhança de triângulos para este caso, podemos obter a seguinte relação:
  
<a name="eq1"></a>
  


<center>
  $$ \dfrac{f(x_{l})}{x &#8211; x_{l} = \dfrac{f(x_{r})}{x-x_{r}$$
</center>


  
multiplicando a Equação [1](#eq1) por $$(x-x\_{l})(x-x\_{r}) $$ , <a name="eq2"></a>
  


<center>
  $$ f(x_{l}) \left( x &#8211; x_{r} \right) = f(x_{r}) \left( x &#8211; x_{l} \right) $$
</center>


  
agrupando termos, esta equação fica melhor escrita como
  
<a name="eq3"></a>
  


<center>
  $$ x \left( f(x_{l}) &#8211; f(x_{r}) \right) = x_{r} f(x_{l}) &#8211; x_{l} f(x_{r}) $$
</center>


  
Dividindo ambos lados da equação por $$f(xl) &#8211; f(xr) $$ ,
  
<a name="eq4"></a>
  


<center>
  $$ x = \dfrac{ x_{r} f(x_{l}) &#8211; x_{l} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) }$$
</center>


  
esta é uma forma de expressar a função de iteração para o Regula Falsi. Ela permite o cálculo da raiz $$x $$ em função dos limites $$x\_{l} $$ e $$x\_{r}$$.

Utilizar a Equação [4](#eq4) para aproximar raízes funciona perfeitamente. Contudo, é possível melhorá-la para que ela utilize menos operações de cálculo. Para isso, vamos separar a subtração dos numeradores em duas frações:
  
<a name="eq5"></a>
  


<center>
  $$ x = \dfrac{ x_{r} f(x_{l}) }{ f(x_{l}) &#8211; f(x_{r}) } &#8211; \dfrac{ x_{l} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) } $$
</center>


  
somando e subtraindo $$x_{r} $$ na Fórmula [5](#eq5),
  
<a name="eq6"></a>
  


<center>
  $$ x = \dfrac{ x_{r} f(x_{l}) }{ f(x_{l}) &#8211; f(x_{r}) } &#8211; \dfrac{ x_{l} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) } + (x_{r} &#8211; x_{r}) = \dfrac{ x_{r} f(x_{l}) }{ f(x_{l}) &#8211; f(x_{r}) } + x_{r} &#8211; \dfrac{ x_{l} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) } &#8211; x_{r} $$
</center>


  
ajustando o termo independente $$x_{r}$$,
  
<a name="eq7"></a>
  


<center>
  $$ x = \left(\dfrac{ x_{r} f(x_{l}) }{ f(x_{l}) &#8211; f(x_{r}) } &#8211; x_{r} \right) + \left( \dfrac{ x_{l} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) } + x_{r}\right) $$
</center>


  
substituindo $$x $$ pela Equação [4](#eq4) na Equação [7](#eq7),
  
<a name="eq8"></a>
  


<center>
  $$ x &#8211; x_{r} = \dfrac{ x_{r} f(x_{l}) }{ f(x_{l}) &#8211; f(x_{r}) } &#8211; \dfrac{ x_{r} f(x_{l}) &#8211; x_{r} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) } $$
</center>


  


<center>
  $$\Downarrow $$
</center>


  
<a name="eq9"></a>
  


<center>
  $$ x = x_{r} + \dfrac{ x_{r} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) } &#8211; \dfrac{x_{l} f(x_{r}) }{ f(x_{l}) &#8211; f(x_{r}) } $$
</center>


  
finalmente,
  
<a name="eq10"></a>
  


<center>
  $$ x = x_{r} &#8211; \dfrac{ f(x_{r}) \left( x_{l} &#8211; x_{r} \right) }{ f(x_{l}) &#8211; f(x_{r}) } $$
</center>


  
A função acima utiliza uma chamada a menos de função &#8212; não chama $$f(x_{l}) $$ &#8212; e possui uma multiplicação a menos. Isto significa uma pequena diminuição no _overhead_, ao ser implementada computacionalmente.

O método da falsa posição possui um algoritmo semelhante ao do Método da Bissecção, com a diferença que, ao invés de dividir o intervalo sempre pela metade, a fim de se obter a aproximação da raiz a partir do ponto médio, utiliza-se a expressão acima para aproximar a raiz.

Os passos seguidos pelo Regulsa Falsi podem ser sumarizados da seguinte forma:

  1. Escolhemos os limites do intervalo que deve incorporar a raiz, chamando os limites de $$x\_{l} $$ e $$x\_{r} $$ . Como uma raiz significa um ponto onde a função muda de sinal, o intervalo contém a raiz se $$F(x\_{r})F(x\_{l}) < 0 $$.
  2. Uma estimativa da raiz pode ser aproximada como $$x = x\_{r} &#8211; \dfrac{F(x\_{r})~(x\_{l} &#8211; x\_{r})}{F(x\_{l}) &#8211; F(x\_{r})} $$, sendo a única expressão que difere do Método da Bissecção.
  3. Verificamos para saber em qual subintervalo a raiz está 
      1. se $$F(x)F(x\_{l}) < 0 $$ , a raiz está no intervalo da esquerda. Faça $$x\_{r} = x $$ e volte ao passo $$2$$.
      2. se $$F(x)F(x\_{l}) > 0 $$ , a raiz não esta no intervalo da esquerda, logo, está no da direita, então faça $$x\_{l} = x $$ e volte ao passo $$2 $$ .
      3. se $$F(x)F(x_{l}) = 0 $$ , a raiz foi encontrada e é $$x $$ .

## 3. Implementação <a name="sec3"></a>

<div>
  <pre lang="python">def RegulaFalsi(F, xl, xr, errto=0.01, imax=1000):
    """
    Return the root of a function using Regula Falsi

    RegulaFalsi(fun, xl, xr, imax, errto)

    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error

    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons

    """
    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl)
    while errno &gt; errto and iterCount &lt; imax:
        xold = x
        iterCount = iterCount + 1
        fr = F(xr)
        x = xr - fr * (xl - xr) / (fl - fr)
        fx = F(x)
        if x != 0:
            errno = fabs((x - xold) / x)
        test = fl * fx
        if test &lt; 0:
            xr = x         
        elif test > 0:
            xl = x
            fl = fx
        else:
            errno = 0
    return x</pre>
</div>

Esta função está presente no arquivo: <a href="http://www.sawp.com.br/code/rootfind/regulafalsi.py" target="_blank">http://www.sawp.com.br/code/rootfind/regulafalsi.py</a>

## 4. Otimizando o Regula Falsi

Embora o Método Regula Falsi possa parecer superior ao da Bissecção, há casos em que seu desempenho é deficiente. Isto ocorre porque sua natureza é unilateral. Ou seja, conforme o programa executa e as iterações continuam, uma das extremidades do intervalo tende à permanecer fixa. Esse comportamento pode levar a uma redução na velocidade de convergência. Normalmente este problema acontece quando se está buscando raízes de uma função com curvatura muito brusca.

Uma maneira de otimizar este problema na convergência é fazer com que o programa perceba que uma extremidade está &#8220;presa&#8221;. Se estiver, o valor desta extremidade fixa é dividido pela metade, bis-seccionando o intervalo.

Esta abordagem, que consiste em aplicar o comportamento do Método da Bisseção no Regula Falsi, chamaremos de &#8220;Método da Falsa Posição Modificado&#8221; ou &#8220;Regula Falsi Otimizado&#8221;.

Os códigos abaixo implementam esse recurso. Os contadores _leftCount_ e _rightCount_ são aplicados para determinar quando uma extremidade está presa por mais de duas iterações. Quando isto ocorre, a função que está fixa é dividida pela metade.

As alterações feitas com base no código demonstrado anteriormente, foram demarcadas com o comentário _&#8220;\#O2&#8221;_ ao lado. A implementação é:

<div>
  <pre lang="python">def RegulaFalsi_O2(F, xl, xr, errto=0.01, imax=1000):
    """
    Return the root of a function using Regula Falsi

    RegulaFalsi_O2(fun, xl, xr, imax, errto)

    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents

    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons

    """
    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl)
    leftCount = 0 # O2
    rightCount = 0 # O2
    while errno >= errto and iterCount &lt; = imax:
        xold = x
        iterCount = iterCount + 1
        fr = F(xr)
        # x = (xl+xr)/2.l ponto onde modifica a Bisseccao
        x = xr - fr * (xl - xr) / (fl - fr)
        fx = F(x)
        if x != 0:
            errno = fabs((x - xold) / x)
        test = fl * fx
        if test &lt; 0: 
            xr = x 
            fr = fx # O2
            rightCount = 0 # O2
            leftCount += 1 # O2
            if leftCount >= 2:
                fl = fl / 2 # O2
        elif test > 0:
            xl = x
            fl = fx
            fl = F(xl) # O2
            leftCount = 0 # O2
            rightCount += 1 #O2
            if rightCount >= 2:
                fr = fr / 2 # O2
        else:
            errno = 0
    return x</pre>
</div>

Um exemplo de utilização desta função pode ser encontrado em: <a href="http://www.sawp.com.br/code/rootfind/regulafalsi_modificado.py" target="_blank">http://www.sawp.com.br/code/rootfind/regulafalsi_modificado.py</a>

## 5. Copyright

Este documento está disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"></a>
  </p>
  
  <p>
    <a name="bibitem1"><b>[1]</b> Ralston, Anthony and Rabinowitz, Philip, <em>A First Course in Numerical Analysis.(2nd ed.)</em> McGraw-Hill and Dover, (2001), 338.</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco, <em>Cálculo Numérico</em> Pearson Prentice Hall, (2006), 83.</a>
  </p>
</fieldset>
