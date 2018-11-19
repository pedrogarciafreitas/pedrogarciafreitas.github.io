---
id: 375
title: '1.1.1 Raízes de Equações &#8212; Métodos Intervalares &#8212; Método da Bissecção'
date: 2010-03-09T12:07:51+00:00
author: SAWP
excerpt: |
  Neste artigo é apresentada uma introdução aos métodos intervalares de busca de raízes. Para tais métodos, a primeira exposição é feita sobre as buscas incrementais, que consistem basicamente em testar a nulidade da imagem da função após cada incremento feito dentro do intervalo.
  
  basicamente todos os métodos intervalares fazem uma busca incremental, modificando apenas os seus critérios de teste. Desta forma, surge naturalmente o Método da Bissecção como consequência da busca de raízes dentro de um intervalo.
layout: post
guid: http://www.sawp.com.br/blog/?p=375
permalink: p=375
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:4685:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> Bissecc<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">500</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.01</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function using Bissection Method
    &nbsp;
    Bissecc(fun, xl, xr, imax, errto)
    &nbsp;
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;</span>
    &nbsp;
    x <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    xold <span style="color: #66cc66;">=</span> x
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xl + xr<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x - xold<span style="color: black;">&#41;</span> / x<span style="color: black;">&#41;</span> * <span style="color: #ff4500;">100</span>
    <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span> * F<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xr <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #808080; font-style: italic;"># test == 0 is when the F(x) is the root</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def Bissecc(F, xl, xr, imax=500, errto=0.01):
    &quot;&quot;&quot;
    Return the root of a function using Bissection Method
    
    Bissecc(fun, xl, xr, imax, errto)
    
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;
    
    x = 0
    iterCount = 0
    errno = 1
    while errno &gt; errto and iterCount &lt; imax:
    xold = x
    x = (xl + xr) / 2
    iterCount += 1
    if x != 0:
    errno = fabs((x - xold) / x) * 100
    test = F(xl) * F(x)
    if test &lt; 0:
    xr = x
    elif test &gt; 0:
    xl = x
    else:
    # test == 0 is when the F(x) is the root
    errno = 0
    return x</p></div>
    ;i:2;s:5258:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> Bissecc_O1<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">500</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.01</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function using Bissection Method
    &nbsp;
    Bissecc_O1(fun, xl, xr, imax, errto)
    &nbsp;
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;</span>
    &nbsp;
    x <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># used in O1</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    xold <span style="color: #66cc66;">=</span> x
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xl + xr<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    fx <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># O1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x - xold<span style="color: black;">&#41;</span> / x<span style="color: black;">&#41;</span> * <span style="color: #ff4500;">100</span>
    <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> * fx <span style="color: #808080; font-style: italic;"># O1 reduce the funcion call:test = F(xl)*F(x)</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xr <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #808080; font-style: italic;"># test == 0 is when the F(x) is the root</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def Bissecc_O1(F, xl, xr, imax=500, errto=0.01):
    &quot;&quot;&quot;
    Return the root of a function using Bissection Method
    
    Bissecc_O1(fun, xl, xr, imax, errto)
    
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;
    
    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl) # used in O1
    while errno &gt; errto and iterCount &lt; imax:
    xold = x
    x = (xl + xr) / 2
    iterCount += 1
    fx = F(x) # O1
    if x != 0:
    errno = fabs((x - xold) / x) * 100
    test = fl * fx # O1 reduce the funcion call:test = F(xl)*F(x)
    if test &lt; 0:
    xr = x
    elif test &gt; 0:
    xl = x
    else:
    # test == 0 is when the F(x) is the root
    errno = 0
    return x</p></div>
    ;i:3;s:5886:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> Bissecc_O2<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.01</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function using Bissection Method
    &nbsp;
    Bissecc_O2(fun, xl, xr, imax, errto)
    &nbsp;
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;</span>
    &nbsp;
    x <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># used in O1</span>
    imax <span style="color: #66cc66;">=</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>ceil<span style="color: black;">&#40;</span>fabs<span style="color: black;">&#40;</span>log<span style="color: black;">&#40;</span>fabs<span style="color: black;">&#40;</span>xr-xl<span style="color: black;">&#41;</span>/errto<span style="color: black;">&#41;</span>/log<span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># used in O2</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    xold <span style="color: #66cc66;">=</span> x
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xl+xr<span style="color: black;">&#41;</span>/<span style="color: #ff4500;">2</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    fx <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># O1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x - xold<span style="color: black;">&#41;</span> / x<span style="color: black;">&#41;</span> * <span style="color: #ff4500;">100</span>
    <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> * fx <span style="color: #808080; font-style: italic;"># O1 reduce the funcion call:test = F(xl)*F(x)</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xr <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #808080; font-style: italic;"># test == 0 implies x is the root</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def Bissecc_O2(F, xl, xr, errto=0.01):
    &quot;&quot;&quot;
    Return the root of a function using Bissection Method
    
    Bissecc_O2(fun, xl, xr, imax, errto)
    
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;
    
    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl) # used in O1
    imax = int(ceil(fabs(log(fabs(xr-xl)/errto)/log(2)))) # used in O2
    while errno &gt; errto and iterCount &lt; imax:
    xold = x
    x = (xl+xr)/2
    iterCount += 1
    fx = F(x) # O1
    if x != 0:
    errno = fabs((x - xold) / x) * 100
    test = fl * fx # O1 reduce the funcion call:test = F(xl)*F(x)
    if test &lt; 0:
    xr = x
    elif test &gt; 0:
    xl = x
    else:
    # test == 0 implies x is the root
    errno = 0
    return x</p></div>
    ;i:4;s:5491:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> Bissecc_O3<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.01</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function using Bissection Method
    &nbsp;
    Bissecc_O3(fun, xl, xr, imax, errto)
    &nbsp;
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;</span>
    &nbsp;
    x <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># used in O1</span>
    imax <span style="color: #66cc66;">=</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>ceil<span style="color: black;">&#40;</span>fabs<span style="color: black;">&#40;</span>log<span style="color: black;">&#40;</span>fabs<span style="color: black;">&#40;</span>xr-xl<span style="color: black;">&#41;</span>/errto<span style="color: black;">&#41;</span>/log<span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># used in O2</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    xold <span style="color: #66cc66;">=</span> x
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xl + xr<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    fx <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># O1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> x <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x - xold<span style="color: black;">&#41;</span> / x<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> * fx <span style="color: #808080; font-style: italic;"># O1 reduce the funcion call:test = F(xl)*F(x)</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xr <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">test</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #808080; font-style: italic;"># test == 0 is when the F(x) is the root</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def Bissecc_O3(F, xl, xr, errto=0.01):
    &quot;&quot;&quot;
    Return the root of a function using Bissection Method
    
    Bissecc_O3(fun, xl, xr, imax, errto)
    
    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &quot;&quot;&quot;
    
    x = 0
    iterCount = 0
    fl = F(xl) # used in O1
    imax = int(ceil(fabs(log(fabs(xr-xl)/errto)/log(2)))) # used in O2
    while iterCount &lt; imax:
    xold = x
    x = (xl + xr) / 2
    iterCount += 1
    fx = F(x) # O1
    if x != 0:
    errno = fabs((x - xold) / x)
    test = fl * fx # O1 reduce the funcion call:test = F(xl)*F(x)
    if test &lt; 0:
    xr = x
    elif test &gt; 0:
    xl = x
    else:
    # test == 0 is when the F(x) is the root
    errno = 0
    return x</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1">(sec1)</a> 



