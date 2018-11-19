---
id: 507
title: '1.3.6 Raízes de Equações &#8212; Raízes de Polinômios &#8212; O Método de Laguerre'
date: 2010-03-10T23:28:59+00:00
author: SAWP
excerpt: O Método de Laguerre é um algoritmo numérico modificado a partir do Método de Newton para encontrar raízes complexas de polinômios. Sendo um método muito eficiente na busca de um zero de função, pois sempre converge à alguma raiz, independente da aproximação inicial dada (propriedade nem sempre presente em outros métodos computacionais). A principal desvantagem do Método de Laguerre é que ele não encontra todas raízes do polinômio, aproximando satisfatoriamente bem apenas à uma delas. Neste artigo, apresento uma pequena demonstração das relações matemáticas usadas na implementação, também presente.
layout: post
guid: http://www.sawp.com.br/blog/?p=507
permalink: /p=507
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5927:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> laguerre<span style="color: black;">&#40;</span>p<span style="color: #66cc66;">,</span> d1p<span style="color: #66cc66;">,</span> d2p<span style="color: #66cc66;">,</span> polDegree<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function (using the Laguerre Method)
    &nbsp;
    laguerre(p, d1p, d2p, polDegree, x0=1.0, errto=0.001, imax=100)
    &nbsp;
    * p: Function where find the roots
    * d1p: analytic derivative of f
    * d2p: second derivative of f
    * polDegree: grau do polinomio
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    return: the root next x0
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Dec 2009
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> polDegree
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1.0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    xn <span style="color: #66cc66;">=</span> x0
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    x0 <span style="color: #66cc66;">=</span> xn
    px <span style="color: #66cc66;">=</span> p<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    d1px <span style="color: #66cc66;">=</span> d1p<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    d2px <span style="color: #66cc66;">=</span> d2p<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    H <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>*d1px*d1px - n*px*d2px<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> fabs<span style="color: black;">&#40;</span>d1px + sqrt<span style="color: black;">&#40;</span>H<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&gt;</span> fabs<span style="color: black;">&#40;</span>d1px - sqrt<span style="color: black;">&#40;</span>H<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    xn <span style="color: #66cc66;">=</span> x0 - n*px/<span style="color: black;">&#40;</span>d1px + sqrt<span style="color: black;">&#40;</span>H<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    xn <span style="color: #66cc66;">=</span> x0 - n*px/<span style="color: black;">&#40;</span>d1px - sqrt<span style="color: black;">&#40;</span>H<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> xn <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>xn-x0<span style="color: black;">&#41;</span>/xn<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> xn</pre></td></tr></table><p class="theCode" style="display:none;">def laguerre(p, d1p, d2p, polDegree=1, x0=1.0, errto=0.001, imax=100):
    &quot;&quot;&quot;
    Return the root of a function (using the Laguerre Method)
    
    laguerre(p, d1p, d2p, polDegree, x0=1.0, errto=0.001, imax=100)
    
    * p: Function where find the roots
    * d1p: analytic derivative of f
    * d2p: second derivative of f
    * polDegree: grau do polinomio
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    
    return: the root next x0
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Dec 2009
    &quot;&quot;&quot;
    n = polDegree
    errno = errto + 1.0
    iterCount = 0
    xn = x0
    while errno &gt; errto and iterCount &lt; imax:
    x0 = xn
    px = p(x0)
    d1px = d1p(x0)
    d2px = d2p(x0)
    H = (n-1)*((n-1)*d1px*d1px - n*px*d2px)
    if fabs(d1px + sqrt(H)) &gt; fabs(d1px - sqrt(H)):
    xn = x0 - n*px/(d1px + sqrt(H))
    else:
    xn = x0 - n*px/(d1px - sqrt(H))
    iterCount += 1
    if xn != 0:
    errno = fabs((xn-x0)/xn)
    return xn</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

O método nomeado em homenagem ao matemático francês Edmond Laguerre, consiste em aproximar raízes de um polinômio $$p(x) $$ . 

