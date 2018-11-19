---
id: 978
title: Aumento de Contraste e Equalização de Histograma
date: 2011-01-10T12:22:11+00:00
author: SAWP
excerpt: Funções de transformações em intensidades (na escala de cinza ou espaços de cores) que utilizam informações extraídas do histograma estão presentes em diversas áreas de processamento de imagens, tais como reconstrução, compressão e segmentação. Neste artigo comentaremos sobre o processamento e equalização de histogramas e os seus efeitos visuais na imagem.
layout: post
guid: http://www.sawp.com.br/blog/?p=978
permalink: p=978
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3277:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> histeq<span style="color: black;">&#40;</span>arr<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot; Enhance contrast using histogram equalization
    USAGE:
    [equalized] = histeq(arr)
    &nbsp;
    INPUT:
    * arr: to be balanced
    &nbsp;
    RETURN:
    * equalized: balanced
    &nbsp;
    AUTHOR:
    * Pedro Garcia [sawp@sawp.com.br], http://www.sawp.com.br
    &nbsp;
    LICENSE:
    * Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/&quot;&quot;&quot;</span>
    &nbsp;
    <span style="color: black;">&#40;</span>hist<span style="color: #66cc66;">,</span> bin_edges<span style="color: black;">&#41;</span> <span style="color: #66cc66;">=</span> histogram<span style="color: black;">&#40;</span>arr.<span style="color: black;">flatten</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">256</span><span style="color: #66cc66;">,</span> normed<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    cumsum_along_axis <span style="color: #66cc66;">=</span> hist.<span style="color: black;">cumsum</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    cumsum_along_axis <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">255.0</span> * cumsum_along_axis / cumsum_along_axis<span style="color: black;">&#91;</span>-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    y <span style="color: #66cc66;">=</span> interp<span style="color: black;">&#40;</span>arr.<span style="color: black;">flatten</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> bin_edges<span style="color: black;">&#91;</span>:-<span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> cumsum_along_axis<span style="color: black;">&#41;</span>
    y <span style="color: #66cc66;">=</span> y.<span style="color: black;">reshape</span><span style="color: black;">&#40;</span>arr.<span style="color: black;">shape</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> y</pre></td></tr></table><p class="theCode" style="display:none;">def histeq(arr):
    &quot;&quot;&quot; Enhance contrast using histogram equalization
    USAGE:
    [equalized] = histeq(arr)
    
    INPUT:
    * arr: to be balanced
    
    RETURN:
    * equalized: balanced
    
    AUTHOR:
    * Pedro Garcia [sawp@sawp.com.br], http://www.sawp.com.br
    
    LICENSE:
    * Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/&quot;&quot;&quot;
    
    (hist, bin_edges) = histogram(arr.flatten(), 256, normed=True)
    cumsum_along_axis = hist.cumsum()
    cumsum_along_axis = 255.0 * cumsum_along_axis / cumsum_along_axis[-1]
    y = interp(arr.flatten(), bin_edges[:-1], cumsum_along_axis)
    y = y.reshape(arr.shape)
    return y</p></div>
    ";}
categories:
  - Digital Image Processing Using Python
---
O histograma de uma imagem digital com \(L \) possíveis níveis de intensidades em um intervalo \([0,G] \) é definido como a seguinte função discreta

<center>
  \( h(r_k) = n_k \)
</center>

onde \(r\_k \) é o \(k-esimo \) nível dentro do intervalo \([0,G] \) e \(n\_k \) é o número de pixels na imagem cuja intensidade é \(r_k \). Geralmente o valor \(G \) é \(255 \), pois quase sempre trabalhamos com imagens em escalas de 8 bits. Contudo, esse valor pode ser \(65535 \) para imagens de 16 bits, \(1.0 \) para alguma representação de imagens que utiliza ponto flutuante, etc.

Muitas vezes precisamos trabalhar com histogramas normalizados, que são obtidos simplesmente dividindo-se todos elementos de \(h(r_k) \) pelo número total de pixels na imagem. Denotaremos essa transformação da seguinte maneira:

<center>
  \( p(r_k) = \dfrac{h(r_k)}{n} = \dfrac{n_k}{n} \)
</center>

onde, \(k=0,1,2,\ldots, L-1 \). Dessa formulação é fácil reconhecer que \(p(r\_k) \) é uma estimativa probabilística da ocorrência do nível de intensidade $r\_k$.

Assumindo que os níveis de intensidades sejam quantidades contínuas e normalizadas no intervalo \([0,1] \), e chamando de \(p_r(r) \) a função densidade de probabilidade dos níveis. Supondo que realizamos a seguinte transformação dos níveis da imagem original para obter os níveis processados:

<center>
  \( s = T(r) = \int_0^r p_r(w) dw \)
</center>

onde \(w \) é uma variável de integração qualquer. A função densidade de probabilidade dos níveis processados serão uniformes, isto é,

