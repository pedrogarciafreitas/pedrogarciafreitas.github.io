---
id: 1350
title: '3.3.3 Aproximação de Funções &#8212; Regressões &#8212; Regressão Polinomial'
date: 2011-10-05T10:19:06+00:00
author: SAWP
excerpt: Nos dois últimos posts apresentamos o desenvolvimento para ajustar dados em uma equação da reta através de mínimos quadrados. Contudo, existem muitos eventos em que o modelo obedece à um comportamento polinomial. Para tais modelos é necessário adaptar o ajuste para uma função polinomial de grau superior.
layout: post
guid: http://www.sawp.com.br/blog/?p=1350
permalink: /p=1350
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:9188:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> polinomial_regression<span style="color: black;">&#40;</span>points<span style="color: #66cc66;">,</span> order <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a FUNCTION with parameters adjusted by polinomial regression
    &nbsp;
    f = polinomial_regression(points)
    &nbsp;
    INPUT:
    * points: list of tuples of sampled points (x_i, y_i)
    * order: order of adjusted polynom (-1 to auto-adjust)
    &nbsp;
    return: a polinomial function f(x) = a_0 + a_1 * x + ... + a_m * x^m
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
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
    c <span style="color: #66cc66;">=</span> col + row
    xc <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>i ** c <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> x<span style="color: black;">&#93;</span>
    s <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span>xc<span style="color: black;">&#41;</span>
    A<span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> s
    A<span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>row<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> s
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>order<span style="color: black;">&#41;</span>:
    bc <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#40;</span>xi ** col<span style="color: black;">&#41;</span> * yi <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: black;">&#40;</span>xi<span style="color: #66cc66;">,</span> yi<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">zip</span><span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    B<span style="color: black;">&#91;</span>col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span>bc<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> B<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> select_degree<span style="color: black;">&#40;</span>points<span style="color: #66cc66;">,</span> order<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> order <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">1</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>points<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> order + <span style="color: #ff4500;">1</span>
    &nbsp;
    n <span style="color: #66cc66;">=</span> select_degree<span style="color: black;">&#40;</span>points<span style="color: #66cc66;">,</span> order<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">zip</span><span style="color: black;">&#40;</span>*points<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> prepare_linear_system<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>
    alphas <span style="color: #66cc66;">=</span> cholesky<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: black;">&#41;</span>
    fun <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> t: <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span>t * a <span style="color: #ff7700;font-weight:bold;">for</span> a <span style="color: #ff7700;font-weight:bold;">in</span> alphas<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> fun</pre></td></tr></table><p class="theCode" style="display:none;">def polinomial_regression(points, order = -1):
    &quot;&quot;&quot;
    Return a FUNCTION with parameters adjusted by polinomial regression
    
    f = polinomial_regression(points)
    
    INPUT:
    * points: list of tuples of sampled points (x_i, y_i)
    * order: order of adjusted polynom (-1 to auto-adjust)
    
    return: a polinomial function f(x) = a_0 + a_1 * x + ... + a_m * x^m
    
    Author: Pedro Garcia [sawp@sawp.com.br]
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
    c = col + row
    xc = [i ** c for i in x]
    s = sum(xc)
    A[row][col] = s
    A[col][row] = s
    for col in xrange(order):
    bc = [(xi ** col) * yi for (xi, yi) in zip(x, y)]
    B[col] = sum(bc)
    return (A, B)
    
    def select_degree(points, order):
    if order &lt; 1:
    return len(points)
    else:
    return order + 1
    
    n = select_degree(points, order)
    (x, y) = zip(*points)
    (A, b) = prepare_linear_system(x, y, n)
    alphas = cholesky(A, b)
    fun = lambda t: sum([t * a for a in alphas])
    return fun</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Nos dois últimos posts apresentamos o desenvolvimento para ajustar dados em uma equação da reta através de mínimos quadrados. Contudo, existem muitos eventos em que o modelo obedece à um comportamento polinomial. Para tais modelos é necessário adaptar o ajuste para uma função polinomial de grau superior. A imagem abaixo ilustra um caso em que a regressão linear não ajusta adequadamente os dados ao comportamento do evento observado. 

