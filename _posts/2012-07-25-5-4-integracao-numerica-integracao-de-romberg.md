---
id: 1665
title: '5.4 Integração Numérica &#8212; Integração de Romberg'
date: 2012-07-25T20:13:35+00:00
author: SAWP
excerpt: O método de Romberg é uma técnica de integração numérica que utiliza refinamentos da regra do trapézio estendida para aumentar a acurácia da aproximação.
layout: post
guid: http://www.sawp.com.br/blog/?p=1665
permalink: /p=1665
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:8043:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> romberg_slow<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> ni<span style="color: #66cc66;">=</span><span style="color: #ff4500;">20</span><span style="color: #66cc66;">,</span> mi<span style="color: #66cc66;">=</span><span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using Romberg's Integration.
    &nbsp;
    integral = romberg_slow(f, xi, xe, ni=20, mi=2)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * ni: initial partitions n
    * mi: initial order m
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
    <span style="color: #ff7700;font-weight:bold;">def</span> R00<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #ff4500;">0.5</span> * <span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>xi<span style="color: black;">&#41;</span> + f<span style="color: black;">&#40;</span>xe<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> Rn0<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    hn <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">2.0</span> ** n<span style="color: black;">&#41;</span>
    g <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> k: f<span style="color: black;">&#40;</span>xi + hn * <span style="color: black;">&#40;</span><span style="color: #ff4500;">2.0</span> * k - <span style="color: #ff4500;">1.0</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    summ <span style="color: #66cc66;">=</span> hn * <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span>g<span style="color: black;">&#40;</span>k<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">2</span> ** <span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #ff4500;">0.5</span> * R<span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span> + summ
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> Rnm<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    frac <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1.0</span> / <span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">4.0</span> ** m<span style="color: black;">&#41;</span> - <span style="color: #ff4500;">1.0</span><span style="color: black;">&#41;</span>
    rec1 <span style="color: #66cc66;">=</span> R<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> m - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    rec2 <span style="color: #66cc66;">=</span> R<span style="color: black;">&#40;</span>n - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> m - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    rec <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">4.0</span> ** m<span style="color: black;">&#41;</span> * rec1 - rec2
    <span style="color: #ff7700;font-weight:bold;">return</span> frac * rec
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> R<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> n <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span> <span style="color: #ff7700;font-weight:bold;">and</span> m <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> R00<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> n <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span> <span style="color: #ff7700;font-weight:bold;">and</span> m <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> Rn0<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> Rnm<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> R<span style="color: black;">&#40;</span>ni<span style="color: #66cc66;">,</span> mi<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def romberg_slow(f, xi, xe, ni=20, mi=2):
    &quot;&quot;&quot;
    Numerical integration using Romberg's Integration.
    
    integral = romberg_slow(f, xi, xe, ni=20, mi=2)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * ni: initial partitions n
    * mi: initial order m
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    def R00():
    return 0.5 * (xe - xi) * (f(xi) + f(xe))
    
    def Rn0(n):
    hn = (xe - xi) / (2.0 ** n)
    g = lambda k: f(xi + hn * (2.0 * k - 1.0))
    summ = hn * sum([g(k) for k in xrange(1, 2 ** (n - 1))])
    return 0.5 * R(n - 1, 0) + summ
    
    def Rnm(n, m):
    frac = 1.0 / ((4.0 ** m) - 1.0)
    rec1 = R(n, m - 1)
    rec2 = R(n - 1, m - 1)
    rec = (4.0 ** m) * rec1 - rec2
    return frac * rec
    
    def R(n, m):
    if n == 0 and m == 0:
    return R00()
    elif n &gt; 0 and m == 0:
    return Rn0(n)
    else:
    return Rnm(n, m)
    return R(ni, mi)</p></div>
    ;i:2;s:7937:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> romberg_fast<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">20</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using Romberg's Integration.
    &nbsp;
    integral = romberg_fast(f, xi, xe, n=20)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of iterations
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
    <span style="color: #ff7700;font-weight:bold;">def</span> calc_trapezoids<span style="color: black;">&#40;</span>s<span style="color: #66cc66;">,</span> k<span style="color: #66cc66;">,</span> i<span style="color: black;">&#41;</span>:
    m <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span> ** <span style="color: black;">&#40;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    si <span style="color: #66cc66;">=</span> trapezoid<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>s<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> si<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> improve_convergence<span style="color: black;">&#40;</span>s<span style="color: #66cc66;">,</span> var<span style="color: #66cc66;">,</span> i<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>:
    sk <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">4</span> ** <span style="color: black;">&#40;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span> * s<span style="color: black;">&#91;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> - var<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">4</span> ** <span style="color: black;">&#40;</span>i - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span> - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>sk<span style="color: #66cc66;">,</span> s<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> s<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> compute<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    var <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    s <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> k + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span>:
    <span style="color: black;">&#40;</span>var<span style="color: #66cc66;">,</span> s<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> calc_trapezoids<span style="color: black;">&#40;</span>s<span style="color: #66cc66;">,</span> k<span style="color: #66cc66;">,</span> i<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: black;">&#40;</span>s<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> var<span style="color: #66cc66;">,</span> s<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> improve_convergence<span style="color: black;">&#40;</span>s<span style="color: #66cc66;">,</span> var<span style="color: #66cc66;">,</span> i<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> s<span style="color: black;">&#91;</span>n - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> compute<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def romberg_fast(f, xi, xe, n=20):
    &quot;&quot;&quot;
    Numerical integration using Romberg's Integration.
    
    integral = romberg_fast(f, xi, xe, n=20)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of iterations
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    def calc_trapezoids(s, k, i):
    m = 2 ** (k - 1)
    si = trapezoid(f, xi, xe, m)
    return (s[i], si)
    
    def improve_convergence(s, var, i, k):
    sk = (4 ** (i - 1) * s[i - 1] - var) / (4 ** (i - 1) - 1)
    return (sk, s[i], s[k])
    
    def compute():
    var = 0.0
    s = [1.0 for i in xrange(0, n)]
    for k in xrange(1, n):
    for i in xrange(1, k + 1):
    if i == 1:
    (var, s[i]) = calc_trapezoids(s, k, i)
    else:
    (s[k], var, s[i]) = improve_convergence(s, var, i, k)
    return s[n - 1]
    
    return compute()</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

