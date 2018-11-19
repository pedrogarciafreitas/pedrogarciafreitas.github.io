---
id: 1711
title: 0.2 Miscelânea — Geração dos Coeficientes do Polinômio de Legendre
date: 2012-08-02T19:48:25+00:00
author: SAWP
excerpt: O polinômio de Legendre aparece com solução da equação diferencial de Legendre, comum em alguns problemas físicos. Além disso, os polinômios de Legendre podem ser úteis para algumas aplicações em métodos computacionais, tais como quadraturas e integração. Neste post veremos como gerar os polinômios de Legendre de qualquer ordem.
layout: post
guid: http://www.sawp.com.br/blog/?p=1711
permalink: p=1711
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3044:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> compute_legendre_polynomials_coeficients<span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Compute the coefficients of the nth Legendre polynomial.
    &nbsp;
    [coefficients] = compute_legendre_polynomials_coeficients(n)
    &nbsp;
    INPUT:
    * n: order of the Legendre polynomial
    &nbsp;
    return: a list containing the polynomial coefficients of nth Legendre
    polynomial (ordered from the highest to lowest)
    &nbsp;
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    &nbsp;
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    &nbsp;
    Jul 2012
    &quot;&quot;&quot;</span>
    b <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2.0</span> ** n
    B <span style="color: #66cc66;">=</span> binomial_coefficients
    a <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span>b * B<span style="color: black;">&#40;</span>n<span style="color: #66cc66;">,</span> k<span style="color: black;">&#41;</span> * B<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>n + k - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2.0</span><span style="color: #66cc66;">,</span> n<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> k <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">xrange</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> n + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    a.<span style="color: black;">reverse</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> a</pre></td></tr></table><p class="theCode" style="display:none;">def compute_legendre_polynomials_coeficients(n):
    &quot;&quot;&quot;
    Compute the coefficients of the nth Legendre polynomial.
    
    [coefficients] = compute_legendre_polynomials_coeficients(n)
    
    INPUT:
    * n: order of the Legendre polynomial
    
    return: a list containing the polynomial coefficients of nth Legendre
    polynomial (ordered from the highest to lowest)
    
    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br
    
    License: Creative Commons
    http://creativecommons.org/licenses/by-nc-nd/2.5/br/
    
    Jul 2012
    &quot;&quot;&quot;
    b = 2.0 ** n
    B = binomial_coefficients
    a = [b * B(n, k) * B((n + k - 1) / 2.0, n) for k in xrange(0, n + 1)]
    a.reverse()
    return a</p></div>
    ";}
categories:
  - Computational Methods
---
Os Polinômios de Legendre, também conhecidos como coeficientes de Legendre, são os elementos de um conjunto formado pelas soluções da equação diferencial de Legendre. Os primeiros polinômios de Legendre são:
  


<center>
  </p> 
  
  <table>
    <tr>
      <td width="20%" align="center">
        n
      </td>
      
      <td align="center">
        \(P_n(x)\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
      </td>
      
      <td align="center">
        \(1\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        1
      </td>
      
      <td align="center">
        \(x\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        2
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac12\end{matrix} (3x^2-1) \,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        3
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac12\end{matrix} (5x^3-3x) \,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        4
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac18\end{matrix} (35x^4-30x^2+3)\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        5
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac18\end{matrix} (63x^5-70x^3+15x)\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        6
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac1{16}\end{matrix} (231x^6-315x^4+105x^2-5)\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        7
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac1{16}\end{matrix} (429x^7-693x^5+315x^3-35x)\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        8
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac1{128}\end{matrix} (6435x^8-12012x^6+6930x^4-1260x^2+35)\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        9
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac1{128}\end{matrix} (12155x^9-25740x^7+18018x^5-4620x^3+315x)\,\)
      </td>
    </tr>
    
    <tr>
      <td align="center">
        10
      </td>
      
      <td align="center">
        \(\begin{matrix}\frac1{256}\end{matrix} (46189x^{10}-109395x^8+90090x^6-30030x^4+3465x^2-63)\,\)
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
  
  <p>
    Esses polinômios podem ser gerados pela seguinte fórmula recursiva:<br /> 
    
    <center>
      </p> 
      
      <table>
        <tr>
          <td align="left">
            \(P_0(x) = 1\)
          </td>
        </tr>
        
        <tr>
          <td align="left">
            \(P_1(x) = x\)
          </td>
        </tr>
        
        <tr>
          <td align="left">
            \((n+1) P_{n+1}(x) = (2n+1) x P_n(x) &#8211; n P_{n-1}(x)\)
          </td>
        </tr>
      </table>
      
      <p>
        </center><br /> ou pela seguinte definição explícita:<br /> 
        
        <center>
          \(P_n(x) = \sum_{k=0}^n a_k \cdot x^k\)
        </center>
        
        <br /> onde o coeficiente do polinômio \(a_n\) é<br /> 
        
        <center>
          \(a_k = 2^n \cdot \binom{n}{k} \cdot \binom{\frac{n+k-1}2}{n}\)
        </center>
        
        <br /> Os primeiros polinômios de Legendre são ilustrados no gráfico abaixo
      </p>
      
      <p>
        <a name="#fig1" href="http://www.sawp.com.br/blog/wp-content/uploads/2012/08/legendre.png"><img class="aligncenter size-full wp-image-416" title="" src="http://www.sawp.com.br/blog/wp-content/uploads/2012/08/legendre.png" alt="numerical" width="567" height="401" /></a>
      </p>
      
      <h2>
        Implementação
      </h2>
      
      <p>
        <pre lang="python">def compute_legendre_polynomials_coeficients(n):
    """
    Compute the coefficients of the nth Legendre polynomial.

    [coefficients] = compute_legendre_polynomials_coeficients(n)

    INPUT:
      * n: order of the Legendre polynomial

    return: a list containing the polynomial coefficients of nth Legendre
            polynomial (ordered from the highest to lowest)

    Author: Pedro Garcia [sawp@sawp.com.br]
    see: http://www.sawp.com.br

    License: Creative Commons
             http://creativecommons.org/licenses/by-nc-nd/2.5/br/

    Jul 2012
    """
    b = 2.0 ** n
    B = binomial_coefficients
    a = [b * B(n, k) * B((n + k - 1) / 2.0, n) for k in xrange(0, n + 1)]
    a.reverse()
    return a</pre>
      </p>
      
      <p>
        Disponível para download em <a href="http://www.sawp.com.br/code/misc/legendre_coefficients_generator.py" target="_blank">http://www.sawp.com.br/code/misc/legendre_coefficients_generator.py</a>
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <h2>
        Copyright
      </h2></p> 
      
      <p>
        Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>.
      </p>
      
      <p>
      </p>
      
      <fieldset>
        <legend> 
        
        <h2>
          References
        </h2></legend> 
        
        <p>
          <a name="bibitem1"><b>[1]</b> </a><a href="http://mathworld.wolfram.com/LegendrePolynomial.html" target="_blank">http://mathworld.wolfram.com/LegendrePolynomial.html</a><br /> </fieldset>
        </p>
