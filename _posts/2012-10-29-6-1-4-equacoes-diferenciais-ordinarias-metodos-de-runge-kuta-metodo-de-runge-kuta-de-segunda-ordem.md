---
id: 1899
title: '6.1.4 Equações Diferenciais Ordinárias &#8212; Métodos de Runge-Kuta &#8212; Métodos de Runge-Kuta de Segunda Ordem'
date: 2012-10-29T16:32:02+00:00
author: SAWP
excerpt: 'Os métodos apresentados anteriormente -- Heun e Ponto Médio -- são ambos métodos de Runge-Kuta de segunda ordem. Nesse post, apresentamos de forma geral os métodos de Runge-Kuta de segunda ordem e começamos a expor o porquê de todos métodos serem classificados somo sub-ordens do Runge-Kuta.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1899
permalink: p=1899
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:4376:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> integral_runge_kuta_order_2<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> y0<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1e6</span><span style="color: #66cc66;">,</span> method<span style="color: #66cc66;">=</span>ralston<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration for solve ODE's using Second Order Runge-Kuta
    &nbsp;
    integral = integral_runge_kuta_order_2(f, xi, xe, n=1e6)
    &nbsp;
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * xi: beginning of integration interval
    * xe: end of integration interval
    * y0: initial estimative for y
    * n: number of points used
    * method: method used to solve a unique step (ralston, heun or midpoint)
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Sep 2012
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> method<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> y
    &nbsp;
    <span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>y0<span style="color: #66cc66;">,</span> xi<span style="color: black;">&#41;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    <span style="color: #ff7700;font-weight:bold;">return</span> integrator<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">,</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def integral_runge_kuta_order_2(f, xi, xe, y0, n=1e6, method=ralston):
    &quot;&quot;&quot;
    Numerical integration for solve ODE's using Second Order Runge-Kuta
    
    integral = integral_runge_kuta_order_2(f, xi, xe, n=1e6)
    
    INPUT:
    * f: derivative function f(x, y) = dy/dx
    * xi: beginning of integration interval
    * xe: end of integration interval
    * y0: initial estimative for y
    * n: number of points used
    * method: method used to solve a unique step (ralston, heun or midpoint)
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Sep 2012
    &quot;&quot;&quot;
    def integrator(x, y, h, n):
    for i in xrange(n):
    (x, y) = method(f, x, y, h)
    return y
    
    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</p></div>
    ;i:2;s:1555:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> ralston<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.75</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.75</span> * h * k1<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> y + <span style="color: black;">&#40;</span><span style="color: #ff4500;">0.333</span> * k1 + <span style="color: #ff4500;">0.6667</span> * k2<span style="color: black;">&#41;</span> * h
    x1 <span style="color: #66cc66;">=</span> x + h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def ralston(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.75 * h, y + 0.75 * h * k1)
    y1 = y + (0.333 * k1 + 0.6667 * k2) * h
    x1 = x + h
    return (x1, y1)</p></div>
    ;i:3;s:1353:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> midpoint<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">0.5</span> * h<span style="color: #66cc66;">,</span> y + <span style="color: #ff4500;">0.5</span> * k1 * h<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> y + k2 * h
    x1 <span style="color: #66cc66;">=</span> x + h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def midpoint(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.5 * h, y + 0.5 * k1 * h)
    y1 = y + k2 * h
    x1 = x + h
    return (x1, y1)</p></div>
    ;i:4;s:1437:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> heun<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> h<span style="color: black;">&#41;</span>:
    k1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    k2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x + h<span style="color: #66cc66;">,</span> y + k1 * h<span style="color: black;">&#41;</span>
    y1 <span style="color: #66cc66;">=</span> y + <span style="color: black;">&#40;</span><span style="color: #ff4500;">0.5</span> * k1 + <span style="color: #ff4500;">0.5</span> * k2<span style="color: black;">&#41;</span> * h
    x1 <span style="color: #66cc66;">=</span> x + h
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def heun(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + h, y + k1 * h)
    y1 = y + (0.5 * k1 + 0.5 * k2) * h
    x1 = x + h
    return (x1, y1)</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Os métodos de Runge-Kuta possuem a seguinte fórmula geral
  


