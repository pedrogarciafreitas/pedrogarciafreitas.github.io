---
id: 457
title: '1.3.1 Raízes de Equações &#8212; Raízes de Polinômios &#8212; Newton-Raphson para polinômios'
date: 2010-03-09T17:33:05+00:00
author: SAWP
excerpt: |
  Os polinômios formam uma classe de função toda especial, contendo propriedades e relações particulares e bem conhecidas. Devido a isso, alguns métodos computacionais foram desenvolvidos de forma a permitir encontrar suas raízes.
  
  Como funções polinomiais formam soluções de diversos problemas físicos, matemáticos e de outras áreas, aplicar o método correto que melhor resolva, certo problema pode ser a chave para uma solução computacionalmente elegante e eficiente.
  
  Este artigo apresenta uma breve introdução aos métodos de busca de zeros de polinômios e dispõe uma adaptação do Método de Newton para suportar raízes complexas -- tipo de solução quase sempre presente para este tipo de função.
layout: post
guid: http://www.sawp.com.br/blog/?p=457
permalink: /p=457
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:9188:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="pascal" style="font-family:monospace;">! <span style="color: #000066;">-</span>
    ! newtonRaphson_c
    ! return the <span style="color: #009900;">&#91;</span>complex<span style="color: #009900;">&#93;</span> root <span style="color: #000000; font-weight: bold;">of</span> a <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #009900;">&#40;</span>using the Newton<span style="color: #000066;">-</span>Raphson Method<span style="color: #009900;">&#41;</span>
    ! G<span style="color: #000066;">:</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #000066; font-weight: bold;">pointer</span>
    ! x<span style="color: #000066;">:</span> some initial point
    ! imax<span style="color: #000066;">:</span> max <span style="color: #000000; font-weight: bold;">of</span> iterations allowed
    ! errto<span style="color: #000066;">:</span> tolerated error
    !
    ! Author<span style="color: #000066;">:</span> Pedro Garcia sawp<span style="color: #000066;">@</span>sawp<span style="color: #000066;">.</span><span style="color: #006600;">com</span><span style="color: #000066;">.</span><span style="color: #006600;">br</span>
    ! see<span style="color: #000066;">:</span> http<span style="color: #000066;">:</span>!www<span style="color: #000066;">.</span><span style="color: #006600;">sawp</span><span style="color: #000066;">.</span><span style="color: #006600;">com</span><span style="color: #000066;">.</span><span style="color: #006600;">br</span>
    !
    ! License<span style="color: #000066;">:</span> Creative Commons
    !          &lt;http <span style="color: #000066;">:</span><span style="color: #808080; font-style: italic;">//creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;</span>
    ! ago <span style="color: #cc66cc;">2009</span>
    !
    complex <span style="color: #000000; font-weight: bold;">function</span> newtonRaphson_c<span style="color: #009900;">&#40;</span>G<span style="color: #000066;">,</span> diffG<span style="color: #000066;">,</span> x<span style="color: #000066;">,</span> errto<span style="color: #000066;">,</span> imax<span style="color: #009900;">&#41;</span>
    implicit none<span style="color: #000066;">;</span>
    complex<span style="color: #000066;">,</span> <span style="color: #000000; font-weight: bold;">external</span> <span style="color: #000066;">::</span> G<span style="color: #000066;">,</span> diffG<span style="color: #000066;">;</span>
    <span style="color: #000066; font-weight: bold;">real</span><span style="color: #000066;">,</span> intent<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">in</span><span style="color: #009900;">&#41;</span> <span style="color: #000066;">::</span> x<span style="color: #000066;">,</span> errto<span style="color: #000066;">;</span>
    <span style="color: #000066; font-weight: bold;">integer</span> <span style="color: #000066;">::</span> imax<span style="color: #000066;">;</span>
    &nbsp;
    ! iteration counter !
    <span style="color: #000066; font-weight: bold;">integer</span> <span style="color: #000066;">::</span> iterCount<span style="color: #000066;">;</span>
    &nbsp;
    ! relative error !
    <span style="color: #000066; font-weight: bold;">real</span><span style="color: #009900;">&#40;</span>kind<span style="color: #000066;">=</span><span style="color: #cc66cc;">8</span><span style="color: #009900;">&#41;</span> <span style="color: #000066;">::</span> errno<span style="color: #000066;">;</span>
    &nbsp;
    ! xi<span style="color: #000066;">+</span><span style="color: #cc66cc;">1</span> !
    complex <span style="color: #000066;">::</span> x1<span style="color: #000066;">,</span>x0<span style="color: #000066;">;</span>
    &nbsp;
    x0 <span style="color: #000066;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #000066;">.,</span><span style="color: #cc66cc;">0</span><span style="color: #000066;">.</span><span style="color: #009900;">&#41;</span><span style="color: #000066;">;</span>
    x1 <span style="color: #000066;">=</span> cmplx<span style="color: #009900;">&#40;</span>x<span style="color: #000066;">,</span> <span style="color: #cc66cc;">0</span><span style="color: #000066;">.</span><span style="color: #006600;">d0</span><span style="color: #009900;">&#41;</span><span style="color: #000066;">;</span>
    errno <span style="color: #000066;">=</span> <span style="color: #cc66cc;">100</span><span style="color: #000066;">.</span><span style="color: #006600;">d0</span><span style="color: #000066;">;</span>
    iterCount <span style="color: #000066;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #000066;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">do</span>
    x0 <span style="color: #000066;">=</span> x1<span style="color: #000066;">;</span>
    x1 <span style="color: #000066;">=</span> x0 <span style="color: #000066;">-</span> G<span style="color: #009900;">&#40;</span>x0<span style="color: #009900;">&#41;</span><span style="color: #000066;">/</span>diffG<span style="color: #009900;">&#40;</span>x0<span style="color: #009900;">&#41;</span><span style="color: #000066;">;</span>
    iterCount <span style="color: #000066;">=</span> iterCount <span style="color: #000066;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #000066;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>x1 <span style="color: #000066;">/=</span> <span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #000066;">.</span><span style="color: #006600;">d0</span><span style="color: #000066;">,</span><span style="color: #cc66cc;">0</span><span style="color: #000066;">.</span><span style="color: #006600;">d0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span><span style="color: #000000; font-weight: bold;">then</span>
    errno <span style="color: #000066;">=</span> <span style="color: #000066;">abs</span><span style="color: #009900;">&#40;</span> <span style="color: #009900;">&#40;</span>cabs<span style="color: #009900;">&#40;</span>x1<span style="color: #009900;">&#41;</span> <span style="color: #000066;">-</span> cabs<span style="color: #009900;">&#40;</span>x0<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #000066;">/</span>cabs<span style="color: #009900;">&#40;</span>x1<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #000066;">*</span> <span style="color: #cc66cc;">100</span><span style="color: #000066;">.</span><span style="color: #006600;">d0</span>
    <span style="color: #000000; font-weight: bold;">end</span> <span style="color: #000000; font-weight: bold;">if</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>errno &lt; errto <span style="color: #000066;">.</span><span style="color: #000000; font-weight: bold;">or</span><span style="color: #000066;">.</span> <span style="color: #006600;">iterCount</span> &gt; imax<span style="color: #009900;">&#41;</span><span style="color: #000000; font-weight: bold;">then</span>
    exit<span style="color: #000066;">;</span>
    <span style="color: #000000; font-weight: bold;">end</span> <span style="color: #000000; font-weight: bold;">if</span>
    <span style="color: #000000; font-weight: bold;">end</span> <span style="color: #000000; font-weight: bold;">do</span>
    &nbsp;
    newtonRaphson_c <span style="color: #000066;">=</span> x1<span style="color: #000066;">;</span>
    return<span style="color: #000066;">;</span>
    <span style="color: #000000; font-weight: bold;">end</span> <span style="color: #000000; font-weight: bold;">function</span> newtonRaphson_c</pre></td></tr></table><p class="theCode" style="display:none;">! -
    ! newtonRaphson_c
    ! return the [complex] root of a function (using the Newton-Raphson Method)
    ! G: function pointer
    ! x: some initial point
    ! imax: max of iterations allowed
    ! errto: tolerated error
    !
    ! Author: Pedro Garcia sawp@sawp.com.br
    ! see: http:!www.sawp.com.br
    !
    ! License: Creative Commons
    !          &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    ! ago 2009
    !
    complex function newtonRaphson_c(G, diffG, x, errto, imax)
    implicit none;
    complex, external :: G, diffG;
    real, intent(in) :: x, errto;
    integer :: imax;
    
    ! iteration counter !
    integer :: iterCount;
    
    ! relative error !
    real(kind=8) :: errno;
    
    ! xi+1 !
    complex :: x1,x0;
    
    x0 = (0.,0.);
    x1 = cmplx(x, 0.d0);
    errno = 100.d0;
    iterCount = 0;
    
    do
    x0 = x1;
    x1 = x0 - G(x0)/diffG(x0);
    iterCount = iterCount + 1;
    
    if(x1 /= (0.d0,0.d0) )then
    errno = abs( (cabs(x1) - cabs(x0))/cabs(x1) ) * 100.d0
    end if
    
    if(errno &lt; errto .or. iterCount &gt; imax)then
    exit;
    end if
    end do
    
    newtonRaphson_c = x1;
    return;
    end function newtonRaphson_c</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

