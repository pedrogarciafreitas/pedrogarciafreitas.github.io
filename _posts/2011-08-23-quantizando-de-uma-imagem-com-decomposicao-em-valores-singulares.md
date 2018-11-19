---
id: 1278
title: Quantização de Imagens Usando Decomposição em Valores Singulares
date: 2011-08-23T21:57:40+00:00
author: CKPYT
excerpt: No contexto do processamento de imagens, a quantização é geralmente feita reduzindo-se a quantidade de níveis de cor (quantização espacial) ou reduzindo-se a quantidade de coeficientes no domínio da frequência (quantização do espaço transformado de Fourier, wavelets, etc). Por exemplo, no padrão JPEG, a quantização é feita sobre os coeficientes da transformada discreta de cosseno, eliminando-se aqueles menos significativos. Nest post, mostramos exemplos de quantização no espaço transformado pela decomposição em valores singulares.
layout: post
guid: http://www.sawp.com.br/blog/?p=1278
permalink: p=1278
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8875:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">import</span> numpy
    <span style="color: #ff7700;font-weight:bold;">from</span> numpy <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">array</span>
    <span style="color: #ff7700;font-weight:bold;">from</span> numpy <span style="color: #ff7700;font-weight:bold;">import</span> linalg
    <span style="color: #ff7700;font-weight:bold;">from</span> scipy.<span style="color: black;">misc</span>.<span style="color: black;">pilutil</span> <span style="color: #ff7700;font-weight:bold;">import</span> imsave<span style="color: #66cc66;">,</span> imread<span style="color: #66cc66;">,</span> imresize
    &nbsp;
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> svd_encode<span style="color: black;">&#40;</span>im<span style="color: #66cc66;">,</span> number_of_coefficients<span style="color: #66cc66;">=</span><span style="color: #ff4500;">50.0</span><span style="color: black;">&#41;</span>:
    img <span style="color: #66cc66;">=</span> im.<span style="color: black;">astype</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'double'</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span>rows<span style="color: #66cc66;">,</span> cols<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> img.<span style="color: black;">shape</span>
    mindim <span style="color: #66cc66;">=</span> <span style="color: #008000;">min</span><span style="color: black;">&#40;</span>rows<span style="color: #66cc66;">,</span> cols<span style="color: black;">&#41;</span>
    total <span style="color: #66cc66;">=</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>numpy.<span style="color: black;">floor</span><span style="color: black;">&#40;</span>number_of_coefficients * mindim / <span style="color: #ff4500;">100.0</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span>u<span style="color: #66cc66;">,</span> s<span style="color: #66cc66;">,</span> v<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> linalg.<span style="color: black;">svd</span><span style="color: black;">&#40;</span>img<span style="color: black;">&#41;</span>
    v <span style="color: #66cc66;">=</span> v.<span style="color: black;">T</span>
    compressed <span style="color: #66cc66;">=</span> numpy.<span style="color: black;">zeros</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>rows<span style="color: #66cc66;">,</span> cols<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> j <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span>total<span style="color: black;">&#41;</span>:
    l <span style="color: #66cc66;">=</span> s<span style="color: black;">&#91;</span>j<span style="color: black;">&#93;</span> * numpy.<span style="color: black;">matrix</span><span style="color: black;">&#40;</span>u<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span> j<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>.<span style="color: black;">T</span>
    vm <span style="color: #66cc66;">=</span> numpy.<span style="color: black;">matrix</span><span style="color: black;">&#40;</span>v<span style="color: black;">&#91;</span>:<span style="color: #66cc66;">,</span> j<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    r <span style="color: #66cc66;">=</span> numpy.<span style="color: black;">dot</span><span style="color: black;">&#40;</span>l<span style="color: #66cc66;">,</span> vm<span style="color: black;">&#41;</span>
    compressed <span style="color: #66cc66;">=</span> compressed + r
    compressed <span style="color: #66cc66;">=</span> numpy.<span style="color: black;">floor</span><span style="color: black;">&#40;</span>compressed<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> compressed
    &nbsp;
    &nbsp;
    <span style="color: #808080; font-style: italic;"># Testing</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'__main__'</span>:
    imgs <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: #483d8b;">'peppers'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'lena'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'cameraman'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'rose'</span><span style="color: black;">&#93;</span>
    f <span style="color: #66cc66;">=</span> imread<span style="color: black;">&#40;</span>imgs<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">&quot;.jpg&quot;</span><span style="color: #66cc66;">,</span> flatten<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">5</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">75</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">15</span><span style="color: black;">&#41;</span>:
    f1 <span style="color: #66cc66;">=</span> svd_encode<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> <span style="color: #008000;">float</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    imsave<span style="color: black;">&#40;</span>imgs<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> + <span style="color: #483d8b;">&quot;.jpg&quot;</span><span style="color: #66cc66;">,</span> f1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> im <span style="color: #ff7700;font-weight:bold;">in</span> imgs:
    <span style="color: #ff7700;font-weight:bold;">print</span> im + <span style="color: #483d8b;">&quot;.jpg&quot;</span>
    f <span style="color: #66cc66;">=</span> imread<span style="color: black;">&#40;</span>im + <span style="color: #483d8b;">&quot;.jpg&quot;</span><span style="color: #66cc66;">,</span> flatten<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    g <span style="color: #66cc66;">=</span> svd_encode<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">50</span><span style="color: black;">&#41;</span>
    imsave<span style="color: black;">&#40;</span>im + <span style="color: #483d8b;">&quot;_svd.jpg&quot;</span><span style="color: #66cc66;">,</span> g<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">import numpy
    from numpy import array
    from numpy import linalg
    from scipy.misc.pilutil import imsave, imread, imresize
    
    
    def svd_encode(im, number_of_coefficients=50.0):
    img = im.astype('double')
    [rows, cols] = img.shape
    mindim = min(rows, cols)
    total = int(numpy.floor(number_of_coefficients * mindim / 100.0))
    [u, s, v] = linalg.svd(img)
    v = v.T
    compressed = numpy.zeros((rows, cols))
    for j in xrange(total):
    l = s[j] * numpy.matrix(u[:, j]).T
    vm = numpy.matrix(v[:, j])
    r = numpy.dot(l, vm)
    compressed = compressed + r
    compressed = numpy.floor(compressed)
    return compressed
    
    
    # Testing
    if __name__ == '__main__':
    imgs = ['peppers', 'lena', 'cameraman', 'rose']
    f = imread(imgs[0] + &quot;.jpg&quot;, flatten=True)
    for i in xrange(5, 75, 15):
    f1 = svd_encode(f, float(i))
    imsave(imgs[0] + str(i) + &quot;.jpg&quot;, f1)
    for im in imgs:
    print im + &quot;.jpg&quot;
    f = imread(im + &quot;.jpg&quot;, flatten=True)
    g = svd_encode(f, 50)
    imsave(im + &quot;_svd.jpg&quot;, g)</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