<center>
  \( y_{i+1} = y_i + \phi (x_i, y_i, h) h \)
</center>


  
onde \(\phi(x\_i, y\_i, h) \) é a função incremento, que assim como no método de Euler, representa a inclinação no i-ésimo intervalo. O objetivo da utilização dessa função é aproximar numericamente uma série de Taylor sem calcular as derivadas de ordem superior. Essa função incremento possui forma geral
  


<center>
  \( \phi = a_1 k1 + a_2 k_2 + \cdots + a_n k_n \)
</center>


  
onde os \(a\_i \) são constantes a serem determinadas e os termos \(k\_i\) são combinações lineares da função diferencial a ser resolvida
  


<center>
  \( f(x,y) = \dfrac{dy}{dx} \)
</center>


  
Assim, os \(k \) &#8216;s são
  


<center>
  <br /> \(k_1 = f(x_1, y_i) \) <br /> \(k_2 = f(x_i + p_1 h, q_{11} k_1 h) \) <br /> \(k_3 = f(x_i + p_2 h, y_i + q_{21} k_1 h + q_{22} k_2 h) \) <br /> \(\vdots \)<br /> \(k_n = f(x_i + p_{n-1} h, y_i + q_{n-1,1} k_1 h + q_{n-1,2} k_2 h + \cdots + q_{n-1,n-1} k_{n-1} h )\)<br />
</center>


  
onde \(q\_{i,j} \) e \(p\_i \) são constantes a serem determinadas de forma que obedeçam as relações de recorrência dos \(k_i\). 

Podemos utilizar vários níveis de aproximações. Isto é, utilizar os \(k_i\)&#8217;s de \(1\) à \(n\). Além disso, existem infinitos valores para os \(p\)&#8217;s e \(q\)&#8217;s que podem ser utilizados nessas relações de recorrência. Sendo assim, vários métodos de Runge-Kuta podem ser deduzidos usando-se um número diferente de termos na função incremento. 

Cada novo \(n \) escolhido corresponde à ordem do método de Runge-Kuta. Ou seja, para \(n=2 \) temos o método de Runge-Kuta de segunda ordem, para \(n=3\) temos o de terceira ordem e assim por diante. Das relações de recorrência, podemos observar que se utilizarmos apenas \(n=1 \), temos o método de Euler, que equivale ao método de Runge-Kuta de primeira ordem. 

Uma vez que a ordem do método é escolhida, devemos nos preocupar em encontrar os vetores \(a\), \(p\) e \(q\). Cada elemento desses vetores pode ser obtido ao igualarmos termo a termo a equação
  


<center>
  \( y_{i+1} = y_i + \phi (x_i, y_i, h) h \)
</center>


  
com a expansão em série de Taylor. 

&nbsp;

## 2. Métodos de Runge-Kuta de Segunda Ordem 

Tomando \(n=2 \) , temos o método de RK de segunda ordem. Assim, com apenas \(2\) elementos de \(k \) escolhidos, temos que
  


<center>
  \( y_{i+1} = y_i + (a_i k_1 + a_2 k_2)h \)
</center>


  
onde
  


<center>
  \(k_1 = f(x_i, y_i) \)
</center>


  
e
  


<center>
  \(k_2 = f(x_i + p_1 h, y_i + q_{11} k_1 h)\)
</center>

O próximo passo é determinarmos os valores de \(a\_1\), \(a\_2\), \(p\_1\) e \(q\_{11}\). Para isso, decompomos \(y\_{i+1}\) em uma série de Taylor de segundo grau em termos de \(y\_i \) e \(f(x\_i, y\_i)\):

