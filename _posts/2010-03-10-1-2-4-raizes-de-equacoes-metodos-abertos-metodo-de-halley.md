---
id: 485
title: '1.2.4 Raízes de Equações &#8212; Métodos Abertos &#8212; Método de Halley'
date: 2010-03-10T22:12:01+00:00
author: SAWP
excerpt: ' O método inventado pelo físico Edmond Halley, é um algoritmo que consiste em aplicar o Método de Newton-Raphson duas vezes, gerando uma fórmula de aproximação com dependência da função, da primeira e da segunda derivada, possuindo a vantagem de convergir cubicamente à raiz.'
layout: post
guid: http://www.sawp.com.br/blog/?p=485
permalink: /p=485
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4450:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> Halley<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> d1f<span style="color: #66cc66;">,</span> d2f<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function (using the Halley Method)
    &nbsp;
    Halley(f, d1f, d2f, x0=1.0, errto=0.001, imax=100)
    &nbsp;
    * f: Function where find the roots
    * d1f: analytic derivative of f
    * d2f: second derivative of f
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    return: the root next x0
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &nbsp;
    Dec 2009
    &quot;&quot;&quot;</span>
    &nbsp;
    xn <span style="color: #66cc66;">=</span> x0
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    x0 <span style="color: #66cc66;">=</span> xn
    xn <span style="color: #66cc66;">=</span> xn - <span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span>*f<span style="color: black;">&#40;</span>xn<span style="color: black;">&#41;</span>*d1f<span style="color: black;">&#40;</span>xn<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span>*d1f<span style="color: black;">&#40;</span>xn<span style="color: black;">&#41;</span>*d1f<span style="color: black;">&#40;</span>xn<span style="color: black;">&#41;</span> - f<span style="color: black;">&#40;</span>xn<span style="color: black;">&#41;</span>*d2f<span style="color: black;">&#40;</span>xn<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> xn <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>xn-x0<span style="color: black;">&#41;</span>/xn<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> xn</pre></td></tr></table><p class="theCode" style="display:none;">def Halley(f, d1f, d2f, x0=1.0, errto=0.001, imax=100):
    &quot;&quot;&quot;
    Return the root of a function (using the Halley Method)
    
    Halley(f, d1f, d2f, x0=1.0, errto=0.001, imax=100)
    
    * f: Function where find the roots
    * d1f: analytic derivative of f
    * d2f: second derivative of f
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    
    return: the root next x0
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    
    Dec 2009
    &quot;&quot;&quot;
    
    xn = x0
    errno = errto + 1
    iterCount = 0
    
    while errno &gt; errto and iterCount &lt; imax:
    x0 = xn
    xn = xn - (2*f(xn)*d1f(xn))/(2*d1f(xn)*d1f(xn) - f(xn)*d2f(xn))
    iterCount += 1
    
    if xn != 0:
    errno = fabs((xn-x0)/xn)
    
    return xn</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> </p> 

O Método de Halley é usado para busca de raízes de funções reais de uma variável que possuam primeira e segunda derivadas contínuas. 

Inventado pelo físico Edmond Halley, é um algoritmo que consiste em aplicar o Método de Newton-Raphson duas vezes, gerando uma expressão com dependência da função, da primeira e da segunda derivada. 

Apesar de exigir a dependência da primeira e segunda derivada, possui a vantagem de convergir a uma taxa cúbica à raiz, ao invés de quadrática, como no caso do Newton-Raphson. 

## 2. Desenvolvimento do Método de Halley <a name="sec2"></a> 

