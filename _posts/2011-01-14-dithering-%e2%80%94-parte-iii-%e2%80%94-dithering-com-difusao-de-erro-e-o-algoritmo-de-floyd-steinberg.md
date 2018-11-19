---
id: 1041
title: Dithering — Parte III — Dithering com Difusão de Erro e o algoritmo de Floyd-Steinberg
date: 2011-01-14T16:28:59+00:00
author: SAWP
excerpt: Dithering (pontilhado) com difusão de erro é uma técnica de halftone que procura distribuir a diferença entre o valor exato de cada pixel e seu valor aproximado a um conjunto de pixels adjacentes. Diversas técnicas foram desenvolvidas com esta proposta, sendo o algoritmo de Floyd-Steinberg o primeiro desenvolvido utilizando esta abordagem.
layout: post
guid: http://www.sawp.com.br/blog/?p=1041
permalink: /p=1041
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:15470:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> floyd_steinberg<span style="color: black;">&#40;</span>originalImage<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">''' Floyd-Steinberg Dithering Algorithm.
    &nbsp;
    dithered = floyd_steinberg(originalImage)
    &nbsp;
    Parameters
    ----------
    originalImage: numpy ndarray, original image
    &nbsp;
    Return
    ----------
    dithered: numpy ndarray, dithered image
    &nbsp;
    References
    ----------
    http://en.wikipedia.org/wiki/Floyd-Steinberg
    &nbsp;
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    '''</span>
    <span style="color: black;">&#40;</span>M<span style="color: #66cc66;">,</span> N<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> originalImage.<span style="color: black;">shape</span>
    threshold <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">127.5</span>
    tmp <span style="color: #66cc66;">=</span> originalImage.<span style="color: #dc143c;">copy</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    dithered <span style="color: #66cc66;">=</span> zeros<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>M<span style="color: #66cc66;">,</span> N<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#40;</span>M<span style="color: #66cc66;">,</span> N<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>M - <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> N - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>:
    dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255</span> * <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;=</span> threshold<span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> - dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.4375</span> * error + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0625</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.3125</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> N<span style="color: black;">&#41;</span>:
    dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255.0</span> * <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;=</span> threshold<span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> - dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.4375</span> * error + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0625</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.3125</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.1875</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255</span> * <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;=</span> threshold<span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> - dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span> + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.3125</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> N - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.1875</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> N - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255</span> * <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;=</span> threshold<span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> - dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.4375</span> * error + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> N<span style="color: black;">&#41;</span>:
    dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255</span> * <span style="color: black;">&#40;</span>tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;=</span> threshold<span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> - dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.4375</span> * error + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255</span> * <span style="color: black;">&#40;</span>tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> N<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;=</span> threshold<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> dithered</pre></td></tr></table><p class="theCode" style="display:none;">def floyd_steinberg(originalImage):
    ''' Floyd-Steinberg Dithering Algorithm.
    
    dithered = floyd_steinberg(originalImage)
    
    Parameters
    ----------
    originalImage: numpy ndarray, original image
    
    Return
    ----------
    dithered: numpy ndarray, dithered image
    
    References
    ----------
    http://en.wikipedia.org/wiki/Floyd-Steinberg
    
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    '
    (M, N) = originalImage.shape
    threshold = 127.5
    tmp = originalImage.copy()
    dithered = zeros((M, N))
    (M, N) = (M - 1, N - 1)
    error = 0
    
    for row in xrange(M):
    dithered[row, 0] = 255 * int(tmp[row, 0] &gt;= threshold)
    error = - dithered[row, 0] + tmp[row, 0]
    tmp[row, 1] = 0.4375 * error + tmp[row, 1]
    tmp[row + 1, 1] = 0.0625 * error + tmp[row + 1, 1]
    tmp[row + 1, 0] = 0.3125 * error + tmp[row + 1, 0]
    
    for col in xrange(1, N):
    dithered[row, col] = 255.0 * int(tmp[row, col] &gt;= threshold)
    error = - dithered[row, col] + tmp[row, col]
    tmp[row, col + 1] = 0.4375 * error + tmp[row, col + 1]
    tmp[row + 1, col + 1] = 0.0625 * error + tmp[row + 1, col + 1]
    tmp[row + 1, col] = 0.3125 * error + tmp[row + 1, col]
    tmp[row + 1, col - 1] = 0.1875 * error + tmp[row + 1, col - 1]
    
    dithered[row, N] = 255 * int(tmp[row, N] &gt;= threshold)
    error = - dithered[row, N] + tmp[row, N]
    tmp[row + 1, N] = 0.3125 * error + tmp[row + 1, N]
    tmp[row + 1, N - 1] = 0.1875 * error + tmp[row + 1, N - 1]
    
    dithered[row, 0] = 255 * int(tmp[row, 0] &gt;= threshold)
    error = - dithered[row, 0] + tmp[row, 0]
    tmp[row, 1] = 0.4375 * error + tmp[row, 1]
    
    for col in xrange(1, N):
    dithered[row, col] = 255 * (tmp[row, col] &gt;= threshold)
    error = - dithered[row, col] + tmp[row, col]
    tmp[row, col + 1] = 0.4375 * error + tmp[row, col + 1]
    
    dithered[row, N] = 255 * (tmp[row, N] &gt;= threshold)
    return dithered</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
