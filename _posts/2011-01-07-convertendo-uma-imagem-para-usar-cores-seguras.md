---
id: 924
title: Convertendo uma Imagem para Usar Cores Seguras
date: 2011-01-07T14:04:41+00:00
author: CKPYT
excerpt: 'Um sistema de representação de cores em imagens -- RGB, HSI, CMY, CMYK -- pode conter diversos valores, permitindo gerar escalas com tonalidades mais ou menos variadas, dependendo da quantidade de informação utilizada na representação (8, 16, 32 ou 24 bits). Todavia, existem 216 cores padronizadas utilizadas para algumas aplicações. Este post apresenta uma função que converte imagens coloridas em suas versões com cores seguras.'
layout: post
guid: http://www.sawp.com.br/blog/?p=924
permalink: p=924
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:11731:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> safecolors<span style="color: black;">&#40;</span>Im<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Convert a RGB image to safe colors.
    &nbsp;
    Parameters
    ----------
    * im: unsafe RGB image (numpy matrix)
    &nbsp;
    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    &quot;&quot;&quot;</span>
    Im <span style="color: #66cc66;">=</span> ceil<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">6.0</span> / <span style="color: #ff4500;">255.0</span><span style="color: black;">&#41;</span> * Im<span style="color: black;">&#41;</span>
    R <span style="color: #66cc66;">=</span> Im<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    G <span style="color: #66cc66;">=</span> Im<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    B <span style="color: #66cc66;">=</span> Im<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    &nbsp;
    R <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>R <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>R<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x00</span><span style="color: black;">&#41;</span>
    R <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>R <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>R<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x33</span><span style="color: black;">&#41;</span>
    R <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>R <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>R<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x66</span><span style="color: black;">&#41;</span>
    R <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>R <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>R<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x99</span><span style="color: black;">&#41;</span>
    R <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>R <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">5</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>R<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0xCC</span><span style="color: black;">&#41;</span>
    R <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>R <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">6</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>R<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0xFF</span><span style="color: black;">&#41;</span>
    &nbsp;
    G <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>G <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x00</span><span style="color: black;">&#41;</span>
    G <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>G <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x33</span><span style="color: black;">&#41;</span>
    G <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>G <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x66</span><span style="color: black;">&#41;</span>
    G <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>G <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x99</span><span style="color: black;">&#41;</span>
    G <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>G <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">5</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0xCC</span><span style="color: black;">&#41;</span>
    G <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>G <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">6</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>G<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0xFF</span><span style="color: black;">&#41;</span>
    &nbsp;
    B <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>B <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>B<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x00</span><span style="color: black;">&#41;</span>
    B <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>B <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>B<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x33</span><span style="color: black;">&#41;</span>
    B <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>B <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>B<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x66</span><span style="color: black;">&#41;</span>
    B <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>B <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>B<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x99</span><span style="color: black;">&#41;</span>
    B <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>B <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">5</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>B<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0xCC</span><span style="color: black;">&#41;</span>
    B <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>B <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">6</span><span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>B<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0xFF</span><span style="color: black;">&#41;</span>
    &nbsp;
    Om <span style="color: #66cc66;">=</span> zeros<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>Im.<span style="color: black;">shape</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> Im.<span style="color: black;">shape</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    Om<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> R
    Om<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> G
    Om<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> B
    <span style="color: #ff7700;font-weight:bold;">return</span> Om</pre></td></tr></table><p class="theCode" style="display:none;">def safecolors(Im):
    &quot;&quot;&quot;
    Convert a RGB image to safe colors.
    
    Parameters
    ----------
    * im: unsafe RGB image (numpy matrix)
    
    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    &quot;&quot;&quot;
    Im = ceil((6.0 / 255.0) * Im)
    R = Im[:,:,0]
    G = Im[:,:,1]
    B = Im[:,:,2]
    
    R = (R == 1).choose(R, 0x00)
    R = (R == 2).choose(R, 0x33)
    R = (R == 3).choose(R, 0x66)
    R = (R == 4).choose(R, 0x99)
    R = (R == 5).choose(R, 0xCC)
    R = (R == 6).choose(R, 0xFF)
    
    G = (G == 1).choose(G, 0x00)
    G = (G == 2).choose(G, 0x33)
    G = (G == 3).choose(G, 0x66)
    G = (G == 4).choose(G, 0x99)
    G = (G == 5).choose(G, 0xCC)
    G = (G == 6).choose(G, 0xFF)
    
    B = (B == 1).choose(B, 0x00)
    B = (B == 2).choose(B, 0x33)
    B = (B == 3).choose(B, 0x66)
    B = (B == 4).choose(B, 0x99)
    B = (B == 5).choose(B, 0xCC)
    B = (B == 6).choose(B, 0xFF)
    
    Om = zeros((Im.shape[0], Im.shape[1], 3))
    Om[:,:,0] = R
    Om[:,:,1] = G
    Om[:,:,2] = B
    return Om</p></div>
    ;i:2;s:1030:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">&quot;__main__&quot;</span>:
    inputim <span style="color: #66cc66;">=</span> imread<span style="color: black;">&#40;</span><span style="color: #483d8b;">'cube.bmp'</span><span style="color: black;">&#41;</span>
    outputim <span style="color: #66cc66;">=</span> safecolors<span style="color: black;">&#40;</span>inputim<span style="color: black;">&#41;</span>
    imsave<span style="color: black;">&#40;</span><span style="color: #483d8b;">'safe.bmp'</span><span style="color: #66cc66;">,</span> outputim<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">if __name__ == &quot;__main__&quot;:
    inputim = imread('cube.bmp')
    outputim = safecolors(inputim)
    imsave('safe.bmp', outputim)</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