A integração de Romberg é um método proposto em 1955, e é utilizado para calcular integrais numéricas com alta velocidade de convergência. Esta técnica é semelhante à regra dos trapézios, uma vez que utiliza esse método sucessivas vezes para calcular o valor da integral. Contudo, difere-se da regra dos trapézios por aplicar a extrapolação de Richardson para acelerar a convergência da aproximação. O método de Romberg é uma forma geral de calcular as fórmulas de Newton-Cotes, uma vez que avalia os integrandos em pontos igualmente espaçados, onde os integrandos precisam ter derivadas contínuas. 

&nbsp;

## 2. Extrapolação de Richardson 

Assim como apresentado anteriormente no post sobre a extrapolação de Richardson, onde mostramos como acelerar a convergência de derivadas numéricas, da mesma forma podemos utilizar esse método para aumentar a acurácia das funções de integração numérica. Desta maneira, a estimativa da integral $$I $$ e o erro associado $$E $$ com a aplicação múltipla da regra do trapézio podem ser representados de um modo geral por
  


<center>
  $$ I = I(h) + E(h) $$
</center>


  
onde $$I $$ é o valor exato da integral, $$I(h) $$ é a aproximação a partir da aplicação da regra do trapézio (em função do passo $$h $$ ) e $$E(h) $$ é o erro de truncamento. Se fizermos duas estimativas independentes usando passos distintos $$h\_1 $$ e $$h\_2 $$ , temos que 

<center>
  $$ I(h_1) + E(h_1) = I(h_2) + E(h_2) $$
</center>


  
Como o erro da aplicação da regra do trapézio é
  


<center>
  $$ E \approx &#8211; \dfrac{b-a}{12} h^2 \bar{f}&#8221; $$
</center>


  
onde $$\bar{f}&#8221; $$ é a derivada média da função nos pontos avaliados. Supondo que $$\bar{f}&#8221; $$ é constante, independente do tamanho do passo, a equação acima pode ser usada para determinar a razão entre os erros:

<center>
  $$ \dfrac{E(h_1)}{E(h_2)} \approx \dfrac{h_1^2}{h_2^2} $$
</center>


  
ou melhor
  


<center>
  $$ E(h_1) \approx E(h_2) \left( \dfrac{h_1}{h_2} \right)^2 $$
</center>


  
que pode ser substituida na equação das integrais:
  


<center>
  $$ I(h_1) + E(h_2) \left( \dfrac{h_1}{h_2} \right)^2 \approx I(h_2) + E(h_2) $$
</center>


  
isolando $$E(h_2) $$ , temos
  


