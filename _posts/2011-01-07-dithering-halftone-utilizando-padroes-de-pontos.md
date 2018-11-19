---
id: 940
title: 'Dithering &#8212; Parte I &#8212; Halftone via Pontilhado Ordenado'
date: 2011-01-07T18:42:21+00:00
author: SAWP
excerpt: 'Halftone (meio-tom) é uma técnica de processamento de imagens que objetiva gerar uma ilusão ótica na imagem para que ela aparente ter mais tons do que realmente possui. '
layout: post
guid: http://www.sawp.com.br/blog/?p=940
permalink: p=940
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:22793:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> halftone<span style="color: black;">&#40;</span>im<span style="color: #66cc66;">,</span> predown <span style="color: #66cc66;">=</span> <span style="color: #008000;">True</span><span style="color: #66cc66;">,</span> histeq <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Convert a image from grayscale image to binary image using halftone
    &nbsp;
    Parameters
    ----------
    * im: numpy matrix (image)
    * predown: boolean (default True)
    divide original image by 3 before halftoning
    * histeq: boolean (default False)
    perform a histogram equalization before halftone
    &nbsp;
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    &quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> halft<span style="color: black;">&#40;</span>im<span style="color: black;">&#41;</span>:
    <span style="color: #808080; font-style: italic;"># provides the threshold levels for binarization</span>
    level9 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level8 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level7 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level6 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level5 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level4 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level3 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level2 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level1 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    level0 <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># create and rescale new image to fit levels</span>
    <span style="color: black;">&#40;</span>h<span style="color: #66cc66;">,</span>l<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> im.<span style="color: black;">shape</span>
    masked <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">10.0</span> / <span style="color: #ff4500;">255.0</span><span style="color: black;">&#41;</span> * im
    masked <span style="color: #66cc66;">=</span> ceil<span style="color: black;">&#40;</span>masked<span style="color: black;">&#41;</span>
    rIm <span style="color: #66cc66;">=</span> zeros<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">3</span> * h<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">3</span> * l<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># generate the halftoned image_path</span>
    k <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    r <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>h<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>l<span style="color: black;">&#41;</span>:
    mask <span style="color: #66cc66;">=</span> masked<span style="color: black;">&#91;</span>i<span style="color: #66cc66;">,</span> j<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">1</span>:
    selected <span style="color: #66cc66;">=</span> level0
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">2</span>:
    selected <span style="color: #66cc66;">=</span> level1
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">3</span>:
    selected <span style="color: #66cc66;">=</span> level2
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span>:
    selected <span style="color: #66cc66;">=</span> level3
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">5</span>:
    selected <span style="color: #66cc66;">=</span> level4
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">6</span>:
    selected <span style="color: #66cc66;">=</span> level5
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">7</span>:
    selected <span style="color: #66cc66;">=</span> level6
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">8</span>:
    selected <span style="color: #66cc66;">=</span> level7
    <span style="color: #ff7700;font-weight:bold;">elif</span> mask <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">9</span>:
    selected <span style="color: #66cc66;">=</span> level8
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    selected <span style="color: #66cc66;">=</span> level9
    xs <span style="color: #66cc66;">=</span> i + k
    xf <span style="color: #66cc66;">=</span> i + k + <span style="color: #ff4500;">3</span>
    ys <span style="color: #66cc66;">=</span> j + r
    yf <span style="color: #66cc66;">=</span> j + r + <span style="color: #ff4500;">3</span>
    &nbsp;
    rIm<span style="color: black;">&#91;</span>xs:xf<span style="color: #66cc66;">,</span> ys:yf<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> selected<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: black;">&#93;</span>
    r <span style="color: #66cc66;">=</span> r + <span style="color: #ff4500;">2</span>
    r <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    k <span style="color: #66cc66;">=</span> k + <span style="color: #ff4500;">2</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> rIm
    &nbsp;
    <span style="color: #808080; font-style: italic;"># try generate halftoned image with original size</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> predown <span style="color: #66cc66;">==</span> <span style="color: #008000;">True</span>:
    im <span style="color: #66cc66;">=</span> imresize<span style="color: black;">&#40;</span>im<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1.0</span> / <span style="color: #ff4500;">3.0</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> histeq <span style="color: #66cc66;">==</span> <span style="color: #008000;">False</span>:
    retIm <span style="color: #66cc66;">=</span> halft<span style="color: black;">&#40;</span>im<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    equalized <span style="color: #66cc66;">=</span> normalize<span style="color: black;">&#40;</span>im<span style="color: black;">&#41;</span>
    equalized <span style="color: #66cc66;">=</span> halft<span style="color: black;">&#40;</span>equalized<span style="color: black;">&#41;</span>
    retIm <span style="color: #66cc66;">=</span> equalized
    retIm <span style="color: #66cc66;">=</span> halft<span style="color: black;">&#40;</span>im<span style="color: black;">&#41;</span>
    retIm <span style="color: #66cc66;">=</span> ceil<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>equalized + retIm<span style="color: black;">&#41;</span> * <span style="color: #ff4500;">0.5</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> retIm</pre></td></tr></table><p class="theCode" style="display:none;">def halftone(im, predown = True, histeq = False):
    &quot;&quot;&quot;
    Convert a image from grayscale image to binary image using halftone
    
    Parameters
    ----------
    * im: numpy matrix (image)
    * predown: boolean (default True)
    divide original image by 3 before halftoning
    * histeq: boolean (default False)
    perform a histogram equalization before halftone
    
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    &quot;&quot;&quot;
    def halft(im):
    # provides the threshold levels for binarization
    level9 = array([[1,1,1],[1,1,1],[1,1,1]])
    level8 = array([[1,0,1],[1,1,1],[1,1,1]])
    level7 = array([[1,0,1],[1,1,1],[1,1,0]])
    level6 = array([[0,0,1],[1,1,1],[1,1,0]])
    level5 = array([[0,0,1],[1,1,1],[1,0,1]])
    level4 = array([[0,0,0],[1,1,1],[0,1,0]])
    level3 = array([[0,0,0],[1,1,0],[0,1,0]])
    level2 = array([[0,0,0],[1,1,0],[0,0,0]])
    level1 = array([[0,0,0],[0,1,0],[0,0,0]])
    level0 = array([[0,0,0],[0,0,0],[0,0,0]])
    
    # create and rescale new image to fit levels
    (h,l) = im.shape
    masked = (10.0 / 255.0) * im
    masked = ceil(masked)
    rIm = zeros((3 * h, 3 * l))
    
    # generate the halftoned image_path
    k = 0
    r = 0
    
    for i in xrange(h):
    for j in xrange(l):
    mask = masked[i, j]
    if mask == 1:
    selected = level0
    elif mask == 2:
    selected = level1
    elif mask == 3:
    selected = level2
    elif mask == 4:
    selected = level3
    elif mask == 5:
    selected = level4
    elif mask == 6:
    selected = level5
    elif mask == 7:
    selected = level6
    elif mask == 8:
    selected = level7
    elif mask == 9:
    selected = level8
    else:
    selected = level9
    xs = i + k
    xf = i + k + 3
    ys = j + r
    yf = j + r + 3
    
    rIm[xs:xf, ys:yf] = selected[:,:]
    r = r + 2
    r = 0
    k = k + 2
    return rIm
    
    # try generate halftoned image with original size
    if predown == True:
    im = imresize(im, 1.0 / 3.0)
    if histeq == False:
    retIm = halft(im)
    else:
    equalized = normalize(im)
    equalized = halft(equalized)
    retIm = equalized
    retIm = halft(im)
    retIm = ceil((equalized + retIm) * 0.5)
    return retIm</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
