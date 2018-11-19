---
id: 1172
title: '3.2.4 Aproximação de Funções &#8212; Análise de Fourier &#8212; A Transformada Discreta de Fourier'
date: 2011-06-06T10:51:22+00:00
author: SAWP
excerpt: Um sinal natural raramente é caracterizado como uma função definida no contínuo, como aquelas descritas pela transformada contínua de Fourier. Em vez disso, os dados são amostrados em tempos discretos. Assim, a forma mais eficiente de conversão entre domínios de problemas reais se dá pela transformada discreta de Fourier.
layout: post
guid: http://www.sawp.com.br/blog/?p=1172
permalink: /p=1172
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:4562:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> dft<span style="color: black;">&#40;</span>inputF<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the coeficients of Discrete Fourier Transform.
    &nbsp;
    f = dft(inputF)
    &nbsp;
    INPUT:
    * f: list with discrete points of frequency-domain
    &nbsp;
    return: list discrete points of time-domain
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Mar 2011
    &quot;&quot;&quot;</span>
    F <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span><span style="color: #008000;">complex</span><span style="color: #66cc66;">,</span> inputF<span style="color: black;">&#41;</span>
    m <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>F<span style="color: black;">&#41;</span>
    f <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    omega <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2.0</span> * pi / m
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>real<span style="color: #66cc66;">,</span> imag<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> n <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    angle <span style="color: #66cc66;">=</span> k * omega * n
    real <span style="color: #66cc66;">=</span> real + F<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> * cos<span style="color: black;">&#40;</span>angle<span style="color: black;">&#41;</span>
    imag <span style="color: #66cc66;">=</span> imag + F<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> * sin<span style="color: black;">&#40;</span>angle<span style="color: black;">&#41;</span>
    f<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>real<span style="color: #66cc66;">,</span> imag<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> f</pre></td></tr></table><p class="theCode" style="display:none;">def dft(inputF):
    &quot;&quot;&quot;
    Return a list with the coeficients of Discrete Fourier Transform.
    
    f = dft(inputF)
    
    INPUT:
    * f: list with discrete points of frequency-domain
    
    return: list discrete points of time-domain
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2011
    &quot;&quot;&quot;
    F = map(complex, inputF)
    m = len(F)
    f = [complex(0.0) for i in xrange(m)]
    omega = 2.0 * pi / m
    for k in xrange(m):
    (real, imag) = (0.0, 0.0)
    for n in xrange(m):
    angle = k * omega * n
    real = real + F[n] * cos(angle)
    imag = imag + F[n] * sin(angle)
    f[k] = complex(real, imag)
    return f</p></div>
    ;i:2;s:4598:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> idft<span style="color: black;">&#40;</span>inputf<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a list with the coeficients of Inverse Discrete Fourier Transform.
    &nbsp;
    F = idft(inputf)
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
    f <span style="color: #66cc66;">=</span> <span style="color: #008000;">map</span><span style="color: black;">&#40;</span><span style="color: #008000;">complex</span><span style="color: #66cc66;">,</span> inputf<span style="color: black;">&#41;</span>
    m <span style="color: #66cc66;">=</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>f<span style="color: black;">&#41;</span>
    F <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #008000;">complex</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    omega <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2.0</span> * pi / m
    <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>real<span style="color: #66cc66;">,</span> imag<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">0.0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> n <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>m<span style="color: black;">&#41;</span>:
    angle <span style="color: #66cc66;">=</span> k * omega * n
    real <span style="color: #66cc66;">=</span> real + f<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> * cos<span style="color: black;">&#40;</span>angle<span style="color: black;">&#41;</span> / m
    imag <span style="color: #66cc66;">=</span> imag - f<span style="color: black;">&#91;</span>n<span style="color: black;">&#93;</span> * sin<span style="color: black;">&#40;</span>angle<span style="color: black;">&#41;</span> / m
    F<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">complex</span><span style="color: black;">&#40;</span>real<span style="color: #66cc66;">,</span> imag<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> F</pre></td></tr></table><p class="theCode" style="display:none;">def idft(inputf):
    &quot;&quot;&quot;
    Return a list with the coeficients of Inverse Discrete Fourier Transform.
    
    F = idft(inputf)
    
    INPUT:
    * f: list with discrete points of time-domain
    
    return: list discrete points of frequency-domain
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Mar 2011
    &quot;&quot;&quot;
    f = map(complex, inputf)
    m = len(f)
    F = [complex(0.0) for i in xrange(m)]
    omega = 2.0 * pi / m
    for k in xrange(m):
    (real, imag) = (0.0, 0.0)
    for n in xrange(m):
    angle = k * omega * n
    real = real + f[n] * cos(angle) / m
    imag = imag - f[n] * sin(angle) / m
    F[k] = complex(real, imag)
    return F</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. A Transformada Discreta de Fourier 