Métodos intervalares que buscam raízes de funções consistem em checar se uma função muda de sinal dentro de um intervalo específico. Conhecidas também como _&#8220;bracketing methods&#8221;_, elas exigem duas estimativas iniciais para a raiz. Estas &#8220;estimativas&#8221; são os limites do intervalo inicial, contenedor da raiz. A partir do intervalo inicial, delimitado pelas estimativas, utilizam-se diferentes métodos para diminuir a largura deste intervalo a fim de aproximar a solução correta. 



## 2. Métodos de buscas incrementais <a name="sec2">(sec2)</a> 



Para entendermos os métodos numéricos que encontram zeros de funções devemos compreender antes o conceito de busca incremental. 

Métodos de buscas incrementais são métodos intervalares que detectam subintervalos no qual a função muda de sinal. Como definido na introdução como _&#8220;bracking methods&#8221;_, devemos alterar o intervalo de forma refinar a busca pela raiz. 

A busca incremental divide o intervalo formado inicialmente em diversos subintervalos, depois busca nestes onde ocorre a mudança de sinal. O processo é repetido no subintervalo onde a raiz foi detectada, dividindo o subintervalo em pedaços menores, a fim de refinar a aproximação da raiz. 

Um problema da potencial para a escolha da busca incremental é a escolha do comprimento do incremento. Se o comprimento é muito pequeno, a busca pode demorar muito tempo. Se o comprimento for muito grande, há possibilidade de o próprio incremento incorporar várias raízes, se elas estiverem muito próximas, não sendo possível detectá-las. 



