---
id: 463
title: '1.3.2 Raízes de Equações &#8212; Raízes de Polinômios &#8212; O Método de Muller'
date: 2010-03-09T18:27:53+00:00
author: SAWP
excerpt: '    O Método de Muller é uma técnica modificada do Método da Secante, mas que ao contrário dessa, não estima a raiz de uma função prolongando uma reta através de dois pontos -- fazendo com que esta reta seja secante à curva da função --, e sim utiliza-se de uma parábola através de três pontos para aproximação da derivada.'
layout: post
guid: http://www.sawp.com.br/blog/?p=463
permalink: /p=463
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:12092:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #66cc66;">!</span> -
    <span style="color: #66cc66;">!</span> muller
    <span style="color: #66cc66;">!</span> <span style="color: #ff7700;font-weight:bold;">return</span> the <span style="color: black;">&#91;</span><span style="color: #008000;">complex</span><span style="color: black;">&#93;</span> root of a function <span style="color: black;">&#40;</span>using the Muller Method<span style="color: black;">&#41;</span>
    <span style="color: #66cc66;">!</span>
    <span style="color: #66cc66;">!</span> F: function pointer
    <span style="color: #66cc66;">!</span> x: some initial point
    <span style="color: #66cc66;">!</span> imax: <span style="color: #008000;">max</span> of iterations allowed
    <span style="color: #66cc66;">!</span> errto: tolerated error
    <span style="color: #66cc66;">!</span>
    <span style="color: #66cc66;">!</span> Author: Pedro Garcia sawp<span style="color: #66cc66;">@</span>sawp.<span style="color: black;">com</span>.<span style="color: black;">br</span>
    <span style="color: #66cc66;">!</span> see: http:<span style="color: #66cc66;">!</span>www.<span style="color: black;">sawp</span>.<span style="color: black;">com</span>.<span style="color: black;">br</span>
    <span style="color: #66cc66;">!</span> License: Creative Commons
    <span style="color: #66cc66;">!</span>          <span style="color: #66cc66;">&lt;</span>http ://creativecommons.<span style="color: black;">org</span>/licenses/by-nc-nd/<span style="color: #ff4500;">2.5</span>/br/<span style="color: #66cc66;">&gt;</span>
    <span style="color: #66cc66;">!</span> ago <span style="color: #ff4500;">2009</span>
    <span style="color: #66cc66;">!</span>
    <span style="color: #008000;">complex</span> function muller<span style="color: black;">&#40;</span>F<span style="color: #66cc66;">,</span> x<span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">,</span> imax<span style="color: black;">&#41;</span>
    implicit none<span style="color: #66cc66;">;</span>
    <span style="color: #008000;">complex</span><span style="color: #66cc66;">,</span> external :: F<span style="color: #66cc66;">;</span>
    real<span style="color: #66cc66;">,</span> intent<span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">in</span><span style="color: black;">&#41;</span> :: errto<span style="color: #66cc66;">;</span>
    real<span style="color: #66cc66;">,</span> intent<span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">in</span><span style="color: black;">&#41;</span> :: x<span style="color: #66cc66;">;</span>
    integer<span style="color: #66cc66;">,</span> intent<span style="color: black;">&#40;</span><span style="color: #ff7700;font-weight:bold;">in</span><span style="color: black;">&#41;</span> :: imax<span style="color: #66cc66;">;</span>
    &nbsp;
    <span style="color: #66cc66;">!</span> iteration counter <span style="color: #66cc66;">!</span>
    integer :: iterCount<span style="color: #66cc66;">;</span>
    &nbsp;
    <span style="color: #66cc66;">!</span> relative error <span style="color: #66cc66;">!</span>
    real :: dx<span style="color: #66cc66;">;</span>
    &nbsp;
    <span style="color: #66cc66;">!</span>
    <span style="color: #008000;">complex</span> :: a<span style="color: #66cc66;">,</span>b<span style="color: #66cc66;">,</span>c<span style="color: #66cc66;">;</span>
    <span style="color: #008000;">complex</span> :: x0<span style="color: #66cc66;">,</span>x1<span style="color: #66cc66;">,</span>x2<span style="color: #66cc66;">,</span>x3<span style="color: #66cc66;">;</span>
    <span style="color: #008000;">complex</span> h0<span style="color: #66cc66;">,</span> h1<span style="color: #66cc66;">,</span> d0<span style="color: #66cc66;">,</span> d1<span style="color: #66cc66;">,</span> delta<span style="color: #66cc66;">,</span> denominator<span style="color: #66cc66;">;</span>
    &nbsp;
    <span style="color: #66cc66;">!</span> initialization block
    call random_seed<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    call random_number<span style="color: black;">&#40;</span>dx<span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    x2 <span style="color: #66cc66;">=</span> cmplx<span style="color: black;">&#40;</span>x<span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span>.<span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    x1 <span style="color: #66cc66;">=</span> cmplx<span style="color: black;">&#40;</span>x + dx*x<span style="color: #66cc66;">,</span><span style="color: #ff4500;">0</span>.<span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    x0 <span style="color: #66cc66;">=</span> cmplx<span style="color: black;">&#40;</span>x - dx*x<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span>.<span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    dx <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">100</span>.<span style="color: black;">d0</span><span style="color: #66cc66;">;</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span><span style="color: #66cc66;">;</span>
    &nbsp;
    do
    iterCount <span style="color: #66cc66;">=</span> iterCount + <span style="color: #ff4500;">1</span><span style="color: #66cc66;">;</span>
    h0 <span style="color: #66cc66;">=</span> x1 - x0<span style="color: #66cc66;">;</span>
    h1 <span style="color: #66cc66;">=</span> x2 - x1<span style="color: #66cc66;">;</span>
    d0 <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span> - f<span style="color: black;">&#40;</span>x2<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>/h0<span style="color: #66cc66;">;</span>
    d1 <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>f<span style="color: black;">&#40;</span>x2<span style="color: black;">&#41;</span> - f<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>/h1<span style="color: #66cc66;">;</span>
    &nbsp;
    a <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>d1 - d0<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>h1+h0<span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    b <span style="color: #66cc66;">=</span> a*h1 + d1<span style="color: #66cc66;">;</span>
    c <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x2<span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    &nbsp;
    delta <span style="color: #66cc66;">=</span> sqrt<span style="color: black;">&#40;</span>b*b - <span style="color: #ff4500;">4</span>.*a*c<span style="color: black;">&#41;</span><span style="color: #66cc66;">;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span><span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>b+delta<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>b-delta<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> then
    denominator <span style="color: #66cc66;">=</span> b + delta<span style="color: #66cc66;">;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>
    denominator <span style="color: #66cc66;">=</span> b - delta<span style="color: #66cc66;">;</span>
    end <span style="color: #ff7700;font-weight:bold;">if</span>
    &nbsp;
    dx <span style="color: #66cc66;">=</span> -<span style="color: #ff4500;">2</span>.*c/denominator<span style="color: #66cc66;">;</span>
    x3 <span style="color: #66cc66;">=</span> x2 + dx<span style="color: #66cc66;">;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span><span style="color: black;">&#40;</span> <span style="color: black;">&#40;</span><span style="color: #008000;">abs</span><span style="color: black;">&#40;</span>dx<span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> errto*real<span style="color: black;">&#40;</span>x<span style="color: black;">&#41;</span> <span style="color: black;">&#41;</span> .<span style="color: #ff7700;font-weight:bold;">or</span>. <span style="color: black;">iterCount</span> <span style="color: #66cc66;">&gt;</span>imax <span style="color: black;">&#41;</span>then
    exit<span style="color: #66cc66;">;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>
    x0 <span style="color: #66cc66;">=</span> x1<span style="color: #66cc66;">;</span>
    x1 <span style="color: #66cc66;">=</span> x2<span style="color: #66cc66;">;</span>
    x2 <span style="color: #66cc66;">=</span> x3<span style="color: #66cc66;">;</span>
    end <span style="color: #ff7700;font-weight:bold;">if</span>
    end do
    &nbsp;
    muller <span style="color: #66cc66;">=</span> x3<span style="color: #66cc66;">;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span><span style="color: #66cc66;">;</span>
    end function muller</pre></td></tr></table><p class="theCode" style="display:none;">! -
    ! muller
    ! return the [complex] root of a function (using the Muller Method)
    !
    ! F: function pointer
    ! x: some initial point
    ! imax: max of iterations allowed
    ! errto: tolerated error
    !
    ! Author: Pedro Garcia sawp@sawp.com.br
    ! see: http:!www.sawp.com.br
    ! License: Creative Commons
    !          &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    ! ago 2009
    !
    complex function muller(F, x, errto, imax)
    implicit none;
    complex, external :: F;
    real, intent(in) :: errto;
    real, intent(in) :: x;
    integer, intent(in) :: imax;
    
    ! iteration counter !
    integer :: iterCount;
    
    ! relative error !
    real :: dx;
    
    !
    complex :: a,b,c;
    complex :: x0,x1,x2,x3;
    complex h0, h1, d0, d1, delta, denominator;
    
    ! initialization block
    call random_seed();
    call random_number(dx);
    x2 = cmplx(x,0.);
    x1 = cmplx(x + dx*x,0.);
    x0 = cmplx(x - dx*x, 0.);
    dx = 100.d0;
    iterCount = 0;
    
    do
    iterCount = iterCount + 1;
    h0 = x1 - x0;
    h1 = x2 - x1;
    d0 = (f(x1) - f(x2))/h0;
    d1 = (f(x2) - f(x1))/h1;
    
    a = (d1 - d0)/(h1+h0);
    b = a*h1 + d1;
    c = f(x2);
    
    delta = sqrt(b*b - 4.*a*c);
    
    if (abs(b+delta) &gt; abs(b-delta)) then
    denominator = b + delta;
    else
    denominator = b - delta;
    end if
    
    dx = -2.*c/denominator;
    x3 = x2 + dx;
    
    if( (abs(dx) &lt; errto*real(x) ) .or. iterCount &gt;imax )then
    exit;
    else
    x0 = x1;
    x1 = x2;
    x2 = x3;
    end if
    end do
    
    muller = x3;
    
    return;
    end function muller</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> 

