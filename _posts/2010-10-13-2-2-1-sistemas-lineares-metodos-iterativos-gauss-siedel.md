---
id: 762
title: '2.2.1 Sistemas Lineares &#8212; Métodos Iterativos &#8212; Gauss-Siedel'
date: 2010-10-13T17:34:59+00:00
author: SAWP
excerpt: '    Neste artigo discutiremos o Método de Gauss-Siedel, que é um algoritmo    iterativo para aproximação de soluções de sistemas lineares. Em problemas que empregam métodos computacionais, o método de Gauss-Siedel é muito útil, uma vez que gera soluções satisfatórias para sistemas de equações muito grandes. Todavia, como é comum de ocorrer em métodos iterativos, esta técnica é sujeita a erros de arrendondamento. Por isso, há certos casos em que o método não convergirá à uma solução. Portanto, apresentaremos neste trabalho uma digressão sobre as vantagens e os contras da utilização de métodos iterativos e do algoritmo de Gauss-Siedel.'
layout: post
guid: http://www.sawp.com.br/blog/?p=762
permalink: /p=762
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:10059:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> gauss_siedel<span style="color: black;">&#40;</span>A<span style="color: #66cc66;">,</span> b<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10E-10</span><span style="color: #66cc66;">,</span> maxiter<span style="color: #66cc66;">=</span><span style="color: #ff4500;">10E5</span><span style="color: #66cc66;">,</span> SOR<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.77</span><span style="color: #66cc66;">,</span> getiters<span style="color: #66cc66;">=</span><span style="color: #008000;">False</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the solution of linear system.
    &nbsp;
    gauss_siedel(A, b)
    &nbsp;
    INPUT:
    * A: coefficients matrix
    * b: a list, relative a vector of independent terms
    &nbsp;
    return:
    if getiters=False:
    a list with unknown vector 'x' of system A*x = b.
    else:
    the tuple (list x, integer iters)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Sep 2010
    &quot;&quot;&quot;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    iters <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    sentry <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span>
    x <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span> / <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    diagonal <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> /<span style="color: #66cc66;">=</span> diagonal
    b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> /<span style="color: #66cc66;">=</span> diagonal
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    summ <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">!=</span> j:
    summ -<span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> summ
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #ff7700;font-weight:bold;">not</span> sentry <span style="color: #ff7700;font-weight:bold;">and</span> iters <span style="color: #66cc66;">&lt;</span> <span style="color: #66cc66;">=</span> maxiter:
    sentry <span style="color: #66cc66;">=</span> <span style="color: #008000;">True</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    xold <span style="color: #66cc66;">=</span> x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    summ <span style="color: #66cc66;">=</span> b<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #66cc66;">!=</span> j:
    summ -<span style="color: #66cc66;">=</span> A<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * x<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> SOR * summ + <span style="color: black;">&#40;</span><span style="color: #ff4500;">1.0</span> - SOR<span style="color: black;">&#41;</span> * xold
    <span style="color: #ff7700;font-weight:bold;">if</span> sentry <span style="color: #ff7700;font-weight:bold;">and</span> x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - xold<span style="color: black;">&#41;</span> / x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto:
    sentry <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span>
    iters +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> getiters:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> iters<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> x</pre></td></tr></table><p class="theCode" style="display:none;">def gauss_siedel(A, b, errto=10E-10, maxiter=10E5, SOR=1.77, getiters=False):
    &quot;&quot;&quot;
    Return a list with the solution of linear system.
    
    gauss_siedel(A, b)
    
    INPUT:
    * A: coefficients matrix
    * b: a list, relative a vector of independent terms
    
    return:
    if getiters=False:
    a list with unknown vector 'x' of system A*x = b.
    else:
    the tuple (list x, integer iters)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Sep 2010
    &quot;&quot;&quot;
    n = len(A)
    errno = 0.0
    iters = 0
    sentry = False
    x = [1.0 / float(n) for i in xrange(n)]
    
    for i in xrange(n):
    diagonal = float(A[i][i])
    for j in xrange(n):
    A[i][j] /= diagonal
    b[i] /= diagonal
    for i in xrange(n):
    summ = b[i]
    for j in xrange(n):
    if i != j:
    summ -= A[i][j] * x[i]
    x[i] = summ
    while not sentry and iters &lt; = maxiter:
    sentry = True
    for i in xrange(n):
    xold = x[i]
    summ = b[i]
    for j in xrange(n):
    if i != j:
    summ -= A[i][j] * x[j]
    x[i] = SOR * summ + (1.0 - SOR) * xold
    if sentry and x[i] != 0:
    errno = abs((x[i] - xold) / x[i])
    if errno &gt; errto:
    sentry = False
    iters += 1
    if getiters:
    return (x, iters)
    else:
    return x</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. O método de Gauss-Siedel 