<center>
  \(<br /> p_s(s) = \left\{<br /> \begin{array}{lcl}<br /> 1 & ~ & 0 \leq s \\<br /> 0 & ~ & otherwise<br /> \end{array}<br /> \right.<br /> \)
</center>

Como imagens são quantidades discretas, nós trabalhamos com histogramas e realizamos a operação de equalização. Ou seja, realizamos o processo acima, mas sem considerarmos uma distribuição contínua. Assim, ao invés de utilizarmos a função densidade de probabilidade, trabalhamos com as probabilidades extraídas das ocorrências contadas no histograma:

<center>
  <br /> \( s_k = T(r_k) = \sum_{j=0}^{k} p_r(r_j) = \sum_{j=0}^{k} \frac{n_j}{n} \)<br />
</center>

para \(k = 0, 1, 2, \ldots, L-1 \), onde \(s\_k \) é o valor de intensidade na saída, correspondendo ao valor da imagem original \(r\_k \). Este processo é implementado na seguinte função:

<pre lang="python">def histeq(arr):
    """ Enhance contrast using histogram equalization
USAGE:
        [equalized] = histeq(arr)

INPUT:
    * arr: to be balanced

RETURN:
    * equalized: balanced

AUTHOR:
    * Pedro Garcia [sawp@sawp.com.br], http://www.sawp.com.br

LICENSE:
    * Creative Commons
      http://creativecommons.org/licenses/by-nc-nd/2.5/br/"""

    (hist, bin_edges) = histogram(arr.flatten(), 256, normed=True)
    cumsum_along_axis = hist.cumsum()
    cumsum_along_axis = 255.0 * cumsum_along_axis / cumsum_along_axis[-1]
    y = interp(arr.flatten(), bin_edges[:-1], cumsum_along_axis)
    y = y.reshape(arr.shape)
    return y</pre>

Como resultado, a transformação gera uma imagem em que os níveis de intensidade são igualmente distribuídos dentro do intervalo \([0,1] \). O resultado visual desta operação é uma imagem com maior contraste, conforme podemos visualizar nas figuras abaixo.

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
          <br /> Equalizada (retorno)<br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_resized.jpg" alt="" title="einstein_resized" width="256" height="314" class="aligncenter size-full wp-image-984" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_resized.jpg 256w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_resized-244x300.jpg 244w" sizes="(max-width: 256px) 100vw, 256px" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_equalized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_equalized.jpg" alt="" title="einstein_equalized" width="256" height="314" class="aligncenter size-full wp-image-985" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_equalized.jpg 256w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/einstein_equalized-244x300.jpg 244w" sizes="(max-width: 256px) 100vw, 256px" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/foch_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/foch_resized.jpg" alt="" title="foch_resized" width="256" height="256" class="aligncenter size-full wp-image-986" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/foch_equalized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/foch_equalized.jpg" alt="" title="foch_equalized" width="256" height="256" class="aligncenter size-full wp-image-987" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/fruits_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/fruits_resized.jpg" alt="" title="fruits_resized" width="256" height="256" class="aligncenter size-full wp-image-988" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/fruits_equalized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/fruits_equalized.jpg" alt="" title="fruits_equalized" width="256" height="256" class="aligncenter size-full wp-image-989" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_resized1.jpg" alt="" title="lena_resized" width="256" height="256" class="aligncenter size-full wp-image-990" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_equalized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/lena_equalized.jpg" alt="" title="lena_equalized" width="256" height="256" class="aligncenter size-full wp-image-991" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_resized.jpg" alt="" title="mars_resized" width="256" height="314" class="aligncenter size-full wp-image-992" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_resized.jpg 256w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_resized-244x300.jpg 244w" sizes="(max-width: 256px) 100vw, 256px" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_equalized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_equalized.jpg" alt="" title="mars_equalized" width="256" height="314" class="aligncenter size-full wp-image-993" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_equalized.jpg 256w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/mars_equalized-244x300.jpg 244w" sizes="(max-width: 256px) 100vw, 256px" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_resized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_resized.jpg" alt="" title="moon_resized" width="256" height="314" class="aligncenter size-full wp-image-994" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_resized.jpg 256w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_resized-244x300.jpg 244w" sizes="(max-width: 256px) 100vw, 256px" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_equalized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_equalized.jpg" alt="" title="moon_equalized" width="256" height="314" class="aligncenter size-full wp-image-995" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_equalized.jpg 256w, http://www.sawp.com.br/blog/wp-content/uploads/2011/01/moon_equalized-244x300.jpg 244w" sizes="(max-width: 256px) 100vw, 256px" /></a><br />
        </center>
      </td>
    </tr>
    
    <tr>
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized1.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_resized1.jpg" alt="" title="degrade_resized" width="256" height="256" class="aligncenter size-full wp-image-996" /></a><br />
        </center>
      </td>
      
      <td>
        <center>
          <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_equalized.jpg"><img src="http://www.sawp.com.br/blog/wp-content/uploads/2011/01/degrade_equalized.jpg" alt="" title="degrade_equalized" width="256" height="256" class="aligncenter size-full wp-image-997" /></a><br />
        </center>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
