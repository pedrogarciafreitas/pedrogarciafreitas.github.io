---
id: 1343
title: '3.3.2 Aproximação de Funções &#8212; Regressões &#8212; Regressão Linear Múltipla'
date: 2011-10-05T09:36:23+00:00
author: SAWP
excerpt: Estendendo o post sobre regressão linear simples, temos o caso em que o vetor y é gerado por uma função com duas ou mais variáveis.
layout: post
guid: http://www.sawp.com.br/blog/?p=1343
permalink: p=1343
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:10908:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> multilinear_regression<span style="color: black;">&#40;</span>points<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a FUNCTION with parameters adjusted by polinomial regression
    &nbsp;
    f = multilinear_regression(points)
    &nbsp;
    INPUT:
    * points: list of tuples of sampled points (x1_i, x2_i, ..., y_i)
    &nbsp;
    return: a linear function f(x) = a_0 + a_1 * x + ... + a_m * x
    &nbsp;
    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Sep 2011
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> prepare_linear_system<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> order<span style="color: black;">&#41;</span>:
    A <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    B <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>row<span style="color: #66cc66;">,</span> order<span style="color: black;">&#41;</span>:
    xc <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>xi * xj <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: black;">&#40;</span>xi<span style="color: #66cc66;">,</span> xj<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">zip</span><span style="color: black;">&#40;</span>x<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> x<span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    s <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span>xc<span style="color: black;">&#41;</span>
    A<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> s
    A<span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> s
    s <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>yl * xl <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: black;">&#40;</span>yl<span style="color: #66cc66;">,</span> xl<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">zip</span><span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>:<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    B<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span>s<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> B<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> extract_points<span style="color: black;">&#40;</span>points<span style="color: black;">&#41;</span>:
    M <span style="color: #66cc66;">=</span> <span style="color: #008000;">zip</span><span style="color: black;">&#40;</span>*points<span style="color: black;">&#41;</span>
    y <span style="color: #66cc66;">=</span> M<span style="color: black;">&#91;</span>-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #008000;">len</span><span style="color: black;">&#40;</span>y<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> line <span style="color: #ff7700;font-weight:bold;">in</span> M<span style="color: black;">&#91;</span>:-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>:
    x +<span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>line<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>
    &nbsp;
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>points<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> extract_points<span style="color: black;">&#40;</span>points<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> prepare_linear_system<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>
    alphas <span style="color: #66cc66;">=</span> cholesky<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    fun <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> t: <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span>ti * a <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: black;">&#40;</span>ti<span style="color: #66cc66;">,</span> a<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">zip</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #008000;">list</span><span style="color: black;">&#40;</span>t<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> alphas<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> fun</pre></td></tr></table><p class="theCode" style="display:none;">def multilinear_regression(points):
    &quot;&quot;&quot;
    Return a FUNCTION with parameters adjusted by polinomial regression
    
    f = multilinear_regression(points)
    
    INPUT:
    * points: list of tuples of sampled points (x1_i, x2_i, ..., y_i)
    
    return: a linear function f(x) = a_0 + a_1 * x + ... + a_m * x
    
    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Sep 2011
    &quot;&quot;&quot;
    def prepare_linear_system(x, y, order):
    A = [[0.0 for i in xrange(order)] for j in xrange(order)]
    B = [0.0 for i in xrange(order)]
    for row in xrange(order):
    for col in xrange(row, order):
    xc = [xi * xj for (xi, xj) in zip(x[row][:], x[col][:])]
    s = sum(xc)
    A[row][col] = s
    A[col][row] = s
    s = [yl * xl for (yl, xl) in zip(y, x[row][:])]
    B[row] = sum(s)
    return (A, B)
    
    def extract_points(points):
    M = zip(*points)
    y = M[-1]
    x = [[1.0 for i in xrange(len(y))]]
    for line in M[:-1]:
    x += [line]
    return (x, y)
    
    n = len(points[0])
    (x, y) = extract_points(points)
    (A, b) = prepare_linear_system(x, y, n)
    alphas = cholesky(A, b)
    fun = lambda t: sum([ti * a for (ti, a) in zip([1] + list(t), alphas)])
    return fun</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Estendendo o post sobre regressão linear simples, temos o caso em que o vetor y é gerado por uma função com duas ou mais variáveis. Isto é, ao invés de ajustarmos uma função dependendo de uma variável \(x \) , utilizamos uma função na forma
    