## 3. Método da bissecção (Método de Bolzano) <a name="sec3">(sec3)</a> 



O método da bissecção pode ser chamado de &#8220;método da divisão do intervalo na metade&#8221; e tem este nome porque é uma busca incremental no qual sempre se divide o intervalo ao meio, gerando dois novos subintervalos, contidos no anterior. 

Após cada subdivisão, aplicam-se os critérios que caracterizam este método: se a função muda de sinal em um intervalo, calcula-se o seu ponto médio. A posição da raiz é determinada como sendo este ponto médio dentro do subintervalo no qual a mudança de sinal ocorreu, repetindo este processo até que a aproximação esteja próxima o suficiente. 

O algoritmo, basicamente, pode ser descrito da seguinte forma: 

  1. Escolhemos os limites do intervalo que incorpora a raiz, chamando estes limites de \(x\_{l} \) e \(x\_{r} \) . Como uma raiz significa um ponto onde a função muda de sinal, o intervalo pode ser verificado como sendo contenedor da raiz se \(F(x\_{r})F(x\_{l}) < 0\). 
  2. Uma estimativa da raiz pode ser aproximada como \(x = \dfrac{ x_{l} + x{r} }{2} \) . Com isso, divide-se o intervalo inicial em dois subintervalos idênticos. 
  3. Verificamos para saber em qual subintervalo a raiz está: 
      1. se \(F(x)F(x\_{l}) < 0 \) , a raiz está no intervalo da esquerda. Faça \(x\_{r} = x \) e volte ao passo \(2 \) . 
      2. se \(F(x)F(x\_{l}) > 0 \) , a raiz não esta no intervalo da esquerda, logo, está no da direita, então faça \(x\_{l} = x \) e volte ao passo \(2 \) . 
      3. se \(F(x)F(x_{l}) = 0 \) , a raiz foi encontrada e é \(x \) .



## 4. Implementação <a name="sec4">(sec4)</a> 



<pre lang="python">def Bissecc(F, xl, xr, imax=500, errto=0.01):
    """
    Return the root of a function using Bissection Method

    Bissecc(fun, xl, xr, imax, errto)

    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error 

    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>
    """

    x = 0
    iterCount = 0
    errno = 1
    while errno > errto and iterCount &lt; imax:
        xold = x
        x = (xl + xr) / 2
        iterCount += 1
        if x != 0:
            errno = fabs((x - xold) / x) * 100
        test = F(xl) * F(x)
        if test &lt; 0:
            xr = x
        elif test > 0:
            xl = x
        else:
            # test == 0 is when the F(x) is the root
           errno = 0
    return x</pre>



Esta implementação funciona bem para qualquer função _F_ que retorne um valor real, sendo que outras variantes destes códigos podem ser implementadas, podendo usar tipos de tamanho maior, recursos de paralelização, etc. Apesar do código acima funcionar bem, ainda podemos melhorá-lo com algumas otimizações. 



### 4.1. Otimizando o Método da Bissecção 



Ainda que o código anterior permita bons resultados, em um programa real pode acontecer da função _F_ precisar ser chamada milhares de vezes. Caso isso ocorra, é extremamente interessante buscar otimizações no método a fim de fornecer um algoritmo menos caro para ser processado. 

No caso de um método numérico, como o da Bissecção, uma possível melhoria de se implementação consiste em minimizar o _overhead_ das chamada de funções, como é feito no código abaixo. Ao comparamos ele com a implementação anterior, é possível observar que algumas variáveis foram inseridas a fim de evitar que uma mesma função seja chamada mais de uma vez para calcular o mesmo valor. Por exemplo: 

