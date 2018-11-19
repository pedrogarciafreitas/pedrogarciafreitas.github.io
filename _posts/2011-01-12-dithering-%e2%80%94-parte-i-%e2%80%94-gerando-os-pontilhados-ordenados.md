---
id: 1001
title: 'Dithering &#8212; Parte II &#8212; Gerando os Pontilhados Ordenados'
date: 2011-01-12T20:11:28+00:00
author: SAWP
excerpt: Continuando o Post anterior, neste texto apresentamos a formulação por trás da geração das máscaras de pixels nos métodos de halftone via pontilhado ordenado.
layout: post
guid: http://www.sawp.com.br/blog/?p=1001
permalink: p=1001
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:4675:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> generate_mask<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return dot-pattern matrix of indicies for ordered dithering of 2^n order
    &nbsp;
    Parameters
    ----------
    * n: order of mask (must be even), integer
    &nbsp;
    Return
    ----------
    * mask: numpy matrix with dot patter order to generate ordered dithering
    &nbsp;
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    &quot;&quot;&quot;</span>
    mask <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: #66cc66;">,</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    mask_order <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span>
    <span style="color: #ff7700;font-weight:bold;">while</span> mask_order <span style="color: #66cc66;">&lt;</span> n:
    u <span style="color: #66cc66;">=</span> ones<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>mask_order<span style="color: #66cc66;">,</span> mask_order<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    m11 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">4</span> * mask + <span style="color: #ff4500;">2</span> * u
    m12 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">4</span> * mask
    m21 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">4</span> * mask + u
    m22 <span style="color: #66cc66;">=</span> mask + u
    top <span style="color: #66cc66;">=</span> concatenate<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>m11<span style="color: #66cc66;">,</span> m12<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> axis<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    down <span style="color: #66cc66;">=</span> concatenate<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>m21<span style="color: #66cc66;">,</span> m22<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> axis<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    mask <span style="color: #66cc66;">=</span> concatenate<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>top<span style="color: #66cc66;">,</span> down<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> axis<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>
    mask_order <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span> * mask_order
    <span style="color: #ff7700;font-weight:bold;">return</span> mask</pre></td></tr></table><p class="theCode" style="display:none;">def generate_mask(n):
    &quot;&quot;&quot;
    Return dot-pattern matrix of indicies for ordered dithering of 2^n order
    
    Parameters
    ----------
    * n: order of mask (must be even), integer
    
    Return
    ----------
    * mask: numpy matrix with dot patter order to generate ordered dithering
    
    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    &quot;&quot;&quot;
    mask = array([[0, 2], [3,1]])
    mask_order = 2
    while mask_order &lt; n:
    u = ones((mask_order, mask_order))
    m11 = 4 * mask + 2 * u
    m12 = 4 * mask
    m21 = 4 * mask + u
    m22 = mask + u
    top = concatenate((m11, m12), axis=1)
    down = concatenate((m21, m22), axis=1)
    mask = concatenate((top, down), axis=0)
    mask_order = 2 * mask_order
    return mask</p></div>
    ;i:2;s:3232:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> generate_ordered_dithering<span style="color: black;">&#40;</span>mask<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return a set of ordered dithering dot patterns
    &nbsp;
    Parameters
    ----------
    * mask: numpy matrix with mask order
    &nbsp;
    Return
    ----------
    * dot_pattern: numpy matrix all dot patterns
    &nbsp;
    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    &quot;&quot;&quot;</span>
    <span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> mask.<span style="color: black;">shape</span>
    total <span style="color: #66cc66;">=</span> m * n - <span style="color: #ff4500;">1</span>
    dot_pattern <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>zeros<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>m<span style="color: #66cc66;">,</span> m<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>total<span style="color: black;">&#41;</span>:
    last <span style="color: #66cc66;">=</span> dot_pattern<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
    <span style="color: #dc143c;">new</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>mask <span style="color: #66cc66;">==</span> i<span style="color: black;">&#41;</span>
    dot_pattern.<span style="color: black;">append</span><span style="color: black;">&#40;</span>last + <span style="color: #dc143c;">new</span><span style="color: black;">&#41;</span>
    dot_pattern <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">array</span><span style="color: black;">&#40;</span>dot_pattern<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> dot_pattern</pre></td></tr></table><p class="theCode" style="display:none;">def generate_ordered_dithering(mask):
    &quot;&quot;&quot;
    Return a set of ordered dithering dot patterns
    
    Parameters
    ----------
    * mask: numpy matrix with mask order
    
    Return
    ----------
    * dot_pattern: numpy matrix all dot patterns
    
    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    &quot;&quot;&quot;
    (m, n) = mask.shape
    total = m * n - 1
    dot_pattern = [zeros((m, m))]
    for i in xrange(total):
    last = dot_pattern[i]
    new = (mask == i)
    dot_pattern.append(last + new)
    dot_pattern = array(dot_pattern)
    return dot_pattern</p></div>
    ;i:3;s:5903:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> ordered_dithering<span style="color: black;">&#40;</span>image<span style="color: #66cc66;">,</span> masks<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Convert a grayscale image in binary halftone image with n levels.
    &nbsp;
    Parameters
    ----------
    * image: numpy matrix, original grayscale image
    * masks: numpy array, set with all dot patterns used in halftone
    &nbsp;
    Return
    ----------
    * binary: numpy matrix, dithered binary image
    &nbsp;
    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas
    &nbsp;
    see: http://www.sawp.com.br
    &quot;&quot;&quot;</span>
    <span style="color: #808080; font-style: italic;"># create and rescale new image to fit levels</span>
    <span style="color: black;">&#40;</span>levels<span style="color: #66cc66;">,</span> m<span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> masks.<span style="color: black;">shape</span>
    <span style="color: black;">&#40;</span>h<span style="color: #66cc66;">,</span> l<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> image.<span style="color: black;">shape</span>
    <span style="color: black;">&#40;</span>step_x<span style="color: #66cc66;">,</span> step_y<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> masks<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>.<span style="color: black;">shape</span>
    masked <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>levels / <span style="color: #ff4500;">255.0</span><span style="color: black;">&#41;</span> * image
    masked <span style="color: #66cc66;">=</span> ceil<span style="color: black;">&#40;</span>masked<span style="color: black;">&#41;</span>
    binary <span style="color: #66cc66;">=</span> zeros<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>m * h<span style="color: #66cc66;">,</span> n * l<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># generate the halftoned image_path</span>
    k <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    r <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>h<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>l<span style="color: black;">&#41;</span>:
    mask <span style="color: #66cc66;">=</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>masked<span style="color: black;">&#91;</span>i<span style="color: #66cc66;">,</span> j<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    selected <span style="color: #66cc66;">=</span> masks<span style="color: black;">&#91;</span>mask - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    xs <span style="color: #66cc66;">=</span> i + k
    xf <span style="color: #66cc66;">=</span> i + k + step_x
    ys <span style="color: #66cc66;">=</span> j + r
    yf <span style="color: #66cc66;">=</span> j + r + step_y
    binary<span style="color: black;">&#91;</span>xs:xf<span style="color: #66cc66;">,</span> ys:yf<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> selected<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span>:<span style="color: black;">&#93;</span>
    r <span style="color: #66cc66;">=</span> r + step_x - <span style="color: #ff4500;">1</span>
    r <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    k <span style="color: #66cc66;">=</span> k + step_y - <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> binary</pre></td></tr></table><p class="theCode" style="display:none;">def ordered_dithering(image, masks):
    &quot;&quot;&quot;
    Convert a grayscale image in binary halftone image with n levels.
    
    Parameters
    ----------
    * image: numpy matrix, original grayscale image
    * masks: numpy array, set with all dot patterns used in halftone
    
    Return
    ----------
    * binary: numpy matrix, dithered binary image
    
    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas
    
    see: http://www.sawp.com.br
    &quot;&quot;&quot;
    # create and rescale new image to fit levels
    (levels, m, n) = masks.shape
    (h, l) = image.shape
    (step_x, step_y) = masks[0].shape
    masked = (levels / 255.0) * image
    masked = ceil(masked)
    binary = zeros((m * h, n * l))
    
    # generate the halftoned image_path
    k = 0
    r = 0
    for i in xrange(h):
    for j in xrange(l):
    mask = int(masked[i, j])
    selected = masks[mask - 1]
    xs = i + k
    xf = i + k + step_x
    ys = j + r
    yf = j + r + step_y
    binary[xs:xf, ys:yf] = selected[:,:]
    r = r + step_x - 1
    r = 0
    k = k + step_y - 1
    return binary</p></div>
    ;i:4;s:1990:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;"># Testing</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">&quot;__main__&quot;</span>:
    im <span style="color: #66cc66;">=</span> imread<span style="color: black;">&#40;</span><span style="color: #483d8b;">'lena.jpg'</span><span style="color: #66cc66;">,</span> flatten<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    im <span style="color: #66cc66;">=</span> imresize<span style="color: black;">&#40;</span>im<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1.0</span>/<span style="color: #ff4500;">4.0</span><span style="color: black;">&#41;</span>
    b <span style="color: #66cc66;">=</span> generate_mask<span style="color: black;">&#40;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span>
    masks <span style="color: #66cc66;">=</span> generate_ordered_dithering<span style="color: black;">&#40;</span>b<span style="color: black;">&#41;</span>
    binary <span style="color: #66cc66;">=</span> ordered_dithering<span style="color: black;">&#40;</span>im<span style="color: #66cc66;">,</span> masks<span style="color: black;">&#41;</span>
    imsave<span style="color: black;">&#40;</span><span style="color: #483d8b;">'lena_binary.jpg'</span><span style="color: #66cc66;">,</span> binary<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;"># Testing
    if __name__ == &quot;__main__&quot;:
    im = imread('lena.jpg', flatten=True)
    im = imresize(im, 1.0/4.0)
    b = generate_mask(4)
    masks = generate_ordered_dithering(b)
    binary = ordered_dithering(im, masks)
    imsave('lena_binary.jpg', binary)</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