<center>
  <br /> \(y = \alpha_0 + \alpha_1 x_1 + \alpha_2 x_2 + \epsilon \)<br />
</center>

Para esse caso, ao invés de ajustarmos os valores experimentais para uma reta, o ajuste é feito para um plano. 

Assim como é feito na regressão linear simples, os valores dos coeficientes são determinados através da soma dos quadrados dos resíduos. Isto é, tomamos
    


<center>
  <br /> \( S_r = \sum_{i=1}^{n} \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_{1i} &#8211; \alpha_2 x_{2i} \right)^2 \)<br />
</center>

e derivamos essa equação em termos de cada coeficiente a ser determinado. Portanto 

<center>
  <br /> \(\frac{dS_r}{d \alpha_0} = -2 \sum \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_{1i} &#8211; \alpha_2 x_{2i} \right) \)<br /> \(\frac{dS_r}{d \alpha_1} = -2 \sum x_{1i} \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_{1i} &#8211; \alpha_2 x_{2i} \right) \)<br /> \(\frac{dS_r}{d \alpha_2} = -2 \sum x_{2i} \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_{1i} &#8211; \alpha_2 x_{2i} \right) \)<br />
</center>

Os coeficientes fornecendo a soma mínima dos quadrados dos resíduos são obtidos igualando-se as derivadas parciais a zero. Podemos expressar esse sistema na forma matricial como
      


<center>
  <br /> \( \left[ \begin{array}{ccc}<br /> n & \sum x_{1i} & \sum x_{2i} \\<br /> \sum x_{1i} & \sum x_{1i}^2 & \sum x_{1i} x_{2i} \\<br /> \sum x_{2i} & \sum x_{1i} x_{2i} & \sum x_{2i}^2<br /> \end{array} \right]<br /> \left[ \begin{array}{c}<br /> \alpha_0 \\ \alpha_1 \\ \alpha_2<br /> \end{array} \right] =<br /> \left[ \begin{array}{c}<br /> \sum y_i \\ \sum x_{1i} y_i \\ \sum x_{2i} y_i<br /> \end{array} \right] \)<br />
</center>

&nbsp;

## 2. Caso Geral 

O caso geral estende o desenvolvimento bidimensional mostrado acima para \(m \) dimensões. Isto é, a função linear tem a forma
    


<center>
  <br /> \(y = \alpha_0 + \alpha_1 x_1 + \alpha_2 x_2 + \cdots + \alpha_m x_m + \epsilon \)<br />
</center>

e erro padrão possui a forma
    


<center>
  <br /> \(s = \sqrt{\dfrac{S_r}{n &#8211; (m + 1)}} \)<br />
</center>

## 3. Implementação 

<pre lang="python">def multilinear_regression(points):
    """
    Return a FUNCTION with parameters adjusted by polinomial regression

    f = multilinear_regression(points)

    INPUT:
      * points: list of tuples of sampled points (x1_i, x2_i, ..., y_i)

    return: a linear function f(x) = a_0 + a_1 * x + ... + a_m * x

    Author: Pedro Garcia [sawp @sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Sep 2011
    """
    def prepare_linear_system(x, y, order):
        A = [[0.0 for i in xrange(order)] for j in xrange(order)]
        B = [0.0 for i in xrange(order)]
        for row in xrange(order):
            for col in xrange(row, order):
                xc = [xi * xj for (xi, xj) in zip(x[row][:], x[col][:])]
                s = sum(xc)
                A[row][col] = s
                A[col][row] = s
            s = [yl * xl for (yl, xl) in zip(y, x[row][:])]
            B[row] = sum(s)
        return (A, B)

    def extract_points(points):
        M = zip(*points)
        y = M[-1]
        x = [[1.0 for i in xrange(len(y))]]
        for line in M[:-1]:
            x += [line]
        return (x, y)

    n = len(points[0])
    (x, y) = extract_points(points)
    (A, b) = prepare_linear_system(x, y, n)
    alphas = cholesky(A, b)
    fun = lambda t: sum([ti * a for (ti, a) in zip([1] + list(t), alphas)])
    return fun</pre>



Esta função está disponível em <a href="http://www.sawp.com.br/code/regression/multilinear_regression.py" target="_blank">http://www.sawp.com.br/code/regression/multilinear_regression.py</a> assim como um exemplo de como utilizá-la. 

&nbsp;

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.

&nbsp;

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a><br /> </fieldset>
