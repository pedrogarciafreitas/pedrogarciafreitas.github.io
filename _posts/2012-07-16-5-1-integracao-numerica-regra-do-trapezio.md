---
id: 1626
title: '5.1 Integração Numérica &#8212; Regra do Trapézio'
date: 2012-07-16T15:45:47+00:00
author: SAWP
excerpt: Neste post veremos como aproximar a área sob um gráfico (integral) com uma sequência de trapézios.
layout: post
guid: http://www.sawp.com.br/blog/?p=1626
permalink: p=1626
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3455:"
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
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    h <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>xe - xi<span style="color: black;">&#41;</span> / n
    t <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>f<span style="color: black;">&#40;</span>xi<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> + <span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span> * f<span style="color: black;">&#40;</span>xi + i * h<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> + <span style="color: black;">&#91;</span>f<span style="color: black;">&#40;</span>xi + n * h<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    integral <span style="color: #66cc66;">=</span> <span style="color: #008000;">sum</span><span style="color: black;">&#40;</span>t<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>h / <span style="color: #ff4500;">2.0</span><span style="color: black;">&#41;</span>
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
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    h = float(xe - xi) / n
    t = [f(xi)] + [2 * f(xi + i * h) for i in xrange(1, n)] + [f(xi + n * h)]
    integral = sum(t) * (h / 2.0)
    return integral</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Da mesma forma como apresentamos nos posts sobre derivação numérica, a integração numérica consiste em uma espécie de interpolação. A ideia é substituir uma função complicada \(f(x) \) por outra composta por operações mais simples e fácil de se integrar. Além disso, como mostramos em diversos posts relacionados aos métodos de interpolação, as fórmulas mais simples que podemos obter são polinômios. Assim, podemos obter esses polinômios através da fórmula de Taylor ou outra estratégia. 

Tais polinômios gerados para integração numérica são chamados de _fórmulas de Newton-Cotes_, que possuem a seguinte forma de aproximação
  


<center>
  \( I = \int_{a}^{b} f(x) dx \approx \int_{a}^{b} f_n(x) dx \)
</center>


  
onde \(f_n(x) \) é um polinômio na forma
  


<center>
  \( f_n(x) = a_0 + a_1 x + a_x x^2 + \cdots + a_{n-1} x^{n-1} + a_n x^n \)
</center>


  
onde \(n \) é o grau do polinômio. Por exemplo, na figura abaixo os gráficos mostram a função original \(f(x) \) em vermelho e duas aproximações distintas em azul. No gráfico da esquerda, um polinômio de primeiro grau (reta) é usado para aproximar a função em duas divisões. O gráfico da direita utiliza um polinômio de grau maior para aproximar a função em cada intervalo. 

<center>
  <br /> <a name="#fig1"></a><br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2012/07/numerical.png"><img class="aligncenter size-full wp-image-416" title="Aproximação da raiz por uma reta." src="http://www.sawp.com.br/blog/wp-content/uploads/2012/07/numerical.png" alt="numerical" width="850" height="400" /></a><br />
</center>

Da figura acima também podemos notar que a integral é melhor aproximada se usarmos uma série de polinômios aplicados por partes à função \(f(x) \), dividindo-se o intervalo de integração em sub-intervalos menores. 

&nbsp;

## 2. A Regra do Trapézio 

A regra do trapézio consiste na utilização de \(f_n(x) \) com \(n=1 \) . Portanto, ela corresponde à primeira fórmula de Newton-Cotes:
  


<center>
  \( I = \int_{a}^{b} f(x) dx \approx \int_{a}^{b} f_1(x) dx \)
</center>


  
onde
  