<pre lang="python">def Bissecc_O1(F, xl, xr, imax=500, errto=0.01):
    """
    Return the root of a function using Bissection Method

    Bissecc_O1(fun, xl, xr, imax, errto)

    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents

    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>
    """

    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl) # used in O1
    while errno > errto and iterCount &lt; imax:
        xold = x
        x = (xl + xr) / 2
        iterCount += 1
        fx = F(x) # O1
        if x != 0:
            errno = fabs((x - xold) / x) * 100
        test = fl * fx # O1 reduce the funcion call:test = F(xl)*F(x)
        if test &lt; 0:
            xr = x
        elif test > 0:
            xl = x
        else:
            # test == 0 is when the F(x) is the root
           errno = 0
    return x</pre>



As linhas inseridas em relação ao código original possuem o comentário _&#8220;\#O1&#8221;_ , indicando a primeira otimização feita. 

Sem as novas linhas inseridas, o código não minimiza a chamada de funções. Enquanto que no caso não otimizado, para cada iteração há duas chamadas de função que calculam o mesmo valor, no caso otimizado esta repetição de cálculo é desfeita quando acumulamos o valor da função anterior na variável _&#8220;fl&#8221;_ . Assim, reduzimos a quantidade de chamadas da função de \(2n \) vezes para apenas \((n+1) \), onde \(n \) é o número de iterações necessárias para convergir à raiz. 

Em casos onde \(n \) seja muito grande, reduzir à metade o número de chamadas de função pode significar uma melhoria considerável para eficiência de todo sistema. 

Outro passo para uma otimização interessante consiste em aplicar alguma espécie de otimização matemática &#8212; reduzindo-se a complexidade do algoritmo, aplicando-se otimização numérica, estocástica etc. Sempre que for aplicável uma otimização numérica, ela deve ser feita. 

Uma propriedade útil do Método da Bissecção é que ele permite que o número de iterações necessárias para se chegar ao erro absoluto &#8212; o erro de tolerância que é passado na implementação, usado como critério de parada &#8212; sejam calculadas antecipadamente, ou seja, antes de começar as iterações. 

Desta forma, antes de começar o algoritmo, o erro absoluto \(E \) pode ser pré-determinado da seguinte maneira:
    
<a name="eq1">(eq1)</a> 

