---
id: 497
title: '1.2.5 Raízes de Equações &#8212; Métodos Abertos &#8212; Método de Steffensen'
date: 2010-03-10T23:03:47+00:00
author: SAWP
excerpt: |
  O Método de Steffensen é uma técnica de busca de raízes de funções muito semelhante ao Método de Newton-Raphson, mas que substitui a derivada da função por uma aproximação.
  
  Este método se difere do Método da Secante por permitir que o delta-quadrado de Aitken seja usado para permitir a aceleração da convergência em alguns casos.
  
  Neste artigo, é apresentado a demonstração do Método de Steffensen, seguido de um comentário sobre o processo de Aitken e como isto é   implementado em um programa.
layout: post
guid: http://www.sawp.com.br/blog/?p=497
permalink: p=497
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:7537:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> Steffensen<span style="color: black;">&#40;</span>f<span style="color: #66cc66;">,</span> x0<span style="color: #66cc66;">=</span><span style="color: #ff4500;">1.0</span><span style="color: #66cc66;">,</span> errto<span style="color: #66cc66;">=</span><span style="color: #ff4500;">0.001</span><span style="color: #66cc66;">,</span> imax<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;
    Return the root of a function (using the Steffensen Method)
    &nbsp;
    Steffensen(f, x0=1.0, errto=0.001, imax=100)
    &nbsp;
    * f: Function where find the roots
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    &nbsp;
    return: the root next x0
    &nbsp;
    Author: Pedro Garcia &lt;sawp @sawp.com.br&gt;
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    &nbsp;
    Dec 2009
    &quot;&quot;&quot;</span>
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> errto + <span style="color: #ff4500;">1</span>
    iterCount <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    x2 <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">&gt;</span> errto <span style="color: #ff7700;font-weight:bold;">and</span> iterCount <span style="color: #66cc66;">&lt;</span> imax:
    h1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x0<span style="color: black;">&#41;</span>
    t1 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x0 + h1<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> fabs<span style="color: black;">&#40;</span>t1 - h1<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    x1 <span style="color: #66cc66;">=</span> x0 - h1*h1/<span style="color: black;">&#40;</span>t1 - h1<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    x2 <span style="color: #66cc66;">=</span> x0
    <span style="color: #ff7700;font-weight:bold;">break</span>
    &nbsp;
    h2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x1<span style="color: black;">&#41;</span>
    t2 <span style="color: #66cc66;">=</span> f<span style="color: black;">&#40;</span>x1 + h2<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> fabs<span style="color: black;">&#40;</span>t2 - h2<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    x2 <span style="color: #66cc66;">=</span> x1 - h2*h2/<span style="color: black;">&#40;</span>t2 - h2<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">break</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># try Aitkens optimization</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>x2 - <span style="color: #ff4500;">2</span>*x1 + x0<span style="color: black;">&#41;</span> <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    alpha <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>x0*x2 - x1*x1<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>x2 - <span style="color: #ff4500;">2</span>*x1 + x0<span style="color: black;">&#41;</span>
    C1 <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>alpha - x1<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>alpha - x0<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    C2 <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>alpha - x2<span style="color: black;">&#41;</span>/<span style="color: black;">&#40;</span>alpha - x1<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>C1 <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: black;">&#40;</span>C2 <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
    x2 <span style="color: #66cc66;">=</span> alpha
    &nbsp;
    iterCount +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> x2 <span style="color: #66cc66;">!=</span> <span style="color: #ff4500;">0</span>:
    <span style="color: #dc143c;">errno</span> <span style="color: #66cc66;">=</span> fabs<span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>x2-x0<span style="color: black;">&#41;</span>/x2<span style="color: black;">&#41;</span>
    &nbsp;
    x0 <span style="color: #66cc66;">=</span> x2
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> x2</pre></td></tr></table><p class="theCode" style="display:none;">def Steffensen(f, x0=1.0, errto=0.001, imax=100):
    &quot;&quot;&quot;
    Return the root of a function (using the Steffensen Method)
    
    Steffensen(f, x0=1.0, errto=0.001, imax=100)
    
    * f: Function where find the roots
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed
    
    return: the root next x0
    
    Author: Pedro Garcia &lt;sawp @sawp.com.br&gt;
    see: http://www.sawp.com.br
    License: Creative Commons
    &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/&gt;
    
    Dec 2009
    &quot;&quot;&quot;
    errno = errto + 1
    iterCount = 0
    x2 = 0
    
    while errno &gt; errto and iterCount &lt; imax:
    h1 = f(x0)
    t1 = f(x0 + h1)
    
    if fabs(t1 - h1) != 0:
    x1 = x0 - h1*h1/(t1 - h1)
    else:
    x2 = x0
    break
    
    h2 = f(x1)
    t2 = f(x1 + h2)
    
    if fabs(t2 - h2) != 0:
    x2 = x1 - h2*h2/(t2 - h2)
    else:
    break
    
    # try Aitkens optimization
    if (x2 - 2*x1 + x0) != 0:
    alpha = (x0*x2 - x1*x1)/(x2 - 2*x1 + x0)
    C1 = fabs((alpha - x1)/(alpha - x0))
    C2 = fabs((alpha - x2)/(alpha - x1))
    
    if (C1 &lt; 1) and (C2 &lt; 1):
    x2 = alpha
    
    iterCount += 1
    
    if x2 != 0:
    errno = fabs((x2-x0)/x2)
    
    x0 = x2
    
    return x2</p></div>
    ";}