Ele possui a vantagem sobre o Método de Bairstow de possuir uma taxa de convergência superior em uma ordem &#8212; ou seja, converge cubicamente &#8211;, não importando a aproximação inicial dada. 

Sendo baseado no Método de Newton, encontra a raiz real mais próxima da estimativa inicial. Contudo, ao contrário do primeiro, que pode não convergir, dependendo da aproximação inicial dada, o Método de Laguerre sempre irá convergir à uma raiz real, independendo de qual seja esta estimativa. Todavia, ele não permite que todas as raízes do polinômio sejam encontradas, além de não possuir garantia de convergência no caso do polinômios possuir raízes complexas. Por isso, uma abordagem interessante ao se trabalhar polinômios é utilizar o método de Bairstow para se encontrar suas raízes e, então, refinar a aproximação utilizando-se o método de Laguerre, uma vez que o primeiro possui uma taxa de convergência menor e costuma ser computacionalmente mais caro. 

## 2. Desenvolvimento do Método de Laguerre <a name="sec2"></a> 

Seja o polinômio:
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ p \left( x \right) =C\prod _{i=1}^{n}x-x_{i} $$<br />
</center>


    
Tomando seu logaritmo,
    
<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ \ln \left( p \left( x \right) \right) =\ln \left( C \right) +\sum _ {i=1}^{n}\ln \left( x-x_{i} \right) $$<br />
</center>


    
Chamaremos de $$S_{1} $$ a derivada da função acima,
    
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ S_{1}={\dfrac {d}{dx}\ln \left( p \left( x \right) \right) = \sum _{i=1}^{n} \left( \ln \left( x-x_{i} \right) \right)^{-1} $$<br />
</center>


    
Tomando $$S_{2} $$ como a derivada segunda da mesma função:
    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ S_{2}={\dfrac {d^{2}{d{x}^{2}}\ln \left( p \left( x \right)\right) = \sum _{i=1}^{n} \left( \ln \left( x-x_{i} \right) \right) ^{-2} $$<br />
</center>

Podemos assumir que a raiz $$x_1 $$ está a uma certa distância $$a $$ de um valor $$x $$ qualquer e que todas as outras estão à uma distância $$b $$ deste mesmo ponto. Ou seja:
    
<a name="eq5">(eq5)</a>
      


<center>
  <br /> $$ a=x-x_{1}$$<br />
</center>

<a name="eq6">(eq6)</a>
      


<center>
  <br /> $$ b=x-x_{i} $$<br />
</center>


    
onde $$i = 2,3,\ldots,n $$ . 

Com estas expressões, podemos escrever $$S\_{1} $$ e $$S\_{2} $$ em termos de $$a $$ e $$b $$ :
    
<a name="eq7">(eq7)</a>
      


<center>
  <br /> $$ S_{1}={a}^{-1}+{\dfrac {n-1}{b} $$<br />
</center>

<a name="eq8">(eq8)</a>
      


<center>
  <br /> $$ S_{2}={a}^{-2}+{\dfrac {n-1}{b}^{2}} $$<br />
</center>


    
Isolando $$b $$ , podemos escrever $$a $$ em termos de $$S\_{1} $$ e $$S\_{2}$$ :
    
<a name="eq9">(eq9)</a>
      


<center>
  <br /> $$ a={\dfrac {n}{S_{1}+\sqrt { \left( n-1 \right) \left( nS_{2}-{S_{1}}^{2} \right) }} $$<br />
</center>


    
tomando $$S\_{1}={\dfrac {\dfrac {d}{dx}p \left( x \right) }{p \left( x \right) } $$ em $$S\_{2} $$ , uma vez que $$S\_{2}={S\_{1}}^{2}-{\dfrac {\dfrac {d^{2}{d{x}^{2}}p \left( x \right) }{p \left( x \right) }$$, teremos:
      


<center>
  <br /> $$ S_{2}={\dfrac { \left( {\dfrac {d}{dx}p \left( x \right) \right) ^{2}-p \left( x \right) {\dfrac {d^{2}{d{x}^{2}}p \left( x \right) }{\left( p \left( x \right) \right) ^{2}} $$<br />
</center>

Desta forma, podemos obter $$a $$ em termos da função $$f(x) $$ e suas derivadas:
    
<a name="eq10">(eq10)</a>
      


<center>
  <br /> $$ a={\dfrac {nf \left( x \right) }{\dfrac {d}{dx}f \left( x \right) + \sqrt {H \left( x \right) }} $$<br />
</center>


    
onde $$H \left( x \right) = \left( n-1 \right) \left( nS\_{2}-{S\_{1}}^{2}\right) $$ , portanto $$H(x)$$ pode ser expresso como:
    
<a name="eq11">(eq11)</a>
      


<center>
  <br /> $$ H \left( x \right) = \left( n-1 \right) \left( \left( n-1 \right) \left( {\dfrac {d}{dx}f \left( x \right) \right) ^{2}-nf \left( x \right) {\dfrac {d^{2}{d{x}^{2}}f \left( x \right) \right) $$<br />
</center>


    
como $$x\_{i+1}=x\_{i}-a $$ , então
    
<a name="eq12">(eq12)</a>
      


<center>
  <br /> $$ x_{i+1}=x_{i}-{\dfrac {nf \left( x_{i} \right) }{\dfrac {d}{dx}f \left( x_{i} \right) +\sqrt {H \left( x_{i} \right) }} $$<br />
</center>

A Equação [12](#eq12) é a usada pelo Método de Laguerre. </p> 

## 3. Taxa de Convergência <a name="seq3"></a> 

A demonstração da taxa de convergência cúbica é muito semelhante àquela apresentada no artigo sobre o Método de Halley, já que ambas recebem a primeira e segunda derivada. Note que naquele artigo utilizamos Séries de Taylor para aproximar à função utilizada no algoritmo. Se seguirmos os mesmos passos com a função polinomial, obteremos a mesma expressão para o erro. </p> 

## 4. Implementação <a name="seq4"></a> 

<pre lang="python">def laguerre(p, d1p, d2p, polDegree=1, x0=1.0, errto=0.001, imax=100):
    """
    Return the root of a function (using the Laguerre Method)

    laguerre(p, d1p, d2p, polDegree, x0=1.0, errto=0.001, imax=100)

    * p: Function where find the roots
    * d1p: analytic derivative of f
    * d2p: second derivative of f
    * polDegree: grau do polinomio 
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed

    return: the root next x0

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
         http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Dec 2009
    """
    n = polDegree
    errno = errto + 1.0
    iterCount = 0
    xn = x0
    while errno > errto and iterCount &lt; imax:
        x0 = xn
        px = p(x0)
        d1px = d1p(x0)
        d2px = d2p(x0)
        H = (n-1)*((n-1)*d1px*d1px - n*px*d2px)
        if fabs(d1px + sqrt(H)) > fabs(d1px - sqrt(H)):
            xn = x0 - n*px/(d1px + sqrt(H))
        else:
            xn = x0 - n*px/(d1px - sqrt(H))
        iterCount += 1
        if xn != 0:
            errno = fabs((xn-x0)/xn)
    return xn</pre>

Note que esta função pode ser utilizada também para aproximação de funções não-polinomiais com bastante sucesso. Alguns exemplos de utilização desta implementação estão em: <a href="http://www.sawp.com.br/code/rootfind/laguerre.py" target="_blank">http://www.sawp.com.br/code/rootfind/laguerre.py</a> </p> </p> 

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a></a><br /> <a name="bibitem1"><b>[1]</b> </a><a href="http://en.wikipedia.org/wiki/Laguerre&#37;27s_method" target="_blank">http://en.wikipedia.org/wiki/Laguerre&#37;27s_method</a><br /> <a name="bibitem2"><b>[2]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 380.</a>
  </p>
</fieldset>