<center>
  $$ E(h_2) \approx \dfrac{I(h_1) &#8211; I(h_2)}{1 &#8211; (h_1 / h_2)^2} $$
</center>


  
Logo, obteremos uma estimativa do erro de truncamento em termos das estimativas da integral e seus tamanhos de passo. Essa estimativa pode então ser substituída em
  


<center>
  $$ I = I(h_2) + E(h_2) $$
</center>


  
para fornecer uma estimativa mais acurada
  


<center>
  $$ I \approx I(h_2) + \dfrac{1}{(h_1/h_2)^2 &#8211; 1} \left[ I(h_2) &#8211; I(h_1) \right] $$
</center>


  
Para o caso em que $$h\_2 = h\_1/2 $$ , temos que
  


<center>
  $$ I \approx \dfrac{4}{3} I(h_2) &#8211; \dfrac{1}{3} I(h_1) $$
</center>

&nbsp;

## 3. O Método de Romberg 

Observe que na última equação acima, os coeficientes somam 1. Isso equivale à fatores de peso de uma média ponderada. Assim, conforme a precisão aumenta, podemos colocar peso relativamente maior na estimativa superior da integral. Essas ponderações são expressas pela seguinte equação:
  


<center>
  $$ I_{j, k} = \dfrac{4^{k-1} I_{j+1, k-1} &#8211; I_{j, k-1}{4^{k-1}-1} $$
</center>


  
onde $$I\_{j+1,k-1} $$ e $$I\_{j, k-1} $$ são as integrais mais e menos acuradas, respectivamente, e $$I_{j, k} $$ é a integral melhorada. O índice $$k$$ representa a respectiva fórmula de Newton-Cotes, isto é, para $$k=1 $$ temos a regra do trapézio, para $$k=2 $$ temos a regra de Simpson, e assim por diante. O índice $$j $$ serve para indicar a estimativa mais acurada da menos acurada (quanto maior $$j $$ , mais acurada). Assim, o método pode ser definido indutivamente da seguinte forma

  * $$R(0,0) = \dfrac{1}{2} \left( b-a \right) \left( f(a) + f(b) \right)$$ 
  * $$R(n,0) = \dfrac{1}{2} R(n-1, 0) + h\_n \sum\_{k=1}^{2^{n-1} f(a + h_n (2k-1))$$ 
  * $$R(n,m) = \dfrac{1}{4^m &#8211; 1} \left( 4^m R(n,m-1) &#8211; R(n-1, m-1) \right)$$ 

onde $$a $$ e $$b $$ são os limites do intervalo de integração, $$n \geq 1 $$ , $m \geq 1 $$ e $$ h_n = \dfrac{b-1}{2^n}$. 

&nbsp;

## 4. Implementação 

A implementação utilizando as fórmulas indutivas é

<div>
  <pre lang="python">def romberg_slow(f, xi, xe, ni=20, mi=2):
    """
    Numerical integration using Romberg's Integration.

    integral = romberg_slow(f, xi, xe, ni=20, mi=2)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * ni: initial partitions n
      * mi: initial order m

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    def R00():
        return 0.5 * (xe - xi) * (f(xi) + f(xe))

    def Rn0(n):
        hn = (xe - xi) / (2.0 ** n)
        g = lambda k: f(xi + hn * (2.0 * k - 1.0))
        summ = hn * sum([g(k) for k in xrange(1, 2 ** (n - 1))])
        return 0.5 * R(n - 1, 0) + summ

    def Rnm(n, m):
        frac = 1.0 / ((4.0 ** m) - 1.0)
        rec1 = R(n, m - 1)
        rec2 = R(n - 1, m - 1)
        rec = (4.0 ** m) * rec1 - rec2
        return frac * rec

    def R(n, m):
        if n == 0 and m == 0:
            return R00()
        elif n > 0 and m == 0:
            return Rn0(n)
        else:
            return Rnm(n, m)
    return R(ni, mi)</pre>
</div>

Contudo, essa implementação ingênua pode ser muito custosa para muitos $$n $$ ou ordens de integração ( $$m $$ ) muito grandes. Assim, uma versão mais eficiente do método de Romberg é listada abaixo: 

<div>
  <pre lang="python">def romberg_fast(f, xi, xe, n=20):
    """
    Numerical integration using Romberg's Integration.

    integral = romberg_fast(f, xi, xe, n=20)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * n: number of iterations

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    def calc_trapezoids(s, k, i):
        m = 2 ** (k - 1)
        si = trapezoid(f, xi, xe, m)
        return (s[i], si)

    def improve_convergence(s, var, i, k):
        sk = (4 ** (i - 1) * s[i - 1] - var) / (4 ** (i - 1) - 1)
        return (sk, s[i], s[k])

    def compute():
        var = 0.0
        s = [1.0 for i in xrange(0, n)]
        for k in xrange(1, n):
            for i in xrange(1, k + 1):
                if i == 1:
                    (var, s[i]) = calc_trapezoids(s, k, i)
                else:
                    (s[k], var, s[i]) = improve_convergence(s, var, i, k)
        return s[n - 1]

    return compute()</pre>
</div>

Um exemplo de utilização dessas funções pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integral_romberg.py" target="_blank">http://www.sawp.com.br/code/integral/integral_romberg.py</a>. 

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