Halftone (meio-tom) é uma técnica de processamento de imagens que emprega padrões de pontos pretos ou brancos para reduzir o número de níveis de cinza de uma representação. Devido ao fato do sistema visual humano atenuar a distinção entre os pontos com tons diferentes, os padrões de pontos pretos e brancos produzem um efeito visual como se a imagem fosse composta por mais tons de cinza.

Esta técnica é muito utilizada em aplicações de impressão em jornais e faxes, onde apenas os níveis brancos e pretos são necessários. Há diferentes abordagens para produção de tais padrões, tais como o pontilhado ordenado (_ordered dithering_) e pontilhado com difusão de erro (_dithered with error difusion_).

Neste exemplo, implementamos um algoritmo de halftoning típico para impressão, baseado em padrões de pontos com pontilhado ordenado. A figura abaixo mostra os padrões que podem ser utilizados para aproximar dez níveis de cinza:
  


<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos1.jpg" alt="" title="padroesdepontos" width="707" height="320" class="aligncenter size-full wp-image-999" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos1.jpg 707w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos1-300x135.jpg 300w" sizes="(max-width: 707px) 100vw, 707px" /></a><br />
</center>

Cada conjunto de níveis de cinza é representado por um padrão \(3 \times 3\) de pontos brancos ou pretos. Uma área de \(3 \times 3\) pixels cheia de pontos pretos é uma aproximação de um nível de cinza preto (ou 0). De forma análoga, uma área \(3 \times 3\) de pontos totalmente brancos será uma aproximação do branco em uma escala de nível de cinza (ou 9). Os demais padrões intermediários entre \(]0, 255[ \) serão re-escalados para o intervalo \([0, 9]\), conforme ilustrado na imagem abaixo.