Um sistema de representação de cores em imagens &#8212; RGB, HSI, CMY, CMYK &#8212; pode conter diversos valores, permitindo gerar escalas com tonalidades mais ou menos variadas, dependendo da quantidade de informação utilizada na representação (8, 16, 32 ou 24 bits). Todavia, existem 216 cores padronizadas utilizadas para algumas aplicações.

Estas 216 cores seguras tem como principal utilização a Web e são usadas pelos navegadores, independentemente a plataforma. O navegador alterará todas as cores da imagem para essas cores seguras para a Web ao visualizar uma cor a imagem na tela de 8 bits. As 216 cores formam um subconjunto das paletas de cores de 8 bits do MacOS. Ao trabalhar apenas com essas cores, é possível ter certeza de que a arte preparada para a Web não ficará pontilhada em um sistema definido com exibição em 256 cores.

Cada uma das 216 cores seguras é formada pelos três valores RGB da paleta de 256, mas estes valores são re-escalonados apenas para os valores 0, 51, 102, 153 ou 255. Assim, a tripla é formada pela combinação desses seis valores &#8212; \((6)^3 = 216\) possíveis valores. Portanto, a conversão consiste apenas em transformar os valores intermediários da maior escala \((0-255) \) nos valores da menor escala para cada pixel (note que no espaço RGB cada pixel possui 3 componentes). A função abaixo ilustra este processo:

<pre lang="python">def safecolors(Im):
    """
    Convert a RGB image to safe colors.

    Parameters
    ----------
    * im: unsafe RGB image (numpy matrix)

    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    """
    Im = ceil((6.0 / 255.0) * Im)
    R = Im[:,:,0]
    G = Im[:,:,1]
    B = Im[:,:,2]

    R = (R == 1).choose(R, 0x00)
    R = (R == 2).choose(R, 0x33)
    R = (R == 3).choose(R, 0x66)
    R = (R == 4).choose(R, 0x99)
    R = (R == 5).choose(R, 0xCC)
    R = (R == 6).choose(R, 0xFF)

    G = (G == 1).choose(G, 0x00)
    G = (G == 2).choose(G, 0x33)
    G = (G == 3).choose(G, 0x66)
    G = (G == 4).choose(G, 0x99)
    G = (G == 5).choose(G, 0xCC)
    G = (G == 6).choose(G, 0xFF)

    B = (B == 1).choose(B, 0x00)
    B = (B == 2).choose(B, 0x33)
    B = (B == 3).choose(B, 0x66)
    B = (B == 4).choose(B, 0x99)
    B = (B == 5).choose(B, 0xCC)
    B = (B == 6).choose(B, 0xFF)

    Om = zeros((Im.shape[0], Im.shape[1], 3))
    Om[:,:,0] = R
    Om[:,:,1] = G
    Om[:,:,2] = B
    return Om</pre>

Esta função pode ser utilizada da seguinte forma:

<pre lang="python">if __name__ == "__main__":
    inputim = imread('cube.bmp')
    outputim = safecolors(inputim)
    imsave('safe.bmp', outputim)</pre>

O resultado deste código é

<center>
  </p> 
  
  <table>
    <tr>
      <td>
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/cube.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/cube.jpg" alt="" title="cube" width="409" height="366" class="aligncenter size-full wp-image-930" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/cube.jpg 409w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/cube-300x268.jpg 300w" sizes="(max-width: 409px) 100vw, 409px" /></a>
      </td>
      
      <td>
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/safe.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/safe.jpg" alt="" title="safe" width="409" height="366" class="aligncenter size-full wp-image-931" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/safe.jpg 409w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/safe-300x268.jpg 300w" sizes="(max-width: 409px) 100vw, 409px" /></a>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          Original
        </center>
      </td>
      
      <td>
        <center>
          Cores seguras
        </center>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
