---
id: 1101
title: Contagem de Moedas Utilizando Processamento de Imagens
date: 2011-02-09T09:01:23+00:00
author: SAWP
excerpt: Como utilizar morfologia matemática em processamento de imagens para contagem automática de dinheiro? Neste post veremos um exemplo de reconhecimento simples de padrões.
layout: post
guid: http://www.sawp.com.br/blog/?p=1101
permalink: p=1101
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5497:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">from</span> numpy <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">array</span>
    <span style="color: #ff7700;font-weight:bold;">from</span> scipy.<span style="color: black;">misc</span>.<span style="color: black;">pilutil</span> <span style="color: #ff7700;font-weight:bold;">import</span> imsave<span style="color: #66cc66;">,</span> imread<span style="color: #66cc66;">,</span> imresize
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> add4dilate
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> binary
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> blob
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> close_holes
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> label
    &nbsp;
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'__main__'</span>:
    f <span style="color: #66cc66;">=</span> imread<span style="color: black;">&#40;</span><span style="color: #483d8b;">'coins.bmp'</span><span style="color: #66cc66;">,</span> flatten<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    binaryImage <span style="color: #66cc66;">=</span> binary<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> k<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>
    binaryImage <span style="color: #66cc66;">=</span> add4dilate<span style="color: black;">&#40;</span>binaryImage<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">8</span><span style="color: black;">&#41;</span>
    binaryImage <span style="color: #66cc66;">=</span> close_holes<span style="color: black;">&#40;</span>binaryImage<span style="color: black;">&#41;</span>
    labeled <span style="color: #66cc66;">=</span> label<span style="color: black;">&#40;</span>binaryImage<span style="color: black;">&#41;</span>
    areasOfCoins <span style="color: #66cc66;">=</span> blob<span style="color: black;">&#40;</span>labeled<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'area'</span><span style="color: #66cc66;">,</span> output<span style="color: #66cc66;">=</span><span style="color: #483d8b;">'data'</span><span style="color: black;">&#41;</span>
    areasOfCoins <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span>areasOfCoins<span style="color: black;">&#41;</span>
    numberOfCoins <span style="color: #66cc66;">=</span> areasOfCoins.<span style="color: black;">shape</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    totalValue <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0.0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>numberOfCoins<span style="color: black;">&#41;</span>:
    coinArea <span style="color: #66cc66;">=</span> areasOfCoins<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> coinArea <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">2000</span>:
    totalValue <span style="color: #66cc66;">=</span> totalValue + <span style="color: #ff4500;">0.50</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    totalValue <span style="color: #66cc66;">=</span> totalValue + <span style="color: #ff4500;">0.05</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> areasOfCoins
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'Total value is $%0.2f'</span> % totalValue</pre></td></tr></table><p class="theCode" style="display:none;">from numpy import array
    from scipy.misc.pilutil import imsave, imread, imresize
    from pymorph import add4dilate
    from pymorph import binary
    from pymorph import blob
    from pymorph import close_holes
    from pymorph import label
    
    
    if __name__ == '__main__':
    f = imread('coins.bmp', flatten=True)
    binaryImage = binary(f, k=100)
    binaryImage = add4dilate(binaryImage, 8)
    binaryImage = close_holes(binaryImage)
    labeled = label(binaryImage)
    areasOfCoins = blob(labeled, 'area', output='data')
    areasOfCoins = array(areasOfCoins)
    numberOfCoins = areasOfCoins.shape[0]
    totalValue = 0.0
    for i in xrange(numberOfCoins):
    coinArea = areasOfCoins[i]
    if coinArea &gt; 2000:
    totalValue = totalValue + 0.50
    else:
    totalValue = totalValue + 0.05
    print areasOfCoins
    print 'Total value is $%0.2f' % totalValue</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
<center>
  <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/02/coins.bmp"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/02/coins.bmp" alt="" title="coins" class="aligncenter size-full wp-image-1102" /></a>
</center>

O seguinte programa serve para calcular a quantidade de dinheiro a partir de uma imagem contendo moedas, tal como a figura acima. Note que a biblioteca <a href="http://www.mmorph.com/pymorph/" target="_blank">PyMorph</a> deve estar devidamente instalada no ambiente.

<pre lang="python">from numpy import array
from scipy.misc.pilutil import imsave, imread, imresize
from pymorph import add4dilate
from pymorph import binary
from pymorph import blob
from pymorph import close_holes
from pymorph import label


if __name__ == '__main__':
    f = imread('coins.bmp', flatten=True)
    binaryImage = binary(f, k=100)
    binaryImage = add4dilate(binaryImage, 8)
    binaryImage = close_holes(binaryImage)
    labeled = label(binaryImage)
    areasOfCoins = blob(labeled, 'area', output='data')
    areasOfCoins = array(areasOfCoins)
    numberOfCoins = areasOfCoins.shape[0]
    totalValue = 0.0
    for i in xrange(numberOfCoins):
        coinArea = areasOfCoins[i]
        if coinArea > 2000:
            totalValue = totalValue + 0.50
        else:
            totalValue = totalValue + 0.05
    print areasOfCoins
    print 'Total value is $%0.2f' % totalValue</pre>