categories:
  - Computational Methods
---
## 1. Introdução <a name="sec1"></a> </p> 

O Método de Steffensen é uma técnica de busca de raízes de funções muito semelhante ao Método de Newton-Raphson, onde substitui a derivada da função por uma aproximação. 

Como todos métodos abertos são formas variantes do Método do Ponto Fixo, abordagem utilizada por Johan Frederik Steffensen consiste em aplicar este método para encontrar uma aproximação para a derivada da função. 

O Método de Steffensen, assim como o de Newton, também possui convergência quadrática, uma vez que utiliza o a fórmula de aceleração de Aitken para convergir à esta taxa usando o Ponto Fixo. </p> 

## 2. O Processo Delta-quadrado de Aitken <a name="sec2"></a> 

Um processo iterativo que converge linearmente possui a seguinte forma:
    
<a name="eq1">(eq1)</a>
      


<center>
  <br /> \(\alpha-x_{i+1}=C_{i} \left( \alpha-x_{i} \right) \)<br />
</center>


    
onde \(\alpha-x\_{i+1}=C\_{i} \left( \alpha-x\_{i} \right) \) . Contudo, quando \(\left| C\_{i} \right| =C \) temos que o erro assintótico é constante. Se neste processo a convergência se manter estável próximo à raiz, então a próxima iteração terá a mesma forma. Ou seja:
   
<a name="eq2">(eq2)</a>
      


<center>
  <br /> \( \alpha-x_{i+2}=C_{i} \left( \alpha-x_{i+1} \right) \)<br />
</center>


    
Tratando estas expressões como um sistema linear, temos que:
    
<a name="eq3">(eq3)</a>
      


<center>
  <br /> \( \alpha-x_{i+2}=C \left( \alpha-x_{i+1} \right) \)<br />
</center>

<a name="eq4">(eq4)</a>
      


<center>
  <br /> \( \alpha-x_{i+1}=C \left( \alpha-x_{i} \right) \)<br />
</center>


    
Substituindo uma expressão na outra, obteremos:
   
<a name="eq5">(eq5)</a>
      


