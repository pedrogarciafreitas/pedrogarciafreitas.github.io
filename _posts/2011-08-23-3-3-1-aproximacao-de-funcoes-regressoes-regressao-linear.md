---
id: 1251
title: '3.3.1 Aproximação de Funções &#8212; Regressões &#8212; Regressão Linear'
date: 2011-08-23T14:58:27+00:00
author: SAWP
excerpt: Neste e nos próximos posts, vamos considerar o problema de aproximar uma função cuja sequência de pontos foram obtidos de forma aproximada, sendo sujeitos à ruídos inerentes do processo de amostra. Assim, os arrendondamentos feitos pelos métodos de interpolação podem acumular erros muito maiores. Os métodos de regressão consistem em um conjunto de técnicas em que os erros funcionais podem ser usados para gerar uma aproximação suave da função.
layout: post
guid: http://www.sawp.com.br/blog/?p=1251
permalink: p=1251
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3797:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> linear_regression<span style="color: black;">&#40;</span>points<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a LINEAR FUNCTION with parameters adjusted by linear regression
    &nbsp;
    f = linear_regression(points)
    &nbsp;
    INPUT:
    * points: list of tuples of sampled points (x_i, y_i)
    &nbsp;
    return: a linear function f(x) = a_0 + a_1 * x
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2011
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>points<span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>sx<span style="color: #66cc66;">,</span> sy<span style="color: #66cc66;">,</span> sxy<span style="color: #66cc66;">,</span> sxx<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: black;">&#40;</span>xi<span style="color: #66cc66;">,</span> yi<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">in</span> points:
    sx +<span style="color: #66cc66;">=</span> xi
    sy +<span style="color: #66cc66;">=</span> yi
    sxy +<span style="color: #66cc66;">=</span> xi * yi
    sxx +<span style="color: #66cc66;">=</span> xi * xi
    <span style="color: black;">&#40;</span>xm<span style="color: #66cc66;">,</span> ym<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>sx / n<span style="color: #66cc66;">,</span> sy / n<span style="color: black;">&#41;</span>
    a1 <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>n * sxy - sx * sy<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span>n * sxx - sx * sx<span style="color: black;">&#41;</span>
    a0 <span style="color: #66cc66;">=</span> ym - a1 * xm
    fun <span style="color: #66cc66;">=</span> <span style="color: #ff7700;font-weight:bold;">lambda</span> t: a0 + a1 * t
    <span style="color: #ff7700;font-weight:bold;">return</span> fun</pre></td></tr></table><p class="theCode" style="display:none;">def linear_regression(points):
    &quot;&quot;&quot;
    Return a LINEAR FUNCTION with parameters adjusted by linear regression
    
    f = linear_regression(points)
    
    INPUT:
    * points: list of tuples of sampled points (x_i, y_i)
    
    return: a linear function f(x) = a_0 + a_1 * x
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2011
    &quot;&quot;&quot;
    n = len(points)
    (sx, sy, sxy, sxx) = (0, 0, 0, 0)
    for (xi, yi) in points:
    sx += xi
    sy += yi
    sxy += xi * yi
    sxx += xi * xi
    (xm, ym) = (sx / n, sy / n)
    a1 = (n * sxy - sx * sy) / (n * sxx - sx * sx)
    a0 = ym - a1 * xm
    fun = lambda t: a0 + a1 * t
    return fun</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Quando um erro substancial estiver associado aos dados, a interpolação polinomial é inapropriada e pode produzir resultados insatisfatórios. Isso ocorre porque pontos obtidos por um experimento geralmente exibem variações significativas entre as amostragens. A estratégia mais precisa para aproximar um conjunto de pontos consiste em determinar uma função de aproximação que
    
ajuste a forma geral dos dados, sem necessariamente passar por todos pontos individualmente. As figuras abaixo mostram esta diferença.

