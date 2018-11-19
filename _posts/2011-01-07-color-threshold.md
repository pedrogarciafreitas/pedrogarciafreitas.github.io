---
id: 904
title: Color Threshold
date: 2011-01-07T08:49:11+00:00
author: CKPYT
excerpt: A idéia é colorir partes de uma imagem em tons de cinza com o objetivo de destacar regiões específicas.
layout: post
guid: http://www.sawp.com.br/blog/?p=904
permalink: p=904
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:5449:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> color_threshold<span style="color: black;">&#40;</span>im<span style="color: #66cc66;">,</span> rr<span style="color: #66cc66;">,</span> cc<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Convert a range of grayscale values in a RGB color.
    &nbsp;
    Parameters
    ----------
    * im: image (numpy matrix)
    * rr: range of threshold (2 elements tuple)
    * cc: RGB color (3 elemnts tuple -- (R,G,B) )
    &nbsp;
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    &quot;&quot;&quot;</span>
    inputR <span style="color: #66cc66;">=</span> im
    inputG <span style="color: #66cc66;">=</span> im
    inputB <span style="color: #66cc66;">=</span> im
    R <span style="color: #66cc66;">=</span> cc<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    G <span style="color: #66cc66;">=</span> cc<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    B <span style="color: #66cc66;">=</span> cc<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    Om <span style="color: #66cc66;">=</span> zeros<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>im.<span style="color: black;">shape</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> im.<span style="color: black;">shape</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>rr<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> rr<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>:
    inputR <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>inputR <span style="color: #66cc66;">==</span> i<span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>inputR<span style="color: #66cc66;">,</span> R<span style="color: black;">&#41;</span>
    inputG <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>inputG <span style="color: #66cc66;">==</span> i<span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>inputG<span style="color: #66cc66;">,</span> G<span style="color: black;">&#41;</span>
    inputB <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>inputB <span style="color: #66cc66;">==</span> i<span style="color: black;">&#41;</span>.<span style="color: black;">choose</span><span style="color: black;">&#40;</span>inputB<span style="color: #66cc66;">,</span> B<span style="color: black;">&#41;</span>
    Om<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> inputR
    Om<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> inputG
    Om<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: #66cc66;">,</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> inputB
    <span style="color: #ff7700;font-weight:bold;">return</span> Om</pre></td></tr></table><p class="theCode" style="display:none;">def color_threshold(im, rr, cc):
    &quot;&quot;&quot;
    Convert a range of grayscale values in a RGB color.
    
    Parameters
    ----------
    * im: image (numpy matrix)
    * rr: range of threshold (2 elements tuple)
    * cc: RGB color (3 elemnts tuple -- (R,G,B) )
    
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    &quot;&quot;&quot;
    inputR = im
    inputG = im
    inputB = im
    R = cc[0]
    G = cc[1]
    B = cc[2]
    Om = zeros((im.shape[0], im.shape[1], 3))
    for i in xrange(rr[0], rr[1]):
    inputR = (inputR == i).choose(inputR, R)
    inputG = (inputG == i).choose(inputG, G)
    inputB = (inputB == i).choose(inputB, B)
    Om[:,:,0] = inputR
    Om[:,:,1] = inputG
    Om[:,:,2] = inputB
    return Om</p></div>
    ;i:2;s:2045:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">&quot;__main__&quot;</span>:
    inputim <span style="color: #66cc66;">=</span> imread<span style="color: black;">&#40;</span><span style="color: #483d8b;">'river.bmp'</span><span style="color: black;">&#41;</span>
    grayrange <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>inputim.<span style="color: #008000;">min</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> inputim.<span style="color: #008000;">min</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span> + <span style="color: #ff4500;">20</span><span style="color: black;">&#41;</span>
    color <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">0xFF</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x00</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0x00</span><span style="color: black;">&#41;</span>
    outputim <span style="color: #66cc66;">=</span> color_threshold<span style="color: black;">&#40;</span>inputim<span style="color: #66cc66;">,</span> grayrange<span style="color: #66cc66;">,</span> color<span style="color: black;">&#41;</span>
    imsave<span style="color: black;">&#40;</span><span style="color: #483d8b;">'colored.bmp'</span><span style="color: #66cc66;">,</span> outputim<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">if __name__ == &quot;__main__&quot;:
    inputim = imread('river.bmp')
    grayrange = (inputim.min(), inputim.min() + 20)
    color = (0xFF, 0x00, 0x00)
    outputim = color_threshold(inputim, grayrange, color)
    imsave('colored.bmp', outputim)</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
A idéia deste exemplo é colorir partes de uma imagem em escala de cinza com alguma cor, objetivando destacar certa região. Uma aplicação precisa destacar regiões mais prováveis de encontrarmos água a partir de uma imagem em escala de cinza. Tomando o rio como referência, podemos usar os tons presente neste para definir os intervalos de thresholding. Assim, há maior probabilidade de encontrarmos água nas regiões pintadas:

<center>
  </p> 
  
  <table>
    <tr>
      <td>
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/river_small.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/river_small.jpg" alt="" title="river_small" width="410" height="409" class="aligncenter size-full wp-image-907" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/river_small.jpg 410w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/river_small-300x300.jpg 300w" sizes="(max-width: 410px) 100vw, 410px" /></a>
      </td>
      
      <td>
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/colored_small.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/colored_small.jpg" alt="" title="colored_small" width="410" height="409" class="aligncenter size-full wp-image-908" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/colored_small.jpg 410w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/colored_small-300x300.jpg 300w" sizes="(max-width: 410px) 100vw, 410px" /></a>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
  
  <p>
    Para fazer isso, usamos a função abaixo, que recebe uma imagem em escala de cinzas, o intervalo dos pontos de corte utilizados para segmentar quais valores da escala serão coloridos e a cor para pintar a região.
  </p>
  
  <pre lang="python">def color_threshold(im, rr, cc):
    """
    Convert a range of grayscale values in a RGB color.

    Parameters
    ----------
    * im: image (numpy matrix)
    * rr: range of threshold (2 elements tuple)
    * cc: RGB color (3 elemnts tuple -- (R,G,B) )

    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    """
    inputR = im
    inputG = im
    inputB = im
    R = cc[0]
    G = cc[1]
    B = cc[2]
    Om = zeros((im.shape[0], im.shape[1], 3))
    for i in xrange(rr[0], rr[1]):
        inputR = (inputR == i).choose(inputR, R)
        inputG = (inputG == i).choose(inputG, G)
        inputB = (inputB == i).choose(inputB, B)
    Om[:,:,0] = inputR
    Om[:,:,1] = inputG
    Om[:,:,2] = inputB
    return Om</pre>
  
  <p>
    Utilizamos esta função da seguinte forma:
  </p>
  
  <pre lang="python">if __name__ == "__main__":
    inputim = imread('river.bmp')
    grayrange = (inputim.min(), inputim.min() + 20)
    color = (0xFF, 0x00, 0x00)
    outputim = color_threshold(inputim, grayrange, color)
    imsave('colored.bmp', outputim)</pre>
  
  <p>
    Este exemplo está disponível em <a href="http://www.sawp.com.br/code/ip/pots49_color_threashold.zip">http://www.sawp.com.br/code/ip/pots49_color_threashold.zip</a>
  </p>
