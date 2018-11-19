---
id: 1065
title: Dithering — Parte IV — Dithering com Difusão de Erro de Jarvis
date: 2011-01-14T18:19:42+00:00
author: CKPYT
excerpt: O algoritmo de pontilhado de Jarvis, Judice e Ninke difunde o erro com mais um passo de distância. É mais lento do que o método de Floyd-Steinberg, pois distribui os erros entre 12 pixels próximos, em vez de 4 pixels nas proximidades, como faz o primeiro.
layout: post
guid: http://www.sawp.com.br/blog/?p=1065
permalink: /p=1065
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:13408:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> jarvis<span style="color: black;">&#40;</span>originalImage<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">''' Original Jarvis Dithering Algorithm.
    &nbsp;
    dithered = jarvis(originalImage)
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
    J.Jarvis, C.Judice, and W.Ninke, ``A survey of techniques for the
    display of continuous tone pictures on bilevel displays,''
    em Comp. Graph and Image  Proc., vol.~5, pp.~13--40, 1976.
    &nbsp;
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    '''</span>
    <span style="color: black;">&#40;</span>M<span style="color: #66cc66;">,</span> N<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> originalImage.<span style="color: black;">shape</span>
    threshold <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">127.5</span>
    tmp <span style="color: #66cc66;">=</span> originalImage.<span style="color: #dc143c;">copy</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #008000;">super</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">127.5</span> * ones<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>M<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    infer <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">127.5</span> * ones<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> N + <span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    tmp <span style="color: #66cc66;">=</span> concatenate<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #008000;">super</span><span style="color: #66cc66;">,</span> tmp<span style="color: #66cc66;">,</span> <span style="color: #008000;">super</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> axis<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    tmp <span style="color: #66cc66;">=</span> concatenate<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>tmp<span style="color: #66cc66;">,</span> infer<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    dithered <span style="color: #66cc66;">=</span> tmp.<span style="color: #dc143c;">copy</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>M<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> col <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> N + <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>:
    dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255.0</span> * <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;=</span> threshold<span style="color: black;">&#41;</span>
    error <span style="color: #66cc66;">=</span> - dithered<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span> + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col<span style="color: black;">&#93;</span>
    &nbsp;
    tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.10417</span> * error + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.14583</span> * error + tmp<span style="color: black;">&#91;</span>row<span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0625</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.10417</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.14583</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.10417</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0625</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    &nbsp;
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.02083</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0625</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.10417</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col + <span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0625</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.02083</span> * error + tmp<span style="color: black;">&#91;</span>row + <span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> col - <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> dithered<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span>:M<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">2</span>:N + <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">def jarvis(originalImage):
    ''' Original Jarvis Dithering Algorithm.
    
    dithered = jarvis(originalImage)
    
    Parameters
    ----------
    originalImage: numpy ndarray, original image
    
    Return
    ----------
    dithered: numpy ndarray, dithered image
    
    References
    ----------
    J.Jarvis, C.Judice, and W.Ninke, ``A survey of techniques for the
    display of continuous tone pictures on bilevel displays,''
    em Comp. Graph and Image  Proc., vol.~5, pp.~13--40, 1976.
    
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    '
    (M, N) = originalImage.shape
    threshold = 127.5
    tmp = originalImage.copy()
    error = 0
    
    super = 127.5 * ones((M, 2))
    infer = 127.5 * ones((2, N + 4))
    tmp = concatenate((super, tmp, super), axis=1)
    tmp = concatenate((tmp, infer))
    dithered = tmp.copy()
    
    for row in xrange(M):
    for col in xrange(2, N + 2):
    dithered[row, col] = 255.0 * int(tmp[row, col] &gt;= threshold)
    error = - dithered[row, col] + tmp[row, col]
    
    tmp[row, col + 2] = 0.10417 * error + tmp[row, col + 2]
    tmp[row, col + 1] = 0.14583 * error + tmp[row, col + 1]
    
    tmp[row + 1, col + 2] = 0.0625 * error + tmp[row + 1, col + 2]
    tmp[row + 1, col + 1] = 0.10417 * error + tmp[row + 1, col + 1]
    tmp[row + 1, col + 0] = 0.14583 * error + tmp[row + 1, col + 0]
    tmp[row + 1, col - 1] = 0.10417 * error + tmp[row + 1, col - 1]
    tmp[row + 1, col - 2] = 0.0625 * error + tmp[row + 1, col - 2]
    
    tmp[row + 2, col + 2] = 0.02083 * error + tmp[row + 2, col + 2]
    tmp[row + 2, col + 1] = 0.0625 * error + tmp[row + 2, col + 1]
    tmp[row + 2, col + 0] = 0.10417 * error + tmp[row + 2, col + 0]
    tmp[row + 2, col - 1] = 0.0625 * error + tmp[row + 2, col - 1]
    tmp[row + 2, col - 2] = 0.02083 * error + tmp[row + 2, col - 2]
    return dithered[0:M, 2:N + 2]</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
