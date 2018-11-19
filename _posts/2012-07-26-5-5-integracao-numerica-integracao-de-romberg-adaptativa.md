---
id: 1673
title: '5.5 Integração Numérica &#8212; Integração de Romberg Adaptativa'
date: 2012-07-26T16:53:18+00:00
author: SAWP
excerpt: A regra de Simpson adaptativa é um algoritmo recursivo de integração numérica que usa uma estimativa do erro para calcular uma integral definida através de múltiplas aplicações do método de Simpson. Como em muitas abordagens numéricas, se o erro estimado ultrapassa um erro tolerado, o algoritmo divide o intervalo de integração em dois sub-intervalos e reaplica o método de Simpson nesses intervalos de forma independente, somando os resultados. Essa técnica acaba por ser mais eficiente que outros métodos de integração por convergir quadraticamente ao resultado.
layout: post
guid: http://www.sawp.com.br/blog/?p=1673
permalink: p=1673
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:3419:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> trapezoid<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10000</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using the Trapezoid Rule.
    &nbsp;
    integral = trapezoid(f, xi, xe, n=10000)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of interval divisions
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    sumatory <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span>f<span style="color: black;">&#40;</span>xi + i * h<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    trapezoids <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>xi<span style="color: black;">&#41;</span> + <span style="color: #ff4500;">2.0</span> * sumatory + f<span style="color: black;">&#40;</span>xi + n * h<span style="color: black;">&#41;</span>
    integral <span style="color: #66cc66;">=</span> trapezoids * <span style="color: black;">&#40;</span>h / <span style="color: #ff4500;">2.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def trapezoid(f, xi, xe, n=10000):
    &quot;&quot;&quot;
    Numerical integration using the Trapezoid Rule.
    
    integral = trapezoid(f, xi, xe, n=10000)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of interval divisions
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    h = float(xe - xi) / n
    sumatory = sum([f(xi + i * h) for i in xrange(1, n)])
    trapezoids = f(xi) + 2.0 * sumatory + f(xi + n * h)
    integral = trapezoids * (h / 2.0)
    return integral</p></div>
    ;i:2;s:7919:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> romberg<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> n<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using Romberg's Integration.
    &nbsp;
    integral = romberg(f, xi, xe, n=20)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of iterations
    &nbsp;
    return: <span style="color: #000099; font-weight: bold;">\i</span>nt_{xi}^{xe} f(x)
    &nbsp;
    Author: Pedro Garcia [sawp @sawp.com.br]
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
    <span style="color: #ff7700;font-weight:bold;">return</span> compute<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def romberg(f, xi, xe, n=10):
    &quot;&quot;&quot;
    Numerical integration using Romberg's Integration.
    
    integral = romberg(f, xi, xe, n=20)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * n: number of iterations
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp @sawp.com.br]
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
    ;i:3;s:6679:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> adaptative_romberg<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10e-10</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Numerical integration using the Adaptative Romberg's.
    &nbsp;
    integral = adaptative_rombergf, xi, xe, errto=10e-10)
    &nbsp;
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * errto: numerical error tolerated in the integration
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
    <span style="color: #ff7700;font-weight:bold;">def</span> apply_romberg<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>:
    middle_point <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>a + b<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span>
    left <span style="color: #66cc66;">=</span> romberg<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> middle_point<span style="color: black;">&#41;</span>
    right <span style="color: #66cc66;">=</span> romberg<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> middle_point<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>left<span style="color: #66cc66;">,</span> middle_point<span style="color: #66cc66;">,</span> right<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> recursion<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> <span style="color: #dc143c;">errno</span><span style="color: #66cc66;">,</span> integral<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>left<span style="color: #66cc66;">,</span> middle<span style="color: #66cc66;">,</span> right<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> apply_romberg<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> a<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    adap <span style="color: #66cc66;">=</span> left + right - integral
    err <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>adap<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">15.0</span>
    rec <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> z: recursion<span style="color: black;">&#40;</span>g<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> <span style="color: #dc143c;">errno</span> / <span style="color: #ff4500;">2.0</span><span style="color: #66cc66;">,</span> z<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> err <span style="color: #66cc66;">&lt;</span> <span style="color: #dc143c;">errno</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> left + right + adap / <span style="color: #ff4500;">15.0</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> rec<span style="color: black;">&#40;</span>a<span style="color: #66cc66;">,</span> middle<span style="color: #66cc66;">,</span> left<span style="color: black;">&#41;</span> + rec<span style="color: black;">&#40;</span>middle<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> right<span style="color: black;">&#41;</span>
    integral <span style="color: #66cc66;">=</span> recursion<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">,</span> romberg<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> xi<span style="color: #66cc66;">,</span> xe<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> integral</pre></td></tr></table><p class="theCode" style="display:none;">def adaptative_romberg(f, xi, xe, errto=10e-10):
    &quot;&quot;&quot;
    Numerical integration using the Adaptative Romberg's.
    
    integral = adaptative_rombergf, xi, xe, errto=10e-10)
    
    INPUT:
    * f: function to be integrated
    * xi: beginning of integration interval
    * xe: end of integration interval
    * errto: numerical error tolerated in the integration
    
    return: \int_{xi}^{xe} f(x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    def apply_romberg(g, a, b):
    middle_point = (a + b) / 2.0
    left = romberg(g, a, middle_point)
    right = romberg(g, middle_point, b)
    return (left, middle_point, right)
    
    def recursion(g, a, b, errno, integral):
    (left, middle, right) = apply_romberg(g, a, b)
    adap = left + right - integral
    err = abs(adap) / 15.0
    rec = lambda x, y, z: recursion(g, x, y, errno / 2.0, z)
    if err &lt; errno:
    return left + right + adap / 15.0
    else:
    return rec(a, middle, left) + rec(middle, b, right)
    integral = recursion(f, xi, xe, errto, romberg(f, xi, xe))
    return integral</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

No post sobre a integração de Romberg, vimos que este método utiliza uma estratégia para aumentar a acurácia da regra do trapézio através de sucessivas aplicações. Também apresentamos o Método de Simpson Adaptativo, que é um algoritmo recursivo de integração numérica que utiliza múltiplas aplicações do método de Simpson, dividindo o intervalo de integração em vários outros sub-intervalos. Ambas estratégias podem ser adaptadas para aprimorar a convergência do método do trapézio. Contudo, podemos substituir o método de Simpson pelo método de Romberg, o que permite um aumento na velocidade de convergência ainda mais significante no algoritmo adaptativo. 

&nbsp;

## 2. O Método 

Seja \(S(a,b) \) o resultado da aproximação da integral utilizando o método de Romberg no intervalo \([a,b] \) . Assim, o resultado da integral será
  


<center>
  \( I = S(a,b) = \int_a^b f(x) dx \)
</center>


  
Onde o critério de parada para a sub-divisão dos intervalos é o mesmo utilizando no Simpson adaptativo.

&nbsp;

## 3. Implementação 

As funções que implementam o método de Romberg adaptativo são:

<div>
  <pre lang="python">def trapezoid(f, xi, xe, n=10000):
    """
    Numerical integration using the Trapezoid Rule.

    integral = trapezoid(f, xi, xe, n=10000)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * n: number of interval divisions

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    h = float(xe - xi) / n
    sumatory = sum([f(xi + i * h) for i in xrange(1, n)])
    trapezoids = f(xi) + 2.0 * sumatory + f(xi + n * h)
    integral = trapezoids * (h / 2.0)
    return integral</pre>
</div>

<div>
  <pre lang="python">def romberg(f, xi, xe, n=10):
    """
    Numerical integration using Romberg's Integration.

    integral = romberg(f, xi, xe, n=20)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * n: number of iterations

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp @sawp.com.br]
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

