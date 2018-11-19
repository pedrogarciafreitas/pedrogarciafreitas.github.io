---
id: 1638
title: '5.2 Integração Numérica &#8212; Regras de Simpson'
date: 2012-07-16T16:52:03+00:00
author: SAWP
excerpt: As regras de Simpson correspondem à segunda e terceira fórmulas de Newton-Cotes. Essas regras consistem em um método de aproximação de integrais definidas a partir de funções quadráticas e cúbicas.
layout: post
guid: http://www.sawp.com.br/blog/?p=1638
permalink: /p=1638
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:4644:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> simpson13<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10000</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using the Simpson 1/3 Rule.
    &nbsp;
    integral = simpson13(f, xi, xe, n=10000)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of interval divisions
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    s <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: i % <span style="color: #ff4500;">2</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>
    fxi <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: f<span style="color: black;">&#40;</span>xi + i * h<span style="color: black;">&#41;</span>
    g <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: s<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">2.0</span> * fxi<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + <span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">not</span> s<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">4.0</span> * fxi<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    sumatory <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: #008000;">map</span><span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    integral <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>fxi<span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> + sumatory + fxi<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>h / <span style="color: #ff4500;">3.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def simpson13(f, xi, xe, n=10000):
    &quot;&quot;&quot;
    Numerical integration using the Simpson 1/3 Rule.
    
    integral = simpson13(f, xi, xe, n=10000)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of interval divisions
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    h = float(xe - xi) / n
    s = lambda i: i % 2 == 0
    fxi = lambda i: f(xi + i * h)
    g = lambda i: s(i) * (2.0 * fxi(i)) + (not s(i)) * (4.0 * fxi(i))
    sumatory = sum(map(g, xrange(1, n)))
    integral = (fxi(0) + sumatory + fxi(n)) * (h / 3.0)
    return integral</p></div>
    ;i:2;s:4693:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> simpson38<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10001</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using the Simpson 3/8 Rule.
    &nbsp;
    integral = simpson38(f, xi, xe, n=10000)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of interval divisions
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    s <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: i % <span style="color: #ff4500;">3</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>
    fxi <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: f<span style="color: black;">&#40;</span>xi + i * h<span style="color: black;">&#41;</span>
    g <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> i: s<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">2.0</span> * fxi<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + <span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">not</span> s<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">3.0</span> * fxi<span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    sumatory <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: #008000;">map</span><span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    integral <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>fxi<span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> + sumatory + fxi<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">3.0</span> * h / <span style="color: #ff4500;">8.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def simpson38(f, xi, xe, n=10001):
    &quot;&quot;&quot;
    Numerical integration using the Simpson 3/8 Rule.
    
    integral = simpson38(f, xi, xe, n=10000)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of interval divisions
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    h = float(xe - xi) / n
    s = lambda i: i % 3 == 0
    fxi = lambda i: f(xi + i * h)
    g = lambda i: s(i) * (2.0 * fxi(i)) + (not s(i)) * (3.0 * fxi(i))
    sumatory = sum(map(g, xrange(1, n)))
    integral = (fxi(0) + sumatory + fxi(n)) * (3.0 * h / 8.0)
    return integral</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

A regra do trapézio, conforme apresentada no post anterior, possui três características que a tornam inapropriada em alguns casos. A primeira propriedade que devemos salientar se dá na sua utilização em relação ao tamanho da aplicação. Isto é, para aplicações individuais em funções bem comportadas, a utilização da regra do trapézio é computacionalmente boa com acurácia suficiente. Contudo, se for necessário uma acurácia muito alta, a regra do trapézio exige um grande esforço computacional, havendo o risco dos cálculos envolvidos estourar a precisão do processador. Ainda que o esforço computacional possa ser desprezível nos computadores atuais, ele pode impactar no desempenho da aplicação quando há um intenso cálculo de integrais ou a própria função a ser integrada é muito complexa. 

Os erros de arrendondamento podem limitar nossa habilidade de determinar integrais. Isso decorre tanto da palavra do computador quanto da grande quantidade de cálculos em ponto flutuante, que podem ir acumulando resíduos ao longo da computação. Assim, além de aplicarmos a regra do trapézio com segmentos menores, outra forma de obter uma estimativa mais acurada de uma integral é utilizar polinômios de grau mais alto para ligar os pontos. As fórmulas polinomiais para aproximação dessas integrais são chamadas de _regras de Simpson_. 

&nbsp;

## 2. Regra 1/3 de Simpson 

A regra 1/3 de Simpson é obtida quando um polinômio interpolador de segundo grau é utilizado. Isto é, $$f\_n(x) = f\_2(x)$$:
  


<center>
  $$ I = \int_{a}^{b} f(x) dx \approx \int_{a}^{b} f_2(x) dx $$
</center>

Se $$a $$ e $$b $$ forem designados por $$x\_0 $$ e $$x\_2 $$ e se $$f_2(x) $$ for representado por um polinômio de Lagrange, temos que a integral acima é
  


<center>
  $$ I = \int_{x_0}^{x_2} \left[ \dfrac{(x-x_1)(x-x_2)}{(x_0-x_1)(x_0-x_2)} f(x_0) + \dfrac{(x-x_0)(x-x_2)}{(x_1-x_0)(x_1-x_2)} f(x_1) + \dfrac{(x-x_0)(x-x_1)}{(x_2-x_0)(x_2-x_1)} f(x_2) \right] ~ dx $$
</center>


  
Essa integral simplificada resulta em
  