Uma forma de obter uma imagem binária é usar a distribuição de erro de Jarvis. Semelhante à abordagem de Floyd-Steinberg, a difusão do erro é produzida através da seguinte máscara:

<center>
  <br /> $$<br /> \begin{array}{| c | c | c | c| c |}<br /> \hline<br /> 0 & 0 & 0 & 0 & 0 \\ \hline<br /> 0 & 0 & 0 & 0 & 0 \\ \hline<br /> 0 & 0 & f(x,y) & 7/48 & 5/48 \\ \hline<br /> 3/48 & 5/48 & 7/48 & 5/48 & 3/48 \\ \hline<br /> 1/48 & 3/48 & 5/48 & 5/48 & 1/48 \\ \hline<br /> \end{array}<br /> $$<br />
</center>

O algoritmo de halftoning que utiliza a difusão de erro de Jarvis, Judice e Ninke é efetuado pela seguinte função:

<pre lang="python">def jarvis(originalImage):
    ''' Original Jarvis Dithering Algorithm.

    dithered = jarvis(originalImage)

    Parameters
    ----------
    originalImage: numpy ndarray, original image

    Return
    ----------
    dithered: numpy ndarray, dithered image

    References
    ----------
    J.Jarvis, C.Judice, and W.Ninke, ``A survey of techniques for the
    display of continuous tone pictures on bilevel displays,''
    em Comp. Graph and Image  Proc., vol.~5, pp.~13--40, 1976.

    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    '''
    (M, N) = originalImage.shape
    threshold = 127.5
    tmp = originalImage.copy()
    error = 0

    super = 127.5 * ones((M, 2))
    infer = 127.5 * ones((2, N + 4))
    tmp = concatenate((super, tmp, super), axis=1)
    tmp = concatenate((tmp, infer))
    dithered = tmp.copy()

    for row in xrange(M):
        for col in xrange(2, N + 2):
            dithered[row, col] = 255.0 * int(tmp[row, col] >= threshold)
            error = - dithered[row, col] + tmp[row, col]

            tmp[row, col + 2] = 0.10417 * error + tmp[row, col + 2]
            tmp[row, col + 1] = 0.14583 * error + tmp[row, col + 1]

            tmp[row + 1, col + 2] = 0.0625 * error + tmp[row + 1, col + 2]
            tmp[row + 1, col + 1] = 0.10417 * error + tmp[row + 1, col + 1]
            tmp[row + 1, col + 0] = 0.14583 * error + tmp[row + 1, col + 0]
            tmp[row + 1, col - 1] = 0.10417 * error + tmp[row + 1, col - 1]
            tmp[row + 1, col - 2] = 0.0625 * error + tmp[row + 1, col - 2]

            tmp[row + 2, col + 2] = 0.02083 * error + tmp[row + 2, col + 2]
            tmp[row + 2, col + 1] = 0.0625 * error + tmp[row + 2, col + 1]
            tmp[row + 2, col + 0] = 0.10417 * error + tmp[row + 2, col + 0]
            tmp[row + 2, col - 1] = 0.0625 * error + tmp[row + 2, col - 1]
            tmp[row + 2, col - 2] = 0.02083 * error + tmp[row + 2, col - 2]
    return dithered[0:M, 2:N + 2]</pre>

A partir desta implementação, obtemos os seguintes resultados:

<center>
  </p> 
  
  <table>
    <tr>
      <td>
        <center>
          Original (entrada)
        </center>
      </td>
      
      <td>
        <center>
          Halftoned (saída)
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized3.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized3.jpg" alt="" title="lena_resized" width="256" height="256" class="aligncenter size-full wp-image-1069" /></a>
        </center>
      </td>
      
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_halftoned2.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_halftoned2.jpg" alt="" title="lena_halftoned" width="256" height="256" class="aligncenter size-full wp-image-1070" /></a>
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_resized2.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_resized2.jpg" alt="" title="flower_resized" width="256" height="256" class="aligncenter size-full wp-image-1071" /></a>
        </center>
      </td>
      
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_halftoned2.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_halftoned2.jpg" alt="" title="flower_halftoned" width="256" height="256" class="aligncenter size-full wp-image-1072" /></a>
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized3.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized3.jpg" alt="" title="degrade_resized" width="256" height="256" class="aligncenter size-full wp-image-1073" /></a>
        </center>
      </td>
      
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_halftoned2.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_halftoned2.jpg" alt="" title="degrade_halftoned" width="256" height="256" class="aligncenter size-full wp-image-1074" /></a>
        </center>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
