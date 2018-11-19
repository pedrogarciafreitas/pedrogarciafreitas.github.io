---
id: 1186
title: '3.2.5 Aproximação de Funções &#8212; Análise de Fourier &#8212; A Transformada Discreta Rápida de Fourier'
date: 2011-06-06T20:01:54+00:00
author: SAWP
excerpt: '    Embora o algoritmo implementado no post anterior calcule adequadamente a transformada discreta de Fourier (TDF), ele é computacionalmente custoso, uma vez que possui ordem de complexidade quadrática. Por isso, para uma amostra de dados considerável, pode ser inviável a utilização daquela função. Neste post veremos a transformada de rápida de Fourier, algoritmo eficiente que é muito utilizado em diversas áreas que utilizam recursos eletrônicos e computacionais, tais como processamento de sinais.'
layout: post
guid: http://www.sawp.com.br/blog/?p=1186
permalink: /p=1186
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:8148:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> fft_sandetukey<span style="color: black;">&#40;</span>inputf<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the coeficients of Fast Fourier Transform
    (Sande-Tukey -- Decimation in Frequency algorithm).
    &nbsp;
    F = fft_sandetukey(inputf)
    &nbsp;
    INPUT:
    * f: list with discrete points of time-domain
    &nbsp;
    return: list discrete points of frequency-domain
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2011
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> fft_st<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> n <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">1</span>:
    d <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    e <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    nh <span style="color: #66cc66;">=</span> n / <span style="color: #ff4500;">2</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>nh<span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> -<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    s <span style="color: #66cc66;">=</span> x<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    t <span style="color: #66cc66;">=</span> x<span style="color: black;">&#91;</span>k + nh<span style="color: black;">&#93;</span>
    e<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> s + t
    d<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> s - t
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>nh<span style="color: black;">&#41;</span>:
    theta <span style="color: #66cc66;">=</span> k * omega * n
    real <span style="color: #66cc66;">=</span> cos<span style="color: black;">&#40;</span>theta<span style="color: black;">&#41;</span>
    imag <span style="color: #66cc66;">=</span> sin<span style="color: black;">&#40;</span>theta<span style="color: black;">&#41;</span>
    d<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> d<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> * <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>real<span style="color: #66cc66;">,</span> imag<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;"># divide and conquer</span>
    bige <span style="color: #66cc66;">=</span> fft_st<span style="color: black;">&#40;</span>e<span style="color: #66cc66;">,</span> nh<span style="color: black;">&#41;</span>
    bigd <span style="color: #66cc66;">=</span> fft_st<span style="color: black;">&#40;</span>d<span style="color: #66cc66;">,</span> nh<span style="color: black;">&#41;</span>
    j <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>nh<span style="color: black;">&#41;</span>:
    x<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> bige<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    x<span style="color: black;">&#91;</span>j + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> bigd<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span>
    j <span style="color: #66cc66;">=</span> j + <span style="color: #ff4500;">2</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    &nbsp;
    f <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span><span style="color: #008000;">complex</span><span style="color: #66cc66;">,</span> inputf<span style="color: black;">&#41;</span>
    m <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>f<span style="color: black;">&#41;</span>
    omega <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">2.0</span> * pi / m
    <span style="color: #ff7700;font-weight:bold;">return</span> fft_st<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> m - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def fft_sandetukey(inputf):
    &quot;&quot;&quot;
    Return a list with the coeficients of Fast Fourier Transform
    (Sande-Tukey -- Decimation in Frequency algorithm).
    
    F = fft_sandetukey(inputf)
    
    INPUT:
    * f: list with discrete points of time-domain
    
    return: list discrete points of frequency-domain
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2011
    &quot;&quot;&quot;
    
    def fft_st(x, n):
    if n != 1:
    d = [complex(0.0) for i in xrange(n)]
    e = [complex(0.0) for i in xrange(n)]
    nh = n / 2
    for k in xrange(nh, -1, -1):
    s = x[k]
    t = x[k + nh]
    e[k] = s + t
    d[k] = s - t
    for k in xrange(nh):
    theta = k * omega * n
    real = cos(theta)
    imag = sin(theta)
    d[k] = d[k] * complex(real, imag)
    # divide and conquer
    bige = fft_st(e, nh)
    bigd = fft_st(d, nh)
    j = 0
    for k in xrange(nh):
    x[j] = bige[k]
    x[j + 1] = bigd[k]
    j = j + 2
    return x
    
    f = map(complex, inputf)
    m = len(f)
    omega = -2.0 * pi / m
    return fft_st(f, m - 1)</p></div>
    ;i:2;s:7555:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> fft_cooleytukey<span style="color: black;">&#40;</span>inputf<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the coeficients of Fast Fourier Transform
    (Sande-Tukey -- Decimation in Time algorithm).
    &nbsp;
    F = fft_cooleytukey(inputf)
    &nbsp;
    INPUT:
    * f: list with discrete points of time-domain
    &nbsp;
    return: list discrete points of frequency-domain
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2011
    &quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> is_power_of_two<span style="color: black;">&#40;</span>number<span style="color: black;">&#41;</span>:
    l <span style="color: #66cc66;">=</span> log<span style="color: black;">&#40;</span>number<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: black;">&#40;</span>l <span style="color: #66cc66;">==</span> floor<span style="color: black;">&#40;</span>l<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> fft_ct<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>:
    length <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> length <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> x
    even <span style="color: #66cc66;">=</span> x<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span>::<span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    odd <span style="color: #66cc66;">=</span> x<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span>::<span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    evenFFT <span style="color: #66cc66;">=</span> fft_cooleytukey<span style="color: black;">&#40;</span>even<span style="color: black;">&#41;</span>
    oddFFT <span style="color: #66cc66;">=</span> fft_cooleytukey<span style="color: black;">&#40;</span>odd<span style="color: black;">&#41;</span>
    pivot <span style="color: #66cc66;">=</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>length / <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>
    omega <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span> * pi / length
    left <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    right <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>pivot<span style="color: black;">&#41;</span>:
    angle <span style="color: #66cc66;">=</span> k * omega
    real <span style="color: #66cc66;">=</span> cos<span style="color: black;">&#40;</span>angle<span style="color: black;">&#41;</span>
    imag <span style="color: #66cc66;">=</span> sin<span style="color: black;">&#40;</span>angle<span style="color: black;">&#41;</span>
    base <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>real<span style="color: #66cc66;">,</span> imag<span style="color: black;">&#41;</span>
    left <span style="color: #66cc66;">=</span> left + <span style="color: black;">&#91;</span>evenFFT<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> + base * oddFFT<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>
    right <span style="color: #66cc66;">=</span> right + <span style="color: black;">&#91;</span>evenFFT<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> - base * oddFFT<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>
    F <span style="color: #66cc66;">=</span> left + right
    <span style="color: #ff7700;font-weight:bold;">return</span> F
    &nbsp;
    f <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span><span style="color: #008000;">complex</span><span style="color: #66cc66;">,</span> inputf<span style="color: black;">&#41;</span>
    n <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>f<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> is_power_of_two<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    F <span style="color: #66cc66;">=</span> fft_ct<span style="color: black;">&#40;</span>f<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    F <span style="color: #66cc66;">=</span> dft<span style="color: black;">&#40;</span>f<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> F</pre></td></tr></table><p class="theCode" style="display:none;">def fft_cooleytukey(inputf):
    &quot;&quot;&quot;
    Return a list with the coeficients of Fast Fourier Transform
    (Sande-Tukey -- Decimation in Time algorithm).
    
    F = fft_cooleytukey(inputf)
    
    INPUT:
    * f: list with discrete points of time-domain
    
    return: list discrete points of frequency-domain
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2011
    &quot;&quot;&quot;
    
    def is_power_of_two(number):
    l = log(number, 2)
    return (l == floor(l))
    
    def fft_ct(x):
    length = len(x)
    if length == 1:
    return x
    even = x[0::2]
    odd = x[1::2]
    evenFFT = fft_cooleytukey(even)
    oddFFT = fft_cooleytukey(odd)
    pivot = int(length / 2)
    omega = 2 * pi / length
    left = []
    right = []
    for k in xrange(pivot):
    angle = k * omega
    real = cos(angle)
    imag = sin(angle)
    base = complex(real, imag)
    left = left + [evenFFT[k] + base * oddFFT[k]]
    right = right + [evenFFT[k] - base * oddFFT[k]]
    F = left + right
    return F
    
    f = map(complex, inputf)
    n = len(f)
    if is_power_of_two(n):
    F = fft_ct(f)
    else:
    F = dft(f)
    return F</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. A Transformada Rápida de Fourier 

