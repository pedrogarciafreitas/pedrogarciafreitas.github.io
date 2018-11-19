---
id: 544
title: '1.2.8 Raízes de Equações &#8212; Métodos Abertos &#8212; Método de Newton Interpolado'
date: 2010-03-12T12:53:31+00:00
author: SAWP
excerpt: Neste artigo, apresentaremos a implementação de uma função de iteração modificada do Método de Newton que permite aproximar uma raiz a uma taxa de convergência de quinta ordem.
layout: post
guid: http://www.sawp.com.br/blog/?p=544
permalink: p=544
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5782:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> Newton5order<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> df<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">500</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of function (Interpolated Newton-Raphson for 5th order)
    &nbsp;
    Newton5order(f, df, x0=1.0, errto=0.001, imax=500)
    &nbsp;
    * f: Function where find roots
    * df: derivative of f
    * x0: next point (estimative)
    * errto: tolerated error ( for aprox. )
    * imax: max of iterations allowed
    &nbsp;
    return: root next x0
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &nbsp;
    Jan 2009
    &quot;&quot;&quot;</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    f0 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    df0 <span style="color: #66cc66;">=</span> df<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> df0 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    x1 <span style="color: #66cc66;">=</span> x0 - f0/df0
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    x1 <span style="color: #66cc66;">=</span> x0 - f0/errto
    &nbsp;
    f1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span>
    df1 <span style="color: #66cc66;">=</span> df<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>df0 * df0 + <span style="color: #ff4500;">7.0</span> * df1 * df1<span style="color: black;">&#41;</span> * df0 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    x2 <span style="color: #66cc66;">=</span> x1 - <span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">5.0</span> * df0 * df0 + <span style="color: #ff4500;">3.0</span> * df1 * df1<span style="color: black;">&#41;</span> * f1<span style="color: black;">&#41;</span> / \
    <span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>df0 * df0 + <span style="color: #ff4500;">7.0</span> * df1 * df1<span style="color: black;">&#41;</span> * df0<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    x2 <span style="color: #66cc66;">=</span> x1
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> x2 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x2 - x0<span style="color: black;">&#41;</span>/x2<span style="color: black;">&#41;</span>
    &nbsp;
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    x0 <span style="color: #66cc66;">=</span> x2
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> x2</pre></td></tr></table><p class="theCode" style="display:none;">def Newton5order(f, df, x0=1.0, errto=0.001, imax=500):
    &quot;&quot;&quot;
    Return the root of function (Interpolated Newton-Raphson for 5th order)
    
    Newton5order(f, df, x0=1.0, errto=0.001, imax=500)
    
    * f: Function where find roots
    * df: derivative of f
    * x0: next point (estimative)
    * errto: tolerated error ( for aprox. )
    * imax: max of iterations allowed
    
    return: root next x0
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    
    Jan 2009
    &quot;&quot;&quot;
    errno = errto + 1
    iterCount = 0
    
    while errno &gt; errto and iterCount &lt; imax:
    f0 = f(x0)
    df0 = df(x0)
    
    if df0 != 0:
    x1 = x0 - f0/df0
    else:
    x1 = x0 - f0/errto
    
    f1 = f(x1)
    df1 = df(x1)
    
    if (df0 * df0 + 7.0 * df1 * df1) * df0 != 0:
    x2 = x1 - ((5.0 * df0 * df0 + 3.0 * df1 * df1) * f1) / \
    ((df0 * df0 + 7.0 * df1 * df1) * df0)
    else:
    x2 = x1
    
    if x2 != 0:
    errno = fabs((x2 - x0)/x2)
    
    iterCount += 1
    x0 = x2
    
    return x2</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

Uma vantagem deste método é que, assim como o Método de Newton, ele requer apenas que a função e a sua primeira derivada seja passada, sendo livre de derivadas superiores, como corre nos Métodos de Halley e de HouseHolder. 

A idéia deste algoritmo está em utilizar o Método de Newton para uma primeira aproximação da raiz, seguida de uma interpolação inversa para refinar esta aproximação. Uma abordagem semelhante foi apresentada no artigo sobre busca de raízes com Interpolação Quadrática Inversa. 

## 2. Desenvolvimento do Método <a name="sec2"></a> 

Pelo Método de Newton sabemos que uma raiz pode ser aproximada a partir da própria função e sua derivada a partir da fórmula:
      
<a name="eq1">(eq1)</a>
      