No artigo anterior &#8220;_[Dithering &#8212; Parte I &#8212; Halftone via Pontilhado Ordenado](http://www.sawp.com.br/blog/?p=940)_&#8220;, apresentamos uma máscara \(3 \times 3 \) que utilizamos para substituir dez tons de cinza para gerar uma imagem binária. Contudo, padrões utilizando máscaras de tamanho \(2 \times 2 \) ou de tamanhos superiores podem ser utilizados para criar um número maior de níveis de cinza.

Os padrões de máscaras com os tamanhos mencionados são ilustrados nas figuras abaixo

<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos_2.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos_2.jpg" alt="" title="padroesdepontos_2" width="700" height="160" class="aligncenter size-full wp-image-1003" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos_2.jpg 700w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos_2-300x68.jpg 300w" sizes="(max-width: 700px) 100vw, 700px" /></a><br />
</center>

<center>
  </p> 
  
  <hr style="width:80%; height: 2px;" />
</center>

<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos_3.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/padroesdepontos_3.jpg" alt="" title="padroesdepontos_3" width="700" height="320" class="aligncenter size-full wp-image-1004" /></a><br />
</center>

Devemos observar que quanto menor a máscara, menor serão a quantidade de pontos gerados por padrão. Isso terá consequência direta na qualidade da imagem binária, pois ela terá menos padrões para diferenciar os diferentes níveis de cinza da imagem original. Além disso, devemos observar que os pontos devem ser dispostos de maneira a minimizar efeitos indesejáveis na imagem resultante, por exemplo, a ocorrência de linhas horizontais ou verticais em uma parte da imagem. Outra consideração importante é que, se um pixel for preto no padrão \(i \), ele também será preto em todos os padrões \(j > i \), reduzindo a ocorrência de falsos contornos na imagem.

