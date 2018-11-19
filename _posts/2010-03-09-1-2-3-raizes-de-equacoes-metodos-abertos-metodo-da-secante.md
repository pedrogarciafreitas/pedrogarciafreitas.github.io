---
id: 450
title: '1.2.3 Raízes de Equações &#8212; Métodos Abertos &#8212; Método da Secante'
date: 2010-03-09T17:20:23+00:00
author: SAWP
excerpt: '    Este artigo demonstra matematicamente a função de iteração do Método da Secante e disponibiliza um algoritmo implementado na linguagem Python.'
layout: post
guid: http://www.sawp.com.br/blog/?p=450
permalink: /p=450
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4517:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> secante<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> xminus1<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.0</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    return the root of a function (using the Secant Method)
    &nbsp;
    secante(F, x0=1.0, xminus1=0.0, errto=0.001, imax=100)
    &nbsp;
    * F: Function where find the roots
    * x0: next point (estimative)
    * xminus: xi-1, used to define another bound
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    &nbsp;
    Dec 2009
    &quot;&quot;&quot;</span>
    &nbsp;
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    x1 <span style="color: #66cc66;">=</span> x0
    x0 <span style="color: #66cc66;">=</span> xminus1
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> &amp;gt<span style="color: #66cc66;">;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount &amp;lt<span style="color: #66cc66;">;</span> imax:
    xminus1 <span style="color: #66cc66;">=</span> x0
    x0 <span style="color: #66cc66;">=</span> x1
    &nbsp;
    <span style="color: #808080; font-style: italic;"># in Newton-Raphson will be x1 = x0 - G(x0)/diffG(x0)</span>
    <span style="color: #808080; font-style: italic;"># in fixed point will be x1 = G(x0)</span>
    x1 <span style="color: #66cc66;">=</span> x0 - <span style="color: black;">&#40;</span>F<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>*<span style="color: black;">&#40;</span>xminus1 - x0<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>F<span style="color: black;">&#40;</span>xminus1<span style="color: black;">&#41;</span> - F<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> x1 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x1 - x0<span style="color: black;">&#41;</span>/x1<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> x1</pre></td></tr></table><p class="theCode" style="display:none;">def secante(F, x0=1.0, xminus1=0.0, errto=0.001, imax=100):
    &quot;&quot;&quot;
    return the root of a function (using the Secant Method)
    
    secante(F, x0=1.0, xminus1=0.0, errto=0.001, imax=100)
    
    * F: Function where find the roots
    * x0: next point (estimative)
    * xminus: xi-1, used to define another bound
    * errto: tolerated error
    * imax: max of iterations allowed
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    
    Dec 2009
    &quot;&quot;&quot;
    
    iterCount = 0
    errno = errto + 1
    x1 = x0
    x0 = xminus1
    
    while errno &amp;gt; errto and iterCount &amp;lt; imax:
    xminus1 = x0
    x0 = x1
    
    # in Newton-Raphson will be x1 = x0 - G(x0)/diffG(x0)
    # in fixed point will be x1 = G(x0)
    x1 = x0 - (F(x0)*(xminus1 - x0))/(F(xminus1) - F(x0))
    
    iterCount += 1
    
    if x1 != 0:
    errno = fabs((x1 - x0)/x1)
    
    return x1</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a>

Como visto no Método de Newton-Raphson, as implementações dependem da derivada para encontrar as raízes. O problema nisso é que nem sempre é possível encontrar uma expressão para derivadas.

Outro inconveniente do Método de Newton-Raphson é que ele depende de duas funções: a própria função, cuja raiz se quer encontrar, e a função da derivada. Dependendo da natureza da função, a obtenção da sua derivada pode ser difícil de se obter, ou então ser uma tarefa computacionalmente custosa, o que implicaria em uma perda de eficiência.

Contudo, é possível aproximar a derivada &#8212; que fornece uma tangente &#8212; por uma secante.

<!--  DESENVOLVIMENTO -->

## 2. Desenvolvimento do Método <a name="sec2"></a>

