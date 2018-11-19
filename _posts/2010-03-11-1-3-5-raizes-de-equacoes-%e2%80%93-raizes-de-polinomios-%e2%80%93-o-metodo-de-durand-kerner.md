---
id: 524
title: 1.3.5 Raízes de Equações – Raízes de Polinômios – O Método de Durand-Kerner
date: 2010-03-11T14:44:29+00:00
author: SAWP
excerpt: '    O Método de Durand-Kerner, também chamado de Método de Weierstrass, é uma técnica numérica usada para obter todas as raízes de um polinômio, que atua de forma semelhante ao Método do Ponto Fixo, mas é generalizado para buscar todos os zeros da função polinomial.'
layout: post
guid: http://www.sawp.com.br/blog/?p=524
permalink: /p=524
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:13172:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"> <span style="color: #ff7700;font-weight:bold;">def</span> duran_kerner<span style="color: black;">&#40;</span>p<span style="color: #66cc66;">,</span> polDegree<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">500</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return all roots of Polynom (using the Duran-Kerner Method)
    &nbsp;
    duran_kerner(p, polDegree=1, x0=1.0, errto=0.001, imax=100)
    &nbsp;
    * p: polynom where find the roots
    * polDegree: polynom degree
    * x0: initial estimative (complex)
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    return: a list with all roots of polynom
    &nbsp;
    Author: Pedro Garcia &lt;sawp @sawp.com.br&gt;
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
    &nbsp;
    n <span style="color: #66cc66;">=</span> polDegree
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1.0</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #008000;">list</span>:
    zold <span style="color: #66cc66;">=</span> x0<span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span> + <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>n-<span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>*<span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #008000;">complex</span>:
    zold <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> x0+<span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    zold <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>*x0<span style="color: #66cc66;">,</span><span style="color: #dc143c;">random</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>*x0<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    &nbsp;
    znew <span style="color: #66cc66;">=</span> n * <span style="color: black;">&#91;</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> <span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>zold<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    prod <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> w <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: black;">&#40;</span><span style="color: #008000;">range</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> + <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>i+<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>zold<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    elem <span style="color: #66cc66;">=</span> zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - zold<span style="color: black;">&#91;</span>w<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> elem <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    elem +<span style="color: #66cc66;">=</span> errto
    prod *<span style="color: #66cc66;">=</span> elem
    &nbsp;
    pz <span style="color: #66cc66;">=</span> p<span style="color: black;">&#40;</span>zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> pz <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    pz +<span style="color: #66cc66;">=</span> errto
    &nbsp;
    znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - pz/prod
    &nbsp;
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>znew<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    t <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - zold<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>/<span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>znew<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&lt;</span> t:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> t
    &nbsp;
    zold <span style="color: #66cc66;">=</span> znew<span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    znew.<span style="color: black;">sort</span><span style="color: black;">&#40;</span>key<span style="color: #66cc66;">=</span><span style="color: #ff7700;font-weight:bold;">lambda</span> r: r.<span style="color: black;">real</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span>filt<span style="color: #66cc66;">,</span> znew<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;"> def duran_kerner(p, polDegree=1, x0=complex(1,1), errto=0.001, imax=500):
    &quot;&quot;&quot;
    Return all roots of Polynom (using the Duran-Kerner Method)
    
    duran_kerner(p, polDegree=1, x0=1.0, errto=0.001, imax=100)
    
    * p: polynom where find the roots
    * polDegree: polynom degree
    * x0: initial estimative (complex)
    * errto: tolerated error
    * imax: max of iterations allowed
    
    return: a list with all roots of polynom
    
    Author: Pedro Garcia &lt;sawp @sawp.com.br&gt;
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
    prod = 1
    
    for w in (range(i) + range(i+1, len(zold))):
    elem = zold[i] - zold[w]
    while elem == 0:
    elem += errto
    prod *= elem
    
    pz = p(zold[i])
    while pz == 0:
    pz += errto
    
    znew[i] = zold[i] - pz/prod
    
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

O Método de Durand-Kerner, também chamado de Método de Weierstrass, é uma técnica numérica usada para obter todas as raízes de um polinômio, que atua de forma semelhante ao Método do Ponto Fixo, mas é generalizado para buscar todos os zeros da função polinomial. </p> 

## 2. Desenvolvimento do Método <a name="sec2"></a> 