O uso de padrões de \(3 \times 3 \) pixels limita a resolução espacial para um terço em cada dimensão da imagem, entretanto, fornece dez níveis de cinza. Certamente, a escolha da relação entre a resolução espacial e a profundidade da imagem dependem de maior perspicácia visual e da distância da qual a imagem é observada. 

Padrões maiores podem ser usados para criar um número maior de níveis de cinza. Padrões de tamanho \(n \times m \) geram \(nm + 1 \) arranjos distintos. Tal conjunto de padrões pode ser ilustrado por meios das matrizes abaixo, tal que um determinado padrão \(i \) é formado pela ativação dos elementos da matriz cujos valores são menores do que \(i \).

<center>
  <br /> \( \begin{array}{| c | c | c | }<br /> \hline<br /> 0 & 2 \\ \hline<br /> 3 & 1 \\<br /> \hline<br /> \end{array} \)<br />
</center>


  


<center>
  <br /> \( \begin{array}{| c | c | c | }<br /> \hline<br /> 6 & 8 & 4 \\ \hline<br /> 1 & 0 & 3 \\ \hline<br /> 5 & 2 & 7 \\<br /> \hline<br /> \end{array} \)<br />
</center>


  


<center>
  <br /> \( \begin{array}{| c | c | c | }<br /> \hline<br /> 3 & 0 & 4 \\ \hline<br /> 5 & 2 & 1 \\<br /> \hline<br /> \end{array} \)<br />
</center>

Máscaras quadras maiores que três podem ser gerados a partir de matrizes de ordem \(2^n \times 2^n \), conforme a seguinte definição recursiva:

<center>
  <br /> \(<br /> D_n = \left[ \begin{array}{cc} 4 D_{n/2} + 2 U_{n/2} & 4 D_{n/2} \\ 4 D_{n/2} + U_{n/2} & D_{n/2} + U_{n/2} \\ \end{array} \right]<br /> \hspace{80px}<br /> n \ge 4<br /> \)<br />
</center>

onde \(D_2 \) é a seguinte matriz de ordem \(2 \times 2 \) :

<center>
  <br /> \(<br /> \begin{array}{| c | c | c | }<br /> \hline<br /> 0 & 2 \\ \hline<br /> 3 & 1 \\<br /> \hline<br /> \end{array}<br /> \)<br />
</center>

e \(U_n \) é uma matriz \(n \times n\), cujos elementos são todos unitários.

## Código

O código para gerar a máscara de padrões é descrito abaixo:

<pre lang="python">def generate_mask(n):
    """
    Return dot-pattern matrix of indicies for ordered dithering of 2^n order

    Parameters
    ----------
    * n: order of mask (must be even), integer

    Return
    ----------
    * mask: numpy matrix with dot patter order to generate ordered dithering

    Written by Pedro Garcia Freitas [sawp@sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    """
    mask = array([[0, 2], [3,1]])
    mask_order = 2
    while mask_order &lt; n:
        u = ones((mask_order, mask_order))
        m11 = 4 * mask + 2 * u
        m12 = 4 * mask
        m21 = 4 * mask + u
        m22 = mask + u
        top = concatenate((m11, m12), axis=1)
        down = concatenate((m21, m22), axis=1)
        mask = concatenate((top, down), axis=0)
        mask_order = 2 * mask_order
    return mask</pre>

Os padrões de pontos gerados pela máscara acima é implementado na função abaixo:

<pre lang="python">def generate_ordered_dithering(mask):
    """
    Return a set of ordered dithering dot patterns

    Parameters
    ----------
    * mask: numpy matrix with mask order

    Return
    ----------
    * dot_pattern: numpy matrix all dot patterns

    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    """
    (m, n) = mask.shape
    total = m * n - 1
    dot_pattern = [zeros((m, m))]
    for i in xrange(total):
        last = dot_pattern[i]
        new = (mask == i)
        dot_pattern.append(last + new)
    dot_pattern = array(dot_pattern)
    return dot_pattern</pre>

Para converter uma imagem em outra binária, usamos a seguinte função:

<pre lang="python">def ordered_dithering(image, masks):
    """
    Convert a grayscale image in binary halftone image with n levels.

    Parameters
    ----------
    * image: numpy matrix, original grayscale image
    * masks: numpy array, set with all dot patterns used in halftone

    Return
    ----------
    * binary: numpy matrix, dithered binary image

    Written by Pedro Garcia Freitas [sawp @sawp.com.br]
    Copyright 2011 by Pedro Garcia Freitas

    see: http://www.sawp.com.br
    """
    # create and rescale new image to fit levels
    (levels, m, n) = masks.shape
    (h, l) = image.shape
    (step_x, step_y) = masks[0].shape
    masked = (levels / 255.0) * image
    masked = ceil(masked)
    binary = zeros((m * h, n * l))

    # generate the halftoned image_path
    k = 0
    r = 0
    for i in xrange(h):
        for j in xrange(l):
            mask = int(masked[i, j])
            selected = masks[mask - 1]
            xs = i + k
            xf = i + k + step_x
            ys = j + r
            yf = j + r + step_y
            binary[xs:xf, ys:yf] = selected[:,:]
            r = r + step_x - 1
        r = 0
        k = k + step_y - 1
    return binary</pre>

Usamos estas funções da seguinte maneira:

<pre lang="python"># Testing
if __name__ == "__main__":
    im = imread('lena.jpg', flatten=True)
    im = imresize(im, 1.0/4.0)
    b = generate_mask(4)
    masks = generate_ordered_dithering(b)
    binary = ordered_dithering(im, masks)
    imsave('lena_binary.jpg', binary)</pre>

para obtermos o seguinte resultado:

<center>
  </p> 
  
  <table>
    <tr>
      <td>
        <center>
          Original
        </center>
      </td>
      
      <td>
        <center>
          Halftoned
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena1.jpg" alt="" title="lena" width="256" height="256" class="aligncenter size-full wp-image-1035" /></a>
        </center>
      </td>
      
      <td>
        <center>
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_binary1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_binary1.jpg" alt="" title="lena_binary" width="256" height="256" class="aligncenter size-full wp-image-1036" /></a>
        </center>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