O Método de Muller é uma técnica modificada do Método da Secante, mas que ao contrário dessa, não estima a raiz de uma função prolongando uma reta através de dois pontos &#8212; fazendo com que esta reta seja secante à curva da função &#8211;, e sim utiliza-se de uma parábola através de três pontos para aproximação da derivada. 

A Figura [1](#fig1) contém uma ilustração de uma aproximação qualquer, utilizando-se pontos em comum entre ambos os métodos. 

<center>
  <br /> <a href="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig19_1.png"><img class="aligncenter size-full wp-image-467" title="Visualização gráfica da aproximação numérica de uma raiz qualquer usando os métodos da Secante e de Muller " src="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig19_1.png" alt="" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig19_1.png 400w, http://www.sawp.com.br/blog/wp-content/uploads/2010/03/fig19_1-300x300.png 300w" sizes="(max-width: 400px) 100vw, 400px" /></a><br />
</center>

Através de um processo iterativo, substitui-se os coeficientes para obter o ponto da parábola que intercepta o eixo abscisso. 

## 2. Desenvolvimento do Método <a name="sec2"></a> 

Pelo fato do Método de Muller aproximar uma parábola, é conveniente descrever uma função de aproximação que tenha a forma quadrática, tal como <a name="eq1">(eq1)</a> 

<p align="center">
  <center>
    $$ f_{i} = a \left( x &#8211; x_{i} \right)^2 + b \left( x &#8211; x_{i} \right) + c $$
  </center>
</p>

Escolhendo três pontos interceptantes à função: $$\left( x0, f(x0) \right) $$, $$\left( x1, f(x1) \right) $$ e $$\left( x2, f(x2) \right) $$ para substituí-los na Equação [1](#eq1) , geramos o conjunto de equações:
    
<a name="eq2">(eq2)</a>

<p align="center">
  <center>
    $$f_{0} = a \left( x &#8211; x_{0} \right)^2 + b \left( x &#8211; x_{0} \right) + c $$
  </center>
</p>

<a name="eq3">(eq3)</a> 

<p align="center">
  <center>
    $$ f_{1} = a \left( x &#8211; x_{1} \right)^2 + b \left( x &#8211; x_{1} \right) + c $$
  </center>
</p>

<a name="eq4">(eq4)</a> 

<p align="center">
  <center>
    $$ f_{2} = a \left( x &#8211; x_{2} \right)^2 + b \left( x &#8211; x_{2} \right) + c $$
  </center>
</p>

Para simplificar a função $$f $$ , tomaremos $$x = 2x\_i &#8211; x\_2 $$ , o que nos leva a
    
obter o conjunto de equações:
    
<a name="eq5">(eq5)</a>

<p align="center">
  <center>
    $$ f_{0} = a \left( x_{0} &#8211; x_{2} \right)^2 + b \left( x_{0} &#8211; x_{2} \right) + c $$
  </center>
</p>

<a name="eq6">(eq6)</a> 

<p align="center">
  <center>
    $$ f_{1} = a \left( x_{1} &#8211; x_{2} \right)^2 + b \left( x_{1} &#8211; x_{2} \right) + c $$
  </center>
</p>

<a name="eq7">(eq7)</a> 

<p align="center">
  <center>
    $$ f_{2} = a \left( x_{2} &#8211; x_{2} \right)^2 + b \left( x_{2} &#8211; x_{2} \right) + c = c $$
  </center>
</p>

A partir destas três equações, podemos determinar as três incógnitas: $$a $$ , $$b $$ e $$c $$ . Como dado pela última equação, $$c=f(x_2) $$ , que é o valor da função avaliada na terceira aproximação. Ao sobstituirmos este coeficiente nas outras equações, obtemos:
    
<a name="eq8">(eq8)</a>

<p align="center">
  <center>
    $$ f(x_{0}) &#8211; f(x_{2}) = a \left( x_{0} &#8211; x_{2} \right) ^2 + b \left( x_{0} &#8211; x_{2} \right) $$
  </center>
</p>

<a name="eq9">(eq9)</a> 

<p align="center">
  <center>
    $$ f(x_{1}) &#8211; f(x_{2}) = a \left( x_{1} &#8211; x_{2} \right) ^2 + b \left( x_{1} &#8211; x_{2} \right) $$
  </center>
</p>

Para simplificar esta demonstração e uma possível codificação, definimos as seguintes variáveis:
    
<a name="eq10">(eq10)</a> 

<p align="center">
  <center>
    $$ h_{0} = x_{1} &#8211; x_{0} $$
  </center>
</p>

<a name="eq11">(eq11)</a> 

<p align="center">
  <center>
    $$ h_{1} = x_{2} &#8211; x_{1} $$
  </center>
</p>

<a name="eq12">(eq12)</a> 

<p align="center">
  <center>
    $$ d_{0} = \dfrac{ f(x_{1}) &#8211; f(x_{0}) }{ x_{1} &#8211; x_{0} } $$
  </center>
</p>

<a name="eq13">(eq13)</a> 

<p align="center">
  <center>
    $$ d_{1} = \dfrac{ f(x_{2}) &#8211; f(x_{1}) }{ x_{2} &#8211; x_{1} } $$
  </center>
</p>

Com essas transformações, as Equações [8](#eq8) e [9](#eq9) podem ser escritas de uma forma mais simplificada:
    
<a name="eq14">(eq14)</a>

<p align="center">
  <center>
    $$ b \left( h_{0} + h_{1} \right) &#8211; a \left( h_{0} + h_{1} \right) ^2 = h_{0}d_{0} + h_{1}d_{1} $$
  </center>
</p>

<a name="eq15">(eq15)</a> 

<p align="center">
  <center>
    $$ h_{1} b &#8211; a h_{1}^2 = h_{1}d_{1} $$
  </center>
</p>

isolando os coeficientes a, b e c,
    
<a name="eq16">(eq16)</a>

<p align="center">
  <center>
    $$ a = \dfrac{ d_{1} &#8211; d_{0} }{ h_{1} &#8211; h_{0} } $$
  </center>
</p>

<a name="eq17">(eq17)</a> 

<p align="center">
  <center>
    $$ b = a h_{1} + d_{1} $$
  </center>
</p>

<a name="eq18">(eq18)</a> 

<p align="center">
  <center>
    $$ c = f(x_{2}) $$
  </center>
</p>

Para encontrarmos a raiz, aplicamos a fórmula quadrática na próxima iteração. Como temos $$x\_{0} $$ , $$x\_{1} $$ e $$x\_{2} $$ , podemos encontrar $$x\_{3} $$ da seguinte maneira:
    
<a name="eq19">(eq19)</a> 

<p align="center">
  <center>
    $$ x_{3} &#8211; x_{2} = &#8211; \dfrac{2 c}{b \pm \sqrt{b^2 &#8211; 4 a c} } $$
  </center>
</p>

isolando $$x_{3} $$,
    
<a name="eq20">(eq20)</a>

<p align="center">
  <center>
    $$ x_{3} = x_{2} &#8211; \dfrac{2 c}{b \pm \sqrt{b^2 &#8211; 4 a c} $$
  </center>
</p>

Em um programa, os passos acima são repetidos até quando a aproximação estiver com um erro tolerável. Sendo assim, em uma generalização, $$x\_0 = x\_{i-3} $$ , $$x\_1 = x\_{i-2} $$ , $$x\_2 = x\_{i-1} $$ e $$x\_3 = x\_{i} $$ e o erro relativo é calculado como:
    
<a name="eq21">(eq21)</a> 

<p align="center">
  <center>
    $$ errno = \dfrac{ x_{3} &#8211; x_{2} }{ x_{3} } $$
  </center>
</p>

Dos passos acima é possível ver que a equação que estima $$x_{3} $$ fornece duas raízes. No método de Muller, a estratégia é escolher o sinal de $$b $$ que majore o denominador, aumentando a velocidade de convergência. 

Embora este algoritmo esteja sendo apresentado na busca de raízes de polinômios, ele pode ser utilizado para encontrar raízes de outras classes de funções, da mesma forma que o Método de Newton-Raphson. 

<!--  IMPLEMENTACAO --></p> 

## 3. Implementação <a name="sec3"></a> 

<div>
  <pre lang="python">! -
! muller
! return the [complex] root of a function (using the Muller Method)
!
! F: function pointer
! x: some initial point
! imax: max of iterations allowed
! errto: tolerated error
!
! Author: Pedro Garcia sawp@sawp.com.br
! see: http:!www.sawp.com.br
! License: Creative Commons
!          &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>
! ago 2009
! 
complex function muller(F, x, errto, imax)
        implicit none;
        complex, external :: F;
        real, intent(in) :: errto;
        real, intent(in) :: x;
        integer, intent(in) :: imax;

        ! iteration counter ! 
        integer :: iterCount;

        ! relative error ! 
        real :: dx;

        !
        complex :: a,b,c;
        complex :: x0,x1,x2,x3;
        complex h0, h1, d0, d1, delta, denominator;

        ! initialization block
        call random_seed();
        call random_number(dx);
        x2 = cmplx(x,0.);        
        x1 = cmplx(x + dx*x,0.);
        x0 = cmplx(x - dx*x, 0.);
        dx = 100.d0;
        iterCount = 0;

        do
                iterCount = iterCount + 1;
                h0 = x1 - x0;
                h1 = x2 - x1;
                d0 = (f(x1) - f(x2))/h0;
                d1 = (f(x2) - f(x1))/h1;

                a = (d1 - d0)/(h1+h0);
                b = a*h1 + d1;
                c = f(x2);

                delta = sqrt(b*b - 4.*a*c);

                if (abs(b+delta) > abs(b-delta)) then
                        denominator = b + delta;
                else
                        denominator = b - delta;
                end if

                dx = -2.*c/denominator;
                x3 = x2 + dx;

                if( (abs(dx) &lt; errto*real(x) ) .or. iterCount >imax )then
                        exit;
                else
                        x0 = x1;
                        x1 = x2;
                        x2 = x3;
                end if
        end do

        muller = x3;

        return;
end function muller</pre>
</div>

Para inicializar _x0_ e _x1_ usamos uma variável aleatória para definir o intervalo em torno do ponto passado _x_. Isso serve para delegar à função a escolha da estimativa inicial dos pontos utilizados pelo Método de Muller. 

Esta abordagem pode gerar um comportamento diferente em cada execução. Ou seja, para um mesmo _x_, em uma execução podem ser necessárias _y_ iterações, enquanto que ao rodar o programa outra vez, a raiz seja convergida em _z_ iterações. 

Podemos evitar este comportamento substituindo as linhas 

<center>
  <br /> <i><br /> x1 = cmplx(x + dx*x, 0.);<br /> x0 = cmplx(x &#8211; dx*x, 0.);<br /> </i><br />
</center>


    
por 

<center>
  <br /> <i><br /> x1 = cmplx(x + s*x, 0.);<br /> x0 = cmplx(x &#8211; s*x, 0.);<br /> </i><br />
</center>


    
onde _s_ é o passo que delimitará os outros pontos de avaliação. Veja que também não é necessário utilizar o mesmo _s_, pois qualquer ponto pode ser utilizado. Poderíamos utilizar sem problemas: 

<center>
  <br /> <i><br /> x1 = cmplx(x + s*x, 0.);<br /> x0 = cmplx(x &#8211; k*x, 0.);<br /> </i><br />
</center>


    
onde $$s \neq k $$ . 

Este código pode ser encontrado em <a href="http://www.sawp.com.br/code/rootfind/muller.f90" target="_blank">http://www.sawp.com.br/code/rootfind/muller.f90</a> </p> 

## 4. Copyright 

Este documento é disponível sob a licença Creative Commons. As regras dos direitos de cópia deste conteúdo estão acessíveis em <a href="http://creativecommons.org/licenses/by-nc-nd/2.5/br/" target="_blank">http://creativecommons.org/licenses/by-nc-nd/2.5/br/</a>. 



<fieldset>
  <legend> 
  
  <h2>
    References
  </h2></legend> 
  
  <p>
    <a name="bibitem1"><b>[1]</b> <cite><a href="http://en.wikipedia.org/wiki/Müller's_method">http://en.wikipedia.org/wiki/Müller&#8217;s_method</a><br /> <a name="bibitem2"><b>[2]</b> D.E Muller, <cite> <em>A Method for Solving Algebraic Equations Using an Automatic Computer.</em>,</cite> MTAC, <b>Vol.10</b>,(1956), 208-215.</p> 
    
    <p>
      </a><br /> <a name="bibitem3"><b>[3]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 373.</p> 
      
      <p>
        </a><br /> </cite></a></fieldset>
      </p>
