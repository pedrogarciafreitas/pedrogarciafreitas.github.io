---
id: 558
title: '1.4.1 Raízes de Equações &#8212; Métodos Mistos &#8212; Método de Brent'
date: 2010-03-12T14:04:50+00:00
author: SAWP
excerpt: 'O Método de Brent é uma combinação simples de diversos métodos computacionais para busca de raízes de função. Os métodos usados no algoritmo de Brent são: Método da Bisseção, da Secante e Interpolação Quadrática Inversa.'
layout: post
guid: http://www.sawp.com.br/blog/?p=558
permalink: p=558
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:17078:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> brent<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">500</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of function (Using the Brent's Method)
    &nbsp;
    brent(f, xl, xr, errto=0.001, imax=500)
    &nbsp;
    * f: Function where find roots
    * xl: left bound of interval
    * xr: right bound of interval
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    return: root next xl
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &nbsp;
    Jan 2009
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    x <span style="color: #66cc66;">=</span> xl
    y <span style="color: #66cc66;">=</span> xr
    xrold <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    mflag <span style="color: #66cc66;">=</span> <span style="color: #008000;">True</span>
    delta <span style="color: #66cc66;">=</span> xr
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> f<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span> * f<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&gt;=</span> <span style="color: #ff4500;">0.0</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> Float<span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;nan&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>xr<span style="color: #66cc66;">,</span> xl<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xl<span style="color: #66cc66;">,</span> xr<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span>
    fr <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span>
    fx <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># try Inverse Quadratic Interpolation</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">!=</span> fx <span style="color: #ff7700;font-weight:bold;">and</span> fr <span style="color: #66cc66;">!=</span> fx:
    delta <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">7</span> * <span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> - fx
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">fl</span> - fr
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> fx - <span style="color: #dc143c;">fl</span>
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> fx - fr
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> fr - <span style="color: #dc143c;">fl</span>
    delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">6</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> fr - fx
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> disturb<span style="color: black;">&#40;</span>ecs<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span><span style="color: black;">&#40;</span>ecs <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> errto
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> ecs
    &nbsp;
    delta <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span>disturb<span style="color: #66cc66;">,</span> delta<span style="color: black;">&#41;</span>
    &nbsp;
    s <span style="color: #66cc66;">=</span> fx * fr * xl / <span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> * delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> + \
    <span style="color: #dc143c;">fl</span> * fr * x / <span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span> * delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> + \
    <span style="color: #dc143c;">fl</span> * fx * xr / <span style="color: black;">&#40;</span>delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#93;</span> * delta<span style="color: black;">&#91;</span><span style="color: #ff4500;">6</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># try Secant's Rule</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    s <span style="color: #66cc66;">=</span> xr - fr*<span style="color: black;">&#40;</span>xr - xl<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>fr - <span style="color: #dc143c;">fl</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: black;">&#40;</span>s <span style="color: #66cc66;">&gt;</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">3</span> * xl + xr<span style="color: black;">&#41;</span>/<span style="color: #ff4500;">4</span> <span style="color: #ff7700;font-weight:bold;">and</span> s <span style="color: #66cc66;">&lt;</span> xr<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> \
    <span style="color: black;">&#40;</span>mflag <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>s - xr<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&gt;=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xr - x<span style="color: black;">&#41;</span>/<span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> \
    <span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">not</span> mflag <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>s - xr<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&gt;=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>x - y<span style="color: black;">&#41;</span>/<span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> \
    <span style="color: black;">&#40;</span>mflag <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xr - x<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> \
    <span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">not</span> mflag <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>x - y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>delta<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    <span style="color: #808080; font-style: italic;"># bissection method</span>
    s <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xr + xl<span style="color: black;">&#41;</span>/<span style="color: #ff4500;">2</span>
    mflag <span style="color: #66cc66;">=</span> <span style="color: #008000;">True</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    mflag <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span>
    &nbsp;
    fs <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>s<span style="color: black;">&#41;</span>
    y <span style="color: #66cc66;">=</span> x
    x <span style="color: #66cc66;">=</span> xr
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">fl</span> * fs <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0.0</span>:
    xr <span style="color: #66cc66;">=</span> s
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    xl <span style="color: #66cc66;">=</span> s
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>xr<span style="color: #66cc66;">,</span> xl<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xl<span style="color: #66cc66;">,</span> xr<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> fs <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span> <span style="color: #ff7700;font-weight:bold;">or</span> f<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #ff7700;font-weight:bold;">break</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xr - xrold<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> delta:
    delta <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xr - xrold<span style="color: black;">&#41;</span>
    &nbsp;
    xrold <span style="color: #66cc66;">=</span> xr
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span>xr - xl<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> xr</pre></td></tr></table><p class="theCode" style="display:none;">def brent(f, xl, xr, errto=0.001, imax=500):
    &quot;&quot;&quot;
    Return the root of function (Using the Brent's Method)
    
    brent(f, xl, xr, errto=0.001, imax=500)
    
    * f: Function where find roots
    * xl: left bound of interval
    * xr: right bound of interval
    * errto: tolerated error
    * imax: max of iterations allowed
    
    return: root next xl
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    
    Jan 2009
    &quot;&quot;&quot;
    
    errno = errto + 1
    iterCount = 0
    x = xl
    y = xr
    xrold = 0
    mflag = True
    delta = xr
    
    if f(xl) * f(xr) &gt;= 0.0:
    return Float(&quot;nan&quot;)
    
    if abs(f(xl)) &lt; abs(f(xr)):
    (xr, xl) = (xl, xr)
    
    while errno &gt; errto and iterCount &lt; imax:
    fl = f(xl)
    fr = f(xr)
    fx = f(x)
    
    # try Inverse Quadratic Interpolation
    if fl != fx and fr != fx:
    delta = 7 * [0]
    delta[1] = fl - fx
    delta[2] = fl - fr
    delta[3] = fx - fl
    delta[4] = fx - fr
    delta[5] = fr - fl
    delta[6] = fr - fx
    
    def disturb(ecs):
    if(ecs == 0):
    return errto
    else:
    return ecs
    
    delta = map(disturb, delta)
    
    s = fx * fr * xl / (delta[1] * delta[2]) + \
    fl * fr * x / (delta[3] * delta[4]) + \
    fl * fx * xr / (delta[5] * delta[6])
    # try Secant's Rule
    else:
    s = xr - fr*(xr - xl)/(fr - fl)
    
    if (not (s &gt; (3 * xl + xr)/4 and s &lt; xr)) or \
    (mflag and abs(s - xr) &gt;= abs(xr - x)/2) or \
    (not mflag and abs(s - xr) &gt;= abs(x - y)/2) or \
    (mflag and abs(xr - x) &lt; abs(delta)) or \
    (not mflag and abs(x - y) &lt; abs(delta)):
    # bissection method
    s = (xr + xl)/2
    mflag = True
    else:
    mflag = False
    
    fs = f(s)
    y = x
    x = xr
    
    if fl * fs &lt; 0.0:
    xr = s
    else:
    xl = s
    
    if abs(f(xl)) &lt; abs(f(xr)):
    (xr, xl) = (xl, xr)
    
    if fs == 0 or f(xr) == 0:
    break
    
    if abs(xr - xrold) &lt; delta:
    delta = abs(xr - xrold)
    
    xrold = xr
    iterCount += 1
    errno = fabs(xr - xl)
    
    return xr</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

O Método de Brent é uma combinação simples de diversos métodos computacionais para busca de raízes de função. Os métodos usados no algoritmo de Brent são: Método da Bisseção, da Secante e Interpolação Quadrática Inversa. 

A ideia por trás deste algoritmo está em aproveitar as vantagens de cada uma das técnicas combinadas, procurando minimizar suas desvantagens. Desta forma, utiliza a Interpolação Quadrática Inversa sempre que as aproximações intermediárias não se sobrepõem (o que acarretaria em uma divisão por zero). Quando há a sobreposição, tenta fazer a próxima aproximação utilizando o Método da Secante. 

Todavia, estas duas últimas técnicas são suscetíveis à divergir ao longo da execução. Caso este comportamento seja detectado, o algoritmo &#8220;ativa&#8221; o Método da Bisseção a fim de reconverter a aproximação ao zero da função. 

Sumarizando, suas maiores vantagens são: tende a convergir rapidamente, não necessita de derivadas e sempre converge, caso a raiz esteja delimitada pelo intervalo necessário ao Método da Bisseção. 

Por outro lado, possui a desvantagem de exigir que um intervalo contendo a raiz seja fornecido, o que reduz a generalidade da aplicação do método em alguns casos. 

Este método, embora não apresente nenhuma novidade em termos matematicamente formais, é um algoritmo que foi vastamente usado e é presente em diversas bibliotecas e softwares como função-chave na aproximação de raízes. 

## 2. Implementação <a name="sec2"></a> 

<div>
  <pre lang="python">def brent(f, xl, xr, errto=0.001, imax=500):
    """
    Return the root of function (Using the Brent's Method)

    brent(f, xl, xr, errto=0.001, imax=500)

    * f: Function where find roots
    * xl: left bound of interval
    * xr: right bound of interval
    * errto: tolerated error
    * imax: max of iterations allowed

    return: root next xl

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
             &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>

    Jan 2009
    """

    errno = errto + 1
    iterCount = 0
    x = xl
    y = xr
    xrold = 0
    mflag = True
    delta = xr

    if f(xl) * f(xr) >= 0.0:
        return Float("nan")

    if abs(f(xl)) &lt; abs(f(xr)):
        (xr, xl) = (xl, xr)

    while errno > errto and iterCount &lt; imax:
        fl = f(xl)
        fr = f(xr)
        fx = f(x)

        # try Inverse Quadratic Interpolation
        if fl != fx and fr != fx:
            delta = 7 * [0] 
            delta[1] = fl - fx
            delta[2] = fl - fr
            delta[3] = fx - fl
            delta[4] = fx - fr
            delta[5] = fr - fl
            delta[6] = fr - fx

            def disturb(ecs):            
                if(ecs == 0):
                    return errto
                else:
                    return ecs

            delta = map(disturb, delta)

            s = fx * fr * xl / (delta[1] * delta[2]) + \
                fl * fr * x / (delta[3] * delta[4]) + \
                fl * fx * xr / (delta[5] * delta[6])
        # try Secant's Rule
        else:
            s = xr - fr*(xr - xl)/(fr - fl)

        if (not (s > (3 * xl + xr)/4 and s &lt; xr)) or \
            (mflag and abs(s - xr) >= abs(xr - x)/2) or \
            (not mflag and abs(s - xr) >= abs(x - y)/2) or \
            (mflag and abs(xr - x) &lt; abs(delta)) or \
            (not mflag and abs(x - y) &lt; abs(delta)):
                # bissection method
                s = (xr + xl)/2
                mflag = True
        else:
            mflag = False

        fs = f(s)
        y = x
        x = xr

        if fl * fs &lt; 0.0:
            xr = s
        else:
            xl = s

        if abs(f(xl)) &lt; abs(f(xr)):
            (xr, xl) = (xl, xr)

        if fs == 0 or f(xr) == 0:
            break

        if abs(xr - xrold) &lt; delta:
            delta = abs(xr - xrold)            

        xrold = xr
        iterCount += 1
        errno = fabs(xr - xl)

    return xr</pre>
</div>

Disponível para download em <a href="http://www.sawp.com.br/code/rootfind/brent.py" target="_blank">http://www.sawp.com.br/code/rootfind/brent.py</a> </p> </p> 

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a></a><br /> <a name="bibitem1"><b>[1]</b> <cite><a href="http://mathworld.wolfram.com/BrentsMethod.html">http://mathworld.wolfram.com/BrentsMethod.html</a></cite></a><br /> <a name="bibitem2"><b>[2]</b> <cite><a href="http://math.fullerton.edu/mathews/n2003/BrentMethodMod.html" target="_blank">http://math.fullerton.edu/mathews/n2003/BrentMethodMod.html</a></cite></a>
  </p>
</fieldset>