<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/escalas.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/escalas.jpg" alt="" title="escalas" width="500" height="400" class="aligncenter size-full wp-image-947" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/escalas.jpg 500w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/escalas-300x240.jpg 300w" sizes="(max-width: 500px) 100vw, 500px" /></a><br />
</center>

É possível notar que utilizamos nove limiares (_threshold_) para a sub-codificação: o intervalo \([0, 25.5[ \) é truncado para \(0 \), \([25.5, 51[ \) é truncado para \(1 \), \([51, 76.5[\) para \(2 \), e assim por diante. Assim, cada pixel na imagem de entrada irá corresponder a um padrão de \(3 \times 3 \) pixels na imagem gerada. Desta forma, a resolução espacial será reduzida a \(33\% \) da resolução espacial original. Isto é, antes da substituição de cada pixel pela máscara devemos reduzir em \(\frac{1}{3} \) as dimensões da imagem para que o resultado tenha o mesmo tamanho da original.

Todo o processo descrito é implementado na seguinte função;

<pre lang="python">def halftone(im, predown = True, histeq = False):
    """
    Convert a image from grayscale image to binary image using halftone

    Parameters
    ----------
    * im: numpy matrix (image)
    * predown: boolean (default True)
        divide original image by 3 before halftoning
    * histeq: boolean (default False)
        perform a histogram equalization before halftone

    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2010 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    """
    def halft(im):
        # provides the threshold levels for binarization
        level9 = array([[1,1,1],[1,1,1],[1,1,1]])
        level8 = array([[1,0,1],[1,1,1],[1,1,1]])
        level7 = array([[1,0,1],[1,1,1],[1,1,0]])
        level6 = array([[0,0,1],[1,1,1],[1,1,0]])
        level5 = array([[0,0,1],[1,1,1],[1,0,1]])
        level4 = array([[0,0,0],[1,1,1],[0,1,0]])
        level3 = array([[0,0,0],[1,1,0],[0,1,0]])
        level2 = array([[0,0,0],[1,1,0],[0,0,0]])
        level1 = array([[0,0,0],[0,1,0],[0,0,0]])
        level0 = array([[0,0,0],[0,0,0],[0,0,0]])

        # create and rescale new image to fit levels
        (h,l) = im.shape
        masked = (10.0 / 255.0) * im
        masked = ceil(masked)
        rIm = zeros((3 * h, 3 * l))

        # generate the halftoned image_path
        k = 0
        r = 0

        for i in xrange(h):
            for j in xrange(l):
                mask = masked[i, j]
                if mask == 1:
                    selected = level0
                elif mask == 2:
                    selected = level1
                elif mask == 3:
                    selected = level2
                elif mask == 4:
                    selected = level3
                elif mask == 5:
                    selected = level4
                elif mask == 6:
                    selected = level5
                elif mask == 7:
                    selected = level6
                elif mask == 8:
                    selected = level7
                elif mask == 9:
                    selected = level8
                else:
                    selected = level9
                xs = i + k
                xf = i + k + 3
                ys = j + r
                yf = j + r + 3
                
                rIm[xs:xf, ys:yf] = selected[:,:]
                r = r + 2
            r = 0
            k = k + 2
        return rIm

    # try generate halftoned image with original size
    if predown == True:
        im = imresize(im, 1.0 / 3.0)
    if histeq == False:
        retIm = halft(im)
    else:
        equalized = normalize(im)
        equalized = halft(equalized)
        retIm = equalized
        retIm = halft(im)
        retIm = ceil((equalized + retIm) * 0.5)
    return retIm</pre>

Os resultados do retorno desta função podem ser vistos abaixo:

<center>
  </p> 
  
  <table>
    <tr>
      <td>
        <center>
          <br /> Original (parâmetro)<br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> Halftoned (retorno)<br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_resized.jpg" alt="" title="flower_resized" width="256" height="256" class="aligncenter size-full wp-image-956" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_halftoned.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/flower_halftoned.jpg" alt="" title="flower_halftoned" width="255" height="255" class="aligncenter size-full wp-image-957" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized.jpg" alt="" title="lena_resized" width="256" height="256" class="aligncenter size-full wp-image-960" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_halftoned.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_halftoned.jpg" alt="" title="lena_halftoned" width="255" height="255" class="aligncenter size-full wp-image-961" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized.jpg" alt="" title="degrade_resized" width="256" height="256" class="aligncenter size-full wp-image-962" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_halftoned.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_halftoned.jpg" alt="" title="degrade_halftoned" width="255" height="255" class="aligncenter size-full wp-image-963" /></a><br />
        </center>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