A compressão sem perdas consiste em reduzir o tamanho de um dado através da codificação da informação com símbolos menores, que ocupam menos espaço. Este tipo de compressão sempre será limitada à entropia da fonte original. Contudo, para algumas aplicações pode ser necessário comprimir a informação para taxas menores que a entropia. Para conseguir essas taxas de compressão, devemos eliminar informação da fonte e codificá-la considerando essas perdas. Este processo de descarte requer que o número de palavras-código da fonte sejam limitados, fazendo com que a quantidade de possíveis saídas da fonte seja maior do que a quantidade de palavras-códigos do objeto comprimido. Sendo assim, as técnicas de limitar a quantidade de palavras-códigos são denominadas técnicas de quantização. 

No contexto do processamento de imagens, a quantização é geralmente feita reduzindo-se a quantidade de níveis de cor (quantização espacial) ou reduzindo-se a quantidade de coeficientes no domínio da frequência (quantização do espaço transformado de Fourier, wavelets, etc). Por exemplo, no padrão JPEG, a quantização é feita sobre os coeficientes da transformada discreta de cosseno, eliminando-se aqueles menos significativos. Nest post, mostramos exemplos de quantização no espaço transformado pela <a href="http://www.sawp.com.br/blog/?p=657" targe="_blank">decomposição SVD</a>. 

Nas imagens abaixo, decompomos uma imagem \(I\) em três matrizes \(U\), \(S\) e \(V\). Tal decomposição distribui os coeficientes mais significantes da informação ao longo do vetor \(S\), de forma ordenada e decrescente em importância. Com esta decomposição reconstruímos a imagem \(I = U \times S \times V^T\) utilizando apenas uma fração dos coeficientes. A listagem mostra a imagem original (primeira) quantizada com 5, 20, 35, 50 e 65% dos coeficientes decompostos da imagem original. Sem seguida, as imagens são codificadas em JPEG, sendo novamente quantizadas, conforme especificações desse padrão. 