<center>
  <br /> \( x_{n+1}=x_{n}-{\dfrac {f \left( x_{n} \right) }{\dfrac {d}{dx}f \left( x_{n} \right) } \)<br />
</center>

Todavia, para facilitar a notação, vamos renomear as variáveis da Equação [1](#eq1) de tal forma que \(x\_{1}=x\_{n+1} \) e \(x\_{0}=x\_{n} \) ,
    
implicando na expressão:
      
<a name="eq2">(eq2)</a>
      


<center>
  <br /> \( x_{1}=x_{0}-{\dfrac {f \left( x_{0} \right) }{\dfrac {d}{dx}f \left( x_{0} \right) } \)<br />
</center>

Aplicando a Equação [2](#eq2) como primeira estimativa, dentro da mesma iteração podemos refinar a aproximação da raiz através da seguinte função:
      
<a name="eq3">(eq3)</a>
      


<center>
  <br /> \( x_{2}=x_{1}-{\dfrac { \left( 5\, \left( {\dfrac {d}{dx}f \left( x_{0} \right) \right) ^{2}+3\, \left( {\dfrac {d}{dx}f \left( x_{1} \right) \right) ^{2} \right) f \left( x_{1} \right) }{ \left( \left( {\dfrac {d}{dx}f \left( x_{0} \right) \right) ^{2}+7\, \left( {\dfrac {d}{dx}f \left( x_{1} \right) \right) ^{2} \right) {\dfrac {d}{dx}f \left( x_{0} \right) } \)<br />
</center>

Para simplificar esta fórmula, adotamos \(df\_{k}={\dfrac {d}{dx}f \left( x\_{k} \right) \) e \(f\_{k}=f \left( x\_{k} \right) \), ou seja, \(df\_{0}={\dfrac {d}{dx}f \left( x\_{0} \right) \) , \(df\_{1}={\dfrac {d}{dx}f \left( x\_{1} \right) \) , \(f\_{0}=f \left( x\_{0} \right) \) , \(f\_{1}=f \left( x\_{1} \right) \) e \(x\_1=x\_0-{\dfrac {f\_{0}}{df\_{0}} \) , e substituímos na Equação [3](#eq3):
      
<a name="eq4">(eq4)</a>
      


<center>
  <br /> \( x_2=x_1-{\dfrac { \left( 5\,{df_{0}}^{2}+3\,{df_{1}}^{2} \right) f_{1}}{ \left( {df_{0}}^{2}+7\,{df_{1}}^{2} \right) df_{0}}\)<br />
</center>

Esta função é de grande utilidade, uma vez que possui os mesmos requisitos do Método de Newton-Raphson &#8212; função e a sua primeira derivada &#8212; mas com eficiência superior. Sendo que a maioria dos métodos numéricos que buscam raízes são derivados a partir do Método de Newton, utilizando este recurso podemos aprimorar diversos algoritmos. 

No artigo em que esta fórmula é apresentada, o autor demonstra a ordem de convergência do seu método, sendo que a análise da taxa de aproximação, pode ser encontrada no artigo _An efficient Newton-type method with fifth-order convergence for solving nonlinear equations_[[1]](#bibitem1). 

<!--  IMPLEMENTACAO  --></p> 

## 3. Implementação <a name="sec3"></a> 

<div>
  <pre lang="python">def Newton5order(f, df, x0=1.0, errto=0.001, imax=500):
    """
    Return the root of function (Interpolated Newton-Raphson for 5th order)

     Newton5order(f, df, x0=1.0, errto=0.001, imax=500)

    * f: Function where find roots
    * df: derivative of f
    * x0: next point (estimative)
    * errto: tolerated error ( for aprox. )
    * imax: max of iterations allowed

    return: root next x0

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>

    Jan 2009
    """
    errno = errto + 1
    iterCount = 0

    while errno > errto and iterCount &lt; imax:
        f0 = f(x0)
        df0 = df(x0)

        if df0 != 0:
            x1 = x0 - f0/df0
        else:
            x1 = x0 - f0/errto

        f1 = f(x1)
        df1 = df(x1)

        if (df0 * df0 + 7.0 * df1 * df1) * df0 != 0:
            x2 = x1 - ((5.0 * df0 * df0 + 3.0 * df1 * df1) * f1) / \
                      ((df0 * df0 + 7.0 * df1 * df1) * df0)
        else:
            x2 = x1        

        if x2 != 0:
            errno = fabs((x2 - x0)/x2)

        iterCount += 1
        x0 = x2

    return x2</pre>
</div>

Um exemplo de como utilizar esta função pode ser encontrado em <a href="http://www.sawp.com.br/code/rootfind/Newton5order.py" target="_blank">http://www.sawp.com.br/code/rootfind/Newton5order.py</a> </p> </p> 

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> L. FANG, L. SUN and G. HE,<cite> <em>An efficient Newton-type method with fifth-order convergence for solving nonlinear equations</em>,</cite> Computational and Applied Mathematics, <b>V.27</b>(N.3)(2008), 269&#8211;274.</a>
  </p>
</fieldset>