Tanto os métodos intervalares quanto os abertos funcionam quase sempre bem para a busca de raízes em um polinômio, dependendo da natureza destas raízes. 

Se este tiver apenas raízes reais, qualquer método para encontrar raízes pode ser utilizado. Entretanto, quando o polinômio apresenta raízes complexas, os métodos que as isolam não podem ser utilizados devido ao problema de se definir um critério de detecção da raiz, já que os limites dos intervalos não se estendem às aproximações complexas. Sendo assim, a maioria dos métodos intervalares e abertos não são aplicáveis para polinômios de raízes complexas. 

Contudo, o Método de Newton-Raphson pode fornecer as raízes complexas, podendo ser implementado em linguagens que suportem um tipo complexo. Sua única desvantagem é que, dependendo do polinômio, ele poderia ter problemas de convergência. Porém, existem outros algoritmos mais eficientes que buscam raízes &#8212; reais e complexas &#8212; de funções polinomiais. 

<!--  DESENVOLVIMENTO --></p> 

## 2. Newton-Raphson para polinômios <a name="sec2"></a> 

<div>
  <pre lang="pascal">! -
! newtonRaphson_c
! return the [complex] root of a function (using the Newton-Raphson Method)
! G: function pointer
! x: some initial point
! imax: max of iterations allowed
! errto: tolerated error 
!
! Author: Pedro Garcia sawp@sawp.com.br
! see: http:!www.sawp.com.br
!
! License: Creative Commons
!          &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>
! ago 2009
! 
complex function newtonRaphson_c(G, diffG, x, errto, imax)
  implicit none;
  complex, external :: G, diffG;
  real, intent(in) :: x, errto;
  integer :: imax;

  ! iteration counter ! 
  integer :: iterCount;

  ! relative error ! 
  real(kind=8) :: errno;

  ! xi+1 ! 
  complex :: x1,x0;

  x0 = (0.,0.);
  x1 = cmplx(x, 0.d0);
  errno = 100.d0;
  iterCount = 0;

  do
    x0 = x1;
    x1 = x0 - G(x0)/diffG(x0);
    iterCount = iterCount + 1;

    if(x1 /= (0.d0,0.d0) )then      
      errno = abs( (cabs(x1) - cabs(x0))/cabs(x1) ) * 100.d0
    end if

    if(errno &lt; errto .or. iterCount > imax)then
      exit;
    end if  
  end do

  newtonRaphson_c = x1;
  return;
end function newtonRaphson_c</pre>
</div>

Este código pode ser encontrado em <a href="http://www.sawp.com.br/code/rootfind/NR_polinomial.f90" target="_blank">http://www.sawp.com.br/code/rootfind/NR_polinomial.f90</a> </p> </p> 

## 3. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 346&#8211;347.</p> 
    
    <p>
      </a><br /> <a name="bibitem2"><b>[2]</b> N.B Franco,<cite> <em>Cálculo Numérico</em>,</cite> Pearson Prentice Hall, (2006), 76.</p> 
      
      <p>
        </a>
      </p></fieldset>
