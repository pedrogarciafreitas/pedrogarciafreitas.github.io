---
id: 919
title: 'imresize &#8212; Alterando as Dimensões da Imagem'
date: 2011-01-07T09:02:53+00:00
author: SAWP
excerpt: Embora o scipy. misc implemente esta função, fica aqui um exemplo simples de dimensionamento de imagens através de interpolação.
layout: post
guid: http://www.sawp.com.br/blog/?p=919
permalink: /p=919
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4450:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> imresize<span style="color: black;">&#40;</span>arr<span style="color: #66cc66;">,</span> newsize<span style="color: #66cc66;">,</span> interp<span style="color: #66cc66;">=</span><span style="color: #483d8b;">'bicubic'</span><span style="color: #66cc66;">,</span> mode<span style="color: #66cc66;">=</span><span style="color: #008000;">None</span><span style="color: black;">&#41;</span>:
    arr <span style="color: #66cc66;">=</span> asarray<span style="color: black;">&#40;</span>arr<span style="color: black;">&#41;</span>
    im <span style="color: #66cc66;">=</span> toimage<span style="color: black;">&#40;</span>arr<span style="color: #66cc66;">,</span>mode<span style="color: #66cc66;">=</span>mode<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>newsize<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #dc143c;">types</span>.<span style="color: black;">IntType</span>:
    newsize <span style="color: #66cc66;">=</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>newsize<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span><span style="color: black;">&#40;</span>newsize<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #dc143c;">types</span>.<span style="color: black;">FloatType</span>:
    newsize <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>im.<span style="color: black;">size</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> * newsize<span style="color: #66cc66;">,</span> im.<span style="color: black;">size</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> * newsize<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    newsize <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>newsize<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> newsize<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    func <span style="color: #66cc66;">=</span> <span style="color: black;">&#123;</span><span style="color: #483d8b;">'nearest'</span>:<span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span><span style="color: #483d8b;">'bilinear'</span>:<span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span><span style="color: #483d8b;">'bicubic'</span>:<span style="color: #ff4500;">3</span><span style="color: #66cc66;">,</span><span style="color: #483d8b;">'cubic'</span>:<span style="color: #ff4500;">3</span><span style="color: black;">&#125;</span>
    im <span style="color: #66cc66;">=</span> im.<span style="color: black;">resize</span><span style="color: black;">&#40;</span>newsize<span style="color: #66cc66;">,</span>resample<span style="color: #66cc66;">=</span>func<span style="color: black;">&#91;</span>interp<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> fromimage<span style="color: black;">&#40;</span>im<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def imresize(arr, newsize, interp='bicubic', mode=None):
    arr = asarray(arr)
    im = toimage(arr,mode=mode)
    if type(newsize) is types.IntType:
    newsize = float(newsize)
    if type(newsize) is types.FloatType:
    newsize = (im.size[0] * newsize, im.size[1] * newsize)
    else:
    newsize = (newsize[1], newsize[0])
    func = {'nearest':0,'bilinear':2,'bicubic':3,'cubic':3}
    im = im.resize(newsize,resample=func[interp])
    return fromimage(im)</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
Podemos alterar as dimensões de uma imagem (representada como uma matriz de tipo _numpy array_) utilizando a seguinte função:

<pre lang="python">def imresize(arr, newsize, interp='bicubic', mode=None):
    arr = asarray(arr)
    im = toimage(arr,mode=mode)
    if type(newsize) is types.IntType:
        newsize = float(newsize)
    if type(newsize) is types.FloatType:
        newsize = (im.size[0] * newsize, im.size[1] * newsize)
    else:
        newsize = (newsize[1], newsize[0])
    func = {'nearest':0,'bilinear':2,'bicubic':3,'cubic':3}
    im = im.resize(newsize,resample=func[interp])
    return fromimage(im)</pre>

No caso, o primeiro parâmetro _arr_ precisa ser uma matriz. _newsize_ deve ser um inteiro ou ponto flutuante, indicando a proporção do redimensionamento, ou uma dupla contendo as novas largura e altura. O parâmetro _interp_ indica qual algoritmo utilizado na interpolação.