_Dithering_ (pontilhado) com difusão de erro é uma técnica de _halftone_ que procura distribuir a diferença entre o valor exato de cada pixel e seu valor aproximado a um conjunto de pixels adjacentes. Diversas técnicas foram desenvolvidas com esta proposta, sendo o algoritmo de Floyd-Steinberg o primeiro desenvolvido utilizando esta abordagem.

Tal algoritmo pode ser apresentada a partir da seguinte implementação:

<pre lang="python">def floyd_steinberg(originalImage):
    ''' Floyd-Steinberg Dithering Algorithm.

    dithered = floyd_steinberg(originalImage)

    Parameters
    ----------
    originalImage: numpy ndarray, original image

    Return
    ----------
    dithered: numpy ndarray, dithered image

    References
    ----------
    http://en.wikipedia.org/wiki/Floyd-Steinberg

    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    '''
    (M, N) = originalImage.shape
    threshold = 127.5
    tmp = originalImage.copy()
    dithered = zeros((M, N))
    (M, N) = (M - 1, N - 1)
    error = 0

    for row in xrange(M):
        dithered[row, 0] = 255 * int(tmp[row, 0] >= threshold)
        error = - dithered[row, 0] + tmp[row, 0]
        tmp[row, 1] = 0.4375 * error + tmp[row, 1]
        tmp[row + 1, 1] = 0.0625 * error + tmp[row + 1, 1]
        tmp[row + 1, 0] = 0.3125 * error + tmp[row + 1, 0]

        for col in xrange(1, N):
            dithered[row, col] = 255.0 * int(tmp[row, col] >= threshold)
            error = - dithered[row, col] + tmp[row, col]
            tmp[row, col + 1] = 0.4375 * error + tmp[row, col + 1]
            tmp[row + 1, col + 1] = 0.0625 * error + tmp[row + 1, col + 1]
            tmp[row + 1, col] = 0.3125 * error + tmp[row + 1, col]
            tmp[row + 1, col - 1] = 0.1875 * error + tmp[row + 1, col - 1]

        dithered[row, N] = 255 * int(tmp[row, N] >= threshold)
        error = - dithered[row, N] + tmp[row, N]
        tmp[row + 1, N] = 0.3125 * error + tmp[row + 1, N]
        tmp[row + 1, N - 1] = 0.1875 * error + tmp[row + 1, N - 1]

    dithered[row, 0] = 255 * int(tmp[row, 0] >= threshold)
    error = - dithered[row, 0] + tmp[row, 0]
    tmp[row, 1] = 0.4375 * error + tmp[row, 1]

    for col in xrange(1, N):
        dithered[row, col] = 255 * (tmp[row, col] >= threshold)
        error = - dithered[row, col] + tmp[row, col]
        tmp[row, col + 1] = 0.4375 * error + tmp[row, col + 1]

    dithered[row, N] = 255 * (tmp[row, N] >= threshold)
    return dithered</pre>

Devemos notar que os valores multiplicados ao erro são pesos que formam a distribuição característica desse algoritmo. Esta forma de distribuição de erro é ilustrada na seguinte matriz:
  


<center>
  <br /> $$<br /> \begin{array}{| c | c | c | }<br /> \hline<br /> 0 & 0 & 0 \\ \hline<br /> 0 & f(x,y) & 7/16 \\ \hline<br /> 3/16 & 5/16 & 1/16 \\<br /> \hline<br /> \end{array}<br /> $$<br />
</center>

O resultado da aplicação desta técnica de pontilhado pode ser vista nas imagens abaixo:

<center>
  </p> 
  
  <table>
    <tr>
      <td>
        Original (entrada)
      </td>
      
      <td>
        Halftoned (saída)
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized2.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized2.jpg" alt="" title="lena_resized" width="256" height="256" class="aligncenter size-full wp-image-1052" /></a>
        </center>
      </td>
      
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_halftoned1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_halftoned1.jpg" alt="" title="lena_halftoned" width="256" height="256" class="aligncenter size-full wp-image-1053" /></a>
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized2.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized2.jpg" alt="" title="degrade_resized" width="256" height="256" class="aligncenter size-full wp-image-1054" /></a>
        </center>
      </td>
      
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_halftoned1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_halftoned1.jpg" alt="" title="degrade_halftoned" width="256" height="256" class="aligncenter size-full wp-image-1055" /></a>
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_resized1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_resized1.jpg" alt="" title="flower_resized" width="256" height="256" class="aligncenter size-full wp-image-1056" /></a>
        </center>
      </td>
      
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_halftoned1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_halftoned1.jpg" alt="" title="flower_halftoned" width="256" height="256" class="aligncenter size-full wp-image-1057" /></a>
        </center>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
  
  <p>
    A partir dos resultados acima, podemos notar o efeito de &#8220;respingo&#8221; que a imagem binária apresenta. Isso ocorre porque a ordem na qual a imagem é percorrida pode produzir resultados diferentes no processo de meio-tom. A varredura da esquerda para a direita que foi implementada pode gerar padrões indesejados, tais como os observados. Para evitar tais efeitos, uma opção é alternar a direção de varredura a cada linha.
  </p>
  
  <p>
    Uma outra abordagem utiliza curvas de preenchimento do espaço para distribuir o erro de quantização da imagem. A curva de Hilbert possui características desejáveis para geração de imagens de halftoning.
  </p>
