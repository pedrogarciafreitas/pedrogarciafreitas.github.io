---
id: 1582
title: '3.3.4 Aproximação de Funções &#8212; Regressões &#8212; Regressão Não-Linear'
date: 2012-06-09T12:00:16+00:00
author: SAWP
excerpt: Neste post apresentamos o método para regressão não-linear ea formulação geral do método de mínimos quadrados, o que nos permite ajustar pontos para funções lineares e não-lineares.
layout: post
guid: http://www.sawp.com.br/blog/?p=1582
permalink: p=1582
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:1727:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> func<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">,</span> a1<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> a0 * <span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span> - exp<span style="color: black;">&#40;</span>-a1 * x<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> diff_a0<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">,</span> a1<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #ff4500;">1.0</span> - exp<span style="color: black;">&#40;</span>-a1 * x<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> diff_a1<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">,</span> a1<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> a0 * x * exp<span style="color: black;">&#40;</span>-a1 * x<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def func(x, a0, a1):
    return a0 * (1 - exp(-a1 * x))
    
    def diff_a0(x, a0, a1):
    return 1.0 - exp(-a1 * x)
    
    def diff_a1(x, a0, a1):
    return a0 * x * exp(-a1 * x)</p></div>
    ;i:2;s:3126:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> get_Z<span style="color: black;">&#40;</span>xpoints<span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> a1<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: black;">&#41;</span>:
    lines <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>xpoints<span style="color: black;">&#41;</span>
    Z <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>lines<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>lines<span style="color: black;">&#41;</span>:
    Z<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> diff_a0<span style="color: black;">&#40;</span>xpoints<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">,</span> a1<span style="color: black;">&#41;</span>
    Z<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> diff_a1<span style="color: black;">&#40;</span>xpoints<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">,</span> a1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> Z</pre></td></tr></table><p class="theCode" style="display:none;">def get_Z(xpoints, a0=1.0, a1=1.0):
    lines = len(xpoints)
    Z = [[0 for i in xrange(2)] for j in xrange(lines)]
    for i in xrange(lines):
    Z[i][0] = diff_a0(xpoints[i], a0, a1)
    Z[i][1] = diff_a1(xpoints[i], a0, a1)
    return Z</p></div>
    ;i:3;s:1981:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> get_D<span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">,</span> a1<span style="color: black;">&#41;</span>:
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>y<span style="color: black;">&#41;</span>
    D <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">0.0</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    D<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> y<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> - func<span style="color: black;">&#40;</span>x<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> a0<span style="color: #66cc66;">,</span> a1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> D</pre></td></tr></table><p class="theCode" style="display:none;">def get_D(y, x, a0, a1):
    n = len(y)
    D = [0.0 for i in xrange(n)]
    for i in xrange(n):
    D[i] = y[i] - func(x[i], a0, a1)
    return D</p></div>
    ;i:4;s:2890:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> calcule_alphas<span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> alphas<span style="color: black;">&#41;</span>:
    Z <span style="color: #66cc66;">=</span> get_Z<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> alphas<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> alphas<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    Zt <span style="color: #66cc66;">=</span> transpose<span style="color: black;">&#40;</span>Z<span style="color: black;">&#41;</span>
    ZtZ <span style="color: #66cc66;">=</span> matmul<span style="color: black;">&#40;</span>Zt<span style="color: #66cc66;">,</span> Z<span style="color: black;">&#41;</span>
    D <span style="color: #66cc66;">=</span> get_D<span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> alphas<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> alphas<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    ZtD <span style="color: #66cc66;">=</span> matmul<span style="color: black;">&#40;</span>Zt<span style="color: #66cc66;">,</span> D<span style="color: black;">&#41;</span>
    A <span style="color: #66cc66;">=</span> cholesky<span style="color: black;">&#40;</span>ZtZ<span style="color: #66cc66;">,</span> ZtD<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#91;</span>i + j <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: black;">&#40;</span>i<span style="color: #66cc66;">,</span> j<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">zip</span><span style="color: black;">&#40;</span>alphas<span style="color: #66cc66;">,</span> A<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">def calcule_alphas(y, x, alphas):
    Z = get_Z(x, alphas[0], alphas[1])
    Zt = transpose(Z)
    ZtZ = matmul(Zt, Z)
    D = get_D(y, x, alphas[0], alphas[1])
    ZtD = matmul(Zt, D)
    A = cholesky(ZtZ, ZtD)
    return [i + j for (i, j) in zip(alphas, A)]</p></div>
    ;i:5;s:2179:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> iterative_general_least_squares<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> y<span style="color: black;">&#41;</span>:
    alphas <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1.0</span><span style="color: black;">&#93;</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    memalpha <span style="color: #66cc66;">=</span> alphas
    alphas <span style="color: #66cc66;">=</span> calcule_alphas<span style="color: black;">&#40;</span>y<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> alphas<span style="color: black;">&#41;</span>
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> calcule_error<span style="color: black;">&#40;</span>alphas<span style="color: #66cc66;">,</span> memalpha<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> alphas</pre></td></tr></table><p class="theCode" style="display:none;">def iterative_general_least_squares(x, y):
    alphas = [1.0, 1.0]
    iterCount = 0
    errno = 1
    while errno &gt; errto and iterCount &lt; imax:
    memalpha = alphas
    alphas = calcule_alphas(y, x, alphas)
    iterCount += 1
    errno = calcule_error(alphas, memalpha)
    return alphas</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução 

