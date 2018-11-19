---
id: 518
title: 1.3.4 Raízes de Equações – Raízes de Polinômios – O Método de Aberth
date: 2010-03-11T14:24:44+00:00
author: SAWP
excerpt: 'O Método de Aberth é uma algoritmo usado para encontrar todas as raízes de um polinômio de grau qualquer. '
layout: post
guid: http://www.sawp.com.br/blog/?p=518
permalink: /p=518
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:15277:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> aberth<span style="color: black;">&#40;</span>p<span style="color: #66cc66;">,</span> d1p<span style="color: #66cc66;">,</span> polDegree<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">500</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return all roots of Polynom (using the Aberth Method)
    &nbsp;
    aberth(p, d1p, polDegree=1, x0=1.0, errto=0.001, imax=100)
    &nbsp;
    * p: polynom where find the roots
    * d1p: analytic derivative of f
    * polDegree: polynom degree
    * x0: initial estimative (complex)
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    return: a list with all roots of polynom
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Dec 2009
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> filt<span style="color: black;">&#40;</span>l<span style="color: black;">&#41;</span>:
    r <span style="color: #66cc66;">=</span> l.<span style="color: black;">real</span>
    i <span style="color: #66cc66;">=</span> l.<span style="color: black;">imag</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>r<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> errto:
    r <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> errto:
    i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>r<span style="color: #66cc66;">,</span> i<span style="color: black;">&#41;</span>
    n <span style="color: #66cc66;">=</span> polDegree
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1.0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #008000;">list</span>:
    zold <span style="color: #66cc66;">=</span> x0<span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span> + <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>n-<span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #008000;">complex</span>:
    zold <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> x0+<span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    zold <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>*x0<span style="color: #66cc66;">,</span><span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>*x0<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    znew <span style="color: #66cc66;">=</span> n * <span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>zold<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    pz <span style="color: #66cc66;">=</span> p<span style="color: black;">&#40;</span>zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> pz <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> +<span style="color: #66cc66;">=</span> <span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    pz <span style="color: #66cc66;">=</span> p<span style="color: black;">&#40;</span>zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    dp1z <span style="color: #66cc66;">=</span> d1p<span style="color: black;">&#40;</span>zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    d <span style="color: #66cc66;">=</span> dp1z/pz
    s <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> w <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: black;">&#40;</span><span style="color: #008000;">range</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> + <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>i+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>zold<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    den <span style="color: #66cc66;">=</span> zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - zold<span style="color: black;">&#91;</span>w<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> den <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    den +<span style="color: #66cc66;">=</span> <span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    s +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>/<span style="color: black;">&#40;</span>den<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>d - s<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - <span style="color: #ff4500;">1.0</span>/<span style="color: black;">&#40;</span>d - s<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - <span style="color: #ff4500;">1.0</span>/<span style="color: black;">&#40;</span>d - s + errto*<span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>znew<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    t <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>/<span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&lt;</span> t:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> t
    zold <span style="color: #66cc66;">=</span> znew<span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    znew.<span style="color: black;">sort</span><span style="color: black;">&#40;</span>key<span style="color: #66cc66;">=</span><span style="color: #ff7700;font-weight:bold;">lambda</span> r: r.<span style="color: black;">real</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span>filt<span style="color: #66cc66;">,</span> znew<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def aberth(p, d1p, polDegree=1, x0=complex(1,1), errto=0.001, imax=500):
    &quot;&quot;&quot;
    Return all roots of Polynom (using the Aberth Method)
    
    aberth(p, d1p, polDegree=1, x0=1.0, errto=0.001, imax=100)
    
    * p: polynom where find the roots
    * d1p: analytic derivative of f
    * polDegree: polynom degree
    * x0: initial estimative (complex)
    * errto: tolerated error
    * imax: max of iterations allowed
    
    return: a list with all roots of polynom
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Dec 2009
    &quot;&quot;&quot;
    
    def filt(l):
    r = l.real
    i = l.imag
    if abs(r) &lt; errto:
    r = 0.0
    if abs(i) &lt; errto:
    i = 0.0
    return complex(r, i)
    n = polDegree
    errno = errto + 1.0
    iterCount = 0
    if type(x0) == list:
    zold = x0[:] + abs(n-len(x0))*[ complex(0,0) ]
    elif type(x0) == complex:
    zold = [ x0+random() for i in xrange(n) ]
    else:
    zold = [ complex(random()*x0,random()*x0) for i in xrange(n) ]
    znew = n * [ complex(0, 0) ]
    while errno &gt; errto and iterCount &lt; imax:
    for i in xrange(len(zold)):
    pz = p(zold[i])
    while pz == 0:
    zold[i] += random()
    pz = p(zold[i])
    dp1z = d1p(zold[i])
    d = dp1z/pz
    s = 0
    for w in (range(i) + range(i+1, len(zold))):
    den = zold[i] - zold[w]
    while den == 0:
    den += random()
    s += 1/(den)
    if (d - s) != 0:
    znew[i] = zold[i] - 1.0/(d - s)
    else:
    znew[i] = zold[i] - 1.0/(d - s + errto*random())
    errno = 0
    for i in xrange(len(znew)):
    if znew[i] != 0:
    t = abs(znew[i] - zold[i])/abs(znew[i])
    if errno &lt; t:
    errno = t
    zold = znew[:]
    iterCount += 1
    znew.sort(key=lambda r: r.real)
    return map(filt, znew)</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 