<center>
  $$ I = \dfrac{h}{3} \left[ f(x_0) + 4 f(x_1) + f(x_2) \right] $$
</center>


  
onde $$h=\dfrac{b-a}{2} = \dfrac{x\_2-x\_0}{2} $$ . Essa equação é conhecida como a regra 1/3 de Simpson, sendo a segunda fórmula de Newton-Cotes. 

&nbsp;

### 2.1. Regra 1/3 em múltiplos intervalos 

Assim como fizemos com a regra do trapézio, dividindo o intervalo de integração em diversos subintervalos, fazemos com a regra de Simpson para melhorarmos a estimativa da integral. Assim, ao dividirmos o intervalo $$[a.b] $$ em $$n $$ segmentos, temos
  


<center>
  $$ h = \dfrac{b-a}{n} $$
</center>


  
Tomando $$b=x\_n $$ e $$a=x\_0 $$ , a integral é representada como
  


<center>
  $$ I = \int_{x_0}^{x_2} f(x) dx + \int_{x_2}^{x_4} f(x) dx + \cdots + \int_{x_{n-2}^{x_n} f(x) dx $$
</center>


  
onde $$f(x) $$ é substituído em cada parte dessa integral por
  


<center>
  $$ f(x) = \dfrac{(x-x_{i+1})(x-x_{i+2})}{(x_i-x_{i+1})(x_{i}-x_{i+2})} f(x_i) + \dfrac{(x-x_i)(x-x_{i+2})}{(x_{i+1}-x_i)(x_{i+1}-x_{i+2})} f(x_{i+1}) + \dfrac{(x-x_i)(x-x_{i+1})}{(x_{i+2}-x_i)(x_{i+2}-x_{i+1})} f(x_{i+2}) $$
</center>


  
Assim, ao substituirmos a equação acima em cada integral individual, temos que
  


<center>
  $$ I \approx 2h \dfrac{f(x_0)+ 4 f(x_1)+f(x_2)}{6} + 2h \dfrac{f(x_2) + 4 f(x_3) + f(x_4)}{6} + \cdots 2h \dfrac{f(x_{n-2}) + 4 f(x_{n-1}) + f(x_n)}{6} $$
</center>


  
que pode ser expressa de uma forma mais simplificada:
  


<center>
  $$ I \approx \dfrac{(b-a)}{3n} \left[ f(x_0) + 4 \sum_{i=1,3,5}^{n-1} f(x_i) + 2 \sum_{j=2,4,6}^{n-2} f(x_j) + f(x_n) \right] $$
</center>

&nbsp;

## 3. Regra 3/8 de Simpson 

De forma análoga à regra 1/3 e à regra do trapézio, a regra 3/8 consiste em tomar um polinômio aproximador. Nesse caso, tomamos a terceira fórmula de Newton-Cotes, $$f\_n(x) = f\_3(x)$$:
  


<center>
  $$ I \int_{a}^{b} f(x) dx \approx \int_{a}^{b} f_3(x) dx $$
</center>


  
que fornece a seguinte fórmula da regra 3/8 de Simpson
  


<center>
  $$ I \approx \dfrac{3h}{8} \left[ f(x_0) + 3 f(x_1) + 3 f(x_2) + f(x_3) \right] $$
</center>

A figura abaixo demonstra a diferença da utilização dos métodos do trapézio (esquerda), regra de Simpson 1/3 (meio) e Simpson 3/8 (direita) para a função $$f(x) = x^x &#8211; x!$$ utilizando 2 partições. Como podemos ver, a escolha do método de interpolação tem grande implicação na acurácia da aproximação. 

<center>
  <br /> <a name="#fig1"></a><br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2012/07/graphics.png"><img class="aligncenter size-full wp-image-416" title="Aproximação da raiz por uma reta." src="http://www.sawp.com.br/blog/wp-content/uploads/2012/07/graphics.png" alt="numerical" width="800" height="266" /></a><br />
</center>

&nbsp;

## 4. Implementação 

Regra de Simpson 1/3:

<pre lang="python">def simpson13(f, xi, xe, n=10000):
    """
    Numerical integration using the Simpson 1/3 Rule.

    integral = simpson13(f, xi, xe, n=10000)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * n: number of interval divisions

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    h = float(xe - xi) / n
    s = lambda i: i % 2 == 0
    fxi = lambda i: f(xi + i * h)
    g = lambda i: s(i) * (2.0 * fxi(i)) + (not s(i)) * (4.0 * fxi(i))
    sumatory = sum(map(g, xrange(1, n)))
    integral = (fxi(0) + sumatory + fxi(n)) * (h / 3.0)
    return integral</pre></p> 

Regra de Simpson 3/8:

<div>
  <pre lang="python">def simpson38(f, xi, xe, n=10001):
    """
    Numerical integration using the Simpson 3/8 Rule.

    integral = simpson38(f, xi, xe, n=10000)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * n: number of interval divisions

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    h = float(xe - xi) / n
    s = lambda i: i % 3 == 0
    fxi = lambda i: f(xi + i * h)
    g = lambda i: s(i) * (2.0 * fxi(i)) + (not s(i)) * (3.0 * fxi(i))
    sumatory = sum(map(g, xrange(1, n)))
    integral = (fxi(0) + sumatory + fxi(n)) * (3.0 * h / 8.0)
    return integral</pre>
</div>

Um exemplo de utilização dessas funções pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integrals_simpson.py" target="_blank">http://www.sawp.com.br/code/integral/integrals_simpson.py</a>. 

&nbsp;

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