Para problemas reais, tais como processamento de sinais, não precisamos conhecer todo o domínio transformado, obtido pela transformada contínua. Ao contrário, as funções podem ser representadas por conjuntos finitos de valores discretos. Em geral, queremos transformar apenas alguns pontos amostrados. 

Seja o intervalo$$[0,t]$$ dividido em $$N$$ subintervalos com largura $$\Delta t = \frac{T}{N}$$ . Especificamos os dados em$$n=0,1,2,\ldots, N &#8211; 1$$ . A transformada discreta de Fourier é definida como

<center>
  $$ F_k = \sum_{n=0}^{N-1} f_n e^{-i k \omega_0 n}$$
</center>

para $$k=0,1,2,\ldots, N &#8211; 1 $$ . De forma análoga, a transformada inversa na forma discreta é

<center>
  $$ f_n = \sum_{k=0}^{N-1} F_k e^{i k \omega_0 n}$$
</center>

As duas equações acima podem ser utilizadas para calcular tanto a transformada de Fourier direta quando a inversa para dados discretos. Como temos um conjunto de transformações de $$n$$ elementos no domínio transformado para os $$n$$ pontos amostrados, a transformada de Fourier discreta requer $$N^2$$ operações complexas. 

Para facilitar a implementação computacional da TFD, utilizaremos a identidade de Euler para decompormos as fórmulas em funções trigonométricas 

<center>
  $$ e^{\pm i a} = cos(a) \pm i sin(a)$$
</center>

para reescrevermos a transformada e a sua inversa como

<center>
  $$ F_k = \frac{1}{N} \sum_{n=0}^{N} \left[ f_n cos(k \omega n) &#8211; i f_n sin(k \omega n) \right]$$
</center>


  
e
  


<center>
  $$ f_n = \sum_{k=0}^{N} \left[ F_k cos(k \omega n) + i F_k sin(k \omega n) \right]$$
</center>

onde $$\omega = \frac{2 \pi}{N}$$ . 

&nbsp;

## 2. Implementação 

A transformada de Fourier discreta:

<div>
  <pre lang="python">def dft(inputF):
    """
    Return a list with the coeficients of Discrete Fourier Transform.

    f = dft(inputF)

    INPUT:
    * f: list with discrete points of frequency-domain

    return: list discrete points of time-domain

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2011
    """
    F = map(complex, inputF)
    m = len(F)
    f = [complex(0.0) for i in xrange(m)]
    omega = 2.0 * pi / m
    for k in xrange(m):
        (real, imag) = (0.0, 0.0)
        for n in xrange(m):
            angle = k * omega * n
            real = real + F[n] * cos(angle)
            imag = imag + F[n] * sin(angle)
        f[k] = complex(real, imag)
    return f</pre>
</div>

e sua inversa:

<div>
  <pre lang="python">def idft(inputf):
    """
    Return a list with the coeficients of Inverse Discrete Fourier Transform.

    F = idft(inputf)

    INPUT:
    * f: list with discrete points of time-domain

    return: list discrete points of frequency-domain

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Mar 2011
    """
    f = map(complex, inputf)
    m = len(f)
    F = [complex(0.0) for i in xrange(m)]
    omega = 2.0 * pi / m
    for k in xrange(m):
        (real, imag) = (0.0, 0.0)
        for n in xrange(m):
            angle = k * omega * n
            real = real + f[n] * cos(angle) / m
            imag = imag - f[n] * sin(angle) / m
        F[k] = complex(real, imag)
    return F</pre>
</div>

Estas funções estão disponíveis em <a href="http://www.sawp.com.br/code/interpolation/dft.py" target="_blank">http://www.sawp.com.br/code/interpolation/dft.py</a> assim como um exemplo de como utilizá-las. 

&nbsp;

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b>Anthony Ralston and Philip Rabinowitz,<cite> <em>A First Course in Numerical Analysis</em> (2nd ed.),</cite> McGraw-Hill and Dover, (2001).</a><br /> <a name="bibitem2"><b>[2]</b>N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall (2006).</a>
  </p>
</fieldset>