Apresentado por Oliver Aberth em seu artigo _&#8220;Iteration Methods for finding all zeros of a polynomial simultaneously&#8221;_, este método permite encontrar todas as raízes de um polinômio, desde que seja conhecido seu grau. 

Possui a vantagem do método de Bairstow de convergir à todas as raízes, sendo elas reais ou complexas, diferentemente do método de Laguerre. 

Sendo derivado do método de Newton, possui convergência quadrática e pode ocorrer das raízes não convergirem para polinômios aproximados (interpoladores de funções não-lineares). 

<!--  DESENVOLVIMENTO -->

## 2. Desenvolvimento do Método <a name="sec2"></a> </p> 

Seja o polinômio de grau $$n $$ formado por uma composição de coeficientes reais:
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ p \left( x \right) = p_{n}{x}^{n}+p_{n-1}{x}^{n-1} + \cdots + p_{1}x+p_{0} $$<br />
</center>

Supondo que este polinômio possui todas raízes complexas, ele pode ser descrito na forma fatorizada:
    
<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ p \left( x \right) =p_{n}\prod _{i=1}^{n}(x-z_{i}) $$<br />
</center>


    
onde $$z_{i} $$ são as raízes complexas de p(x). 

Podemos adicionar um termo neste produtório tal que $${C}{(x &#8211; z_{i})} = 1 $$ , que implica um termo a mais no produtório da Equação [2](#eq2). Contudo, ao invés de notarmos este produtório pelos índices $$i=1 \ldots n $$ , vamos tomar $$i=0 \ldots n $$.
    
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ p \left( x \right) =C\prod _{i=0}^{n}(z-x_{i}) $$<br />
</center>

Comparando as Fórmulas [2](#eq2) e [3](#eq3), observamos que a segunda é um polinômio que recebe um termo a mais em $$i=0 $$ . Para que $$p(x) $$ continue sendo o mesmo, o novo termo deve ser nulo ou então a seguinte relação válida:
    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ C=p_{n} \left( z_{k} \right) $$<br />
</center>

Isolando $$p_{n} $$ na Equação [2](#eq2) e levando na Equação [4](#eq4), temos que:
    
<a name="eq5">(eq5)</a>
      


<center>
  <br /> $$ C \left( x_{i} \right) ={\dfrac {p \left( x_{i} \right) }{\prod _{k=0}^{n}(x_{i}-z_{k})} $$<br />
</center>

Pelo método de Newton-Raphson, sabemos que uma raiz pode ser encontrada através da seguinte função de iteração:
    
<a name="eq6">(eq6)</a>
      


<center>
  <br /> $$ x_{i+1}=x_{i}-{\dfrac {f \left( x_{i} \right) }{\dfrac {d}{dx}f \left( x_{i} \right) } $$<br />
</center>


    
Usando a relação [5](#eq5) como sendo a fórmula a ser aplicada Equação [6](#eq6):
    
<a name="eq7">(eq7)</a>
      


<center>
  <br /> $$ f \left( x \right) =C \left( x \right) $$<br />
</center>


    
Resultando em:
    
<a name="eq8">(eq8)</a>
      


<center>
  <br /> $$ z_{i+1}=z_{i}-{\dfrac {C \left( z_{i} \right) }{\dfrac {d}{dx}C \left( z_{i} \right) } $$<br />
</center>

Uma propriedade interessante da função de iteração usada no Método de Newton é que ela equivale ao inverso da derivada do logaritmo da função. Ou seja, uma fórmula facilmente obtida usando-se a Regra da Cadeia[[1]](#bibitem1) é:
    
<a name="eq9">(eq9)</a>
      


<center>
  <br /> $$ {\dfrac {\dfrac {d}{dx}C \left( x \right) }{C \left( x \right) }={\dfrac {d}{dx}\ln \left( C \left( x \right) \right)$$<br />
</center>

Tomando o logaritmo da Equação [5](#eq5),
    
<a name="eq10">(eq10)</a>
      


<center>
  <br /> $$ \ln \left( C \left( x \right) \right) =\ln \left( {\dfrac {p \left( x_{i} \right) }{\prod _{k=0}^{n}(x_{i}-z_{k})} \right)$$<br />
</center>


    
onde
    
<a name="eq11">(eq11)</a>
      


<center>
  <br /> $$ \ln \left( C \left( x \right) \right) =\ln \left( p \left( x_{i} \right) \right) -\ln \left( \prod _{k=0}^{n}(x_{i}-z_{k})\right)$$<br />
</center>


    
como
    
<a name="eq12">(eq12)</a>
      


<center>
  <br /> $$ \ln \left( \prod _{k=0}^{n}x_{i}-z_{k} \right) =\sum _{k=0}^{n} \ln \left( \left| x-z_{k} \right| \right) $$<br />
</center>


    
Substituindo a equação [12](#eq12) em [11](#eq11),
    
<a name="eq13">(eq13)</a>
      


<center>
  <br /> $$ \ln \left( C \left( x \right) \right) =\ln \left( p \left( x_{i} \right) \right) -\sum _{k=0}^{n}\ln \left( \left| x-z_{k}\right| \right)$$<br />
</center>


    
Levando a Equação [13](#eq13) na Equação [9](#eq9), temos que:
    
<a name="eq14">(eq14)</a>
      


<center>
  <br /> $$ {\dfrac {\dfrac {d}{dx}C \left( x \right) }{C \left( x \right) }={\dfrac {\partial }{\partial x} \left( \ln \left( p \left( x \right) \right) -\sum _{j=0}^{n}\ln \left( \left| x-z_{j} \right| \right) \right) $$<br />
</center>

Aplicando novamente a relação mencionada para a expressão [9](#eq9), conseguimos eliminar o logaritmo do polinômio, onde deixamos a relação apenas com a própria função polinomial e sua derivada:
    
<a name="eq15">(eq15)</a>
      


<center>
  <br /> $$ {\dfrac {\dfrac {d}{dx}C \left( x \right) }{C \left( x \right) }={\dfrac {\dfrac {d}{dx}p \left( x \right) }{p \left( x \right) }-\sum _{j=0}^{n} \left( x-z_{j} \right) ^{-1}$$<br />
</center>


    
como o inverso da Equação [15](#eq15) é exatamente a função de iteração do Método de Newton, temos que:
    
<a name="eq16">(eq16)</a>
      


<center>
  <br /> $$ {\dfrac {C \left( z_{i} \right) }{\dfrac {d}{dx}C \left( z_{i} \right) }= \left( {\dfrac {\dfrac {d}{dx}p \left( x \right) }{p \left( x \right) }-\sum _{j=0}^{n} \left( x-z_{j} \right) ^{-1} \right) ^{-1} $$<br />
</center>


    
ou seja, do Método de Newton
    
<a name="eq17">(eq17)</a>
      


<center>
  <br /> $$ z_{i+1}=z_{i}-{\dfrac {C \left( z_{i} \right) }{\dfrac {d}{dx}C \left( z_{i} \right) } $$<br />
</center>


    
obtemos a expressão do Método de Aberth:
    
<a name="eq18">(eq18)</a>
      


<center>
  <br /> $$ z_{i+1}=z_{i}- \left( {\dfrac {\dfrac {d}{dx}p \left( x \right) }{ p \left( x \right) }-\sum _{j=0}{j \neq i}^{n} \left( z_{i}-z_{j} \right) ^{-1} \right) ^{-1} $$<br />
</center>

<!--  IMPLEMENTACAO -->

## 3. Implementação <a name="sec3"></a> 



<div>
  <pre lang="python">def aberth(p, d1p, polDegree=1, x0=complex(1,1), errto=0.001, imax=500):
    """
    Return all roots of Polynom (using the Aberth Method)

    aberth(p, d1p, polDegree=1, x0=1.0, errto=0.001, imax=100)

    * p: polynom where find the roots
    * d1p: analytic derivative of f
    * polDegree: polynom degree
    * x0: initial estimative (complex)
    * errto: tolerated error
    * imax: max of iterations allowed

    return: a list with all roots of polynom

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
         http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Dec 2009
    """

    def filt(l):
        r = l.real
        i = l.imag
        if abs(r) &lt; errto:
            r = 0.0
        if abs(i) &lt; errto:
            i = 0.0
        return complex(r, i)
    n = polDegree
    errno = errto + 1.0
    iterCount = 0
    if type(x0) == list:
        zold = x0[:] + abs(n-len(x0))*[ complex(0,0) ]
    elif type(x0) == complex:
        zold = [ x0+random() for i in xrange(n) ]
    else:
        zold = [ complex(random()*x0,random()*x0) for i in xrange(n) ]
    znew = n * [ complex(0, 0) ]
    while errno > errto and iterCount &lt; imax:
        for i in xrange(len(zold)):
            pz = p(zold[i])
            while pz == 0:
                zold[i] += random()
                pz = p(zold[i])  
            dp1z = d1p(zold[i])              
            d = dp1z/pz
            s = 0
            for w in (range(i) + range(i+1, len(zold))):
                den = zold[i] - zold[w]
                while den == 0:
                    den += random()
                s += 1/(den)
            if (d - s) != 0:
                znew[i] = zold[i] - 1.0/(d - s)
            else:
                znew[i] = zold[i] - 1.0/(d - s + errto*random())
        errno = 0
        for i in xrange(len(znew)):
            if znew[i] != 0:
                t = abs(znew[i] - zold[i])/abs(znew[i])
                if errno &lt; t:
                    errno = t
        zold = znew[:]
        iterCount += 1
    znew.sort(key=lambda r: r.real)
    return map(filt, znew)</pre>
</div>



Como todas raízes são desconhecidas, lista cujas raízes serão armazenadas é iniciada com valores aleatórios distribuídos sobre o plano complexo. Esta construção toma como base o valor passado no parâmetro $$x\_{0} $$ . Caso a estimativa inicial $$x\_{0} $$ seja uma lista, o algoritmo as utiliza e completa os outros elementos com um valor nulo. Contudo, é recomendável que todas as $$n $$ raízes recebam uma estimativa inicial. Além disso, a função _filt_ filtra os resultados cujo valor deu abaixo do erro estimado, servindo apenas para melhorar a visualização do resultado. Além disso, sob algumas restrições, esta implementação também permite que funções não-polinomiais sejam aproximadas com sucesso, como pode ser visto neste exemplo de utilização: <a href="http://www.sawp.com.br/code/rootfind/aberth.py" target="_blank">http://www.sawp.com.br/code/rootfind/aberth.py</a> 

<!--  COMENTÁRIOS  --></p> 

## 4. Conclusões <a name="sec4"></a> 

Assim como o método de Bairstow, o método de Aberth converge a uma taxa quadrática à todas raízes de um polinômio qualquer, sendo uma das soluções mais gerais e elegantes existentes. 

Possui a vantagem sobre o método de Bairstow de não exigir que sejam passados os coeficientes do polinômio como parâmetro para o algoritmo, sendo mais conveniente quando trabalhamos com uma função conhecida, com alto grau e grande quantidade de coeficientes. 

Todavia, possui a desvantagem de necessitar de uma função que compute a derivada analítica do polinômio, o que geralmente é fácil de se obter, mas que pode consumir considerável tempo de processamento. 

Além disso, como a função de iteração de Aberth é obtida diretamente do Método de Newton, ela carrega a desvantagem da estimativa inicial para convergir ao resultado correto. </p> 

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a></a><br /> <a name="bibitem1"><b>[1]</b> B.G. Thomas,<cite> <em>Cálculo, volume 1</em>,</cite> Addison Wesley, <b>V.1</b>,(2002), 179.</a><br /> <a name="bibitem2"><b>[2]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 358&#8211;359.</a><br /> <a name="bibitem3"><b>[3]</b> D.A Bini,<cite> <em>Numerical computation of polynomial zeros by means of Aberth&#8217;s method</em>,</cite> Numerical Algorithms, <b>V.13</b>,(1996), 179&#8211;200.</a><br /> <a name="bibitem5"><b>[5]</b> </a><a href="http://en.wikipedia.org/wiki/Horner_scheme" target="_blank">http://en.wikipedia.org/wiki/Horner_scheme</a><br /> <a name="bibitem4"><b>[4]</b> </a><a href="http://en.wikipedia.org/wiki/Aberth_method" target="_blank">http://en.wikipedia.org/wiki/Aberth_method</a>
  </p>
</fieldset>
