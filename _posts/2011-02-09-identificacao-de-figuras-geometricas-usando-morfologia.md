---
id: 1092
title: Identificação de Figuras Geométricas usando Morfologia
date: 2011-02-09T08:55:34+00:00
author: SAWP
excerpt: Neste post veremos como utilizar operações de conjuntos e lógicas para reconhecimento de padrões simples.
layout: post
guid: http://www.sawp.com.br/blog/?p=1092
permalink: p=1092
wp-syntax-cache-content:
  - |
    a:9:{i:1;s:1598:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">from</span> numpy <span style="color: #ff7700;font-weight:bold;">import</span> logical_xor <span style="color: #ff7700;font-weight:bold;">as</span> xor
    <span style="color: #ff7700;font-weight:bold;">from</span> numpy <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">array</span>
    <span style="color: #ff7700;font-weight:bold;">from</span> scipy.<span style="color: black;">misc</span>.<span style="color: black;">pilutil</span> <span style="color: #ff7700;font-weight:bold;">import</span> imsave<span style="color: #66cc66;">,</span> imread
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> binary
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> blob
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> close_holes
    <span style="color: #ff7700;font-weight:bold;">from</span> pymorph <span style="color: #ff7700;font-weight:bold;">import</span> label</pre></td></tr></table><p class="theCode" style="display:none;">from numpy import logical_xor as xor
    from numpy import array
    from scipy.misc.pilutil import imsave, imread
    from pymorph import binary
    from pymorph import blob
    from pymorph import close_holes
    from pymorph import label</p></div>
    ;i:2;s:711:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">f <span style="color: #66cc66;">=</span> imread<span style="color: black;">&#40;</span><span style="color: #483d8b;">'blocks1.png'</span><span style="color: #66cc66;">,</span> flatten<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    binaryImage <span style="color: #66cc66;">=</span> binary<span style="color: black;">&#40;</span>f<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">f = imread('blocks1.png', flatten=True)
    binaryImage = binary(f)</p></div>
    ;i:3;s:3338:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: black;">&#40;</span>N<span style="color: #66cc66;">,</span> M<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> binaryImage.<span style="color: black;">shape</span>
    totalOfPixels <span style="color: #66cc66;">=</span> N * M
    whitePixels <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>binaryImage <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>.<span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    blackPixels <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>binaryImage <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>.<span style="color: #008000;">sum</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    whitePixelsFraction <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #008000;">float</span><span style="color: black;">&#40;</span>whitePixels<span style="color: black;">&#41;</span> / <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>totalOfPixels<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * <span style="color: #ff4500;">100.0</span>
    blackPixelsFraction <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #008000;">float</span><span style="color: black;">&#40;</span>blackPixels<span style="color: black;">&#41;</span> / <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>totalOfPixels<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> * <span style="color: #ff4500;">100.0</span>
    output <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">&quot;(a) The image contains %d white pixels (%0.2f%%) &quot;</span>
    output +<span style="color: #66cc66;">=</span> <span style="color: #483d8b;">&quot;and %d black (%0.2f%%)&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Answers: &quot;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> output % <span style="color: black;">&#40;</span>whitePixels<span style="color: #66cc66;">,</span> whitePixelsFraction<span style="color: #66cc66;">,</span> \
    blackPixels<span style="color: #66cc66;">,</span> blackPixelsFraction<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">(N, M) = binaryImage.shape
    totalOfPixels = N * M
    whitePixels = (binaryImage &gt; 0).sum()
    blackPixels = (binaryImage == 0).sum()
    whitePixelsFraction = (float(whitePixels) / float(totalOfPixels)) * 100.0
    blackPixelsFraction = (float(blackPixels) / float(totalOfPixels)) * 100.0
    output = &quot;(a) The image contains %d white pixels (%0.2f%%) &quot;
    output += &quot;and %d black (%0.2f%%)&quot;
    print &quot;Answers: &quot;
    print output % (whitePixels, whitePixelsFraction, \
    blackPixels, blackPixelsFraction)</p></div>
    ;i:4;s:1863:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">binaryWithoutHoles <span style="color: #66cc66;">=</span> close_holes<span style="color: black;">&#40;</span>binaryImage<span style="color: black;">&#41;</span>
    labeledWithoutHoles <span style="color: #66cc66;">=</span> label<span style="color: black;">&#40;</span>binaryWithoutHoles<span style="color: black;">&#41;</span>
    objectsWithoutHolesArea <span style="color: #66cc66;">=</span> blob<span style="color: black;">&#40;</span>labeledWithoutHoles<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'area'</span><span style="color: #66cc66;">,</span> output<span style="color: #66cc66;">=</span><span style="color: #483d8b;">'data'</span><span style="color: black;">&#41;</span>
    objectsWithoutHolesArea <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span>objectsWithoutHolesArea<span style="color: black;">&#41;</span>
    recognizedObjects <span style="color: #66cc66;">=</span> objectsWithoutHolesArea.<span style="color: black;">shape</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;(b) The image have %d objects&quot;</span> % recognizedObjects</pre></td></tr></table><p class="theCode" style="display:none;">binaryWithoutHoles = close_holes(binaryImage)
    labeledWithoutHoles = label(binaryWithoutHoles)
    objectsWithoutHolesArea = blob(labeledWithoutHoles, 'area', output='data')
    objectsWithoutHolesArea = array(objectsWithoutHolesArea)
    recognizedObjects = objectsWithoutHolesArea.shape[0]
    print &quot;(b) The image have %d objects&quot; % recognizedObjects</p></div>
    ;i:5;s:1788:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">diff <span style="color: #66cc66;">=</span> xor<span style="color: black;">&#40;</span>binaryImage<span style="color: #66cc66;">,</span> binaryWithoutHoles<span style="color: black;">&#41;</span>
    labeledHoles <span style="color: #66cc66;">=</span> label<span style="color: black;">&#40;</span>diff<span style="color: black;">&#41;</span>
    holesCentroids <span style="color: #66cc66;">=</span> blob<span style="color: black;">&#40;</span>labeledHoles<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'centroid'</span><span style="color: #66cc66;">,</span> output<span style="color: #66cc66;">=</span><span style="color: #483d8b;">'data'</span><span style="color: black;">&#41;</span>
    holesCentroids <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span>holesCentroids<span style="color: black;">&#41;</span>
    numberOfDetectedHoles <span style="color: #66cc66;">=</span> holesCentroids.<span style="color: black;">shape</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;(c) The image have %d holes&quot;</span> % numberOfDetectedHoles</pre></td></tr></table><p class="theCode" style="display:none;">diff = xor(binaryImage, binaryWithoutHoles)
    labeledHoles = label(diff)
    holesCentroids = blob(labeledHoles, 'centroid', output='data')
    holesCentroids = array(holesCentroids)
    numberOfDetectedHoles = holesCentroids.shape[0]
    print &quot;(c) The image have %d holes&quot; % numberOfDetectedHoles</p></div>
    ;i:6;s:2293:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">labeledWithHoles <span style="color: #66cc66;">=</span> label<span style="color: black;">&#40;</span>binaryImage<span style="color: black;">&#41;</span>
    objectsWithHolesArea <span style="color: #66cc66;">=</span> blob<span style="color: black;">&#40;</span>labeledWithHoles<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'area'</span><span style="color: #66cc66;">,</span> output<span style="color: #66cc66;">=</span><span style="color: #483d8b;">'data'</span><span style="color: black;">&#41;</span>
    objectsWithHolesArea <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span>objectsWithHolesArea<span style="color: black;">&#41;</span>
    totalOfObjectsWithHoles <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>recognizedObjects<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> objectsWithoutHolesArea<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!=</span> objectsWithHolesArea<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>:
    totalOfObjectsWithHoles +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;(d) %d objects have one or more holes&quot;</span> % totalOfObjectsWithHoles</pre></td></tr></table><p class="theCode" style="display:none;">labeledWithHoles = label(binaryImage)
    objectsWithHolesArea = blob(labeledWithHoles, 'area', output='data')
    objectsWithHolesArea = array(objectsWithHolesArea)
    totalOfObjectsWithHoles = 0
    for i in xrange(recognizedObjects):
    if objectsWithoutHolesArea[i] != objectsWithHolesArea[i]:
    totalOfObjectsWithHoles += 1
    print &quot;(d) %d objects have one or more holes&quot; % totalOfObjectsWithHoles</p></div>
    ;i:7;s:2602:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">numberOfSquares <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    objectsWithoutHolesBB <span style="color: #66cc66;">=</span> blob<span style="color: black;">&#40;</span>labeledWithoutHoles<span style="color: #66cc66;">,</span> \
    <span style="color: #483d8b;">'boundingbox'</span><span style="color: #66cc66;">,</span> output<span style="color: #66cc66;">=</span><span style="color: #483d8b;">'data'</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>recognizedObjects<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: #66cc66;">,</span> x2<span style="color: #66cc66;">,</span> y2<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> objectsWithoutHolesBB<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    incorporatesRegionArea <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>x1 - x2<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>y1 - y2<span style="color: black;">&#41;</span>
    onlyObjectArea <span style="color: #66cc66;">=</span> objectsWithoutHolesArea<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> incorporatesRegionArea <span style="color: #66cc66;">==</span> onlyObjectArea:
    numberOfSquares +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;(e) The image contains %d squares&quot;</span> % numberOfSquares</pre></td></tr></table><p class="theCode" style="display:none;">numberOfSquares = 0
    objectsWithoutHolesBB = blob(labeledWithoutHoles, \
    'boundingbox', output='data')
    for i in xrange(recognizedObjects):
    (x1, y1, x2, y2) = objectsWithoutHolesBB[i]
    incorporatesRegionArea = (x1 - x2) * (y1 - y2)
    onlyObjectArea = objectsWithoutHolesArea[i]
    if incorporatesRegionArea == onlyObjectArea:
    numberOfSquares += 1
    print &quot;(e) The image contains %d squares&quot; % numberOfSquares</p></div>
    ;i:8;s:2566:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">perforatedSquares <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>recognizedObjects<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: #66cc66;">,</span> x2<span style="color: #66cc66;">,</span> y2<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> objectsWithoutHolesBB<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    incorporatesRegionArea <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>x1 - x2<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>y1 - y2<span style="color: black;">&#41;</span>
    onlyObjectWithoutHoleArea <span style="color: #66cc66;">=</span> objectsWithoutHolesArea<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    onlyObjectWithHoleArea <span style="color: #66cc66;">=</span> objectsWithHolesArea<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> incorporatesRegionArea <span style="color: #66cc66;">==</span> onlyObjectWithoutHoleArea <span style="color: #ff7700;font-weight:bold;">and</span> \
    onlyObjectWithoutHoleArea <span style="color: #66cc66;">!=</span> onlyObjectWithHoleArea:
    perforatedSquares +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;(f) %d squares are perfored&quot;</span> % perforatedSquares</pre></td></tr></table><p class="theCode" style="display:none;">perforatedSquares = 0
    for i in xrange(recognizedObjects):
    (x1, y1, x2, y2) = objectsWithoutHolesBB[i]
    incorporatesRegionArea = (x1 - x2) * (y1 - y2)
    onlyObjectWithoutHoleArea = objectsWithoutHolesArea[i]
    onlyObjectWithHoleArea = objectsWithHolesArea[i]
    if incorporatesRegionArea == onlyObjectWithoutHoleArea and \
    onlyObjectWithoutHoleArea != onlyObjectWithHoleArea:
    perforatedSquares += 1
    print &quot;(f) %d squares are perfored&quot; % perforatedSquares</p></div>
    ;i:9;s:2574:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">notPerforedCircles <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>recognizedObjects<span style="color: black;">&#41;</span>:
    <span style="color: black;">&#40;</span>x1<span style="color: #66cc66;">,</span> y1<span style="color: #66cc66;">,</span> x2<span style="color: #66cc66;">,</span> y2<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> objectsWithoutHolesBB<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    incorporatesRegionArea <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>x1 - x2<span style="color: black;">&#41;</span> * <span style="color: black;">&#40;</span>y1 - y2<span style="color: black;">&#41;</span>
    onlyObjectWithoutHoleArea <span style="color: #66cc66;">=</span> objectsWithoutHolesArea<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    onlyObjectWithHoleArea <span style="color: #66cc66;">=</span> objectsWithHolesArea<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> incorporatesRegionArea <span style="color: #66cc66;">!=</span> onlyObjectWithoutHoleArea <span style="color: #ff7700;font-weight:bold;">and</span> \
    onlyObjectWithoutHoleArea <span style="color: #66cc66;">==</span> onlyObjectWithHoleArea:
    notPerforedCircles +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;(f) %d circles have no holes&quot;</span> % notPerforedCircles</pre></td></tr></table><p class="theCode" style="display:none;">notPerforedCircles = 0
    for i in xrange(recognizedObjects):
    (x1, y1, x2, y2) = objectsWithoutHolesBB[i]
    incorporatesRegionArea = (x1 - x2) * (y1 - y2)
    onlyObjectWithoutHoleArea = objectsWithoutHolesArea[i]
    onlyObjectWithHoleArea = objectsWithHolesArea[i]
    if incorporatesRegionArea != onlyObjectWithoutHoleArea and \
    onlyObjectWithoutHoleArea == onlyObjectWithHoleArea:
    notPerforedCircles += 1
    print &quot;(f) %d circles have no holes&quot; % notPerforedCircles</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
Dada a imagem

<center>
  <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/02/blocks1.png"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/02/blocks1.png" alt="" title="blocks1" width="384" height="331" class="aligncenter size-full wp-image-1096" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/02/blocks1.png 384w, http://www.sawp.com.br/blog/wp-content/uploads/2011/02/blocks1-300x258.png 300w" sizes="(max-width: 384px) 100vw, 384px" /></a>
</center>

nosso problema é determinar os seguintes itens:

  * (a) Qual a fração de pixels da imagem são brancos?
  * (b) Quantos objetos estão na imagem?
  * (c) A imagem contém quantos buracos?
  * (d) Quantos objetos possuem um ou mais buracos?
  * (e) Quantos objetos quadrados estão presentes na imagem?
  * (f) Identifique os objetos quadrados que possuem buracos.
  * (g) Identifique os objetos circulares que não possuem buracos.

Para resolvermos este problema, necessitaremos das seguintes bibliotecas de processamento de imagens: <a href="http://www.mmorph.com/pymorph/"  target="_blank">PyMorph</a> e <a href="http://www.scipy.org/" target="_blank">SciPy</a>.

As funções utilizadas são declaradas no início do arquivo:

<pre lang="python">from numpy import logical_xor as xor
from numpy import array
from scipy.misc.pilutil import imsave, imread
from pymorph import binary
from pymorph import blob
from pymorph import close_holes
from pymorph import label</pre>

Considerando que a imagem em questão se chama &#8216;blocks1.png&#8217;, abrimos esta imagem e garantimos uma representação binária para os demais processamentos:

<pre lang="python">f = imread('blocks1.png', flatten=True)
binaryImage = binary(f)</pre>

Agora resolvemos os itens

**(a) Qual a fração de pixels da imagem são brancos?**

<pre lang="python">(N, M) = binaryImage.shape
totalOfPixels = N * M
whitePixels = (binaryImage > 0).sum()
blackPixels = (binaryImage == 0).sum()
whitePixelsFraction = (float(whitePixels) / float(totalOfPixels)) * 100.0
blackPixelsFraction = (float(blackPixels) / float(totalOfPixels)) * 100.0
output = "(a) The image contains %d white pixels (%0.2f%%) "
output += "and %d black (%0.2f%%)"
print "Answers: "
print output % (whitePixels, whitePixelsFraction, \
                blackPixels, blackPixelsFraction)</pre>

**(b) Quantos objetos estão na imagem?**

<pre lang="python">binaryWithoutHoles = close_holes(binaryImage)
labeledWithoutHoles = label(binaryWithoutHoles)
objectsWithoutHolesArea = blob(labeledWithoutHoles, 'area', output='data')
objectsWithoutHolesArea = array(objectsWithoutHolesArea)
recognizedObjects = objectsWithoutHolesArea.shape[0]
print "(b) The image have %d objects" % recognizedObjects</pre>

**(c) A imagem contém quantos buracos?**

<pre lang="python">diff = xor(binaryImage, binaryWithoutHoles)
labeledHoles = label(diff)
holesCentroids = blob(labeledHoles, 'centroid', output='data')
holesCentroids = array(holesCentroids)
numberOfDetectedHoles = holesCentroids.shape[0]
print "(c) The image have %d holes" % numberOfDetectedHoles</pre>

**(d) Quantos objetos possuem um ou mais buracos?**

<pre lang="python">labeledWithHoles = label(binaryImage)
objectsWithHolesArea = blob(labeledWithHoles, 'area', output='data')
objectsWithHolesArea = array(objectsWithHolesArea)
totalOfObjectsWithHoles = 0
for i in xrange(recognizedObjects):
    if objectsWithoutHolesArea[i] != objectsWithHolesArea[i]:
        totalOfObjectsWithHoles += 1
print "(d) %d objects have one or more holes" % totalOfObjectsWithHoles</pre>

**(e) Quantos objetos quadrados estão presentes na imagem?**

<pre lang="python">numberOfSquares = 0
objectsWithoutHolesBB = blob(labeledWithoutHoles, \
                             'boundingbox', output='data')
for i in xrange(recognizedObjects):
    (x1, y1, x2, y2) = objectsWithoutHolesBB[i]
    incorporatesRegionArea = (x1 - x2) * (y1 - y2)
    onlyObjectArea = objectsWithoutHolesArea[i]
    if incorporatesRegionArea == onlyObjectArea:
        numberOfSquares += 1
print "(e) The image contains %d squares" % numberOfSquares</pre>

**(f) Identifique os objetos quadrados que possuem buracos.**

<pre lang="python">perforatedSquares = 0
for i in xrange(recognizedObjects):
    (x1, y1, x2, y2) = objectsWithoutHolesBB[i]
    incorporatesRegionArea = (x1 - x2) * (y1 - y2)
    onlyObjectWithoutHoleArea = objectsWithoutHolesArea[i]
    onlyObjectWithHoleArea = objectsWithHolesArea[i]
    if incorporatesRegionArea == onlyObjectWithoutHoleArea and \
       onlyObjectWithoutHoleArea != onlyObjectWithHoleArea:
        perforatedSquares += 1
print "(f) %d squares are perfored" % perforatedSquares</pre>

**(g) Identifique os objetos circulares que não possuem buracos.**

<pre lang="python">notPerforedCircles = 0
for i in xrange(recognizedObjects):
    (x1, y1, x2, y2) = objectsWithoutHolesBB[i]
    incorporatesRegionArea = (x1 - x2) * (y1 - y2)
    onlyObjectWithoutHoleArea = objectsWithoutHolesArea[i]
    onlyObjectWithHoleArea = objectsWithHolesArea[i]
    if incorporatesRegionArea != onlyObjectWithoutHoleArea and \
       onlyObjectWithoutHoleArea == onlyObjectWithHoleArea:
        notPerforedCircles += 1
print "(f) %d circles have no holes" % notPerforedCircles</pre>
