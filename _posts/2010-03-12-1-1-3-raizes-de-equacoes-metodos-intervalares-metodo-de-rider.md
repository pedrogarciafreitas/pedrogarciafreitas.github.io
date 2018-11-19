---
id: 563
title: '1.1.3 Raízes de Equações &#8212; Métodos Intervalares &#8212; Método de Rider'
date: 2010-03-12T14:53:58+00:00
author: SAWP
excerpt: 'O Método de Ridder consiste em avaliar a aproximação parcial -- obtida em cada iteração pelo Método da Falsa Posição -- em uma função de ajuste exponencial, a fim de otimizar a busca pela raiz.'
layout: post
guid: http://www.sawp.com.br/blog/?p=563
permalink: p=563
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:9067:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> ridders<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> xl<span style="color: #66cc66;">,</span> xr<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.01</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1000</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function (Using the Ridder's Method)
    &nbsp;
    ridders(fun, xl, xr, imax, errto)
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
    x <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    fr <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xr<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>xl<span style="color: black;">&#41;</span>
    d0 <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>fr - <span style="color: #dc143c;">fl</span><span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> xr - fr*<span style="color: black;">&#40;</span>xl-xr<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span><span style="color: #dc143c;">fl</span> - fr<span style="color: black;">&#41;</span>
    fx <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    &nbsp;
    a <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #dc143c;">fl</span> - fx<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>fx - fr<span style="color: black;">&#41;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #dc143c;">fl</span> - fx<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span><span style="color: #dc143c;">fl</span> - a*fx<span style="color: black;">&#41;</span>
    beta <span style="color: #66cc66;">=</span> b - <span style="color: #ff4500;">1</span>
    alfa <span style="color: #66cc66;">=</span> a - <span style="color: #ff4500;">1</span>
    lnb <span style="color: #66cc66;">=</span> beta - beta*beta/<span style="color: #ff4500;">2</span> + beta*beta*beta/<span style="color: #ff4500;">3</span>
    lna <span style="color: #66cc66;">=</span> alfa - alfa*alfa/<span style="color: #ff4500;">2</span> + alfa*alfa*alfa/<span style="color: #ff4500;">3</span>
    root <span style="color: #66cc66;">=</span> xl + d0*lnb/lna
    froot <span style="color: #66cc66;">=</span> F<span style="color: black;">&#40;</span>root<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">fl</span> * fx <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> xl <span style="color: #66cc66;">&lt;</span> root <span style="color: #ff7700;font-weight:bold;">and</span> root <span style="color: #66cc66;">&lt;</span> x:
    <span style="color: #ff7700;font-weight:bold;">if</span> fx * froot <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> root
    xr <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    xr <span style="color: #66cc66;">=</span> root
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    xr <span style="color: #66cc66;">=</span> x
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">fl</span> * fx <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> x <span style="color: #66cc66;">&lt;</span> root <span style="color: #ff7700;font-weight:bold;">and</span> root <span style="color: #66cc66;">&lt;</span> xr:
    <span style="color: #ff7700;font-weight:bold;">if</span> fx * froot <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">0</span>:
    xl <span style="color: #66cc66;">=</span> x
    xr <span style="color: #66cc66;">=</span> root
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    xl <span style="color: #66cc66;">=</span> root
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> froot
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    xl <span style="color: #66cc66;">=</span> x
    <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">=</span> fx
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">fl</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    x <span style="color: #66cc66;">=</span> xl
    <span style="color: #ff7700;font-weight:bold;">break</span>
    &nbsp;
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xr - xl<span style="color: black;">&#41;</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def ridders(F, xl, xr, errto=0.01, imax=1000):
    &quot;&quot;&quot;
    Return the root of a function (Using the Ridder's Method)
    
    ridders(fun, xl, xr, imax, errto)
    
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
    fr = F(xr)
    fl = F(xl)
    d0 = abs(fr - fl)
    x = xr - fr*(xl-xr)/(fl - fr)
    fx = F(x)
    
    a = (fl - fx)/(fx - fr)
    b = (fl - fx)/(fl - a*fx)
    beta = b - 1
    alfa = a - 1
    lnb = beta - beta*beta/2 + beta*beta*beta/3
    lna = alfa - alfa*alfa/2 + alfa*alfa*alfa/3
    root = xl + d0*lnb/lna
    froot = F(root)
    
    if fl * fx &lt; 0:
    if xl &lt; root and root &lt; x:
    if fx * froot &lt; 0:
    xl = root
    xr = x
    else:
    xr = root
    else:
    xr = x
    elif fl * fx &gt; 0:
    if x &lt; root and root &lt; xr:
    if fx * froot &lt; 0:
    xl = x
    xr = root
    else:
    xl = root
    fl = froot
    else:
    xl = x
    fl = fx
    else:
    if fl == 0:
    x = xl
    break
    
    errno = abs(xr - xl)
    iterCount += 1
    return x</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

O Método de Ridder consiste em avaliar a aproximação parcial &#8212; obtida em cada iteração pelo Método da Falsa Posição &#8212; em uma função de ajuste exponencial, a fim de otimizar a busca pela raiz. 

A ideia é semelhante àquela usada pelo Método de Brent, cuja busca intervalar é combinada com um método aberto que possua taxa de convergência superior. Assim como o Método de Brent, possui a vantagem de convergir sempre a uma taxa média superior aos dos métodos intervalares normais. </p> 

## 2. Desenvolvimento do Método <a name="sec2"></a> 

Como queremos encontrar \(f \left( x \right) =0 \) , vamos tomar
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> \(f \left( x \right) = A+B{e^{Cx}}\)<br />
</center>

Sejam três valores de x que estejam delimitando de alguma forma um intervalo que contenha a raiz tal que \(\{x\_{left}, x\_{predictor}, x\_{right}\} \) , cuja amplitude seja \(d\_{{0}}= \left| x\_{{left}}-x\_{{right}} \right| \) .Podemos utilizar o Método da Falsa posição para obter uma aproximação da raiz a partir desses pontos neste intervalo: 

<a name="eq2">(eq2)</a>
      


<center>
  <br /> \( x_{{predictor}}=FalsaPosicao \left( x_{{left}},x_{{{\it right}}} \right) \)<br />
</center>

A proposição feita por Ridder é de realizar uma segunda aproximação a partir da fórmula: 

<a name="eq3">(eq3)</a>
      


<center>
  <br /> \( x_{{corrector}}=x_{{left}}+d_{{0}} \left\{ {\frac {\ln \left( \beta \right) }{\ln \left( \alpha \right) }} \right\} \)<br />
</center>


    
onde: 

<a name="eq4">(eq4)</a>
      


<center>
  <br /> \( \alpha={\frac {f_{{left}}-f_{{predictor}}}{f_{{predictor}}-f_{{right}}}} \)<br />
</center>

<a name="eq5">(eq5)</a>
      


<center>
  <br /> \(\beta={\frac {f_{{left}}-f_{{predictor}}}{f_{{predictor}}-\alpha\,f_{{right}}}} \)<br />
</center>

<a name="eq6">(eq6)</a>
      


<center>
  <br /> \( f_{{predictor}}=f \left( x_{{predictor}} \right) \)<br />
</center>

<a name="eq7">(eq7)</a>
      


<center>
  <br /> \( f_{{left}}=f \left( x_{{left}} \right) \)<br />
</center>

<a name="eq8">(eq8)</a>
      


<center>
  <br /> \( f_{{right}}=f \left( x_{{right}} \right) \)<br />
</center>

Da série logarítmica[[afken]](#bibitemafken), temos:
    
<a name="eq9">(eq9)</a>
      


<center>
  <br /> \( \ln \left( 1+x \right) =\sum _{n=1}^{\infty }{\frac { \left( -1\right) ^{n-1}{x}^{n}}{n}} = x-\dfrac{1}{2}\,{x}^{2}+\dfrac{1}{3}\,{x}^{3} \)<br />
</center>

Uma aproximação satisfatória para o caso pode ser obtida usando-se até o terceiro termo. Desta forma, para \( x=\beta-1 \) temos: 

<a name="eq10">(eq10)</a>
      


<center>
  <br /> \( \ln \left( 1+ \left\{ \beta-1 \right\} \right) =\beta-1-\dfrac{1}{2}\, \left( \beta-1 \right) ^{2}+\dfrac{1}{3}\, \left( \beta-1 \right) ^{3} \)<br />
</center>


    
portanto, 

<a name="eq11">(eq11)</a>
      


<center>
  <br /> \( \ln \left( \beta \right) =\beta-1-\dfrac{1}{2}\, \left( \beta-1 \right) ^{2}+\dfrac{1}{3}\, \left( \beta-1 \right) ^{3} \)<br />
</center>


    
Para simplificarmos a notação, adotaremos \(\phi\_{{\beta}}=\beta-1 \) e \(\phi\_{{\alpha}}=\alpha-1 \) . Desta forma, obtemos facilmente as expressões necessárias para aplicarmos ao método: 

<a name="eq12">(eq12)</a>
      


<center>
  <br /> \( \ln \left( \beta \right) =\phi_{{\beta}}-\dfrac{1}{2}\,{\phi_{{\beta}}}^{2}+\dfrac{1}{3}\,{\phi_{{\beta}}}^{3} \)<br />
</center>

e

<a name="eq13">(eq13)</a>
      


<center>
  <br /> \( \ln \left( \alpha \right) =\phi_{{\alpha}}-\dfrac{1}{2}\, {\phi_{{\alpha}}}^{2} +\dfrac{1}{3}\,{\phi_{{\alpha}}}^{3} \)<br />
</center>

<!--  IMPLEMENTACAO  --></p> 

## 3. Implementação <a name="sec3"></a> 

&nbsp;

<div>
  <pre lang="python">def ridders(F, xl, xr, errto=0.01, imax=1000):
     """
     Return the root of a function (Using the Ridder's Method)

     ridders(fun, xl, xr, imax, errto)

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
          fr = F(xr)
          fl = F(xl)
          d0 = abs(fr - fl)
          x = xr - fr*(xl-xr)/(fl - fr)
          fx = F(x)

          a = (fl - fx)/(fx - fr)
          b = (fl - fx)/(fl - a*fx)
          beta = b - 1
          alfa = a - 1
          lnb = beta - beta*beta/2 + beta*beta*beta/3
          lna = alfa - alfa*alfa/2 + alfa*alfa*alfa/3
          root = xl + d0*lnb/lna
          froot = F(root)

          if fl * fx &lt; 0:
               if xl &lt; root and root &lt; x:
                    if fx * froot &lt; 0:
                         xl = root
                         xr = x
                    else:
                         xr = root
               else:
                    xr = x
          elif fl * fx > 0:
               if x &lt; root and root &lt; xr:
                    if fx * froot &lt; 0:
                         xl = x
                         xr = root
                    else:
                         xl = root
                         fl = froot
               else:
                    xl = x
                    fl = fx
          else:
               if fl == 0:
                    x = xl
               break

          errno = abs(xr - xl)
          iterCount += 1
     return x</pre>
</div>

Disponível para download em <a href="http://www.sawp.com.br/code/rootfind/riders.py" target="_blank">http://www.sawp.com.br/code/rootfind/riders.py</a> </p> </p> 

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a></a><br /> <a name="bibitemafken"><b>[afken]</b> G. ARFKEN and H. WEBER, <cite> <em>Mathematical methods for physicists</em>, </cite> Elsevier, <b>6th Edition</b>(ISBN 978-85-352-2050-6) (2007), 269&#8211;270.</a><br /> <a name="bibitem1"><b>[1]</b> </a><a href="http://en.wikipedia.org/wiki/Ridders&#37;27_method" target="_blank">http://en.wikipedia.org/wiki/Ridders&#37;27_method</a>
  </p>
</fieldset>