Considere a função iteração abaixo:
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ x_{i+1}=x_{i}-{\dfrac {u_{i}}{Q \left( u_{i} \right) } $$<br />
</center>


    
onde $$u\_{i}={\dfrac {f\_{i} \left( x \right) }{\dfrac {d}{dx}f_{i} \left( x \right) } $$ e $$Q$$ é um polinômio. 

O Método de Halley diz que se $$Q $$ for uma função linear, então é possível obter uma função iteração de terceira ordem, obedecendo a forma do método de Newton-Raphson[[1]](#bibitem1). 

Supondo uma função $$g $$ tal que
    
<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ g={\dfrac {f \left( x \right) }{\sqrt {\dfrac {d}{dx}f \left( x\right) }} $$<br />
</center>


    
A função $$f $$ é aquela cuja raiz tal que $$f(x) = 0 $$ queremos encontrar. Agora derivamos a função g definida acima, gerando a expressão
    
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ {\dfrac {d}{dx}g \left( x \right) =\sqrt {\dfrac {d}{dx}f \left( x \right) }-\dfrac{1}{2}\,{\dfrac {f \left( x \right) {\dfrac {d^{2}{d{x}^{2}}f \left( x \right)}{ \left( {\dfrac {d}{dx}f \left( x \right) \right) ^{3/2}} $$<br />
</center>


    


<center>
  <br /> $$\Downarrow $$<br />
</center>


    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ {\dfrac {d}{dx}g \left( x \right) =\dfrac{1}{2}\,{\dfrac {2\, \left( {\dfrac {d}{ dx}f \left( x \right) \right) ^{2}-f \left( x \right) {\dfrac {d^{2} {d{x}^{2}}f \left( x \right) }{ \left( {\dfrac {d}{dx}f \left( x\right) \right) ^{3/2}} $$<br />
</center>

Agora usaremos a função de iteração do Método de Newton-Raphson. Contudo, ao invés de utilizarmos a função $$f $$ e sua derivada na busca da raiz, usaremos as expressões derivadas de $$g $$ , ou seja
      
<a name="eq5">(eq5)</a>
      


<center>
  <br /> $$ x_{n+1}=x_{n}-{\dfrac {g \left( x_{n} \right) }{\dfrac {d}{dx}g \left( x_{n} \right) }$$<br />
</center>


    
onde
    
<a name="eq6">(eq6)</a>
      


<center>
  <br /> $$ {\dfrac {g \left( x_{n} \right) }{\dfrac {d}{dx}g \left( x_{n} \right) }=f \left( x \right) {\dfrac {1}{\sqrt {\dfrac {d}{dx}f\left( x \right) }}\left( \sqrt {\dfrac {d}{dx}f \left( x \right) }-1/2\,{\dfrac {f \left( x \right) {\dfrac {d^{2}{d{x}^{2}}f \left( x\right) }{ \left( {\dfrac {d}{dx}f \left( x\right) \right) ^{3/2}} \right) ^{-1}$$<br />
</center>

A Equação [6](#eq6) pode ser reescrita de uma forma mais simples,
    
<a name="eq7">(eq7)</a>
      


<center>
  <br /> $$ {\dfrac {g \left( x_{n} \right) }{\dfrac {d}{dx}g \left( x_{n} \right) }=2\,{\dfrac {f \left( x \right) {\dfrac {d}{dx}f \left( x \right) }{2\, \left( {\dfrac {d}{dx}f \left( x \right) \right) ^{2} &#8211; f \left( x \right) {\dfrac {d^{2}{d{x}^{2}}f \left( x \right) } $$<br />
</center>

Aplicando a Equação [7](#eq7) na iteração da Equação [5](#eq5) geramos a expressão usada pelo Método de Halley:
    
<a name="eq8">(eq8)</a>
      


<center>
  <br /> $$ x_{n+1}=x_{n}-2\,{\dfrac {f \left( x \right) {\dfrac {d}{dx}f \left( x \right) }{2\, \left( {\dfrac {d}{dx}f \left( x \right) \right) ^{2}-f \left( x \right) {\dfrac {d^{2}{d{x}^{2}}f \left( x \right) } $$<br />
</center>

<!-- IMPLEMENTAÇÃO -->

## 3. Implementação <a name="sec3"></a> </p> 



<div>
  <pre lang="python">def Halley(f, d1f, d2f, x0=1.0, errto=0.001, imax=100):
    """
    Return the root of a function (using the Halley Method)

    Halley(f, d1f, d2f, x0=1.0, errto=0.001, imax=100)

    * f: Function where find the roots
    * d1f: analytic derivative of f
    * d2f: second derivative of f
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed

    return: the root next x0

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>

    Dec 2009
    """

    xn = x0
    errno = errto + 1
    iterCount = 0

    while errno > errto and iterCount &lt; imax:
        x0 = xn
        xn = xn - (2*f(xn)*d1f(xn))/(2*d1f(xn)*d1f(xn) - f(xn)*d2f(xn))
        iterCount += 1

        if xn != 0:
            errno = fabs((xn-x0)/xn)

    return xn</pre>
</div>

Um exemplo de utilização desta função pode ser encontrado em: <a href="http://www.sawp.com.br/code/rootfind/halley.py" target="_blank">http://www.sawp.com.br/code/rootfind/halley.py</a> </p> 

## 4. Conclusões <a name="sec4"></a> 

O Método de Halley utiliza uma transformação $$g(f(x)) $$ para aplicação do método de Newton-Raphson. Este tipo de abordagem é muito comum quando queremos criar uma função de iteração que acelere a convergência à raiz. 

Existe uma generalização da abordagem utilizada por Halley para quando deseja-se construir um algoritmo de busca de raízes com taxa de convergência com ordem superior à três, conhecido como &#8220;Transformada de Householder&#8221;. </p> </p> 

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a></a><br /> <a name="bibitem1"><b>[1]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 401&#8211;402.</p> 
    
    <p>
      </a><br /> <a name="bibitem2"><b>[2]</b> </a><a href="http://math.fullerton.edu/mathews/n2003/Halley%27sMethodMod.html" target="_blank">http://math.fullerton.edu/mathews/n2003/Halley&#8217;sMethodMod.htm</a>
    </p></fieldset>