<center>
  \( y_{i+1} = y_i + f(x_i, y_i) h + \dfrac{f'(x_i, y_i)}{2!} h^2 \)
</center>


  
em que \(f'(x\_i, y\_i) \) deve ser determinado pela regra da cadeia

<center>
  \( f'(x_i, y_i) = \dfrac{\partial f(x,y)}{\partial x} + \dfrac{\partial f(x,y)}{\partial y} \dfrac{dy}{dx} \)
</center>


  
Utilizando as duas últimas equações acima, temos que

<center>
  \( y_{i+1} = y_i + f(x_i, y_i) h + \left(\dfrac{\partial f(x,y)}{\partial x} + \dfrac{\partial f(x,y)}{\partial y} \dfrac{dy}{dx} \right) \dfrac{h^2}{2!} \)
</center>

A série de Taylor para uma função de duas variáveis é definida por

<center>
  \( g(x+r, y+s) = g(x,y) + r \dfrac{\partial g}{\partial x} + s \dfrac{\partial g}{\partial y} + \cdots \)
</center>


  
Aplicando esse método para expandir \(k\_2 = f(x\_i + p\_1 h, y\_i + q\_{11} k\_1 h) \), isto é,

<center>
  \( k_2 = f(x_i + p_1 h, y_i + q_{11} k_1 h) = f(x_i, y_i) + p_1 h \dfrac{\partial f}{\partial x} + q_{11} k_1 h \dfrac{\partial f}{\partial y} + O(h^2) \)
</center>


  
Substituindo agora \(k\_1 \) e \(k\_2 \) na equação de segunda ordem, temos que

<center>
  \( y_{i+1} = y_i + \left( a_1 f(x_i, y_i) + a_2 f(x_i, y_i) \right) h + \left( a_2 p_1 \dfrac{\partial f}{\partial x} + a_2 q_{11} f(x_i, y_i) \dfrac{\partial f}{\partial y}\right) h^2 + O(h^3) \)
</center>


  
onde os termos abaixo devem valer o seguinte
  


<center>
  <br /> \(a_1 + a_2 = 1 \), \(a_2 p_1 = \dfrac{1}{2} \), e \(a_2 q_{11} = \dfrac{1}{2} \)<br />
</center>

Como temos três equações com quatro incógnitas, devemos escolher um valor para uma das incógnitas para determinar as outras três. Suponha que especifiquemos um valor para \(a\_2 \) , com isso podemos determinar \(a\_1\) , \(p\_1\) e \(q\_{11}\). Isto é,
  


<center>
  <br /> \(a_1 = 1 &#8211; a_2 \), \(p_1 = q_{11} = \dfrac{1}{2 a_2}\)<br />
</center>


   
Note que é possível escolher infinitos valores para \(a_2 \) , o que determina infinitas fórmulas para resolver o Runge-Kuta de segunda ordem. Segue abaixo as escolhas mais frequentemente usadas.

&nbsp;

### 2.1. Método de Heun 

Escolhendo-se \(a\_2 = \frac{1}{2}\), temos que \(a\_1 = \frac{1}{2}\) e \(p\_1 = q\_{11} = 1\). Esses parâmetros, quando substituídos na equação do método, nos fornece
  


<center>
  \( y_{i+1} = y_i + \left( \dfrac{1}{2} k_1 + \dfrac{1}{2} k_2 \right) h \)
</center>


  
onde
  


<center>
  \( k_1 = f(x_i, y_i) \)
</center>


  
e
  


<center>
  \( k_2 = f(x_i + h, y_i + k_1 h) \)
</center>

Observe que \(k\_1\) é a inclinação no início do intervalo e \(k\_2 \) é a inclinação no final do intervalo. Assim, o Runge-Kuta de segunda ordem com o parâmetro \(a_2\) escolhido como \(0.5\) equivale ao método de Heun sem iteração. 

&nbsp;

### 2.2. Método do Ponto Médio 

Quando escolhemos \(a\_2 = 1 \) , temos que \(a\_1 = 0 \) , \(p\_1 = q\_{11} = \frac{1}{2}\) o que nos dá
  


<center>
  \( y_{i+1} = y_i + k_2 h \)
</center>


  
onde
  


<center>
  \( k_1 = f(x_i, y_i) \)
</center>


  
e
  


<center>
  \( k_2 = f\left( x_i + \frac{1}{2} h, y_i + \frac{1}{2} k_1 h \right) \)
</center>


  
que equivale ao método do ponto médio.

&nbsp;

### 2.3. Método de Ralston 

Ralston e Rabinowitz[[1]](#bibitem1) demonstram que a escolha de \(a\_2 = \frac{2}{3} \) fornece um limitante inferior para o erro de truncamento para o método de segunda ordem. Com esse valor, temos que \(a\_1 = \frac{1}{3}\), \(p\_1 = q\_{11} = \frac{3}{4}\) e temos

<center>
  \( y_{i+1} = y_i + \left( \frac{1}{3} k_1 + \frac{2}{3} k_2 \right) h \)
</center>


  
onde
  


<center>
  \( k_1 = f(x_i, y_i) \)
</center>


  
e
  


<center>
  \( k_2 = f\left( x_i + \frac{3}{4} h, y_i + \frac{3}{4} k_1 \right) h \)
</center>

&nbsp;

## 3. Implementação 

&nbsp;

<div>
  <pre lang="python">def integral_runge_kuta_order_2(f, xi, xe, y0, n=1e6, method=ralston):
    """
    Numerical integration for solve ODE's using Second Order Runge-Kuta

    integral = integral_runge_kuta_order_2(f, xi, xe, n=1e6)

    INPUT:
      * f: derivative function f(x, y) = dy/dx
      * xi: beginning of integration interval
      * xe: end of integration interval
      * y0: initial estimative for y
      * n: number of points used
      * method: method used to solve a unique step (ralston, heun or midpoint)

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Sep 2012
    """
    def integrator(x, y, h, n):
        for i in xrange(n):
            (x, y) = method(f, x, y, h)
        return y

    (y, x) = (y0, xi)
    h = abs(xe - xi) / n
    return integrator(x, y, h, int(n))</pre>
</div>

Onde temos as variantes locais _ralston_, _heun_ e _midpoint_, conforme demonstrado na seção anterior. Essas funções são passadas no parâmetro _method_ da função acima implementada. Essas funções são implementadas abaixo. 

<div>
  <pre lang="python">def ralston(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.75 * h, y + 0.75 * h * k1)
    y1 = y + (0.333 * k1 + 0.6667 * k2) * h
    x1 = x + h
    return (x1, y1)</pre>
</div>

<div>
  <pre lang="python">def midpoint(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + 0.5 * h, y + 0.5 * k1 * h)
    y1 = y + k2 * h
    x1 = x + h
    return (x1, y1)</pre>
</div>

<div>
  <pre lang="python">def heun(f, x, y, h):
    k1 = f(x, y)
    k2 = f(x + h, y + k1 * h)
    y1 = y + (0.5 * k1 + 0.5 * k2) * h
    x1 = x + h
    return (x1, y1)</pre>
</div>

Observe que outras variantes podem ser passadas como parâmetro na função _integral\_runge\_kuta\_order\_2_. Assim, se desejarmos utilizar outras fórmulas decorrentes de outras escolhas de \(a_2\), podemos implementá-las de forma que sempre tenham a assinatura de entrada _(f, x, y, h)_ e retorno _(x1, y1)_. 

Um exemplo de utilização dessas funções pode ser obtido em <a href="http://www.sawp.com.br/code/ode/runge_kuta_order_2.py" target="_blank">http://www.sawp.com.br/code/ode/runge_kuta_order_2.py</a>. 

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <br /> <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