<center>
  <br /> \( {\dfrac {\alpha-x_{i+2}}{\alpha-x_{i+1}}={\dfrac {\alpha-x_{i+1}}{\alpha-x_{i}} \)<br />
</center>


    
logo, resolvendo alfa:
    
<a name="eq6">(eq6)</a>
      


<center>
  <br /> \( \alpha={\dfrac {x_{i}x_{i+2}-{x_{i+1}}^{2}{x_{i+2}-2\,x_{i+1}+x_{i}}\)<br />
</center>

A expressão acima é conhecida como &#8220;Fórmula de Aitken&#8221; e é utilizada para acelerar a convergência da sequência linear dos elementos de \(x \) , e o processo de obtenção dela é conhecido como &#8220;processo delta-quadrado de Aitken&#8221;[[1]](#bibitem1). </p> 

## 3. Desenvolvimento do Método de Laguerre <a name="sec3">(sec3)</a> 

Como uma raiz \(x\_{n} \) de uma função \(f \) é um valor tal que \(f(x\_{n}) = 0 \) , para uma função com derivada contínua, vamos supor que ela satisfaça a seguinte condição:
    
<a name="eq7">(eq7)</a>
      


<center>
  <br /> \( -1 < {\dfrac {d}{dx}f \left( x \right) < 0 [/latex]
</center>

Note que esta suposição é pouco adequada, pois nem sempre é possível usarmos uma estimativa inicial próxima o suficiente da raiz para que a aproximação atinja a condição em é verdadeira. Sendo assim, poderia haver casos em que o método convergiria rápido, enquanto haveria outros casos em que ele demoraria demasiadamente. 

Sendo assim, vamos tomar a definição de derivada:
     
<a name="eq8">(eq8)</a>
      


<center>
  <br /> [latex] {\dfrac {d}{dx}f \left( x \right) ={\dfrac {f \left( x+\Delta\,x \right) -f \left( x \right) }{\Delta\,x} \)<br />
</center>


    
por conveniência, tomamos \(\Delta\,x=h \) na Equação [8](#eq8),
    
<a name="eq9">(eq9)</a>
      


<center>
  <br /> \( {\dfrac {d}{dx}f \left( x \right) ={\dfrac {f \left( x+h \right) -f \left( x \right) }{h} \)<br />
</center>

Para atingirmos a condição requerida no começo desta seção, usamos o intervalo em \(x \) tal que
    
<a name="eq10">(eq10)</a>
      


<center>
  <br /> \( h=f \left( x \right) \)<br />
</center>


    
Note que esta aproximação é aplicada sucessivas vezes no processo iterativo é o Método do Ponto Fixo. Como dito na introdução deste artigo, usamos este método para aproximar a derivada da função:
   
<a name="eq11">(eq11)</a>
      


<center>
  <br /> \( {\dfrac {d}{dx}f \left( x_{i} \right) ={\dfrac {f \left( x_{i}+h \right) -f \left( x_{i} \right) }{h} = {\dfrac {f \left( x_{i}+f \left( x_{i}\right) \right) -f \left( x_{i} \right) }{f \left( x_{i} \right) } \)<br />
</center>

Pelo método de Newton-Raphson, temos:
    
<a name="eq12">(eq12)</a>
      


<center>
  <br /> \( x_{i+1}=x_{i}-{\dfrac {f \left( x_{i} \right) }{\dfrac {d}{dx}f \left( x_{i} \right) }\)<br />
</center>


    
Aplicando a aproximação da derivada na expressão acima, obtemos:
    
<a name="eq13">(eq13)</a>
      


<center>
  <br /> \( x_{i+1}=x_{i}-{\dfrac { \left( f \left( x_{i} \right) \right) ^{2}{f \left( x_{i}+f \left( x_{i} \right) \right) -f \left( x_{i} \right) }\)<br />
</center>

<a name="eq14">(eq14)</a>
      


<center>
  <br /> \( x_{i+2}=x_{i+1}-{\dfrac { \left( f \left( x_{i+1} \right) \right) ^{2}{f \left( x_{i+1}+f \left( x_{i+1} \right) \right) -f \left( x_{i+1}\right) } \)<br />
</center>


     
Para evitar o problema da convergência citado, usaremos o processo do Delta-quadrado, demonstrado na Seção [2](#sec2):
    
<a name="eq15">(eq15)</a>
      


<center>
  <br /> \( \alpha={\dfrac {x_{i}x_{i+2}-{x_{i+1}}^{2}{x_{i+2}-2\,x_{i+1}+x_{i}} \)<br />
</center>

O processo de Aitken aplicado às Equações [13](#eq13) e [14](#eq14) nos fornece uma nova aproximação tal que
   
<a name="eq16">(eq16)</a>
      


<center>
  <br /> \( x_{i+3} = \alpha={\dfrac {x_{i}x_{i+2}-{x_{i+1}}^{2}{x_{i+2}-2\,x_{i+1}+x_{i}} \)<br />
</center></p> 

## 4. Implementação <a name="seq4"></a> 

<div>
  <pre lang="python">def Steffensen(f, x0=1.0, errto=0.001, imax=100):
    """
    Return the root of a function (using the Steffensen Method)

     Steffensen(f, x0=1.0, errto=0.001, imax=100)

    * f: Function where find the roots
    * x0: next point (estimative)
    * errto: tolerated error
    * imax: max of iterations allowed

    return: the root next x0

    Author: Pedro Garcia &lt;sawp @sawp.com.br>
    see: http://www.sawp.com.br
    License: Creative Commons
         &lt;http ://creativecommons.org/licenses/by-nc-nd/2.5/br/>

    Dec 2009
    """
    errno = errto + 1
    iterCount = 0
    x2 = 0

    while errno > errto and iterCount &lt; imax:
        h1 = f(x0)
        t1 = f(x0 + h1)

        if fabs(t1 - h1) != 0:
            x1 = x0 - h1*h1/(t1 - h1)
        else:
            x2 = x0
            break

        h2 = f(x1)
        t2 = f(x1 + h2)

        if fabs(t2 - h2) != 0:
            x2 = x1 - h2*h2/(t2 - h2)
        else:
            break

        # try Aitkens optimization
        if (x2 - 2*x1 + x0) != 0:
            alpha = (x0*x2 - x1*x1)/(x2 - 2*x1 + x0)
            C1 = fabs((alpha - x1)/(alpha - x0))
            C2 = fabs((alpha - x2)/(alpha - x1))

            if (C1 &lt; 1) and (C2 &lt; 1):
                x2 = alpha

        iterCount += 1

        if x2 != 0:
            errno = fabs((x2-x0)/x2)

        x0 = x2

    return x2</pre>
  
  <p>
    </sawp></div>
  </p>
  
  <p>
    Note que no código acima o delta-quadrado só é usado sob certas condições. Isto se dá porque nem sempre é possível utilizar o processo, uma vez que ele requer que a constante C obedeça à certas condições, mencionadas na Seção <a href="#sec2">2</a>.
  </p>
  
  <p>
    Outro fator a ser observado neste código, que não foi mencionado no desenvolvimento do texto, é a inserção das variáveis <i>t1 </i> e <i>t2 </i>, que servem para avaliar a variação da aproximação em torno de um ponto. Quando esta variação é muito pequena, podemos tomar como sendo o limite naquele ponto.
  </p>
  
  <p>
    Um exemplo da utilização desta função pode ser encontrado em: <a href="http://www.sawp.com.br/code/rootfind/steffensen.py" target="_blank">http://www.sawp.com.br/code/rootfind/steffensen.py</a>
  </p></p> 
  
  <p>
    <h2>
      5. Conclusão <a name="seq5"></a>
    </h2>
  </p>
  
  <p>
    Como visto, o Método de Steffensen utiliza uma aproximação numérica para a derivada e a aplica no método de Newton. O resultado disto é uma fórmula que também possui convergência quadrática, mas que não requer a função derivada, sendo uma opção muito mais abrangente ao ser programada. O ponto fraco deste método está na estimativa inicial. Assim como no método do Ponto Fixo, pode ocorrer da sequência não convergir ao longo da execução, devido à suposição de que \(h=f(x) \) . Para tentar evitar este comportamento, aplicamos a Fórmula de Aitken no programa. Contudo, para iterações onde a ordem de convergência é maior que um, ela não deveria ser usada, pois ela surge de uma suposição de que a sequência é linear.
  </p>
  
  <p>
    Caso seja necessário implementar aceleração de convergência para sequências não-lineares, uma bibliografia a ser consultada é <i>&#8220;Iterative Methods for Solution of Equations&#8217;</i>&#8216;<a href="#bibitem2">[2]</a>.
  </p></p> </p> 
  
  <p>
    <h2>
      6. Copyright
    </h2>
  </p>
  
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
      <a></a><br /> <a name="bibitem1"><b>[1]</b> Ralston, Anthony and Rabinowitz, Philip,<cite> <em>A First Course in Numerical Analysis.</em>,(2nd ed.)</cite> McGraw-Hill and Dover, (2001), 358&#8211;359.</a><br /> <a name="bibitem2"><b>[2]</b> J.F. Traub and N.J Cliffs,<cite> <em>Iterative Methods for Solution of Equations</em></cite> Prentice Hall, (1964), 185.</a><br /> <a name="bibitem3"><b>[3]</b> <cite>http://en.wikipedia.org/wiki/Steffensen%27s_method</cite></a><br /> <a name="bibitem4"><b>[4]</b> L. W. Johnson and D. R. Scholz,<cite> <em>On Steffensen&#8217;s Method</em>,</cite> Journal on Numerical Analysis, <b>Vol.5</b>(N.2)(1968), 296&#8211;302.</a>
    </p>
  </fieldset>
  
  <p>
    </center>
  </p>