A resolução de sistemas lineares através de métodos iterativos foram desenvolvidos como uma forma específica de busca de raízes a partir de derivações dos métodos que buscam raízes em funções não-lineares. Como em todos métodos numéricos iterativos, a abordagem para solução consiste em escolher um valor inicial (estimado) para convergir à uma solução a partir deste. Como sistemas lineares utilizam um conjunto de equações tais que as raízes devam satisfazê-las simultaneamente, os métodos iterativos são úteis neste contexto. 

Como trata-se de um sistema linear de equações, o método de Gauss-Siedel resolve problemas na forma
      


<center>
  $$ Ax = b $$
</center>

Primeiramente, suponhamos um sistema de três equações, gerando uma matriz de coeficientes $$3 \times 3 $$ . Se a diagonal é formada apenas por elementos não-nulos, podemos isolar $$x\_1 $$ na primeira equação, $$x\_2 $$ na segunda e $$x_3 $$ na terceira. Assim, obteremos
      


<center>
  $$ x_1 = \dfrac{b_1 &#8211; a_{12}x_2 &#8211; a_{13}x_3}{a_{11},<br /> x_2 = \dfrac{b_2 &#8211; a_{21}x_1 &#8211; a_{23}x_3}{a_{22},<br /> x_3 = \dfrac{b_3 &#8211; a_{31}x_1 &#8211; a_{32}x_2}{a_{33} $$
</center>

Pelas equações acima notamos que para estimar $$x\_1 $$ , inicialmente precisamos de $$x\_2 $$ e $$x_3 $$ . A ideia do método consiste em escolher um valor inicial para estas variáveis e, em seguida, fazer sucessivas substituições até que os valores de $$x $$ estejam se aproximando de uma solução. Por esta razão, o método de Gauss-Siedel é conhecido como _método das substituições sucessivas_. 

Para generalizar a ideia do parágrafo anterior, denotaremos o método através de duas variáveis $$j $$ e $$i $$ , onde $$j $$ é a componente do vetor de incógnitas e $$i $$ é a iteração. Desta maneira, uma variável qualquer é expressa como $$x_{i}^{j} $$ . Considerando o sistema de $$n $$ equações e $$n $$ incógnitas, começamos por calcular a primeira variável
      


<center>
  $$ x_{i+1}^{(1)} = &#8211; \dfrac{1}{a_{11}<br /> \left( \sum_{j=2}^{n} a_{1j}x_{i}^{(j)} -b_1 \right) $$
</center>


      
Para próxima componente $$j=2 $$ , utilizamos a segunda equação, já substituindo $$x_{i+1}^{(j)} $$ pelo valor calculado anteriormente
      


<center>
  $$ x_{i+1}^{(2)} = &#8211; \dfrac{1}{a_{22}<br /> \left( a_{21}x_{i+1}^{(1)} +<br /> \sum_{j=3}^{n} a_{2j}x_{i}^{(j)} &#8211; b_2 \right) $$
</center>


      
a partir destas duas últimas equações, podemos facilmente observar a relação de recorrência, a qual expressamos como a fórmula geral do método de Gauss-Siedel:
      


<center>
  $$ x_{i+1}^{(r)} = &#8211; \dfrac{1}{a_{rr}<br /> \left( \sum_{j=1}^{r-1} a_{rj}x_{i+1}^{(j)} +<br /> \sum_{j=r+1}^{n} a_{rj}x_{i}^{(j)} &#8211; b_r \right) $$
</center>


      
onde $$r = 1, 2, \ldots, n $$ . 

&nbsp;

## 2. Convergência do Método de Gauss-Siedel 

Assim como todo método de busca de raízes iterativo, o algoritmo de Gauss-Siedel é uma técnica baseada no método do ponto fixo, fazendo com que o método de Gauss-Siedel seja suscetível à duas limitações fundamentais: 

  1. casos onde não há convergência 
  2. casos onde a convergência é muito lenta 

Para ambas situações, observamos que os valores do sistema que condicionam os casos problemáticos. Para verificar quais casos são estes, deduzimos os critérios de convergência a partir de duas equações não-lineares $$u(x\_1, x\_2) $$ e $$v(x\_1, x\_2) $$ tal que
    


<center>
  $$<br /> \left| \dfrac{\partial u}{\partial x_1} \right| +<br /> \left| \dfrac{\partial u}{\partial x_2} \right| < 1 [/latex]
</center>


    
e
    
</center>

<center>
  [latex]<br /> \left| \dfrac{\partial v}{\partial x_1} \right| +<br /> \left| \dfrac{\partial v}{\partial x_2} \right| < 1 [/latex]
</center>


    
Supondo [latex]u $$ e $$v $$ como sendo duas funções lineares pertencente à um sistema com apenas duas variáveis, temos que tais funções são expressas como
    
</center>

<center>
  $$<br /> u(x_1, x_2) = \frac{b_1}{a_{11} &#8211; \frac{a_{12}{a_{11} x_2<br /> $$
</center>


    
e
    


<center>
  $$<br /> v(x_1, x_2) = \frac{b_2}{a_{22} &#8211; \frac{a_{21}{a_{22} x_1<br /> $$
</center>


    
Para sistemas lineares, as derivadas parciais eliminam todas as componentes que não contém a variável a qual estamos diferenciando, ou seja
    


<center>
  <br /> $$<br /> \frac{\partial u}{\partial x_1} = 0 \text{~,~}<br /> \frac{\partial u}{\partial x_2} = &#8211; \frac{a_{12}{a_{11}<br /> $$
</center>


    
e
    


<center>
  <br /> $$<br /> \frac{\partial v}{\partial x_1} = &#8211; \frac{a_{21}{a_{22}<br /> \text{~,~} \frac{\partial v}{\partial x_2} = 0<br /> $$
</center>


    
Utilizando os critérios das funções $$u $$ e $$v $$ , podemos reescrever as condições como
    


<center>
  <br /> $$<br /> \left| \frac{a_{12}{a_{11} \right| < 1 \text{~e~} \left| \frac{a_{21}{a_{22} \right| < 1 [/latex]
</center>


    
Isso significa que para haver convergência, o sistema precisa ter os maiores coeficientes concentrados na diagonal. Ou seja,
    
</center>

<center>
  <br /> [latex]<br /> |a_{ii}| = \sum_{j=1 and j \ne i}^{n} |a_{ij}|<br /> $$
</center>

&nbsp;

## 3. Aceleração de Processos Iterativos Estacionários 

A taxa de convergência de um processo iterativo estacionário depende do raio espectral do vetor de elementos independentes. Assim, qualquer qualquer modificação no vetor $$b $$ implica em uma modificação na taxa de convergência. Isto é, a redução do raio espectral de $$b $$ irá aumentar a taxa de convergência. Considerando que queremos acelerar a convergência às raízes no processo iterativo, adotaremos um método conhecido como _relaxação sucessiva_. 

Primeiramente, rearranjamos o sistema linear para uma forma onde todos elementos da diagonal são unitários, ou seja, $$a_{rr}=1 $$ . Isso pode ser feito dividindo-se toda a linha pelo elemento da diagonal pertencente à ela. 

Pelo método de Gauss-Siedel, sabemos que
    


<center>
  $$ x_{i+1}^{(r)} = &#8211; \sum_{j=1}^{r-1} a_{rj} x_{i+1}^{(j)} &#8211;<br /> \sum_{j=r+1}^{n} a_{rj} x_{i}^{(j)} + b_r<br /> = x_{i}^{(r)}<br /> &#8211; \sum_{j=1}^{r-1} a_{rj} x_{i+1}^{(j)} &#8211;<br /> \sum_{j=r+1}^{n} a_{rj} x_{i}^{(j)} + b_r $$
</center>


    
para $$a_{rr} = 1 $$ . Assim, podemos melhorar a formula acima reescrevendo-a como
    
<a name="eqrelaxada">(eqrelaxada)</a> 

<center>
  $$<br /> x_{i+1}^{(r)} = x_{i}^{(r)} &#8211; \omega \left(<br /> \sum_{j=1}^{r-1} a_{rj} x_{i+1}^{(j)} &#8211;<br /> \sum_{j=r+1}^{n} a_{rj} x_{i}^{(j)} + b_r \right)<br /> $$
</center>


    
onde $$\omega $$ é o _fator de relaxação_ do processo iterativo. 

Para facilitar a visualização deste processo, imagine que a matriz de coeficientes é decomposta e escrita na forma
    


<center>
  $$ A = D + L + U $$
</center>


    
onde $$D $$ é uma matriz diagonal, $$L $$ é triangular inferior e $$U $$ é triangular superior. Assim, podemos escrever o método de Gauss-Siedel como
    


<center>
  $$ x_{i+1} = B_{\omega} x_i + C_{\omega} b $$
</center>


    
onde $$B\_{\omega} = \dfrac{(1 &#8211; \omega)I &#8211; \omega U}{I + \omega L} $$ e $$c\_{\omega} = \dfrac{\omega}{I + \omega L} $$ . 

Tal processo pode ser interpretado como uma seleção baseada em uma média ponderada dos resultados da iteração anterior e da iteração corrente:
    


<center>
  $$<br /> x_{i+1}^{(j)} = \omega x_{i+1}^{(j)} + (1 &#8211; \omega) x_{i}^{(j)}<br /> $$
</center>


    
onde $$\omega $$ deve ser escolhido como um valor entre $$0 $$ e $$2 $$ . 

&nbsp;

### 3.1. Interpretações para $$\omega $$ </p> 

Para $$\omega = 1 $$ , temos que $$\omega &#8211; 1 = 0 $$ e o resultado não é modificado. Contudo, se $$\omega $$ estiver no intervalo entre $$0 $$ e $$1 $$ , o resultado é uma média ponderada do resultado atual e do anterior. Neste último caso, temos uma _sub-relaxação_, que é usada para forçar o sistema a convergir, mesmo que ele seja não-convergente. 

Para $$\omega $$ no intervalo entre $$1 $$ e $$2 $$ , supomos que o condicionamento do sistema é certamente convergente, mas converge muito lentamente. Neste caso, $$\omega $$ atua como um fator de peso que favorece a convergência entre duas iterações. Assim, dizemos que esta abordagem é uma _super-relaxação_, também conhecida como _sucessive overrelaxation_ &#8212; **SOR**. 

&nbsp;

### 3.2. Análise de SOR </p> 

A escolha de $$\omega $$ requer um certo cuidado, uma vez que este valor é fortemente ligado aos dados do sistema, sendo dependente do problema e determinado de maneira empírica. Para exemplificar a utilização de um fator de relaxação, a seguir apresentamos o comportamento do método de Gauss-Siedel para um sistema em relação à diferentes valores de $$\omega $$ . 

O primeiro procedimento para análise consiste em resolver um sistema linear na forma $$Ax = b $$ diversas vezes, variando apenas a variável de relaxação no intervalo $$[0,2] $$ com um passo de $$0.05 $$ e verificando o comportamento das iterações necessárias para resolução do problema. Tal procedimento nos permite gerar o gráfico da Figura [sor1](#figsor1). 

<center>
  <br /> 
  
  <div id="attachment_769" style="width: 710px" class="wp-caption aligncenter">
    <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/10/general.png"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2010/10/general.png" alt="" title="sorxiteracoes" width="700" height="400" class="size-full wp-image-769" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/10/general.png 700w, http://www.sawp.com.br/blog/wp-content/uploads/2010/10/general-300x171.png 300w" sizes="(max-width: 700px) 100vw, 700px" /></a>
    
    <p class="wp-caption-text">
      Mostra o número de iterações necessárias para resolver o mesmo sistema linear sem variação na precisão do resultado
    </p>
  </div>
  
  <br />
</center>

Como podemos observar da Figura [sor1](#figsor1), o ponto ótimo para resolução desse sistema consiste em utilizar um valor para o fator de relaxação próximo ao ponto $$1.8 $$ . Sendo assim, repetimos o experimento para o subintervalo $$[1.7,1.9] $$ e observamos o comportamento ilustrado na
     
Figura [sor2](#figsor2). 

<center>
  <br /> 
  
  <div id="attachment_771" style="width: 800px" class="wp-caption aligncenter">
    <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/10/subinterval1719.png"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2010/10/subinterval1719.png" alt="" title="Iteracoesxsor" width="790" height="446" class="size-full wp-image-771" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/10/subinterval1719.png 790w, http://www.sawp.com.br/blog/wp-content/uploads/2010/10/subinterval1719-300x169.png 300w" sizes="(max-width: 790px) 100vw, 790px" /></a>
    
    <p class="wp-caption-text">
      Mostra o número de iterações necessárias para resolver o mesmo sistema linear sem variação na precisão do resultado no intervalo próximo ao mínimo global
    </p>
  </div>
  
  <br />
</center>

Desta última figura podemos concluir que o valor que minimiza o tempo de resolução do sistema linear consiste em um $$\omega = 1.772 $$ , sendo notável a diferença no desempenho proporcionada por por este valor: menos de $$3500 $$ iterações ante as $$1000000 $$ iterações do pior caso, significando uma melhoria de quase $$286\% $$ . 

A Figura [sor2](#figsor2) também nos fornece informações para avaliação da necessidade de escolha empírica do valor do parâmetro de relaxação. Se notarmos o comportamento do gráfico após o valor ótimo, notamos que o crescimento é contínuo, mas com uma pequena oscilação. Este tipo de comportamento gera diversos pontos de mínimo, o que torna o problema de encontrar o valor ótimo um problema difícil de se automatizar com eficiência. Geralmente, problemas como estes são resolvidos com heurísticas &#8212; tais como algoritmos genéticos &#8212; e costumam ser muito mais caros de se resolver do que problemas de resolução de sistemas lineares, o que torna injustificável a utilização da busca pelo valor ótimo do fator de relaxação. 

Portanto, para definir um $$\omega $$ adequado para algum problema, é preferível que façamos alguns testes com instâncias menores do problema geral para conseguirmos obter um valor próximo ao ideal. 

&nbsp;

## 4. Implementação 

<div>
  <pre lang="python">
def gauss_siedel(A, b, errto=10E-10, maxiter=10E5, SOR=1.77, getiters=False):
    """
    Return a list with the solution of linear system.

    gauss_siedel(A, b)

    INPUT:
    * A: coefficients matrix
    * b: a list, relative a vector of independent terms

    return: 
            if getiters=False:
                a list with unknown vector 'x' of system A*x = b.
            else:
                the tuple (list x, integer iters)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Sep 2010
    """
    n = len(A)
    errno = 0.0
    iters = 0
    sentry = False
    x = [1.0 / float(n) for i in xrange(n)]

    for i in xrange(n):
        diagonal = float(A[i][i])
        for j in xrange(n):
            A[i][j] /= diagonal
        b[i] /= diagonal
    for i in xrange(n):
        summ = b[i]
        for j in xrange(n):
            if i != j:
                summ -= A[i][j] * x[i]
        x[i] = summ
    while not sentry and iters &lt; = maxiter:
        sentry = True
        for i in xrange(n):
            xold = x[i]
            summ = b[i]
            for j in xrange(n):
                if i != j:
                    summ -= A[i][j] * x[j]
            x[i] = SOR * summ + (1.0 - SOR) * xold
            if sentry and x[i] != 0:
                errno = abs((x[i] - xold) / x[i])
                if errno > errto:
                    sentry = False
        iters += 1
    if getiters:
        return (x, iters)
    else:
        return x</pre>
</div>

Nesta implementação fazemos duas considerações importantes para a melhoria do desempenho: 

  * a primeira consiste em dividir cada linha da matriz de coeficientes e dos termos independentes pelo elemento respectivo da diagonal. Conforme discutimos na seção de análise de convergência, isto reduz o número total de operações no algoritmo. 
  * a segunda consideração está na definição da variável de controle **sentry**. Esta variável verifica o erro da aproximação e controla a execução da função. Somente se alguma das equações possuir um erro de aproximação maior do que o erro tolerado é que a variável de controle permite a execução. O uso da variável **sentry** nos permite economizar alguns laços de repetição e evitar cálculos desnecessários. </p> 

Esta função está disponível em <a href="http://www.sawp.com.br/code/linear/gausssiedel.py" target="_blank">http://www.sawp.com.br/code/linear/gausssiedel.py</a>, assim como um exemplo de como utilizá-la. 

&nbsp;

## 5. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.



&nbsp;

<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001), 423-424.</a>
  </p>
  
  <p>
    <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 69.</a>
  </p>
</fieldset>