<center>
  \( E^0 = x_{r}^0 &#8211; x_{l}^0 \)
</center>

chamando o intervalo inicial delimitado por \(\left[ x\_{l}, x\_{r} \right] \) de 

<a name="eq2">(eq2)</a>

<center>
  \( \Delta x^0 = x_{r}^0 &#8211; x_{l}^0 \)
</center>

temos que, o erro absoluto no início do programa será 

<a name="eq3">(eq3)</a>

<center>
  \( E^0 = \Delta x^0 \)
</center>

Portanto, este erro será dado como o tamanho do intervalo, que será sempre reduzido à metade a cada iteração. Sendo assim, logo na primeira iteração o erro terá a forma: 

<a name="eq4">(eq4)</a>

<center>
  \( E^0 = \dfrac{1}{2} \Delta x^0 \)
</center>

como a cada iteração, este processo é repetido, o n-ésimo erro absoluto será sempre a metade do erro anterior, sendo possível relacioná-lo com o primeiro intervalo dado: 

<a name="eq5">(eq5)</a>

<center>
  \( E^n = \dfrac{ \Delta x^0 }{ 2^n } \)
</center>

ou seja, se o erro de tolerância necessita de \(n \) iterações, então ele será o _n-ésimo_ erro dado pela fórmula acima. 

Chamaremos de \(E_{wanted} \) o erro máximo desejado, que é definido de acordo com as necessidades do programa em que a implementação está envolvida. A partir dele podemos prever o número de iterações máximas que serão necessárias para o método convergir satisfatoriamente à raiz.
    
<a name="eq6">(eq6)</a> 

<center>
  \( E_{wanted} = \dfrac{ \Delta x^0 }{ 2^n } \)
</center>

<center>
  <br /> \(\Downarrow \)<br />
</center>


    
<a name="eq7">(eq7)</a>

<center>
  \( 2^n = \dfrac{ \Delta x^0 }{ E_{wanted} } \)
</center>

<center>
  <br /> \(\Downarrow \)
</center>


    
<a name="eq8">(eq8)</a>

<center>
  \( ln(2^n) = ln \left( \dfrac{ \Delta x^0 }{ E_{wanted} } \right) \)
</center>

<center>
  <br /> \(\Downarrow \)
</center>


    
<a name="eq9">(eq9)</a>

<center>
  \( n~ln(2) = ln \left( \dfrac{ \Delta x^0 }{ E_{wanted} } \right) = ln(\Delta x^0) &#8211; ln(E_{wanted}) \)
</center>

<center>
</center>

logo, o número de iterações máximas necessárias será:
    
<a name="eq10">(eq10)</a>

<center>
  \( n = \dfrac{ ln \left( \dfrac{\Delta x^0}{ E_{wanted} } \right) }{ ln(2) } \)
</center>

Em um código real, ao aplicarmos este recurso, podemos reduzir o número de parâmetros passados, fornecendo à função apenas o erro de tolerância desejado. Um exemplo desta abordagem implementada pode ser vista abaixo: 



<pre lang="python">def Bissecc_O2(F, xl, xr, errto=0.01):
    """
    Return the root of a function using Bissection Method

    Bissecc_O2(fun, xl, xr, imax, errto)

    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error ( for aprox. ), in percents

    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>
    """

    x = 0
    iterCount = 0
    errno = 1
    fl = F(xl) # used in O1
    imax = int(ceil(fabs(log(fabs(xr-xl)/errto)/log(2)))) # used in O2
    while errno > errto and iterCount &lt; imax:
        xold = x
        x = (xl+xr)/2
        iterCount += 1
        fx = F(x) # O1
        if x != 0:
            errno = fabs((x - xold) / x) * 100
        test = fl * fx # O1 reduce the funcion call:test = F(xl)*F(x)
        if test &lt; 0:
            xr = x
        elif test > 0:
            xl = x
        else:
            # test == 0 implies x is the root
            errno = 0
    return x</pre>



Como o objetivo destas modificações é otimizar o programa, retiramos os testes baseados na convergência, visto que eles são desnecessários, pois o Método da Bissecção sempre converge e o número de iterações máximo é previsto. Desta forma, a variável _errno_ se torna desnecessária, e sua retirada reduz o número de desvios condicionais que o programa deve fazer. Desta forma, o código mais otimizado possível é: 

<pre lang="python">def Bissecc_O3(F, xl, xr, errto=0.01):
    """
    Return the root of a function using Bissection Method

    Bissecc_O3(fun, xl, xr, imax, errto)

    * fun: Function where find the roots
    * xl: left bound of interval
    * xr: right bound of interval
    * imax: max of iterations allowed
    * errto: tolerated error

    Author: Pedro Garcia [sawp@sawp.com.br]
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>
    """

    x = 0
    iterCount = 0
    fl = F(xl) # used in O1
    imax = int(ceil(fabs(log(fabs(xr-xl)/errto)/log(2)))) # used in O2
    while iterCount &lt; imax:
        xold = x
        x = (xl + xr) / 2
        iterCount += 1
        fx = F(x) # O1
        if x != 0:
            errno = fabs((x - xold) / x)
        test = fl * fx # O1 reduce the funcion call:test = F(xl)*F(x)
        if test &lt; 0:
            xr = x
        elif test > 0:
            xl = x
        else:
            # test == 0 is when the F(x) is the root
           errno = 0
    return x</pre>



Estes códigos estão disponíveis para download em: 

  * <a href="http://www.sawp.com.br/code/rootfind/bisseccao.py" target="_blank">http://www.sawp.com.br/code/rootfind/bisseccao.py</a>
  * <a href="http://www.sawp.com.br/code/rootfind/bisseccao_optimized1.py" target="_blank">http://www.sawp.com.br/code/rootfind/bisseccao_optimized1.py</a>
  * <a href="http://www.sawp.com.br/code/rootfind/bisseccao_optimized2.py" target="_blank">http://www.sawp.com.br/code/rootfind/bisseccao_optimized2.py</a>
  * <a href="http://www.sawp.com.br/code/rootfind/bisseccao_optimized3.py" target="_blank">http://www.sawp.com.br/code/rootfind/bisseccao_optimized3.py</a>

## 5. Copyright 



Este documento está disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 40-42.</p> 
    
    <p>
      </a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 66.</a>
    </p></fieldset>