<div>
  <pre lang="python">def adaptative_romberg(f, xi, xe, errto=10e-10):
    """
    Numerical integration using the Adaptative Romberg's.

    integral = adaptative_rombergf, xi, xe, errto=10e-10)

    INPUT:
      * f: function to be integrated
      * xi: beginning of integration interval
      * xe: end of integration interval
      * errto: numerical error tolerated in the integration

    return: \int_{xi}^{xe} f(x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    def apply_romberg(g, a, b):
        middle_point = (a + b) / 2.0
        left = romberg(g, a, middle_point)
        right = romberg(g, middle_point, b)
        return (left, middle_point, right)

    def recursion(g, a, b, errno, integral):
        (left, middle, right) = apply_romberg(g, a, b)
        adap = left + right - integral
        err = abs(adap) / 15.0
        rec = lambda x, y, z: recursion(g, x, y, errno / 2.0, z)
        if err &lt; errno:
            return left + right + adap / 15.0
        else:
            return rec(a, middle, left) + rec(middle, b, right)
    integral = recursion(f, xi, xe, errto, romberg(f, xi, xe))
    return integral</pre>
</div>

Um exemplo de utilização dessas funções pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integral_romberg_adaptative.py" target="_blank">http://www.sawp.com.br/code/integral/integral_romberg_adaptative.py</a>. 

&nbsp;

## 4. Copyright 

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
  </p></p>
</fieldset>