<center>
  </p> 
  
  <table>
    <tr valign="top">
      <td>
        <div id="attachment_1280" style="width: 210px" class="wp-caption aligncenter">
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers.jpg"><img class="size-full wp-image-1280 " title="peppers" src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers.jpg" alt="" width="200" height="200" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers.jpg 512w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers-300x300.jpg 300w" sizes="(max-width: 200px) 100vw, 200px" /></a>
          
          <p class="wp-caption-text">
            Original
          </p>
        </div>
      </td>
      
      <td>
        <div id="attachment_1281" style="width: 210px" class="wp-caption aligncenter">
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers5.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers5.jpg" alt="" title="peppers5" width="200" height="200" class="size-full wp-image-1281" /></a>
          
          <p class="wp-caption-text">
            Reconstruída com 5% dos coeficientes SVD
          </p>
        </div>
      </td>
      
      <td>
        <div id="attachment_1282" style="width: 210px" class="wp-caption aligncenter">
          <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers20.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers20.jpg" alt="" title="peppers20" width="200" height="200" class="size-full wp-image-1282" /></a>
          
          <p class="wp-caption-text">
            Reconstruída com 20% dos coeficientes SVD
          </p>
        </div>
      </td>
    </tr><tr valign="top""> 
    
    <td>
      <div id="attachment_1283" style="width: 210px" class="wp-caption aligncenter">
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers35.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers35.jpg" alt="" title="peppers35" width="200" height="200" class="size-full wp-image-1283" /></a>
        
        <p class="wp-caption-text">
          Reconstruída com 35% dos coeficientes SVD
        </p>
      </div>
    </td>
    
    <td>
      <div id="attachment_1284" style="width: 210px" class="wp-caption aligncenter">
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers50.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers50.jpg" alt="" title="peppers50" width="200" height="200" class="size-full wp-image-1284" /></a>
        
        <p class="wp-caption-text">
          Reconstruída com 50% dos coeficientes SVD
        </p>
      </div>
    </td>
    
    <td>
      <div id="attachment_1285" style="width: 210px" class="wp-caption aligncenter">
        <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers65.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/peppers65.jpg" alt="" title="peppers65" width="200" height="200" class="size-full wp-image-1285" /></a>
        
        <p class="wp-caption-text">
          Reconstruída com 65% dos coeficientes SVD
        </p>
      </div>
    </td></tr>
  </table>
  
  <p>
    </center>
  </p>
  
  <p>
    Visualmente, podemos notar que a qualidade da imagem melhora, conforme mais valores singulares são selecionados na reconstrução. Contudo, considerando que a codificação JPEG realiza uma segunda quantização, os resultados visuais são satisfatórios.
  </p>
  
  <p>
    Para analisar objetivamente a influencia da quantização SVD sobre as imagens, codificamos o conjunto de imagens abaixo com as componentes SVD, aproveitando 50% dos coeficientes e descartando os outros 50. Com o resultado dessa quantização calculamos o PSNR e a taxa de compressão obtida.
  </p>
  
  <p>
    As imagens são:
  </p>
  
  <p>
    <center>
      </p> 
      
      <table>
        <tr>
          <td>
            <div id="attachment_1291" style="width: 210px" class="wp-caption aligncenter">
              <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena.jpg" alt="" title="lena" width="200" height="200" class="size-full wp-image-1291" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena.jpg 512w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena-300x300.jpg 300w" sizes="(max-width: 200px) 100vw, 200px" /></a>
              
              <p class="wp-caption-text">
                Original
              </p>
            </div>
          </td>
          
          <td>
            <div id="attachment_1292" style="width: 210px" class="wp-caption aligncenter">
              <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena_svd.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena_svd.jpg" alt="" title="lena_svd" width="200" height="200" class="size-full wp-image-1292" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena_svd.jpg 512w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/lena_svd-300x300.jpg 300w" sizes="(max-width: 200px) 100vw, 200px" /></a>
              
              <p class="wp-caption-text">
                SVD-Quantizada
              </p>
            </div>
          </td>
        </tr>
        
        <tr>
          <td>
            <div id="attachment_1293" style="width: 210px" class="wp-caption aligncenter">
              <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/cameraman.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/cameraman.jpg" alt="" title="cameraman" width="200" height="200" class="size-full wp-image-1293" /></a>
              
              <p class="wp-caption-text">
                Original
              </p>
            </div>
          </td>
          
          <td>
            <div id="attachment_1294" style="width: 210px" class="wp-caption aligncenter">
              <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/cameraman_svd.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/cameraman_svd.jpg" alt="" title="cameraman_svd" width="200" height="200" class="size-full wp-image-1294" /></a>
              
              <p class="wp-caption-text">
                SVD-Quantizada
              </p>
            </div>
          </td>
        </tr>
        
        <tr>
          <td>
            <div id="attachment_1295" style="width: 210px" class="wp-caption aligncenter">
              <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose.jpg" alt="" title="rose" width="200" height="200" class="size-full wp-image-1295" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose.jpg 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose-300x300.jpg 300w" sizes="(max-width: 200px) 100vw, 200px" /></a>
              
              <p class="wp-caption-text">
                Original
              </p>
            </div>
          </td>
          
          <td>
            <div id="attachment_1296" style="width: 210px" class="wp-caption aligncenter">
              <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose_svd.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose_svd.jpg" alt="" title="rose_svd" width="200" height="200" class="size-full wp-image-1296" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose_svd.jpg 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2011/08/rose_svd-300x300.jpg 300w" sizes="(max-width: 200px) 100vw, 200px" /></a>
              
              <p class="wp-caption-text">
                SVD-Quantizada
              </p>
            </div>
          </td>
        </tr>
      </table>
      
      <p>
        </center>
      </p>
      
      <p>
        Os resultados objetivos são:
      </p>
      
      <p>
        <center>
          </p> 
          
          <table border="0" cellpadding="50" cellspace="5">
            <tr bgcolor="#CCCCCC">
              <th align="center" valign="middle">
                Imagem
              </th>
              
              <th align="center" valign="middle">
                PSNR
              </th>
              
              <th align="center" valign="middle">
                Tamanho do Arquivo <br />Sem SVD (bytes)
              </th>
              
              <th align="center" valign="middle">
                Tamanho do Arquivo <br />com SVD (bytes)
              </th>
              
              <th align="center" valign="middle">
                Taxa de Compressão
              </th>
            </tr>
            
            <tr>
              <td align="center" valign="middle">
                peppers
              </td>
              
              <td align="center" valign="middle">
                23.51
              </td>
              
              <td align="center" valign="middle">
                73441
              </td>
              
              <td align="center" valign="middle">
                36443
              </td>
              
              <td align="center" valign="middle">
                2.01
              </td>
            </tr>
            
            <tr>
              <td align="center" valign="middle">
                lena
              </td>
              
              <td align="center" valign="middle">
                28.79
              </td>
              
              <td align="center" valign="middle">
                65294
              </td>
              
              <td align="center" valign="middle">
                34995
              </td>
              
              <td align="center" valign="middle">
                1.86
              </td>
            </tr>
            
            <tr>
              <td align="center" valign="middle">
                cameraman
              </td>
              
              <td align="center" valign="middle">
                33.92
              </td>
              
              <td align="center" valign="middle">
                19545
              </td>
              
              <td align="center" valign="middle">
                10914
              </td>
              
              <td align="center" valign="middle">
                1.79
              </td>
            </tr>
            
            <tr>
              <td align="center" valign="middle">
                rose
              </td>
              
              <td align="center" valign="middle">
                38.99
              </td>
              
              <td align="center" valign="middle">
                169752
              </td>
              
              <td align="center" valign="middle">
                64131
              </td>
              
              <td align="center" valign="middle">
                2.64
              </td>
            </tr>
          </table>
          
          <p>
            </center>
          </p>
          
          <p>
            Segue abaixo o código para quantização usando SVD.
          </p>
          
          <div>
            <pre lang="python">import numpy