<center>
  \( f_1(x) = f(a) + \frac{f(b) &#8211; f(a)}{b &#8211; a} (x &#8211; a) \)
</center>

A área sob \(f_1(x) \) é uma estimativa da integral de \(f(x) \) entre os extremos \(a \) e \(b \) . Para obtermos essa estimativa, expressamos a equação acima como
  


<center>
  \( f_1(x) = \frac{f(b)-f(a)}{b-a}x + f(a) &#8211; \frac{af(b) &#8211; af(a)}{b-a} \)
</center>


  
Agrupando os dois últimos termos, obtemos
  


<center>
  \( f_1(x) = \frac{f(b)-f(a)}{b-a}x + \frac{bf(a) &#8211; af(a) &#8211; af(b) + af(a)}{b-a} \)
</center>


  
ou
  


<center>
  \( f_1(x) = \frac{f(b)-f(a)}{b-a}x + \frac{bf(a) &#8211; af(b)}{b-a} \)
</center>


  
que é então integrada, fornecendo
  


<center>
  \( I = \frac{f(b)-f(a)}{b-a} \frac{x^2}{2} + x \frac{bf(a)-af(b)}{b-a} \)
</center>


  
Na expressão integrada que vemos acima, usamos o intervalo delimitado por \(x=a \) e \(x=b \) . Esse resultado pode ser calculado por
  


<center>
  \( I = \frac{f(b)-f(a)}{b-a}\frac{b^2-a^2}{2} + \frac{bf(a)-af(b)}{b-a}(b-a) \)
</center>


  
Agora, como \(b^2-a^2 = (b-a)(b+a) \) , temos
  


<center>
  \( I = [f(b)-f(a)] \frac{b+a}{2} + bf(a) &#8211; af(b) \)
</center>


  
que ao fazermos a multiplicação e agruparmos os termos, temos
  


<center>
  \( I = (b-a) \frac{f(a)+f(b)}{2} \)
</center>


  
que é a fórmula da regra dos trapézios.

&nbsp;

### 2.1. Divisão de intervalos 

Para melhorar a acurácia da integração, devemos dividir o intervalo de integração de \(a \) e \(b \) em diversos segmentos e aplicar o método a cada asegmento. Cada área correspondente aos segmentos individuais podem então ser somadas para fornecer a integral para o intervalo inteiro. A figura abaixo mostra como um conjunto de trapézios formados em cada subintervalo dividido se aproxima da integral. 

<center>
  <br /> <a name="#fig2"></a><br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2012/07/integration1.gif"><img class="aligncenter size-full wp-image-416" title="Aproximação da raiz por uma reta." src="http://www.sawp.com.br/blog/wp-content/uploads/2012/07/integration1.gif" alt="numerical" width="400" height="400" /></a><br />
</center>

Dividindo o intervalo de integração \([a,b] \) em \(n \) partes, temos \(n \) segmentos de mesma largura tal que
  


<center>
  \( h = \frac{b &#8211; a}{n} \)
</center>


  
Se \(a \) e \(b \) forem respectivamente renomeados por \(x\_0 \) e \(x\_n \) , a integral total pode ser obtida por
  


<center>
  \( I = \int_{x_0}^{x_1} f(x) dx + \int_{x_1}^{x_2} f(x) dx + \cdots + \int_{x_{n-1}}^{x_n} f(x) dx \)
</center>


  
Substituindo cada integral pela regra do trapézio, obtemos
  


<center>
  \( I = h \frac{f(x_0)+f(x_1)}{2} + h \frac{f(x_1)+f(x_2)}{2} + \cdots + h \frac{f(x_{n-1})+f(x_n)}{2} \)
</center>


  
Agrupando os termos da equação acima, temos
  


<center>
  \( I = \frac{h}{2} \left[ f(x_0) + 2 \sum_{i=1}^{n-1} f(x_i) + f(x_n) \right] \)
</center>


  
que é a expressão usada na implementação da regra dos trapézios.

&nbsp;

## 3. Estimativa do Erro 

Como a soma dos coeficientes de \(f(x) \) no numerador dividido por \(2n \) é igual a 1, a altura média representa uma média ponderada dos valores da função. De acordo com a última equação apresentada na seção anterior, os pontos interiores tem um peso duas vezes maior do que as extremidades. Assim, um erro para a aplicação múltipla da regra dos trapézios pode ser obtido pela soma dos erros individuais em cada segmento, o que dá
  


<center>
  \( E = &#8211; \frac{(b-a)^3}{12n^3} \sum_{i=1}^{n} f&#8221;(\varepsilon_i) \)
</center>


  
em que \(f&#8221;(\varepsilon\_i) \) é a segunda derivada em um ponto \(\varepsilon\_i \) localizado no segmento \(i \) . Esse resultado pode ser simplificado por uma estimativa do valor médio da segunda derivada no intervalo todo como
  


<center>
  \( g&#8221; \approx \frac{\sum_{i=1}^{n}f&#8221;(\varepsilon_i)}{n} \)
</center>


  
Portanto, \(\sum f&#8221;(\varepsilon_i) \approx ng&#8221; \) e a expressão do erro em função do número de intervalos pode ser escrita como
  


<center>
  \( E(n) = &#8211; \frac{(b-a)^3}{12n^2} g&#8221; \)
</center>


  
Onde \(g&#8221;\) é a média das derivadas de segunda ordem. 

&nbsp;

## 4. Implementação 

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

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    h = float(xe - xi) / n
    t = [f(xi)] + [2 * f(xi + i * h) for i in xrange(1, n)] + [f(xi + n * h)]
    integral = sum(t) * (h / 2.0)
    return integral</pre>

Um exemplo de utilização dessa função pode ser obtido em <a href="http://www.sawp.com.br/code/integral/integral_trapezoid.py" target="_blank">http://www.sawp.com.br/code/integral/integral_trapezoid.py</a>. 

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