<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig17.png"><img class="aligncenter size-full wp-image-452" title="Visualização gráfica da aproximação numérica de uma raiz qualquer usando os métodos da Secante e de Newton-Raphson" src="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig17.png" alt="" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig17.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig17-300x300.png 300w" sizes="(max-width: 400px) 100vw, 400px" /></a><br />
</center>

A Figura [metodo](#figmetodo) ilustra a descrição gráfica do Método da Secante (verde) e o de Newton-Raphson (em azul), sendo possível observar que ambas técnicas são muito semelhantes entre si, uma vez que as duas estimam a raiz extrapolando-se uma tangente da função no ponto $$\left( xi, f(xi) \right) $$ até o eixo abscisso. Logo, no caso de Newton-Raphson a inclinação da tangente é dada pela própria derivada, enquanto no da Secante usa-se uma diferença dividida para estimar a inclinação.

A aproximação da secante é dada pela seguinte relação:
  


<center>
  <br /> <a name="eq1"></a><br /> $$ \dfrac{d}{dx} f(x_{i}) = \dfrac{ f(x_{i-1}) &#8211; f(x_{i}) }{ x_{i-1} &#8211; x_{i} } $$<br />
</center>

A aproximação desta derivada é substituída na equação do Método de Newton-Raphson:
  


<center>
  <br /> <a name="eq2"></a><br /> $$ x_{i+1} = x_{i} &#8211; \dfrac{ f(x_{i}) }{ \dfrac{d}{d x} f(x_{i}) } $$<br />
</center>


  


<center>
  <br /> $$\Downarrow $$<br />
</center>

<center>
  <br /> <a name="eq3"></a><br /> $$ x_{i+1} = x_{i} &#8211; \dfrac{ f(x_{i}) ~ \left( x_{i-1} &#8211; x_{i} \right) }{f(x_{i-1}) &#8211; f(x_{i}) } $$<br />
</center>

A Equação [3](#eq3) acima é a fórmula do Método da Secante, sendo intimamente relacionado com o Método de Newton, pois o primeiro é uma modificação do segundo. Contudo, a abordagem da secante tem a vantagem de não necessitar da derivada da função, exigindo apenas uma estimativa inicial de x.

Ainda pelo gráfico, visualizamos que a aproximação da secante está mais distante que a de Newton para um mesmo $$x_{i} $$ . Isso ocorre porque o método de Newton-Raphson converge muito mais rapidamente. Sendo assim, concluimos que o Método da Secante deva ser preferido apenas quando não for possível obter a derivada da função.

## 3. Implementação <a name="sec3"></a>

Como na implementação de Newton-Raphson, o Método da Secante consiste em modificar o do Ponto Fixo, utilizando a equação deduzida neste artigo para calcular a raiz:

<div>
  <pre lang="python">def secante(F, x0=1.0, xminus1=0.0, errto=0.001, imax=100):
    """
    return the root of a function (using the Secant Method)

    secante(F, x0=1.0, xminus1=0.0, errto=0.001, imax=100)

    * F: Function where find the roots
    * x0: next point (estimative)
    * xminus: xi-1, used to define another bound
    * errto: tolerated error
    * imax: max of iterations allowed

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons

    Dec 2009
    """

    iterCount = 0
    errno = errto + 1
    x1 = x0
    x0 = xminus1

    while errno &gt; errto and iterCount &lt; imax:
        xminus1 = x0
        x0 = x1

        # in Newton-Raphson will be x1 = x0 - G(x0)/diffG(x0)
        # in fixed point will be x1 = G(x0)
        x1 = x0 - (F(x0)*(xminus1 - x0))/(F(xminus1) - F(x0))

        iterCount += 1

        if x1 != 0:
            errno = fabs((x1 - x0)/x1)

    return x1</pre>
</div>

Um exemplo de utilização desta função pode ser encontrado em <a href="http://www.sawp.com.br/code/rootfind/secante.py" target="_blank">http://www.sawp.com.br/code/rootfind/secante.py</a>

## 4. Copyright

Este documento está disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.