<table>
  <tr>
    <td>
      <div id="attachment_1254" style="width: 260px" class="wp-caption aligncenter">
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1a.png"><img class="size-full wp-image-1254" title="fig1a" src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1a.png" alt="Points" width="250" height="250" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1a.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1a-300x300.png 300w" sizes="(max-width: 250px) 100vw, 250px" /></a>
        
        <p class="wp-caption-text">
          Dados amostrados com erros significativos
        </p>
      </div>
    </td>
    
    <td>
      <div id="attachment_1255" style="width: 260px" class="wp-caption aligncenter">
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1b.png"><img class="size-full wp-image-1255" title="fig1b" src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1b.png" alt="Interpolation" width="250" height="250" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1b.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1b-300x300.png 300w" sizes="(max-width: 250px) 100vw, 250px" /></a>
        
        <p class="wp-caption-text">
          Ajuste polinomial oscilando além do intervalo dos dados
        </p>
      </div>
    </td>
    
    <td>
      <div id="attachment_1256" style="width: 260px" class="wp-caption aligncenter">
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1c.png"><img class="size-full wp-image-1256" title="fig1a" src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1c.png" alt="Regression" width="250" height="250" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1c.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/fig1c-300x300.png 300w" sizes="(max-width: 250px) 100vw, 250px" /></a>
        
        <p class="wp-caption-text">
          Ajuste mais satisfatório usando regressão linear
        </p>
      </div>
    </td>
  </tr>
</table>

Pelos gráficos, notamos que uma reta é a função que melhor caracteriza a sequência de dados e não passa nenhum ponto. A técnica para tal ajuste consiste na utilização de regressão linear. Embora este exemplo seja uma distribuição simples, métodos de regressão são geralmente ótimos para aproximações de valores à um modelo funcional. Neste e nos demais posts, apresentamos casos e técnicas de regressão, derivadas da regressão por mínimos quadrados. 

&nbsp;

## 2. Regressão Linear 

A forma mais simples de aproximação por mínimos quadrados é o ajuste de uma reta na forma 

<center>
  <br /> \(y = \alpha_0 + \alpha_1 x + \epsilon \)<br />
</center>

a um conjunto de pontos amostrados \((x\_1, y\_1), (x\_2, y\_2), \ldots, (x\_n, y\_n) \) . Onde \(\alpha\_0 \) é o coeficiente linear, \(\alpha\_1 \) é o coeficiente angular da reta e \(\epsilon \) é o resíduo (erro de aproximação) entre o modelo e a amostra, que pode ser isolado da equação acima, tendo representação 