[<img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/10/regressao.png" alt="" title="regressao" width="400" height="400" class="aligncenter size-full wp-image-1353" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/10/regressao.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2011/10/regressao-300x300.png 300w" sizes="(max-width: 400px) 100vw, 400px" />](http://www.sawp.com.br/blog/wp-content/uploads/2011/10/regressao.png) 

&nbsp;

## 2. Regressão Polinomial 

A regressão polinomial pode ser vista como uma generalização da regressão linear. Para isso, podemos ver a regressão linear simples como o ajuste de um polinômio de grau um. Assim, ao invés de ajustarmos a função
    


<center>
  <br /> $$y = \alpha_0 + \alpha_1 x + \epsilon $$<br />
</center>


  
utilizamos
    


<center>
  <br /> $$y = \alpha_0 + \alpha_1 x + \alpha_2 x^2 + \cdots + \alpha_m x ^m + \epsilon $$<br />
</center>


    
Para ajustarmos os parâmetros dessa função, basta que resolvamos um sistema de $$m + 1 $$ equações lineares simultâneas, similarmente ao desenvolvimento da regressão linear múltipla. Assim, no caso da regressão polinomial, o erro padrão pode ser formulado como
    


<center>
  <br /> $$s = \sqrt{\dfrac{S_r}{n &#8211; (m + 1)}$$<br />
</center>. 

Como exemplo, vamos tomar o ajuste dos dados apresentados no gráfico do início desse texto. Desta figura, podemos notar que o comportamento dos pontos segue uma função parabólica, o que sugere que devemos ajustar um polinômio de segundo grau:
    


<center>
  <br /> $$y = \alpha_0 + \alpha_1 x + \alpha_2 x^2 + \epsilon $$<br />
</center>


  
Nesse caso, a soma dos quadrados dos resíduos é
    


<center>
  <br /> $$S_r = \sum_{i=1}^{n} \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_i &#8211; \alpha_2 x_{i}^2 \right)^2 $$<br />
</center>

Assim como fizemos para regressão linear, tomamos a derivada da equação acima com relação à cada um dos coeficientes desconhecidos do polinômio:
    


<center>
  <br /> $$\dfrac{dS_r}{d \alpha_0} = -2 \sum_{i=1}^{n} \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_i &#8211; \alpha_2 x_i^2 \right) $$ <br /> $$\dfrac{dS_r}{d \alpha_1} = -2 \sum_{i=1}^{n} x_i \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_i &#8211; \alpha_2 x_i^2 \right) $$ <br /> $$\dfrac{dS_r}{d \alpha_2} = -2 \sum_{i=1}^{n} x_i^2 \left( y_i &#8211; \alpha_0 &#8211; \alpha_1 x_i &#8211; \alpha_2 x_i^2 \right) $$ <br />
</center>


  
Igualando estas equações à zero e obtemos o seguinte conjunto de equações:
    


<center>
  <br /> $$n \alpha_0 + \alpha_1 \sum_{i=1}^{n} x_i + \alpha_2 \sum_{i=1}^{n} x_i^2 = \sum_{i=1}^{n} y_i $$ <br /> $$\alpha_0 \sum_{i=1}^{n} x_i + \alpha_1 \sum_{i=1}^{n} x_i^2 + \alpha_2 \sum_{i=1}^{n} x_i^3 = \sum_{i=1}^{n} y_i x_i $$ <br /> $$\alpha_0 \sum_{i=1}^{n} x_i^2 + \alpha_1 \sum_{i=1}^{n} x_i^3 + \alpha_2 \sum_{i=1}^{n} x_i^4 = \sum_{i=1}^{n} y_i x_i^2 $$ <br />
</center>

Dessas três últimas equações lineares, temos apenas três incógnitas: $$\alpha\_0 $$ , $$\alpha\_1 $$ e $$\alpha_2 $$ . Assim, resolvendo essas equações, temos os parâmetros ajustados. 

&nbsp;

## 3. Implementação 

Como podemos notar, para um conjunto de $$n = m + 1 $$ pontos amostrados, é possível ajustar um polinômio de grau $$m $$ ou menor. Na implementação abaixo utilizamos um ajuste automático do grau polinomial, escolhendo o valor de $$m $$ que minimize o erro padrão. 

Note que na função abaixo, utilizamos o método de Cholesky para resolução do sistema linear. Poderíamos utilizar qualquer outro método, não sendo esse escolhido obrigatório para o ajuste correto dos dados. 

<pre lang="python">def polinomial_regression(points, order = -1):
    """
    Return a FUNCTION with parameters adjusted by polinomial regression

    f = polinomial_regression(points)

    INPUT:
      * points: list of tuples of sampled points (x_i, y_i)
      * order: order of adjusted polynom (-1 to auto-adjust)

    return: a polinomial function f(x) = a_0 + a_1 * x + ... + a_m * x^m

    Author: Pedro Garcia [sawp@sawp.com.br]
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
                c = col + row
                xc = [i ** c for i in x]
                s = sum(xc)
                A[row][col] = s
                A[col][row] = s
        for col in xrange(order):
            bc = [(xi ** col) * yi for (xi, yi) in zip(x, y)]
            B[col] = sum(bc)
        return (A, B)

    def select_degree(points, order):
        if order &lt; 1:
            return len(points)
        else:
            return order + 1

    n = select_degree(points, order)
    (x, y) = zip(*points)
    (A, b) = prepare_linear_system(x, y, n)
    alphas = cholesky(A, b)
    fun = lambda t: sum([t * a for a in alphas])
    return fun</pre>

Esta função está disponível em <a href="http://www.sawp.com.br/code/regression/polinomial_regression.py" target="_blank">http://www.sawp.com.br/code/regression/polinomial_regression.py</a> assim como um exemplo de como utilizá-la. 

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
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