A transformada rápida de Fourier é um algoritmo desenvolvido para calcular a transformada discreta de Fourier utilizando menos recursos computacionais. Conhecida por FFT (_Fast Fourier Transform_), Sua eficiência se deve ao fato dela reaproveitar resultados computados anteriormente, reduzindo o número total de operações aritméticas. 

Algoritmos que implementam FFTs exploram a simetria e a periodicidade das funções trigonométricas para calcular a transformada. Este tipo de abordagem reduz a quantidade de $$N^2 $$ operações, necessárias para computar a TDF, para $$N log_2 N $$ operações. Em problemas reais, isto significa um ganho de eficiência considerável, conforme podemos comparar no gráfico abaixo: 

<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/06/g1.png"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/06/g1.png" alt="" title="g1" width="570" height="388" class="aligncenter size-full wp-image-1189" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/06/g1.png 570w, http://www.sawp.com.br/blog/wp-content/uploads/2011/06/g1-300x204.png 300w" sizes="(max-width: 570px) 100vw, 570px" /></a><br />
</center>

Em 1965, J.W. Cooley e J.W. Tukey publicaram o primeiro algoritmo para o cálculo da transformada rápida de Fourier, utilizando-se decimação no domínio do tempo. Posteriormente, muitos algoritmos derivaram-se da técnica de Cooley-Tukey, utilizando-se do princípio de que uma transformada discreta pode ser dividida &#8212; decimada &#8212; em transformadas menores, uma vez que muitas
    
