---
id: 1607
title: '4.1 Derivação Numérica &#8212; Fórmulas de Derivação Numérica'
date: 2012-06-25T11:13:57+00:00
author: SAWP
excerpt: 'Derivação numérica é a técnica de obter valores aproximados para a derivada de uma função usando valores da função em um conjunto de pontos e propriedades conhecidas da função. '
layout: post
guid: http://www.sawp.com.br/blog/?p=1607
permalink: /p=1607
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:2707:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> diff1<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.0001</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the 1st derivative function evaluated in point x.
    &nbsp;
    diff_f_xi = diff1(fun, x, h=0.001)
    &nbsp;
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    &nbsp;
    return: f'(X=x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jun 2012
    &quot;&quot;&quot;</span>
    a <span style="color: #66cc66;">=</span> -f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">2</span> * h<span style="color: black;">&#41;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">8</span> * f<span style="color: black;">&#40;</span>x + h<span style="color: black;">&#41;</span>
    c <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">8</span> * f<span style="color: black;">&#40;</span>x - h<span style="color: black;">&#41;</span>
    d <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x - <span style="color: #ff4500;">2</span> * h<span style="color: black;">&#41;</span>
    diff <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>a + b + c + d<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">12</span> * h<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> diff</pre></td></tr></table><p class="theCode" style="display:none;">def diff1(f, x, h=0.0001):
    &quot;&quot;&quot;
    Return the 1st derivative function evaluated in point x.
    
    diff_f_xi = diff1(fun, x, h=0.001)
    
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    
    return: f'(X=x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jun 2012
    &quot;&quot;&quot;
    a = -f(x + 2 * h)
    b = 8 * f(x + h)
    c = -8 * f(x - h)
    d = f(x - 2 * h)
    diff = (a + b + c + d) / (12 * h)
    return diff</p></div>
    ;i:2;s:2969:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> diff2<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.00001</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the 2nd derivative function evaluated in point x.
    &nbsp;
    diff_f_xi = diff2(fun, x, h=0.001)
    &nbsp;
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    &nbsp;
    return: f&quot;(X=x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jun 2012
    &quot;&quot;&quot;</span>
    a <span style="color: #66cc66;">=</span> -f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">2</span> * h<span style="color: black;">&#41;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">16</span> * f<span style="color: black;">&#40;</span>x + h<span style="color: black;">&#41;</span>
    c <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">30</span> * f<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    d <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">16</span> * f<span style="color: black;">&#40;</span>x - h<span style="color: black;">&#41;</span>
    e <span style="color: #66cc66;">=</span> -f<span style="color: black;">&#40;</span>x - <span style="color: #ff4500;">2</span> * h<span style="color: black;">&#41;</span>
    diff <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>a + b + c + d + e<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">12</span> * h ** <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> diff</pre></td></tr></table><p class="theCode" style="display:none;">def diff2(f, x, h=0.00001):
    &quot;&quot;&quot;
    Return the 2nd derivative function evaluated in point x.
    
    diff_f_xi = diff2(fun, x, h=0.001)
    
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    
    return: f&quot;(X=x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jun 2012
    &quot;&quot;&quot;
    a = -f(x + 2 * h)
    b = 16 * f(x + h)
    c = -30 * f(x)
    d = 16 * f(x - h)
    e = -f(x - 2 * h)
    diff = (a + b + c + d + e) / (12 * h ** 2)
    return diff</p></div>
    ;i:3;s:3272:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> diff3<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.00001</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the 3rd derivative function evaluated in point x.
    &nbsp;
    diff_f_xi = diff3(fun, x, h=0.001)
    &nbsp;
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    &nbsp;
    return: f&quot;'(X=x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jun 2012
    &quot;&quot;&quot;</span>
    a <span style="color: #66cc66;">=</span> -f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">3</span> * h<span style="color: black;">&#41;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">8</span> * f<span style="color: black;">&#40;</span>x + <span style="color: #ff4500;">2</span> * h<span style="color: black;">&#41;</span>
    c <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">13</span> * f<span style="color: black;">&#40;</span>x + h<span style="color: black;">&#41;</span>
    d <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">13</span> * f<span style="color: black;">&#40;</span>x - h<span style="color: black;">&#41;</span>
    e <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">8</span> * f<span style="color: black;">&#40;</span>x - <span style="color: #ff4500;">2</span> * h<span style="color: black;">&#41;</span>
    ff <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x - <span style="color: #ff4500;">3</span> * h<span style="color: black;">&#41;</span>
    diff <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>a + b + c + d + e + ff<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span><span style="color: #ff4500;">8</span> * h ** <span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> diff</pre></td></tr></table><p class="theCode" style="display:none;">def diff3(f, x, h=0.00001):
    &quot;&quot;&quot;
    Return the 3rd derivative function evaluated in point x.
    
    diff_f_xi = diff3(fun, x, h=0.001)
    
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    
    return: f&quot;'(X=x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jun 2012
    &quot;&quot;&quot;
    a = -f(x + 3 * h)
    b = 8 * f(x + 2 * h)
    c = -13 * f(x + h)
    d = 13 * f(x - h)
    e = -8 * f(x - 2 * h)
    ff = f(x - 3 * h)
    diff = (a + b + c + d + e + ff) / (8 * h ** 3)
    return diff</p></div>
    ;i:4;s:2969:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> diff4<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> h<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.0001</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the 4th derivative function evaluated in point x.
    &nbsp;
    diff_f_xi = diff4(fun, x, h=0.001)
    &nbsp;
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    &nbsp;
    return: f&quot;&quot;(X=x)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jun 2012
    &quot;&quot;&quot;</span>
    a <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    b <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">4</span> * f<span style="color: black;">&#40;</span>x - h<span style="color: black;">&#41;</span>
    c <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">6</span> * f<span style="color: black;">&#40;</span>x - <span style="color: #ff4500;">2</span> * h<span style="color: black;">&#41;</span>
    d <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">4</span> * f<span style="color: black;">&#40;</span>x - <span style="color: #ff4500;">3</span> * h<span style="color: black;">&#41;</span>
    e <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x - <span style="color: #ff4500;">4</span> * h<span style="color: black;">&#41;</span>
    diff <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>a + b + c + d + e<span style="color: black;">&#41;</span> / <span style="color: black;">&#40;</span>h ** <span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> diff</pre></td></tr></table><p class="theCode" style="display:none;">def diff4(f, x, h=0.0001):
    &quot;&quot;&quot;
    Return the 4th derivative function evaluated in point x.
    
    diff_f_xi = diff4(fun, x, h=0.001)
    
    INPUT:
    * f: function to derivate
    * x: evaluation point
    * h: step size
    
    return: f&quot;&quot;(X=x)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jun 2012
    &quot;&quot;&quot;
    a = f(x)
    b = -4 * f(x - h)
    c = 6 * f(x - 2 * h)
    d = -4 * f(x - 3 * h)
    e = f(x - 4 * h)
    diff = (a + b + c + d + e) / (h ** 4)
    return diff</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Apesar dos livros de análise numérica se dividirem em distintas seções para representar diversas técnicas de resolução de problemas, problemas numéricos são, geralmente, reduzidos aos modelos apresentados nos posts anteriores (busca de raízes, solução de sistemas, regressão e interpolação). Os métodos de integração e diferenciação numérica são casos específicos de interpolação de funções. 

Uma vez que na interpolação nós nos estudamos os casos onde a função é representada por uma tabela de valores, na derivação numérica nós buscamos ajustar a derivada da função a partir de valores gerados pela função em si. Para observarmos a relação entre a derivação numérica e a interpolação, inicialmente veremos como obter a diferenciação numérica a partir dos dados. Em seguida, estudaremos como é feita a derivação numérica de uma função a partir dela mesma. 

&nbsp;

## 2. Derivação Numérica dos Dados 

Quando uma função é representada por uma tabela de valores, a abordagem mais óbvia é diferenciar a fórmula interpoladora de Lagrange, apresentada no post 3.1.3. Isso nos dá que
  


<center>
  $$ f^{(k)}(x) = \sum_{j=1}^{n} l_{j}^{(k)}(x) f(a_j) + \frac{d^k}{dx^k} \left[ \frac{p_n(x)}{n!} f^{(n)}(\xi) \right] = y^{(k)}(x) + \frac{d^k}{dx^k} \left[ E(x) \right] $$
</center>


  
Em particular, para $$k=1 $$ , temos
  


<center>
  $$ f'(x) = \sum_{j=1}^{n} l&#8217;_j(x) f(a_k) + \frac{d}{dx} \left[ \frac{p_n(x)}{n!} f^{(n)}(\xi) \right] $$
</center>


  
onde a derivada $$l_j(x) $$ pode ser facilmente obtida pela interpolação de Lagrange, conforme mostramos no post 3.1.3. A determinação do erro $$E(x)$$ é obtida por
  


<center>
  $$ \frac{d^k}{dx^k} \left[ E(x) \right] = \frac{f^{(n)}(\xi)}{(n &#8211; k)!} \prod_{j=1}^{n-k} (x &#8211; \eta_j) $$
</center>


  
onde os $$n-k $$ pontos distintos $$\eta_j $$ são independentes de $$x$$ e são conhecidos nos intervalos
  


<center>
  $$ a_j < \eta_j < a_{j+k} $$
</center>


  
em $$j=1,\ldots,n-k $$ , $$\xi $$ é o menos intervalo $$I $$ que contém $$x $$ e $$\eta\_j$$. Se, no caso dos valores da função serem dados nos pontos de dados, são dados os valores das funções derivadas em alguns pontos. Assim, podemos derivar os coeficientes $$w\_{ij}^{(k)}(x)$$ pela fórmula
  


<center>
  $$ f^{(k)}(x) \approx \sum_{j=1}^{n} \sum_{i=0}^{m_j} w_{ij}^{(k)}(x) f^{(i)}(a_j) $$
</center>

Uma abordagem alternativa para determinar a diferenciação numérica de dados para aproximação da primeira e segunda derivada é computar a interpolação spline cúbica e diferenciá-la. Para qualquer valor de $$x $$ , nós podemos determinar dois nós $$a\_j $$ e $$a\_{j+1} $$ tal que $$a\_j < x < a\_{j+1} $$ . Assim, $$y'(x) \approx S&#8217;\_j(x) $$ e $$y&#8221; \approx S&#8221;\_j(x) $$ , onde $$S\_j(x) $$ é o pedaço da spline interpoladora &#8212; um polinômio de terceiro grau definido em $$[a\_j, a_{j+1}] $$ . A partir do que foi demonstrado no post 3.1.7, assumimos que, assintóticamente, temos $$h $$ , a distância máxima entre dois nós da spline,
  


<center>
  $$ max |f^{(k)}(x) &#8211; S^k(x) | = O(h^{4-k}) $$
</center>


  
para $$k=1,2 $$ . Isso indica que a primeira e a segunda derivada da spline interpoladora é aproximadamente a derivada da função. Podemos ver isso mais claramente quando assumimos que os espaços são igualmente espaçados nos pontos amostrados. Temos, então, que
  


<center>
  $$ y^{(k)}(x) = \frac{1}{h^k} \sum_{j=1}^{n} l_j^{(k)}(m) f(a_i) $$
</center>


  
onde $$x=a\_0 + h m $$ , a diferenciação de $$l\_j(m) $$ em relação à $$m $$ vem do fato de que
  


<center>
  $$ \frac{dy}{dx} = \frac{dy}{dm} \frac{dm}{dx} = \frac{1}{m} \frac{dy}{dm} $$
</center>

De formula similar, podemos derivar outras fórmulas de interpolação e obter a derivada como a diferença dos valores interpolados. Por exemplo, quando usamos a fórmula de Newton, temos que
  


<center>
  $$ \frac{d^k}{dx^k} y(a_0 + hm) = \frac{1}{h^k} \frac{d^k}{dm^k} y(a_0 + hm) = \frac{1}{h^k} \sum_{j=0}^{n} \frac{d^k}{dm^k} \binom{m}{j} \Delta^j f_0 = \frac{1}{h^k} \sum_{j=k}^{n} \frac{d^k}{dm^k} \binom{m}{j} \Delta^j f_0 $$
</center>


  
O aparecimento do fator $$\frac{1}{h^k} $$ torna explícito o fato de que a diferenciação numérica consiste na aproximação da função derivada por divisão de pequenos intervalos. Portanto, $$h $$ deve ser um valor pequeno o suficiente para, considerando um erro de aproximação tolerado &#8212; lembrando que na solução analítica temos $$h \rightarrow 0 $$ . 

&nbsp;

## 3. Derivação Numérica de Funções 

Quando precisamos computar a derivada da uma função que pode ser avaliada em qualquer ponto em um dado intervalo $$I $$ , podemos construir os pontos utilizados na interpolação dessa função derivada. Se $$x + h $$ e $$x &#8211; h $$ estão contidos em $$I $$ , utilizamos a expansão da série de Taylor:
  


<center>
  $$ f(x+h) = f(x) + h f'(x) + \frac{h^2}{2} f&#8221;(x) + \cdots $$
</center>


  
e
  


<center>
  $$ f(x-h) = f(x) &#8211; h f'(x) + \frac{h^2}{2} f&#8221;(x) &#8211; \cdots $$
</center>


  
Subtraindo essas duas equações e dividindo por $$2h $$ , os temos restantes são
  


<center>
  $$ f'(x) = \frac{f(x+h) &#8211; f(x-h)}{2h} + \sum_{i=1}^{\infty} \frac{f^{(2i+1)}(x)}{(2i+1)!} h^{2i} $$
</center>


  
substituindo esse $$f'(x) $$ na série de Taylor e isolando $$f&#8221;(x)$$ , temos uma aproximação para a segunda derivada
  


<center>
  $$ f&#8221;(x) = \frac{f(x+h) &#8211; 2f(x) + f(x-h)}{h^2} + \sum_{i=1}^{\infty} \frac{2 f^{(2i+2)}(x)}{(2i+2)!} h^{2i} $$
</center>


  
Portanto, para um $$h $$ suficiente pequeno, temos que o somatório de valores muito pequenos consiste de um resíduo, o que nos permite aproximar a primeira e a segunda derivada por
  


<center>
  $$ f'(x) \approx \frac{f(x+h) &#8211; f(x-h)}{2h} $$
</center>


  
e
  


<center>
  $$ f&#8221;(x) \approx \frac{f(x+h) &#8211; 2f(x) + f(x-h)}{h^2} $$
</center>


  
Assim, nossa estratégia consiste em avaliar as funções no ponto $$x $$ a partir de um valor $$h $$ suficientemente pequeno para o problema dado. 

Note que podemos substituir $$f'(x)$$ e $$f&#8221;(x)$$ na série de Taylor para obter $$f&#8221;'(x)$$, que por sua vez pode ser utilizada para obter $$f&#8221;&#8221;(x)$$ e assim sucessivamente até obtermos a $$n$$ derivada desejada. Note também que o resultado truncado da primeira e segunda derivada possui erro $$O(h)$$. Contudo, utilizando mais pontos, podemos ter uma aproximação mais acurada, com erro $$O(h^2)$$. Isto é, em vez de utilizarmos
  


<center>
  $$ f'(x) = \frac{f(x+h) &#8211; f(x-h)}{2h} + O(h) $$
</center>


  
podemos utilizar a expressão
  


<center>
  $$ f'(x) = \frac{-f(x+2h) + 4f(x+h) &#8211; 3f(x)}{2h} + O(h^2) $$
</center>

Observe que na equação acima utilizamos 3 pontos para obter a primeira derivada. Esse segundo termo vêm da utilização de $$f&#8221;(x)$$ na fórmula de Taylor, isolando-se $$f'(x) $$ . Além disso, utilizamos os pontos $$x $$ , $$x+h $$ e $$x+2h $$ . A utilização de pontos sucessivos ao ponto de avaliação é chamada de _diferenças divididas finitas progressivas_. Contudo, podemos utilizar os pontos anteriores (_regressiva_) ou ambos (_centrada_). Quanto mais próximo do ponto de avaliação, mais precisa é a aproximação. Por isso, as _diferenças divididas finitas centradas_ possuem maior acurácia. 

Nas próximas subseções, listamos as fórmulas das primeiras quadro derivadas numéricas utilizando as três escolhas de pontos. Para facilitar a notação, definimos como $$x\_{i+h} = x + ih $$ e $$x\_{i-h} = x &#8211; ih $$ . 

&nbsp;

### 3.1. Diferença Dividida Finita Progressiva 

  * Primeira derivada: 
      * $$O(h)$$ : $$f'(x) = \frac{f(x\_{i+1}) &#8211; f(x\_i)}{h} $$ 
      * $$O(h^2) $$ : $$f'(x) = \frac{-f(x\_{i+2}) + 4f(x\_{i+1}) &#8211; 3f(x_i)}{2h} $$ 
  * Segunda derivada: 
      * $$O(h)$$ : $$f&#8221;(x) = \frac{f(x\_{i+2}) + 2f(x\_{i+1}) + f(x_i)}{h^2} $$ 
      * $$O(h^2)$$ : $$f&#8221;(x) = \frac{-f(x\_{i+3}) + 4f(x\_{i+2}) &#8211; 5f(x\_{i+1}) + 2f(x\_i)}{h^2}$$ 
  * Terceira derivada: 
      * $$O(h)$$ : $$f&#8221;'(x) = \frac{f(x\_{i+3}) &#8211; 3f(x\_{i+2}) + 3f(x\_{i+1}) -f(x\_i)}{h^3} $$ 
      * $$O(h^2) $$ : $$f&#8221;'(x) = \frac{-3f(x\_{i+4}) + 14f(x\_{i+3}) &#8211; 24f(x\_{i+2}) + 18f(x\_{i+1}) &#8211; 5f(x_i)}{2h^3}$$ 
  * Quarta derivada: 
      * $$O(h) $$ : $$f&#8221;&#8221;(x) = \frac{f(x\_{i+4}) &#8211; 4f(x\_{i+3}) +6f(x\_{i+2}) &#8211; 4f(x\_{i+1}) + f(x_i)}{h^4}$$ 
      * $$O(h^2) $$ : $$f&#8221;&#8221;(x) = \frac{-2f(x\_{i+5}) + 11f(x\_{i+4}) &#8211; 24f(x\_{i+3}) + 26f(x\_{i+2}) &#8211; 14f(x\_{i+1}) + 3f(x\_i)}{h^4}$$ 

&nbsp;

### 3.2. Diferença Dividida Finita Regressiva 

  * Primeira derivada: 
      * $$O(h) $$ : $$f'(x) = \frac{-f(x\_{i-1}) + f(x\_i)}{h} $$ 
      * $$O(h^2) $$ : $$f'(x) = \frac{f(x\_{i-2}) &#8211; 4f(x\_{i-1}) + 3f(x_i)}{2h} $$ 
  * Segunda derivada: 
      * $$O(h) $$ : $$f&#8221;(x) = \frac{f(x\_{i-2}) &#8211; 2f(x\_{i-1}) + f(x_i)}{h^2} $$ 
      * $$O(h^2) $$ : $$f&#8221;(x) = \frac{-f(x\_{i-3}) + 4f(x\_{i-2}) &#8211; 5f(x\_{i-1}) + 2f(x\_i)}{h^2}$$ 
  * Terceira derivada: 
      * $$O(h) $$ : $$f&#8221;'(x) = \frac{-f(x\_{i-3}) + 3f(x\_{i-2}) &#8211; 3f(x\_{i-1}) + f(x\_i)}{h^3}$$ 
      * $$O(h^2) $$ : $$f&#8221;'(x) = \frac{3f(x\_{i-4}) &#8211; 14f(x\_{i-3}) + 24f(x\_{i-2}) &#8211; 18f(x\_{i-1}) + 5f(x_i)}{2h^3}$$ 
  * Quarta derivada: 
      * $$O(h)$$ : $$f&#8221;&#8221;(x) = \frac{f(x\_{i-4}) &#8211; 4f(x\_{i-3}) + 6f(x\_{i-2}) &#8211; 4f(x\_{i-1}) + f(x_i)}{h^4}$$ 
      * $$O(h^2)$$ : $$f&#8221;&#8221;(x) = \frac{-2f(x\_{i-5}) + 11f(x\_{i-4}) -24f(x\_{i-3}) + 26f(x\_{i-2}) &#8211; 14f(x\_{i-1}) + 3f(x\_i)}{h^4}$$ 

&nbsp;

### 3.3. Diferença Dividida Finita Centrada 

  * Primeira derivada: 
      * $$O(h^2)$$: $$f'(x) = \frac{f(x\_{i+1}) &#8211; f(x\_{i-1})}{2h} $$ 
      * $$O(h^4)$$: $$f'(x) = \frac{-f(x\_{i+2}) + 8f(x\_{i+1}) -8f(x\_{i-1}) + f(x\_{i-2})}{12h}$$ 
  * Segunda derivada: 
      * $$O(h^2)$$: $$f&#8221;(x) = \frac{f(x\_{i+1}) &#8211; 2f(x\_i) + f(x_{i-1})}{h^2} $$ 
      * $$O(h^4)$$: $$f&#8221;(x) = \frac{-f(x\_{i+2}) + 16f(x\_{i+1}) &#8211; 30f(x\_i) + 16f(x\_{i-1}) &#8211; f(x_{i-2})}{12h^2}$$ 
  * Terceira derivada: 
      * $$O(h^2)$$: $$f&#8221;'(x) = \frac{f(x\_{i+2}) &#8211; 2f(x\_{i+1}) + 2f(x\_{i-1}) &#8211; f(x\_{i-2})}{2h^3}$$ 
      * $$O(h^4)$$: $$f&#8221;'(x) = \frac{-f(x\_{i+3}) + 8f(x\_{i+2}) &#8211; 13f(x\_{i+1}) + 13f(x\_{i-1}) &#8211; 8f(x\_{i-2}) + f(x\_{i-3})}{8h^3}$$ 
  * Quarta derivada: 
      * $$O(h^2)$$: $$f&#8221;&#8221;(x) = \frac{f(x\_{i+2}) &#8211; 4f(x\_{i+1}) + 6f(x\_i) &#8211; 4f(x\_{i-1}) + f(x_{i-2})}{h^4}$$ 
      * $$O(h^4)$$: $$f&#8221;&#8221;(x) = \frac{-f(x\_{i+3}) + 12f(x\_{i+2}) + 39f(x\_{i+1}) + 56f(x\_i) &#8211; 39f(x\_{i-1}) + 12f(x\_{i-2}) + f(x_{i-3})}{6h^4}$$ 

&nbsp;

## 4. Implementação 

Conforme demonstrado, as diferenças finitas centradas produzem fórmulas mais acuradas. Sendo assim, o ideal é sempre implementarmos essas fórmulas. Portanto, seguem abaixo a implementação das funções _diff1_, _diff2_, _diff3_ e _diff4_, responsáveis por calcular a primeira, segunda, terceira e quarta derivada, respectivamente. No exemplo de utilização, que pode ser encontrado em <a href="http://www.sawp.com.br/code/derivatives/numerical_derivatives.py" target="_blank">http://www.sawp.com.br/code/derivatives/numerical_derivatives.py</a>, observamos um caso em que a escolha de $$h $$ repercurte num problema as vezes comum na utilização de métodos numéricos: o problema do truncamento de ponto flutuante. No caso, vemos que a derivada de quarta ordem produz um erro muito grande, à limitação da precisão computacional. Assim, nos post seguinte demonstramos como esse problema pode ser minimizado.

<pre lang="python">def diff1(f, x, h=0.0001):
    """
    Return the 1st derivative function evaluated in point x.

    diff_f_xi = diff1(fun, x, h=0.001)

    INPUT:
      * f: function to derivate
      * x: evaluation point
      * h: step size

    return: f'(X=x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jun 2012
    """
    a = -f(x + 2 * h)
    b = 8 * f(x + h)
    c = -8 * f(x - h)
    d = f(x - 2 * h)
    diff = (a + b + c + d) / (12 * h)
    return diff</pre>

<pre lang="python">def diff2(f, x, h=0.00001):
    """
    Return the 2nd derivative function evaluated in point x.

    diff_f_xi = diff2(fun, x, h=0.001)

    INPUT:
      * f: function to derivate
      * x: evaluation point
      * h: step size

    return: f"(X=x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jun 2012
    """
    a = -f(x + 2 * h)
    b = 16 * f(x + h)
    c = -30 * f(x)
    d = 16 * f(x - h)
    e = -f(x - 2 * h)
    diff = (a + b + c + d + e) / (12 * h ** 2)
    return diff</pre>

<pre lang="python">def diff3(f, x, h=0.00001):
    """
    Return the 3rd derivative function evaluated in point x.

    diff_f_xi = diff3(fun, x, h=0.001)

    INPUT:
      * f: function to derivate
      * x: evaluation point
      * h: step size

    return: f"'(X=x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jun 2012
    """
    a = -f(x + 3 * h)
    b = 8 * f(x + 2 * h)
    c = -13 * f(x + h)
    d = 13 * f(x - h)
    e = -8 * f(x - 2 * h)
    ff = f(x - 3 * h)
    diff = (a + b + c + d + e + ff) / (8 * h ** 3)
    return diff</pre>

<pre lang="python">def diff4(f, x, h=0.0001):
    """
    Return the 4th derivative function evaluated in point x.

    diff_f_xi = diff4(fun, x, h=0.001)

    INPUT:
      * f: function to derivate
      * x: evaluation point
      * h: step size

    return: f""(X=x)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jun 2012
    """
    a = f(x)
    b = -4 * f(x - h)
    c = 6 * f(x - 2 * h)
    d = -4 * f(x - 3 * h)
    e = f(x - 4 * h)
    diff = (a + b + c + d + e) / (h ** 4)
    return diff</pre>

&nbsp;

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.

  


<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a><br /> </fieldset>
