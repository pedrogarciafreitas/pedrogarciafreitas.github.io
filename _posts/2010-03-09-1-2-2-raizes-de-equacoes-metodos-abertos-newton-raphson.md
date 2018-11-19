---
id: 439
title: '1.2.2 Raízes de Equações &#8212; Métodos Abertos &#8212; Newton Raphson'
date: 2010-03-09T16:29:54+00:00
author: SAWP
excerpt: |
  O método de Newton-Raphson é um método aberto, pois a convergência que ele provê à raiz não depende da delimitação de um intervalo, possuindo as propriedades descritas para Método do Ponto Fixo.
  
  Provavelmente é o método numérico mais aplicado computacionalmente para a aproximação de raízes, graças à sua capacidade de rápida convergência, associada à simplicidade de sua formulação.
layout: post
guid: http://www.sawp.com.br/blog/?p=439
permalink: /p=439
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3818:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> newtonRaphson<span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> diffG<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">,</span> imax<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    return the root of a function (using the Newton-Raphson Method)
    &nbsp;
    newtonRaphson(fun, diffFun, x0, errto, imax)
    &nbsp;
    * fun: Function where find the roots
    * diffFun: analytic derivative of fun
    * x0: next point (estimative)
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
    x1 <span style="color: #66cc66;">=</span> x0 - G<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>/diffG<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># fixed point x1 = G(x0)</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x1 - x0<span style="color: black;">&#41;</span>/x1<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> &amp;gt<span style="color: #66cc66;">;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount &amp;lt<span style="color: #66cc66;">;</span> imax:
    x0 <span style="color: #66cc66;">=</span> x1
    x1 <span style="color: #66cc66;">=</span> x0 - G<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>/diffG<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;"># in fixed point will be x1 = G(x0)</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> x1 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x1 - x0<span style="color: black;">&#41;</span>/x1<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> x1</pre></td></tr></table><p class="theCode" style="display:none;">def newtonRaphson(G, diffG, x0, errto, imax):
    &quot;&quot;&quot;
    return the root of a function (using the Newton-Raphson Method)
    
    newtonRaphson(fun, diffFun, x0, errto, imax)
    
    * fun: Function where find the roots
    * diffFun: analytic derivative of fun
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons
    
    Dec 2009
    &quot;&quot;&quot;
    
    x1 = x0 - G(x0)/diffG(x0) # fixed point x1 = G(x0)
    iterCount = 0
    errno = fabs((x1 - x0)/x1)
    
    while errno &amp;gt; errto and iterCount &amp;lt; imax:
    x0 = x1
    x1 = x0 - G(x0)/diffG(x0) # in fixed point will be x1 = G(x0)
    iterCount += 1
    
    if x1 != 0:
    errno = fabs((x1 - x0)/x1)
    
    return x1</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução<a name="sec1"></a>

O método de Newton-Raphson é outro método aberto, pois a convergência à raiz não depende da delimitação de um intervalo, possuindo as propriedades descritas do Método do Ponto Fixo.

Provavelmente é o método numérico mais aplicado computacionalmente para a aproximação de raízes, graças à sua capacidade de rápida convergência.

## 2. Desenvolvimento do Método<a name="sec2"></a>

<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig16.png"><img class="aligncenter size-full wp-image-446" title="Visualização gráfica da aproximação numérica de uma raiz" src="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig16.png" alt="" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig16.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig16-300x300.png 300w" sizes="(max-width: 400px) 100vw, 400px" /></a><br />
</center>

Na Figura [metodo](#figmetodo), observamos que a partir da aproximação inicial da raiz $$x\_{i} $$ é possível estender uma reta tangente do ponto $$\left( x\_{i}, f(x\_{i}) \right) $$ . O ponto onde esta tangente intercepta o eixo das abcissas é a segunda estimativa, $$x\_{i+1} $$ . Desta figura, é visível que a inclinação é equivalente à 

<center>
  <br /> <a name="eq1"></a><br /> $$ \dfrac{ d }{ d x } f(x_{i}) = \dfrac{ f(x_{i}) }{ \left( x_{i} &#8211; x_{i+1} \right) } $$<br />
</center>

isolando $$x_{i+1} $$ , aparece naturalmente a iteração conhecida como o Método de Newton:

<center>
  <br /> <a name="eq2"></a><br /> $$ x_{i+1} = x_{i} &#8211; \dfrac{f(x_{i})}{\dfrac{ d }{ d x } f(x_{i})} $$<br />
</center>

Como no Método do Ponto Fixo, basta executar sucessivas aproximações para convergir à raiz, tendo como critério de parada um erro pré-definido.

<!--  IMPLEMENTACAO -->

## 3. Implementação <a name="sec3"></a>

A implementação deste método consiste em basicamente alterar o código do Ponto Fixo de forma utilizar a chamada da expressão deduzida ao invés da própria função $$G $$:

<div>
  <pre lang="python">def newtonRaphson(G, diffG, x0, errto, imax):
    """
    return the root of a function (using the Newton-Raphson Method)

    newtonRaphson(fun, diffFun, x0, errto, imax)

    * fun: Function where find the roots
    * diffFun: analytic derivative of fun
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    License: Creative Commons

    Dec 2009
    """

  x1 = x0 - G(x0)/diffG(x0) # fixed point x1 = G(x0)
  iterCount = 0
    errno = fabs((x1 - x0)/x1)

  while errno &gt; errto and iterCount &lt; imax:
    x0 = x1
    x1 = x0 - G(x0)/diffG(x0) # in fixed point will be x1 = G(x0)
    iterCount += 1

    if x1 != 0:
      errno = fabs((x1 - x0)/x1)

  return x1</pre>
</div>

Veja que a implementação do método de Newton-Raphson é dependente de mais uma função, que precisa ser declarada. Embora este método não dependa da escolha da melhor função _G_, como ocorre no método do Ponto Fixo, o codificador precisa implementar tanto a função que se deseja conhecer a raiz como a sua derivada.

Um exemplo de utilização deste código pode ser encontrado em <a href="http://www.sawp.com.br/code/rootfind/newtonraphson.py" target="_blank">http://www.sawp.com.br/code/rootfind/newtonraphson.py</a>

## 4. Observações <a name="sec4"></a>

Embora o método do Newton-Raphson seja quase sempre o mais eficiente na busca de raízes, ele nem sempre é aplicável. Um exemplo interessante está em comparar as funções de avaliação do Método do Ponto Fixo e as do código de Newton-Raphson.

Ao utilizarmos Newton-Raphson para buscar a raiz da função:

<center>
  <br /> <em>G1 = exp(1.d0)**(-x/2.d0)</em><br />
</center>

e usando sua derivada:

<center>
  <br /> <em> diffG1 = (1/2)*(exp(1.d0))**(-(1.d0/2.d0)*x)</em><br />
</center>

o programa gera um resultado que não converge à raiz. Provavelmente se o código for compilado e executado, o resultado será _&#8220;NaN&#8221;_ ou _&#8220;infinity&#8221;_.

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
    <a name="bibitem1"></a>
  </p>
  
  <p>
    <a name="bibitem2"></a></fieldset>