Nos posts anteriores, vimos como ajustar algumas funções simples pelo método de mínimos quadrados. Antes de apresentarmos o método para regressão não-linear, estudaremos a formulação geral do método de mínimos quadrados, o que nos permite ajustar pontos para funções lineares e não-lineares. 

[<img src="http://www.sawp.com.br/blog/wp-content/uploads/2012/06/fig1a.png" alt="" title="regressao" width="400" height="400" class="aligncenter size-full wp-image-1353" />](http://www.sawp.com.br/blog/wp-content/uploads/2012/06/fig1a.png) 

### 1.1. Mínimos Quadrados Linear Geral 

Todos os métodos de regressão apresentados nos posts anteriores &#8212; linear simples, linear múltiplo e polinomial &#8212; pertencem à um mesmo modelo geral de mínimos quadrados, descrito por

<center>
  \( y = a_0 z_0 + a_1 z_1 + \cdots + a_m z_m + \epsilon\) <a name="eq1"></a>
</center>

onde cada \(z_i \) é uma _função-base_. Como ilustração, temos o caso em que \(Z\_0=1 \) , \(z\_1=x\_1 \) , \(z\_2=x\_2 \) , \(\cdots \) , \(z\_m=x\_m \) é exatamente a função usada no método de regressão linear. Além disso, temos o caso em que cada função-base é um monômio, tal como \(z\_0=x^0=1 \) , \(z\_1=x \) , \(z\_2=x^2 \) , \(z\_3=x^3 \) , \(\cdots \) , \(z\_m=x^m \) , que constitui o caso de regressão polinomial. 

Matricialmente, a equação [1](#eq1) pode ser expressa como
    


<center>
  <br /> \( Y = ZA + E \) <a name="eq2"></a><br />
</center>


  
onde \(Z \) é a matriz dos valores calculados das funções-base nos valores medidos de cada variável independente. Isto é, cada variável corresponde à uma linha dessa matriz e cada coluna é uma amostragem. Assim,
  


<center>
  <br /> \(<br /> Z =<br /> \left[ \begin{array}{cccc}<br /> z_{01} & z_{11} & \cdots & z_{m1} \\<br /> z_{02} & z_{12} & \cdots & z_{m2} \\<br /> \vdots & \vdots & \ddots & \vdots \\<br /> z_{0n} & z_{1n} & \cdots & z_{mn}<br /> \end{array} \right]<br /> \)<br />
</center>


  
onde \(m \) é o número de variáveis do modelo e \(n \) é o número de pontos amostrados. O vetor \(Y \) contém os valores os valores observados das variáveis independentes
  


<center>
  <br /> \(<br /> Y =<br /> \left[ \begin{array}{c}<br /> y_{1} \\<br /> y_{2} \\<br /> \vdots \\<br /> y_{n}<br /> \end{array} \right]<br /> \)<br />
</center>


  
O vetor \(A \) contém os coeficientes que desejamos ajustar no modelo
  


<center>
  <br /> \(<br /> A =<br /> \left[ \begin{array}{c}<br /> a_{0} \\<br /> a_{1} \\<br /> \vdots \\<br /> a_{m}<br /> \end{array} \right]<br /> \)<br />
</center>


  
e \(E \) é o vetor de resíduos (erros)
  


<center>
  <br /> \(<br /> E =<br /> \left[ \begin{array}{c}<br /> \epsilon_{1} \\<br /> \epsilon_{2} \\<br /> \vdots \\<br /> \epsilon_{n}<br /> \end{array} \right]<br /> \)<br />
</center>

Assim, como demonstrado nos posts anteriores, o objetivo da regressão é minimizar o erro, que fazemos através da minimização da seguinte soma dos quadrados dos resíduos:
  


<center>
  <br /> \( S_r = \sum_{i=1}^{n} \left(y_i &#8211; \sum_{j=0}^{m} a_j z_{ji} \right)^2 \)<br />
</center>

Essa soma pode ser minimizada tomando-se suas derivadas parciais em relação a cada um dos coeficientes a serem ajustados e igualando-se a equação resultante a zero. Desta maneira, temos que os coeficientes são obtidos ao resolver o sistema
  


<center>
  <br /> \( Z^T Z A = Z^T Y \) <a name="eqnormal"></a>
</center>



## 2. Regressão Não-linear 

Como nos casos dos mínimos quadrados linear, a regressão não-linear baseia-se na obtenção dos coeficientes que minimizam os resíduos, com a diferença que o processo de minimização é feito iterativamente por meio do método de Gauss-Newton. Esse método consiste em expressar a função não-linear através de uma aproximação linear por expansão em série de Taylor. Assim, a teoria dos mínimos quadrados pode ser usada para obter-se novas estimativas dos parâmetros desconhecidos. 

Para ilustrar esse método, a relação entre a equação não-linear e os dados pode ser expressa como
   


<center>
  <br /> \( y_i = f(x_i; a_0, a_1, a_2, \ldots, a_m) + \epsilon_i \) <a name="eq3"></a><br />
</center>


  
onde \(y\_i \) é uma amostra da variável dependente; \(f(x\_i; a\_0, a\_1, a\_2, \ldots, a\_m) \) é a função independente da variável \(x\_i \) e dependente dos parâmetros \(a\_0, a\_1, a\_2, \ldots, a\_m \); e \(\epsilon\_i\) é um resíduo qualquer. Por conveniência, omitimos os parâmetros,
  


<center>
  <br /> \( y_i = f(x_i) + \epsilon_i \) <a name="eq4"></a>
</center>

Expandimos esse modelo por uma série de Taylor em torno dos parâmetros e truncamos após a primeira derivada. Isto é, para um modelo com \(m \) parâmetros, temos
  


<center>
  <br /> \(<br /> f(x_i)_{j+1} = f(x_i)_j +<br /> \frac{\partial f(x_i)_j}{\partial a_0} \Delta a_0 +<br /> \frac{\partial f(x_i)_j}{\partial a_1} \Delta a_1 +<br /> \cdots +<br /> \frac{\partial f(x_i)_j}{\partial a_m} \Delta a_m<br /> \) <a name="eq5"></a><br />
</center>


  
onde \(j \) é a aproximação inicial, \(j+1 \) é a previsão, \(\Delta a\_0 = a\_{0,j+1} &#8211; a\_{0, j} \) e \(\Delta a\_1 = a\_{1,j+1} &#8211; a\_{1, j}\). Com isso, linearizamos o
  
modelo inicial com relação aos parâmetros. Levando a Equação [4](#eq4) na Equação [5](#eq5), temos
  


<center>
  <br /> \(<br /> y_i &#8211; f(x_i)_j =<br /> \frac{\partial f(x_i)_j}{\partial a_0} \Delta a_0 +<br /> \frac{\partial f(x_i)_j}{\partial a_1} \Delta a_1 +<br /> \cdots +<br /> \frac{\partial f(x_i)_j}{\partial a_m} \Delta a_m +<br /> \epsilon_i<br /> \) <a name="eq6"></a><br />
</center>


  
ou, na forma matricial, temos um sistema igual da Equação [2](#eq2),
  


<center>
  <br /> \( D = Z A + E \) <a name="eq7"></a><br />
</center>


  
onde \(Z \) é a matriz das derivadas parciais da função calculada na aproximação inicial,
  


<center>
  <br /> \(<br /> Z =<br /> \left[ \begin{array}{cccc}<br /> \frac{\partial f_1}{\partial a_0} &<br /> \frac{\partial f_1}{\partial a_1} &<br /> \cdots &<br /> \frac{\partial f_1}{\partial a_m} \\<br /> \frac{\partial f_2}{\partial a_0} &<br /> \frac{\partial f_2}{\partial a_1} &<br /> \cdots &<br /> \frac{\partial f_2}{\partial a_m} \\<br /> \vdots & \vdots & \ddots & \vdots \\<br /> \frac{\partial f_n}{\partial a_0} &<br /> \frac{\partial f_n}{\partial a_1} &<br /> \cdots &<br /> \frac{\partial f_n}{\partial a_m} \\<br /> \end{array} \right]<br /> \)<br />
</center>


  
onde \(n \) é o número de amostrars e \(\frac{\partial f\_i}{\partial a\_k} \) é a derivada parcial da função com relação ao k-ésimo parâmetro calculada no i-ésimo ponto dado. O vetor \(D \) contém as diferenças entre as medidas e os valores da função ajustada,
  


<center>
  <br /> \(<br /> D =<br /> \left[ \begin{array}{c}<br /> y_1 &#8211; f(x_1) \\<br /> y_2 &#8211; f(x_2) \\<br /> \vdots \\<br /> y_n &#8211; f(x_n)<br /> \end{array} \right]<br /> \)<br />
</center>


  
e o vetor \(\Delta A \) contém a variação nos valores dos parâmetros que estão sendo ajustados,
  


<center>
  <br /> \(<br /> A =<br /> \left[ \begin{array}{c}<br /> \Delta a_0 \\<br /> \Delta a_1 \\<br /> \vdots \\<br /> \Delta a_n \\<br /> \end{array} \right]<br /> \)<br />
</center>

Assim, a Equação [7](#eq7) pode ser reescrita como a seguinte equação normal (conforme apresentado na Equação [normal](#eqnormal):
  


<center>
  <br /> \( Z^T Z A = Z^T D \) <a name="eqsys"></a><br />
</center>


  
A resolução deste sistema ajusta o conjunto de coeficientes da função não-linear. 

Devemos notar que o vetor dos coeficientes ( \(A \) ) resolve uma variação dos coeficientes e não os valores dos coeficientes em si. Isso descreve um processo iterativo, ou seja, esse conjunto de equações pode ser resolvidas sucessivas vezes, substituindo os valores de \(A\) pelos novos valores melhorados como em
  


<center>
  </p> 
  
  <table border="0" cellpadding="1">
    <tr>
      <td>
        \( a_{0,j+1} = a_{0,j} + \Delta a_0 \)
      </td>
    </tr>
    
    <tr>
      <td>
        \( a_{0,j+1} = a_{1,j} + \Delta a_1 \)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        \( \vdots \)
      </td>
    </tr>
    
    <tr>
      <td>
        \( a_{m,j+1} = a_{m,j} + \Delta a_m \)
      </td>
    </tr>
  </table>
  
  <p>
    </center><br /> Este processo iterativo é repetido até que a solução convirja à um valor de erro tolerado, que pode ser calculado utilizando a seguinte equação<br /> 
    
    <center>
      <br /> \( \left|\epsilon_a\right|_k = \left|\frac{a_{k,j+1} &#8211; a_{k,j}}{a_{k,j+1}}\right| \)<br />
    </center>
  </p>
  
  <p>
  </p>
  
  <p>
    <h2>
      3. Implementação
    </h2>
  </p>
  
  <p>
    Para ilustrarmos a utilização da regressão linear, implementaremos a seguinte função<br /> 
    
    <center>
      <br /> \( f(x) = \alpha_0(1 &#8211; e^{-\alpha_1 x}) \)<br />
    </center>
    
    <br /> ilustrando cada passo e o respectivo código, seguindo a ordem do algoritmo descrito na seção anterior. O primeiro passo é definir uma aproximação inicial para \(\alpha_0 \) e \(\alpha_1 \) e selecionar um erro de tolerância \(\epsilon \) . Como a função possui dos coeficientes a serem ajustados, o vetor dos coeficientes terá apenas dois elementos, ou seja \(A = [\alpha_0, \alpha_1]^T \) . Além disso, escolhemos \(\epsilon=0.1 \) .
  </p>
  
  <p>
    O próximo passo é obter as derivadas parciais da função com relação aos parâmetros \(\alpha_0 \) e \(\alpha_1 \) . Isto é,<br /> 
    
    <center>
      <br /> \( \frac{\partial f}{\partial \alpha_0} = 1 &#8211; e^{-\alpha_1 x} \) e \( \frac{\partial f}{\partial \alpha_1} = \alpha_0 x e^{-\alpha_1 x} \)<br />
    </center>
    
    <br /> Na implementação temos que as funções necessárias \(f \) , \(\frac{\partial f}{\partial \alpha_0}\) e \(\frac{\partial f}{\partial \alpha_1}\) são, respectivamente,
  </p>
  
  <div>
    <pre lang="python">def func(x, a0, a1):
    return a0 * (1 - exp(-a1 * x))

def diff_a0(x, a0, a1):
    return 1.0 - exp(-a1 * x)

def diff_a1(x, a0, a1):
    return a0 * x * exp(-a1 * x)</pre>
    
    <p>
      </div>
    </p>
    
    <p>
      As equações acima são usadas para calcular a matriz \(Z \) , conforme mostrado na seção anterior<br /> 
      
      <center>
        <br /> \(<br /> Z =<br /> \left[ \begin{array}{cc}<br /> \frac{\partial f_1}{\partial a_0} &<br /> \frac{\partial f_1}{\partial a_1} \\<br /> \frac{\partial f_2}{\partial a_0} &<br /> \frac{\partial f_2}{\partial a_1} \\<br /> \vdots & \vdots \\<br /> \frac{\partial f_n}{\partial a_0} &<br /> \frac{\partial f_n}{\partial a_1} \\<br /> \end{array} \right]<br /> \)<br />
      </center>
      
      <br /> Essa matriz é construída com a seguinte implementação
    </p>
    
    <div>
      <pre lang="python">def get_Z(xpoints, a0=1.0, a1=1.0):
    lines = len(xpoints)
    Z = [[0 for i in xrange(2)] for j in xrange(lines)]
    for i in xrange(lines):
        Z[i][0] = diff_a0(xpoints[i], a0, a1)
        Z[i][1] = diff_a1(xpoints[i], a0, a1)
    return Z</pre>
      
      <p>
        </div>
      </p>
      
      <p>
        O passo seguinte consiste em obter o vetor \(D \) que, conforme demonstrado, será a diferença entre a função ajustada e o valor amostrado
      </p>
      
      <div>
        <pre lang="python">def get_D(y, x, a0, a1):
    n = len(y)
    D = [0.0 for i in xrange(n)]
    for i in xrange(n):
        D[i] = y[i] - func(x[i], a0, a1)
    return D</pre>
        
        <p>
          </div>
        </p>
        
        <p>
          Agora, de posse de \(Z \) e \(D \) , podemos obter o vetor \(A \) resolvendo o sistema da Equação <a href="#eqsys">sys</a>. Os passos para resolução desse sistema são listados nos comandos abaixo
        </p>
        
        <div>
          <pre lang="python">def calcule_alphas(y, x, alphas):
    Z = get_Z(x, alphas[0], alphas[1])
    Zt = transpose(Z)
    ZtZ = matmul(Zt, Z)
    D = get_D(y, x, alphas[0], alphas[1])
    ZtD = matmul(Zt, D)
    A = cholesky(ZtZ, ZtD)
    return [i + j for (i, j) in zip(alphas, A)]</pre>
          
          <p>
            </div>
          </p>
          
          <p>
            Logo, os coeficientes já estão mais ajustados em relação à aproximação inicial. Contudo, esse procedimento pode ser repetido para melhorar ainda mais os parâmetros \(\alpha \) . Logo, definimos uma nova função que ajusta tais parâmetros através de sucessivas substituições de \(\alpha \):
          </p>
          
          <div>
            <pre lang="python">def iterative_general_least_squares(x, y):
    alphas = [1.0, 1.0]
    iterCount = 0
    errno = 1
    while errno > errto and iterCount &lt; imax:
        memalpha = alphas
        alphas = calcule_alphas(y, x, alphas)
        iterCount += 1
        errno = calcule_error(alphas, memalpha)
    return alphas</pre>
            
            <p>
              </div> 
              
              <p>
                Onde a variável <i>memalpha</i> armazena o \(\alpha \) da iteração anterior para o calculo do erro; <i>itercount</i> é um contador usado para limitar o número máximo de repetições, caso haja uma convergência muito lenta do algoritmo.
              </p>
              
              <p>
                Um exemplo completo que utiliza essas funções pode ser encontrado em <a href="http://www.sawp.com.br/code/regression/nonlinear_regression.py" target="_blank">http://www.sawp.com.br/code/regression/nonlinear_regression.py</a>.
              </p>
              
              <p>
              </p>
              
              <h2>
                4. Copyright
              </h2>
              
              <p>
                Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.
              </p>
              
              <p>
              </p>
              
              <fieldset>
                <legend> 
                
                <h2>
                  References
                </h2></legend> 
                
                <p>
                  <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a><br /></fieldset>
