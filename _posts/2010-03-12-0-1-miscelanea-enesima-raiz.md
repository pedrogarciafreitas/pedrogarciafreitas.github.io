---
id: 570
title: '0.1 Miscelânea &#8212; Enésima Raiz'
date: 2010-03-12T15:02:06+00:00
author: SAWP
excerpt: 'Este artigo demonstra uma aplicação direta do Método de Newton, que é a expressão para obtenção da enésima raiz de  "fi" através de uma implementação computacional.'
layout: post
guid: http://www.sawp.com.br/blog/?p=570
permalink: /p=570
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3781:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> nth_root<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">,</span> errto <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1E-5</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the nth-root of a number.
    &nbsp;
    nth_root(x, n, errto = 1E-5)
    &nbsp;
    * x: Float value
    * n: nth-root
    * errto: tolerated aproximation error (default: 1E-5)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Marc 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    zold <span style="color: #66cc66;">=</span> x/<span style="color: #ff4500;">2.0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto:
    znew <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span>/n<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>*zold + x/zold**<span style="color: black;">&#40;</span>n-<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> zold <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>znew - zold<span style="color: black;">&#41;</span>/<span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>znew<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">break</span>
    zold <span style="color: #66cc66;">=</span> znew
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> znew</pre></td></tr></table><p class="theCode" style="display:none;">def nth_root(x, n, errto = 1E-5):
    &quot;&quot;&quot;
    Return the nth-root of a number.
    
    nth_root(x, n, errto = 1E-5)
    
    * x: Float value
    * n: nth-root
    * errto: tolerated aproximation error (default: 1E-5)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Marc 2010
    &quot;&quot;&quot;
    
    n = int(n)
    x = float(x)
    zold = x/2.0
    errno = errto + 1
    
    while errno &gt; errto:
    znew = (1.0/n) * ((n-1)*zold + x/zold**(n-1))
    if zold != 0:
    errno = abs(znew - zold)/abs(znew)
    else:
    break
    zold = znew
    
    return znew</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Desenvolvimento do Método </p> 

Para obtermos uma função que retorne a raiz arbitrária de um número qualquer $$\phi $$ , podemos supor que $$phi $$ é uma constante que se relacione com o parâmetro de entrada $$x $$ da seguinte forma:
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> $$ x^n = \phi $$<br />
</center>


    
onde $$n $$ é um inteiro qualquer e $$\phi $$ é um valor real positivo, isto é:
      


<center>
  <br /> $$\phi > 0 $$<br />
</center>

Através desta expressão, vamos supor uma função $$f(x) $$ tal que
    
<a name="eq2">(eq2)</a>
      


<center>
  <br /> $$ f(x) = x^n &#8211; \phi $$<br />
</center>

A função $$f(x) $$ possui algumas propriedades interessantes. A primeira delas é que sabemos que $$f(x) = 0 $$ sempre, pois a Equação [1](#eq1) é verdadeira. Além disso, $$f(x) $$ pode ser facilmente derivada:
    
<a name="eq3">(eq3)</a>
      


<center>
  <br /> $$ \dfrac{d}{dx}f(x) = nx^{n-1} $$<br />
</center>


    
Desta forma, o problema de retirar a raiz $$n $$ de $$\phi $$ se reduz a um problema de busca do zero da função $$f(x) $$ . Como temos $$f(x) $$ e sua derivada, podemos utilizar o Método de Newton para encontrarmos esta raiz:
    
<a name="eq4">(eq4)</a>
      


<center>
  <br /> $$ x_{k+1} = x_k &#8211; \dfrac{f(x)}{\frac{d}{dx}f(x)} $$<br />
</center>


    
Assim,
    


<center>
  <br /> $$x_{k+1} = x_k &#8211; \dfrac{x_k^n &#8211; \phi}{nx_k^{n-1} $$ \\<br /> $$x_{k+1} = x_k &#8211; \dfrac{x_k}{n} + \dfrac{\phi}{x_k^{n-1} $$<br />
</center>

Simplificando a última equação, obtemos o algoritmo da enésima raiz:
    
<a name="eq5">(eq5)</a>
      


<center>
  <br /> $$ x_{k+1} = \dfrac{1}{n} \left[ (n-1)x_k + \dfrac{\phi}{x_k^{n-1} \right] $$<br />
</center>

## 2. Implementação 

<div>
  <pre lang="python">def nth_root(x, n, errto = 1E-5):
    """
     Return the nth-root of a number.

     nth_root(x, n, errto = 1E-5)

     * x: Float value
     * n: nth-root
     * errto: tolerated aproximation error (default: 1E-5)

     Author: Pedro Garcia [sawp@sawp.com.br]
     see: http://www.sawp.com.br

     License: Creative Commons
         http://creativecommons.org/licenses/by-nc-nd/2.5/br/

     Marc 2010
    """

    n = int(n)
    x = float(x)
    zold = x/2.0
    errno = errto + 1

    while errno > errto:
        znew = (1.0/n) * ((n-1)*zold + x/zold**(n-1))
        if zold != 0:
            errno = abs(znew - zold)/abs(znew)
        else:
            break
        zold = znew

    return znew</pre>
</div>

Disponível para download em <a href="http://www.sawp.com.br/code/misc/nth_root.py" target="_blank">http://www.sawp.com.br/code/misc/nth_root.py</a> </p> </p> 

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> </a><a href="http://en.wikipedia.org/wiki/Nth_root_algorithm" target="_blank">http://en.wikipedia.org/wiki/Nth_root_algorithm</a>
  </p>
</fieldset>