Seja $$p(x) $$ a função polinomial cujas raízes queremos encontrar. Sabemos que podemos escrever este polinômio como um produtório da função linear dependente de $$x $$ e das suas raízes $$z_{k} $$ :
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ p \left( x \right) = \left( x-z_{1} \right) \left( x-z_{2} \right) \ldots \left( x &#8211; z_{n} \right) =\prod _{i=1}^{n} (x-z_{i}) $$<br />
</center>

Para encontrarmos a i-ésima raiz deste polinômio, podemos simplesmente isolá-la, gerando a seguinte expressão:
      
<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ z_{i}=x-{\frac {p \left( x \right) }{\prod_{j=1}{j\neq i}^{n} ~(x-z_{j})} $$<br />
</center>


    
Note que podemos encontrar a i-ésima raiz, utilizando uma iteração que leva em conta a aproximação de todas as outras j-ésimas raízes. Sendo assim, podemos expressar o produtório acima como:
      
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ z_{i}=x-{\frac {p \left( x \right) }{\prod _{j=1}^{i-1} ~(x-z_{j})} \prod _{j=i+1}^{n} ~(x-z_{j})} $$<br />
</center>


    
Permitindo-nos obter as raízes através da seguinte função de iteração:
      
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ z_{i+1}=z_{i}-{\frac {p \left( z_{i} \right) }{\prod _{j=1}^{i-1}(z_{i}-z_{j}) ~ \prod _{j=i+1}^{n} ~(z_{i}-z_{j})}$$<br />
</center>

Note que esta função não possui uma derivação baseada na fórmula de iteração do Método de Newton-Raphson, possuindo uma forma muito semelhante ao do Método do Ponto Fixo. Essa característica indica que o método nem sempre converge, sendo problemático para raízes múltiplas, uma vez é exigido que $$z\_{i} \neq z\_{j} $$ . 

A convergência do Método de Durand-Kerner também não possui taxa constante. Como não utiliza o critério de Newton, nem sempre converge quadraticamente, sendo que pode possuir esta taxa sob algumas circunstâncias, enquanto converge linearmente para outras. Um estudo sobre a convergência deste método pode ser encontrado no artigo _&#8220;A convergence theorem for a method for simultaneous determination of all zeros of a polynomial&#8221;_[[1]](#bibitem1). 

<!--  IMPLEMENTACAO  --></p> 

## 3. Implementação <a name="sec3"></a> 

<div>
  <pre lang="python"> def duran_kerner(p, polDegree=1, x0=complex(1,1), errto=0.001, imax=500):
    """
    Return all roots of Polynom (using the Duran-Kerner Method)

    duran_kerner(p, polDegree=1, x0=1.0, errto=0.001, imax=100)

    * p: polynom where find the roots
    * polDegree: polynom degree
    * x0: initial estimative (complex)
    * errto: tolerated error
    * imax: max of iterations allowed

    return: a list with all roots of polynom

    Author: Pedro Garcia &lt;sawp @sawp.com.br>
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
            prod = 1

            for w in (range(i) + range(i+1, len(zold))):
                elem = zold[i] - zold[w]
                while elem == 0:
                    elem += errto
                prod *= elem

            pz = p(zold[i])
            while pz == 0:
                pz += errto

            znew[i] = zold[i] - pz/prod

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
  
  <p>
    </sawp></div>
  </p>
  
  <p>
    Veja um exemplo da utilização desta função em <a href="http://www.sawp.com.br/code/rootfind/durankerner.py" target="_blank">http://www.sawp.com.br/code/rootfind/durankerner.py</a>.
  </p>
  
  <p>
    <!--  COMENTÁRIOS  -->
  </p></p> 
  
  <p>
    <h2>
      4. Conclusões <a name="sec4"></a>
    </h2>
  </p>
  
  <p>
    O Método de Durand-Kerner é simples de se implementar e possui a vantagem de não exigir funções adicionais para calcular as derivadas da função cujas raízes queremos descobrir. Além disso, permite ainda que todas as raízes sejam encontradas, sendo elas reais ou complexas.
  </p>
  
  <p>
    Todavia, quando o polinômio possui raízes múltiplas, acaba por gerar um denominador zero na função de iteração. Para contornar este problema, a estratégia adotada na implementação acima foi acrescentar um fator na ordem do erro tolerado para a aproximação. Isso serve para que a divisão seja feita na ordem do erro, ao invés do zero, mas mantendo a aproximação sob um valor tolerável.
  </p>
  
  <p>
    Outro problema encontrado ao utilizar o Método de Durand-Kerner em um programa real é que o produtório presente no denominador da Equação <a href="#eq4">4</a> produza valores que estão fora do intervalo suportado pela arquitetura (<i>underflow</i> e <i>overflow</i> aritmético).
  </p></p> </p> 
  
  <p>
    <h2>
      5. Copyright
    </h2>
  </p>
  
  <p>
    Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.
  </p>
  
  <p>
  </p>
  
  <fieldset>
    <legend> 
    
    <h2>
      References
    </h2></legend> 
    
    <p>
      <a></a><br /> <a name="bibitem1"><b>[1]</b> P. Marica,<cite> <em>A convergence theorem for a method for simultaneous determination of all zeros of a polynomial</em>,</cite> l&#8217;institut mathematique Beograd, <b>V.28</b>(N.42),(1980), 158&#8211;168.</a><br /> <a name="bibitem2"><b>[2]</b> <cite><a href="http://home.roadrunner.com/~jbmatthews/misc/groots.htm" target="_blank">http://home.roadrunner.com/~jbmatthews/misc/groots.htm</a></cite></a><br /> </fieldset>
    </p>