from numpy import array
from numpy import linalg
from scipy.misc.pilutil import imsave, imread, imresize


def svd_encode(im, number_of_coefficients=50.0):
    img = im.astype('double')
    [rows, cols] = img.shape
    mindim = min(rows, cols)
    total = int(numpy.floor(number_of_coefficients * mindim / 100.0))
    [u, s, v] = linalg.svd(img)
    v = v.T
    compressed = numpy.zeros((rows, cols))
    for j in xrange(total):
        l = s[j] * numpy.matrix(u[:, j]).T
        vm = numpy.matrix(v[:, j])
        r = numpy.dot(l, vm)
        compressed = compressed + r
    compressed = numpy.floor(compressed)
    return compressed


# Testing
if __name__ == '__main__':
    imgs = ['peppers', 'lena', 'cameraman', 'rose']
    f = imread(imgs[0] + ".jpg", flatten=True)
    for i in xrange(5, 75, 15):
        f1 = svd_encode(f, float(i))
        imsave(imgs[0] + str(i) + ".jpg", f1)
    for im in imgs:
        print im + ".jpg"
        f = imread(im + ".jpg", flatten=True)
        g = svd_encode(f, 50)
        imsave(im + "_svd.jpg", g)</pre>
          </div>
          
          <p>
          </p>
          
          <p>
            O código completo e a comparação das imagens pode ser obtido no endereço: <a href="http://www.sawp.com.br/code/ip/post68_svd_processing_image.tar.gz" >http://www.sawp.com.br/code/ip/post68_svd_processing_image.tar.gz</a>.
          </p>