operações são redundantes. 

Outras abordagens permitem o cálculo da FFT, mas sem melhoria na complexidade do algoritmo. Além das classes de algoritmos derivados de Cooley-Tukey, temos aqueles que implementam decimação no domínio da frequência. Esses algoritmos são também conhecidos como métodos de Sande-Tukey. 

### 1.1. Algoritmo de Sande-Tukey 

Para que seja possível calcular a FFT por este algoritmo, devemos ter como entrada uma quantidade par de valores. Ou seja,

<center>
  $$N = 2 ^ M$$
</center>


    
Como apresentado em outro post, a transformada discreta de Fourier é definida como
    


<center>
  $$F_k = \sum_{j=0}^{N} f_j e^{-i \frac{2 \pi}{N} j k} $$
</center>


    
para $$k = 0, 1, \ldots, N $$ . 

Supondo que dividimos cada amostra na metade, e decompondo a equação acima em termos de $$\frac{N}{2} $$ pontos, temos que:

<center>
  $$F_k = \sum_{j=0}^{(N/2) &#8211; 1} f_j e^{\frac{-i 2 \pi k j}{N} + \sum_{j=N/2}^{N} f_j e^{\frac{-i 2 \pi k j}{N}$$
</center>

Se criarmos uma nova variável $$m = j &#8211; \frac{N}{2} $$ , observamos que a segunda somatória possui o mesmo número de elementos da primeira:

<center>
  $$F_k = \sum_{j=0}^{(N/2) &#8211; 1} f_j e^{\frac{-i 2 \pi k j}{N} + \sum_{m=0}^{(N/2) &#8211; 2} f_{m+N} e^{-i (2 \pi / N) k (m + N/2)}$$
</center>

com isso, podemos agrupar novamente os termos em um único somatório

<center>
  $$F_k = \sum_{j=0}^{(N/2) &#8211; 1} (f_j + e^{-i \pi k} f_{n+N/2}) e^{\frac{-i 2 \pi k j}{N}$$
</center>

Ao utilizarmos a propriedade
    


<center>
  $$e^{-i \pi k} = (-1) ^ k$$
</center>

notamos que os pontos são sempre projetados. Isto é, para $$k $$ par, esse fator é igual à $$1 $$ , para $$k $$ ímpar é $$-1 $$ . Com isso, decompomos a transformada em duas, uma relativa às pares

<center>
  $$F_{2k} = \sum_{j=0}^{(N/2)-1} (f_j + f_{j+N/2}) e^{\frac{-i 2 \pi k j}{N/2}$$
</center>

e outra relativa às ímpares

<center>
  $$F_{2k+1} = \sum_{j=0}^{(N/2)-1} (f_j &#8211; f_{j+N/2}) e^{\frac{-i 2 \pi k j}{N/2} e^{\frac{-i2 \pi j}{N}$$
</center>

para $$k = 0, 1, \ldots, N $$. 

Se definirmos
    


<center>
  $$W = e ^{-i \frac{2 \pi}{N}$$
</center>

podemos reescrever a TDF como

<center>
  $$F_k = \sum_{j=0}^{N} f_n W^{jk}$$
</center>

e as equações decompostas como

<center>
  $$F_{2k} = \sum_{j=0}^{(N/2)-1} (f_j + f_{j+N/2}) W^{2jk}$$
</center>


    
e
    


<center>
  $$F_{2K+1} = \sum_{j=0}^{(N/2)-1} (f_j &#8211; f_{j+N/2}) W^j W^{2jk}$$
</center>

Dessas expressões, podemos notar que elas se relacionam por

<center>
  $$g_j = f_j + f_{j+N/2}$$
</center>

e

<center>
  $$h_j = (f_j + f_{j+N/2}) W^j$$
</center>

portanto,

<center>
  $$F_{2k} = G_k $$ e $$F_{2k+1} = H_k $$
</center>

Ou seja, em vez de um utilizarmos $$N $$ pontos, utilizamos dois cálculos para $$N/2$$ pontos. 

A TDF é calculada formando-se inicialmente as sequências $$g\_n$$ e $$h\_n$$ e então calculando-se as TDFs para $$\frac{N}{2} $$ pontos para obtermos as transformadas ímpares e pares, independentemente. Os pesos $$W^j$$ são frequentemente chamados de _twiddle factors_ na literatura. 

O processo de dividir a transformada em duas transformadas independentes, tratando apenas $$\frac{N}{2} $$ pontos, é repetida novamente para cada novo intervalo seccionado. Ou seja, calculamos as TDFs para $$\frac{N}{4}$$ pontos das quatro sequências de comprimento $$\frac{N}{4} $$ compostas dos primeiros e últimos pontos. Assim, repetindo-se esta estratégia até a solução, teremos aproximadamente $$N \log_2 N $$ operações. 

&nbsp;

### 1.2. Algoritmo de Cooley-Tukey 

A abordagem que utiliza decimação no tempo, utiliza-se do inverso do que faz o algoritmo de Sande-Tukey. Embora os dois métodos sejam diferentes na ordem de processamento dos dados, ambos possuem complexidade equivalente, de $$N \log_2 N$$ operações. Neste algoritmo, a amostra original é dividida inicialmente em pontos rotulados com numeração par e ímpar, e as diversas TDFs são aplicadas sobre essas divisões. 

&nbsp;

## 2. Implementação 

### 2.1. Algoritmo de Sande-Tukey 

<div>
  <pre lang="python">def fft_sandetukey(inputf):
    """
    Return a list with the coeficients of Fast Fourier Transform
    (Sande-Tukey -- Decimation in Frequency algorithm).

    F = fft_sandetukey(inputf)

    INPUT:
    * f: list with discrete points of time-domain

    return: list discrete points of frequency-domain

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2011
    """

    def fft_st(x, n):
        if n != 1:
            d = [complex(0.0) for i in xrange(n)]
            e = [complex(0.0) for i in xrange(n)]
            nh = n / 2
            for k in xrange(nh, -1, -1):
                s = x[k]
                t = x[k + nh]
                e[k] = s + t
                d[k] = s - t
            for k in xrange(nh):
                theta = k * omega * n
                real = cos(theta)
                imag = sin(theta)
                d[k] = d[k] * complex(real, imag)
            # divide and conquer
            bige = fft_st(e, nh)
            bigd = fft_st(d, nh)
            j = 0
            for k in xrange(nh):
                x[j] = bige[k]
                x[j + 1] = bigd[k]
                j = j + 2
        return x

    f = map(complex, inputf)
    m = len(f)
    omega = -2.0 * pi / m
    return fft_st(f, m - 1)</pre>
</div>

Esta função está disponível em <a href="http://www.sawp.com.br/code/interpolation/fft_sandetukey.py" target="_blank">http://www.sawp.com.br/code/interpolation/fft_sandetukey.py</a> assim como um exemplo de como utilizá-la. 

### 2.2. Algoritmo de Cooley-Tukey 

<div>
  <pre lang="python">def fft_cooleytukey(inputf):
    """
    Return a list with the coeficients of Fast Fourier Transform
    (Sande-Tukey -- Decimation in Time algorithm).

    F = fft_cooleytukey(inputf)

    INPUT:
    * f: list with discrete points of time-domain

    return: list discrete points of frequency-domain

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2011
    """

    def is_power_of_two(number):
        l = log(number, 2)
        return (l == floor(l))

    def fft_ct(x):
        length = len(x)
        if length == 1:
            return x
        even = x[0::2]
        odd = x[1::2]
        evenFFT = fft_cooleytukey(even)
        oddFFT = fft_cooleytukey(odd)
        pivot = int(length / 2)
        omega = 2 * pi / length
        left = []
        right = []
        for k in xrange(pivot):
            angle = k * omega
            real = cos(angle)
            imag = sin(angle)
            base = complex(real, imag)
            left = left + [evenFFT[k] + base * oddFFT[k]]
            right = right + [evenFFT[k] - base * oddFFT[k]]
        F = left + right
        return F

    f = map(complex, inputf)
    n = len(f)
    if is_power_of_two(n):
        F = fft_ct(f)
    else:
        F = dft(f)
    return F</pre>
</div>

Esta função está disponível em <a href="http://www.sawp.com.br/code/interpolation/fft_cooleytukey.py" target="_blank">http://www.sawp.com.br/code/interpolation/fft_cooleytukey.py</a> assim como um exemplo de como utilizá-la. 

&nbsp;

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
