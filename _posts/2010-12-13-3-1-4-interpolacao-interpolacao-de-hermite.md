---
id: 880
title: '3.1.4 Aproximação de Funções &#8212; Interpolação &#8212; Interpolação de Hermite'
date: 2010-12-13T15:09:30+00:00
author: SAWP
excerpt: A interpolação de Hermite é um método que utiliza tanto amostras da função quanto da sua derivada para ajustá-la em uma curva. Neste artigo, demonstramos a formulação desse método e um exemplo de como implementá-lo
layout: post
guid: http://www.sawp.com.br/blog/?p=880
permalink: p=880
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:9395:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> interpolation_hermite<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> x_j<span style="color: #66cc66;">,</span> f_j<span style="color: #66cc66;">,</span> diffF_j<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return x evaluated in Hermite interpolation function.
    &nbsp;
    interpolation_hermite(x, x_j, f_j, diffF_j, n=0)
    &nbsp;
    INPUT:
    * x: evalue at this point
    * x_j: LIST, tabular points
    * f_j: LIST, tabular points (must be same size of x_j)
    * diffF_j: LIST, derivative points of x_j (f'(x_j))
    * n: polynomial degree (optional)
    &nbsp;
    return:
    * y(x): interpolated and evaluated x value
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Dec 2010
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>f_j<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Error: wrong type parameters&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;NaN&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>f_j<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">or</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>diffF_j<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Error: the tabular points must have same size&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;NaN&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> n <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x_j<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    n <span style="color: #66cc66;">=</span> n + <span style="color: #ff4500;">1</span>
    &nbsp;
    p <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #808080; font-style: italic;"># lagrange polinomial</span>
    xj <span style="color: #66cc66;">=</span> x_j<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    ljn_num <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    ljn_den <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    xi <span style="color: #66cc66;">=</span> x_j<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">!=</span> j:
    ljn_num *<span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>x - xi<span style="color: black;">&#41;</span>
    ljn_den *<span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xj - xi<span style="color: black;">&#41;</span>
    ljn <span style="color: #66cc66;">=</span> ljn_num / ljn_den
    &nbsp;
    <span style="color: #808080; font-style: italic;"># hermite interpolation</span>
    diff_ljn <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    xi <span style="color: #66cc66;">=</span> x_j<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">!=</span> j:
    diff_ljn +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span> / <span style="color: black;">&#40;</span>xj - xi<span style="color: black;">&#41;</span>
    &nbsp;
    hjn <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span> - <span style="color: #ff4500;">2</span> * <span style="color: black;">&#40;</span>x - xj<span style="color: black;">&#41;</span> * diff_ljn<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>ljn * ljn<span style="color: black;">&#41;</span>
    hjn_ <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>x - xj<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>ljn * ljn<span style="color: black;">&#41;</span>
    p +<span style="color: #66cc66;">=</span> hjn * f_j<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> + hjn_ * diffF_j<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> p</pre></td></tr></table><p class="theCode" style="display:none;">def interpolation_hermite(x, x_j, f_j, diffF_j, n=0):
    &quot;&quot;&quot;
    Return x evaluated in Hermite interpolation function.
    
    interpolation_hermite(x, x_j, f_j, diffF_j, n=0)
    
    INPUT:
    * x: evalue at this point
    * x_j: LIST, tabular points
    * f_j: LIST, tabular points (must be same size of x_j)
    * diffF_j: LIST, derivative points of x_j (f'(x_j))
    * n: polynomial degree (optional)
    
    return:
    * y(x): interpolated and evaluated x value
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Dec 2010
    &quot;&quot;&quot;
    
    if type(x_j) != type(f_j) or type(x_j) != type([]):
    print &quot;Error: wrong type parameters&quot;
    return float(&quot;NaN&quot;)
    
    if len(x_j) != len(f_j) or len(x_j) != len(diffF_j):
    print &quot;Error: the tabular points must have same size&quot;
    return float(&quot;NaN&quot;)
    
    if n &lt; = 0:
    n = len(x_j)
    else:
    n = n + 1
    
    p = 0.0
    for j in xrange(n):
    # lagrange polinomial
    xj = x_j[j]
    ljn_num = 1.0
    ljn_den = 1.0
    for i in xrange(n):
    xi = x_j[i]
    if i != j:
    ljn_num *= (x - xi)
    ljn_den *= (xj - xi)
    ljn = ljn_num / ljn_den
    
    # hermite interpolation
    diff_ljn = 0
    for i in xrange(n):
    xi = x_j[i]
    if i != j:
    diff_ljn += 1.0 / (xj - xi)
    
    hjn = (1.0 - 2 * (x - xj) * diff_ljn) * (ljn * ljn)
    hjn_ = (x - xj) * (ljn * ljn)
    p += hjn * f_j[j] + hjn_ * diffF_j[j]
    return p</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Interpolação de Hermite 

Seja a fórmula geral da interpolação

<center>
  \( f(x) = \sum_{j=1}^{n} \sum_{i=0}^{m_j} A_{ij}(x) \frac{d^{(i)} f(a_j)}{d x^{(i)}} + E(x) \)
</center>

consideramos \(m_j = 1 \) para \(j = 1, \ldots, r \) , isto é, supomos que a primeira derivada também é uma função conhecida em \(r \) dos \(n \) pontos tabulares. Ou seja, a fórmula acima, quando desenvolvida até a primeira derivada, terá a forma

<center>
  \( f(x) = \sum_{j=1}^{n} h_j(x) f(a_j) + \sum_{j=1}^{r} h_j'(x) f'(a_j) + E(x) \)
</center>

portanto, desprezando o erro da aproximação, temos \(y(x) \) interpolada por

<center>
  \( y(x) = \sum_{j=1}^{n} h_{j_\alpha}(x) f(a_j) + \sum_{j=1}^{r} h_{j_\beta}(x) f'(a_j) \)
</center>

onde \(h\_{j\_\alpha}(x) \) e \(h\_{j\_\beta}(x) \) são polinômios. Novamente, usando o critério da aproximação exata, queremos minimizar o erro \(E(x) \) tal que \(E(a\_j) = 0 \). Utilizando a interpolação de Lagrange, podemos utilizar as seguintes condições para satisfazerem \(h\_{j\_\alpha}(x) \) e \(h\_{j_\beta}(x) \) :
    


<center>
  \(p_n(x) = (x &#8211; a_1) \cdots (x &#8211; a_n) \)
</center>


    


<center>
  \(p_r(x) = (x &#8211; a_1) \cdots (x &#8211; a_r) \)
</center>


    


<center>
  \(l_{jn}(x) = \frac{p_n(x)}{ (x-a_j) p_n'(a_j)} \)
</center>


    


<center>
  \( l_{jr}(x) = \frac{p_r(x)}{(x-a_j) p_r'(a_j)} \)
</center>


    
nestas condições, temos que \(h_j(x) \) é
    


<center>
  \(<br /> h_{j_\alpha}(x) = \left\{<br /> \begin{array}{lcl}<br /> t_j(x) l_{jn}(x) l_{jr}(x) & ~ & j = 1,\ldots ,r \\<br /> l_{jn}(x) \frac{p_r(x)}{p_r(a_j)} & ~ & j = r + 1, \ldots, n<br /> \end{array}<br /> \right.<br /> \)
</center>


    
onde \(t\_j(x) \) é um polinômio de primeiro grau tal que \(h\_{j\_\alpha}(x) \) é de grau \(n+r-1 \) . Para satisfazer as condições de convergência, precisamos ter \(t\_j(a\_j) = 1 \) e \(t\_j'(a\_j) + l\_{jn}'(a\_j) + l\_{jr}'(a_j) = 0 \) . 

De maneira semelhante, fazemos para \(h\_{j\_\beta}(x) \) :
    


<center>
  \(h_{j_\beta}(x) = s_j(x) l_{jr}(x) l_{jn}(x) \)
</center>


    
onde \(s\_j(x) \) é um polinômio de primeiro grau com \(s\_j(a\_j) = 0 \) e \(s\_j'(a_j) = 1 \) . 

Tomando \(t\_j(x) = 1 &#8211; (x &#8211; a\_j)[l\_{jn}'(a\_j) + l\_{jr}'(a\_j)] \) e \(s\_j(x) = x &#8211; a\_j \) , temos que
    


<center>
  \( h_{j_\alpha}(x) = \left\{<br /> \begin{array}{lcl}<br /> \left[ 1 &#8211; (x &#8211; a_j)[l_{jn}'(a_j) + l_{jr}'(a_j)] \right] l_{jn}(x)l_{jr}(x) & ~ & j = 1,\ldots ,r \\<br /> l_{jn}(x) \frac{p_r(x)}{p_r(a_j)} & ~ & j = r + 1, \ldots, n<br /> \end{array} \right| \)
</center>


     
e
     


<center>
  \( h_{j_\beta}(x) = (x &#8211; a_j) l_{jr}(x) l_{jn}(x) \)
</center>

Ou seja, a _Fórmula Interpoladora de Hermite_ é 

<center>
  \( f(x) = \sum_{j=1}^{n} h_{j_\alpha}(x) f(a_j) +<br /> \sum_{j=1}^{n} h_{j_\beta}(x) f'(a_j)<br /> \)
</center>


      
com \(h\_{j\_\alpha}(x) = \left[1 &#8211; 2 (x &#8211; a\_j) l\_j'(a\_j)\right] l\_j^2(x) \) e \(h\_{j\_\beta}(x) = (x &#8211; a\_j) l\_j^2(x) \) . 

&nbsp; 

## 2. Implementação 

<div>
  <pre lang="python">def interpolation_hermite(x, x_j, f_j, diffF_j, n=0):
    """
    Return x evaluated in Hermite interpolation function.

    interpolation_hermite(x, x_j, f_j, diffF_j, n=0)

    INPUT:
      * x: evalue at this point
      * x_j: LIST, tabular points
      * f_j: LIST, tabular points (must be same size of x_j)
      * diffF_j: LIST, derivative points of x_j (f'(x_j))
      * n: polynomial degree (optional)

    return:
      * y(x): interpolated and evaluated x value

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Dec 2010
    """

    if type(x_j) != type(f_j) or type(x_j) != type([]):
        print "Error: wrong type parameters"
        return float("NaN")

    if len(x_j) != len(f_j) or len(x_j) != len(diffF_j):
        print "Error: the tabular points must have same size"
        return float("NaN")

    if n &lt; = 0:
        n = len(x_j)
    else:
        n = n + 1

    p = 0.0
    for j in xrange(n):
        # lagrange polinomial
        xj = x_j[j]
        ljn_num = 1.0
        ljn_den = 1.0
        for i in xrange(n):
            xi = x_j[i]
            if i != j:
                ljn_num *= (x - xi)
                ljn_den *= (xj - xi)
        ljn = ljn_num / ljn_den

        # hermite interpolation
        diff_ljn = 0
        for i in xrange(n):
            xi = x_j[i]
            if i != j:
                diff_ljn += 1.0 / (xj - xi)

        hjn = (1.0 - 2 * (x - xj) * diff_ljn) * (ljn * ljn)
        hjn_ = (x - xj) * (ljn * ljn)
        p += hjn * f_j[j] + hjn_ * diffF_j[j]
    return p
  </pre>
</div>

Esta função está disponível em <a href="http://www.sawp.com.br/code/interpolation/interpolation_hermite.py" target="_blank">http://www.sawp.com.br/code/interpolation/interpolation_hermite.py</a> assim como um exemplo de como utilizá-la. 

&nbsp;

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</p> 
    
    <p>
      </a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 69.</p> 
      
      <p>
        </a>
      </p></fieldset>