<center>
  <br /> \(\epsilon = y &#8211; \alpha_0 &#8211; \alpha_1 x \)<br />
</center>

Assim, o erro de aproximação deve ser minimizado, a fim de que possamos ajustar os parâmetros \(\alpha\_0 \) e \(\alpha\_1 \) de forma que o modelo corresponda mais fielmente ao fenômeno observado. 

&nbsp;

## 3. Critério de Ajuste 

Para ajustarmos a reta que melhor aproximasse a todos os pontos, poderíamos utilizar como critério de erro a diferença absoluta entre o modelo e o valor amostrado. A estratégia de solução do ajuste consistiria em minimizar a soma dos erros residuais individuais, isto é 

<center>
  <br /> \( \sum_{i=1}^{n} | \epsilon_i | = \sum_{i=1}^{n} \left| y_i &#8211; \alpha_0 &#8211; \alpha_1 x_i \right| \)<br />
</center>

onde \(n \) é o número total de pontos. Contudo, este critério é inadequado.

Como podemos ver, este problema consiste na minimização do erro \(\epsilon \) . Portanto, uma estratégia consistiria em utilizar o critério _minimax_. A ideia aqui é escolher a reta que minimize a distancia máxima que um ponto individual tenha da reta. Contudo, essa técnica possui um problema quando o conjunto de pontos amostrados possui um valor muito discrepante dos demais, ou seja, quando há uma grande variância no erro dos pontos. Geralmente, critério minimax é utilizado para reduzir uma função adequada à uma simples. 

A abordagem que contorna todas as deficiências acima consiste na minimização da soma dos quadrados dos resíduos entre o \(y \) medido e o \(y \) calculado a partir do modelo linear. Ou Seja, 

<center>
  <br /> \(S_r = \sum_{i=1}^{n} \epsilon_i^2 = \sum_{i=1}^{n} \left( y_{i,amostrado} &#8211; y_{i,modelo} \right)^2 = \sum_{i=1}^{n} \left( y_i &#8211; \alpha_0 -\alpha_1 x_i \right)^2 \)<br />
</center>

A utilização desse critério possui a vantagem fornecer uma única reta para um dado conjunto de dados. 

&nbsp;

## 4. Ajuste dos Parâmetros por Mínimos Quadrados 

Para determinar os valores de \(\alpha\_0 \) e \(\alpha\_1 \) , derivamos a última equação acima por cada coeficiente. Isto é 

<center>
  <br /> \(\frac{\partial S_r}{\partial \alpha_0} = -2 \sum_{i=1}^{n} (y_i &#8211; \alpha_0 &#8211; \alpha_1 x_i) \)<br />
</center>

e 

<center>
  <br /> \(\frac{\partial S_r}{\partial \alpha_1} = -2 \sum_{i=1}^{n} (y_i &#8211; \alpha_0 &#8211; \alpha_1 x_i) x_i \)<br />
</center></p> 

Como queremos minimizar ao máximo o erro, tomamos como a soma da derivada de \(\epsilon_i \) como sendo zero. Isto é 

<center>
  <br /> \(\frac{\partial S_r}{\partial \alpha_0} = \sum_{i=1}^{n} \frac{\partial e_i^2}{\partial \alpha_0} = 0 \)<br />
</center>

Portanto, igualando as derivadas a zero, obtemos \(S_r \) mínimo. Assim, as equações podem ser expressas como 

<center>
  <br /> \(0 = \sum_{i=1}^{n} y_i &#8211; \sum_{i=1}^{n} \alpha_0 &#8211; \sum_{i=1}^{n} \alpha_1 x_i \)<br />
</center>

e 

<center>
  <br /> \(0 = \sum_{i=1}^{n} y_i x_i &#8211; \sum_{i=1}^{n} \alpha_0 x_i &#8211; \sum_{i=1}^{n} \alpha_1 x_i^2 \)<br />
</center>

Agora, tomando 

<center>
  <br /> \(\sum_{i=1}^{n} \alpha_0 = n \alpha_0 \)<br />
</center>

podemos expressar essas equações como um conjunto de duas equações lineares simultâneas em termos das variáveis \(\alpha\_0 \) e \(\alpha\_1 \) : </p> 

<center>
  <br /> \(n \alpha_0 + \left( \sum_{i=1}^{n} x_i \right) \alpha_1 = \sum_{i=1}^{n} y_i \)<br />
</center>

e 

<center>
  <br /> \(\left( \sum_{i=1}^{n} x_i \right) \alpha_0 + \left( x_i^2 \right) \alpha_1 = \sum_{i=1}^{n} x_i y_i \)<br />
</center>

Dessas equações, podemos isolar \(\alpha\_0 \) e \(\alpha\_1 \) : 

<center>
  <br /> \(\alpha_1 = \dfrac{n \sum_{i=1}^{n} x_i y_i &#8211; \sum_{i=1}^{n} x_i \sum_{i=1}^{n} y_i}{n \sum_{i=1}^{n} x_i^2 &#8211; (\sum_{i=1}^{n} x_i)^2} \)<br />
</center>

e 

<center>
  <br /> \(\alpha_0 = \dfrac{\sum_{i=1}^{n} y_i}{n} &#8211; \alpha_1 \dfrac{\sum_{i=1}^{n} x_i}{n} \)<br />
</center></p> 

&nbsp;

## 5. Implementação 

<pre lang="python">def linear_regression(points):
    """
    Return a LINEAR FUNCTION with parameters adjusted by linear regression

    f = linear_regression(points)

    INPUT:
    * points: list of tuples of sampled points (x_i, y_i)

    return: a linear function f(x) = a_0 + a_1 * x

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2011
    """
    n = len(points)
    (sx, sy, sxy, sxx) = (0, 0, 0, 0)
    for (xi, yi) in points:
        sx += xi
        sy += yi
        sxy += xi * yi
        sxx += xi * xi
    (xm, ym) = (sx / n, sy / n)
    a1 = (n * sxy - sx * sy) / (n * sxx - sx * sx)
    a0 = ym - a1 * xm
    fun = lambda t: a0 + a1 * t
    return fun</pre>



Esta função está disponível em <a href="http://www.sawp.com.br/code/regression/linear_regression.py" target="_blank">http://www.sawp.com.br/code/regression/linear_regression.py</a> assim como um exemplo de como utilizá-la. 

&nbsp;

## 6. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 

&nbsp;

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</p> 
    
    <p>
      </a><br /> </fieldset>
    </p>
