---
id: 264
title: 'The Quake3&#8217;s Fast InvSqrt()'
date: 2009-03-30T18:57:13+00:00
author: SAWP
excerpt: |
  O inverso da raiz quadrada é uma função presente em diversos problemas matemáticos, físicos e estatísticos. Vários métodos numéricos são aplicados para busca da melhor forma de se expressar 1/sqrt(x).
  Este artigo discute e analisa um código encontrado nas fontes de vários bibliotecas de C: O InvSqrt é uma função que chama a atenção por sua beleza que vai além da aplicação de um método numérico e utiliza uma manipulação de recursos computacionais para gerar uma função mais veloz.
layout: post
guid: http://www.sawp.com.br/blog/?p=264
permalink: /p=264
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:545:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="c" style="font-family:monospace;">x <span style="color: #339933;">=</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span><span style="color: #993333;">float</span><span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">&amp;</span>i<span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">x = *(float*)&amp;i;</p></div>
    ;i:2;s:714:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="c" style="font-family:monospace;">x <span style="color: #339933;">=</span> x <span style="color: #339933;">*</span> <span style="color: #009900;">&#40;</span><span style="color:#800080;">1.5f</span> – xhalf <span style="color: #339933;">*</span> x <span style="color: #339933;">*</span> x<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// xhalf = 0.5x e x = y, nas demonstracoes</span></pre></td></tr></table><p class="theCode" style="display:none;">x = x * (1.5f – xhalf * x * x);
    // xhalf = 0.5x e x = y, nas demonstracoes</p></div>
    ";}
categories:
  - Miscellaneous
---
## 1.Introdução

O inverso da raiz quadrada é uma função presente em diversos problemas matemáticos, físicos e estatísticos. Aplicações algébricas de normalização, desvio padrão e até na indústria de videogames possuem freqüente utilização da simples expressão:

<p style="text-align: center;">
  <p style="text-align: center;">
    <img class="aligncenter size-full wp-image-265" title="fig11__1" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__1.gif" alt="fig11__1" width="34" height="32" />
  </p>
  
  <p style="text-align: center;">
    <p style="text-align: center;">
      <p>
        E foi na programação de um jogo que surgiu uma função que acabou por se tornar famosa entre os programadores por conseguir rodar até 4 vezes mais rápido que a implementação derivada da função sqrt(x), nativa da biblioteca do C.
      </p>
      
      <p style="text-align: center;">
        <p>
          A função que realizava o cálculo tão mais rapidamente com um erro associado de 1,75x10E-4 se apresentou muito eficiente na época e significou uma melhora considerável na execução do Quake – jogo que utilizava esta operação frenquentemente e para qual foi desenvolvida. O seu código é:
        </p>
        
        <pre lang="”c”">float InvSqrt(float x){
	float xhalf = 0.5f*x;
	int i = *(int*)&x;

	i = 0x5F3759DF – (i>>1);
	x = *(float*)&i;
	x = x*(1.5f – xhalf*x*x);

	return x;
}</pre>
        
        <p style="text-align: center;">
          <p>
            Sua verdadeira autoria é desconhecida. Contudo, tudo indica que foi programada por John Carmack, na época programador do Quake 3, onde surgiu.
          </p>
          
          <p style="text-align: center;">
            <p>
              Para entender esta a genial “sacada” é necessário conhecer o algoritmo matemático usado e como ele foi optimizado graças ao conhecimento do padrão de ponto flutuante pelo autor.
            </p>
            
            <p style="text-align: center;">
              <h2>
                2.O Método de Newton-Rapson
              </h2>
              
              <p style="text-align: center;">
                <p>
                  O algoritmo utilizado foi um método de aproximações numéricas já bastante conhecido em muitos projetos computacionais, conhecido como “Aproximação de Newton”, ou “Método de Newton-Rapson”.
                </p>
                
                <p style="text-align: center;">
                  <p>
                    Este é um método linear iterativo utilizado para encontrar raízes x de uma função f(x) a partir de uma estimativa inicial baseado na idéia de usar retas tangentes para substituir o gráfico y = f(x) próximo de onde f é zero.
                  </p>
                  
                  <p style="text-align: center;">
                    <p>
                      Para tal, cria-se uma função G, chamada “função iteração” xnew = G( xold ) , a partir da função f(x) para se chegar à raiz de f(x). Sendo assim, a convergência deste método será tão rápida quanto for |G'(xold)|.
                    </p>
                    
                    <p style="text-align: center;">
                      <p>
                        O método de Newton-Rapson modifica o método iterativo linear simples (Método do Ponto Fixo Modificado) fazendo com que |G'( xold )|->0. Assim, a fórmula iterativa fica:
                      </p>
                      
                      <p style="text-align: center;">
                        <img class="aligncenter size-full wp-image-266" title="fig11__2" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__2.gif" alt="fig11__2" width="134" height="47" />
                      </p>
                      
                      <p style="text-align: center;">
                        <p>
                          Uma propriedade importante para a função InvSqrt é que o Método de Newton-Rapson converge quadraticamente. Uma interpretação gráfica do método pode ser vista na figura abaixo:
                        </p>
                        
                        <p style="text-align: center;">
                          <img class="aligncenter size-full wp-image-267" title="fig11__3" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__3.gif" alt="fig11__3" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__3.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__3-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
                        </p>
                        
                        <p style="text-align: center;">
                          <h3>
                            2.1.Newton-Rapson na InvSqrt
                          </h3>
                          
                          <p style="text-align: center;">
                            <p>
                              Queremos o retorno da função y=y(x) tal que:
                            </p>
                            
                            <p style="text-align: center;">
                              <br /><img class="aligncenter size-full wp-image-268" title="fig11__4" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__4.gif" alt="fig11__4" width="69" height="32" /><br />
                            </p>
                            
                            <p>
                              contudo, queremos o valor de y, que é a inversa da raíz quadrada. Sendo assim, procuramos a função inversa tal que:
                            </p>
                            
                            <p style="text-align: center;">
                              <br /><img class="aligncenter size-full wp-image-269" title="fig11__5" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__5.gif" alt="fig11__5" width="48" height="13" /><br /> <br /><img class="aligncenter size-full wp-image-270" title="fig11__6" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__6.gif" alt="fig11__6" width="52" height="32" /><br /> <br /><img class="aligncenter size-full wp-image-271" title="fig11__7" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__7.gif" alt="fig11__7" width="45" height="28" /><br /> <br /><img class="aligncenter size-full wp-image-272" title="fig11__8" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__8.gif" alt="fig11__8" width="44" height="31" /><br /> <br /><img class="aligncenter size-full wp-image-273" title="fig11__9" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__9.gif" alt="fig11__9" width="66" height="31" /><br />
                            </p>
                            
                            <p>
                              como sabemos que o Método de Newton-Rapson para encontrar raízes f(x) = 0, então poderíamos substituir a variável x pela y, que é a que queremos encontrar.
                            </p>
                            
                            <p style="text-align: center;">
                              <br /><img class="aligncenter size-full wp-image-274" title="fig11__10" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__10.gif" alt="fig11__10" width="49" height="13" /><br />
                            </p>
                            
                            <p>
                              como
                            </p>
                            
                            <p style="text-align: center;">
                              <br /><img class="aligncenter size-full wp-image-275" title="fig11__11" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__11.gif" alt="fig11__11" width="49" height="13" /><br /> <br /><img class="aligncenter size-full wp-image-276" title="fig11__12" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__12.gif" alt="fig11__12" width="13" height="13" /><br /> <br /><img class="aligncenter size-full wp-image-277" title="fig11__13" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__13.gif" alt="fig11__13" width="66" height="31" /><br />
                            </p>
                            
                            <p>
                              então
                            </p>
                            
                            <p style="text-align: center;">
                              <br /><img class="aligncenter size-full wp-image-278" title="fig11__14" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__14.gif" alt="fig11__14" width="82" height="31" /><br />
                            </p>
                            
                            <p>
                              aplicando o Método de Newton, teremos que:
                            </p>
                            
                            <p style="text-align: center;">
                              <img class="aligncenter size-full wp-image-279" title="fig11__15" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__15.gif" alt="fig11__15" width="134" height="47" />
                            </p>
                            
                            <p>
                              onde sabemos f(y),
                            </p>
                            
                            <p style="text-align: center;">
                              <img class="aligncenter size-full wp-image-278" title="fig11__14" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__14.gif" alt="fig11__14" width="82" height="31" />
                            </p>
                            
                            <p>
                              logo
                            </p>
                            
                            <p style="text-align: center;">
                              <img class="aligncenter size-full wp-image-280" title="fig11__16" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__16.gif" alt="fig11__16" width="91" height="31" />
                            </p>
                            
                            <p>
                              finalmente, a expressão para encontrar o valor de y é:
                            </p>
                            
                            <p style="text-align: center;">
                              <img class="aligncenter size-full wp-image-281" title="fig11__17" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__17.gif" alt="fig11__17" width="160" height="31" />
                            </p>
                            
                            <p>
                              que pode ser reduzida para:
                            </p>
                            
                            <p style="text-align: center;">
                              <img class="aligncenter size-full wp-image-282" title="fig11__18" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__18.gif" alt="fig11__18" width="134" height="20" />
                            </p>
                            
                            <p>
                              ou passando 0.5 para expressão dentro dos parentes,
                            </p>
                            
                            <p style="text-align: center;">
                              <img class="aligncenter size-full wp-image-283" title="fig11__19" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__19.gif" alt="fig11__19" width="143" height="20" />
                            </p>
                            
                            <p>
                              lembrando que quanto maior o número de iterações, mais próximo da raiz será o valor do resultado.
                            </p>
                            
                            <h2>
                              3.I3E 754 de 1985
                            </h2>
                            
                            <p>
                              Para entender a maior “mágica” deste código, é necessário saber como os números de ponto flutuante são armazenados na memória e interpretados pelo processador.<br /> Em ciências exatas é comum se ver a notação científica de base 10 para expressar valores muito grandes ou muito pequenos. Esta notação consiste em usar apenas um único dígito à esquerda do valor decimal. Por exemplo, um valor em notação científica na base 10 é:
                            </p>
                            
                            <p style="text-align: center;">
                              0,8 x 10^-8
                            </p>
                            
                            <p style="text-align: center;">
                              <p>
                                Da mesma forma, podemos expressar números em notação científica em base 2. Por exemplo:
                              </p>
                              
                              <p style="text-align: center;">
                                1,0 x 2^7 (em base 2)
                              </p>
                              
                              <p>
                                Contudo, como não se está trabalhando com a base 10, é conveniente renomear os valores após a vírgula de decimais para ponto binário.<br /> A expressão “ponto flutuante” vêm porque a representação dos números em que o ponto binário não é fixo &#8211; por isso flutua. A linguagem em que o InvSqrt foi implementada, C, utiliza esta o nome “float” para estes números de ponto flutuantes.<br /> Desta forma, internamente o computador armazena todos expoentes em base 2, algo como:
                              </p>
                              
                              <p style="text-align: center;">
                                1,0 x 10^111 ( binário equivalente à 1,0 x 2^7 )
                              </p>
                              
                              <p>
                                Observe que a representação de ponto flutuante implica em encontrar uma relação entre o tamanho da fração e o tamanho do expoente, pois o número de bits da palavra do processador é fixo. Assim, quando se aumenta o tamanho da fração, reduz-se o valor do expoente.<br /> Logo, os números em ponto flutuante seguem o formato:
                              </p>
                              
                              <p style="text-align: center;">
                                (-1)^s x F x 2^E
                              </p>
                              
                              <p>
                                onde s é o sinal do número de ponto flutuante de maior relevância e que também é o bit que indicará o sinal do número (s=0 implica em número positivo, s=1, negativo).
                              </p>
                              
                              <p>
                                F envolve o campo de fração e E são os bits de expoente. Com base nessa lógica, foi elaborado um padrão para pontos flutuantes chamado &#8220;padrão IEEE 754&#8221;, que é implementado em quase todos processadores fabricados desde 1985. A adoção deste padrão permitiu uma portabilidade muito maior entre plataformas e melhorou muito a qualidade numérica de operações aritméticas com valores reais.<br /> Para entender o padrão, veja na tabela abaixo como se relacionam os bits na palavra de uma arquitetura de 32 bits:
                              </p>
                              
                              <p style="text-align: center;">
                                <img class="aligncenter size-full wp-image-284" title="fig11_20ieee754_1_float" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_20ieee754_1_float.jpg" alt="fig11_20ieee754_1_float" width="649" height="60" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_20ieee754_1_float.jpg 649w, http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_20ieee754_1_float-300x27.jpg 300w" sizes="(max-width: 649px) 100vw, 649px" />
                              </p>
                              
                              <p>
                                Note que reservando 8 bits para o expoente temos que 7 bits são utilizados para o valor do expoente e 1 sinal é reservado para o sinal do expoente. Isso equivale em decimal à um range de 2&#215;10^-38 a 2&#215;10^38.<br /> Seguindo a mesma idéia da notação de ponto flutuante de precisão simples (float), é implementada a precisão dupla (tipo “double”). Esta porém, utiliza 2 registradores de 32 bits em arquiteturas com esta palavra de processador, ou 1 registrador de 64 bits para a representação de ponto flutuante com precisão maior.<br /> No caso da precisão dupla em processadores 32 bits, 1 registrador armazena 32 bits para a fração e outro registrador possui a seguinte divisão:
                              </p>
                              
                              <p style="text-align: center;">
                                <img class="aligncenter size-full wp-image-285" title="fig11_21ieee754_2_double" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_21ieee754_2_double.jpg" alt="fig11_21ieee754_2_double" width="645" height="63" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_21ieee754_2_double.jpg 645w, http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_21ieee754_2_double-300x29.jpg 300w" sizes="(max-width: 645px) 100vw, 645px" />
                              </p>
                              
                              <p>
                                Ou seja, tanto em arquiteturas de 64 quanto de 32 bits são reservados 52 bits para fração (20 mesmo registrador + 32 de um segundo registrador em processadores 32 bits), 11 bits para expoente (1 de sinal + 10 de valor) e 1 bit para o sinal do número.<br /> Logo, a precisão dupla permite um range de valores de 2&#215;10^-308 a 2&#215;10^308.<br /> Outro ponto importante para compreensão do InvSqrt é saber que os projetistas do IEEE 754 construíram esta representação para que se pudesse ser facilmente processada utilizando os mesmos circuitos de comparação de inteiros – provavelmente já implementados nas arquiteturas da época. O motivo disso está relacionado com o melhor aproveitamento dos registradores (que não precisam ser dedicados à valores de ponto flutuante ou valores inteiros) e para permitir um teste rápido de comparação (instruções bne e beq aproveitadas para qualquer tipo de dado).
                              </p>
                              
                              <p>
                                Assim, a representação do IEEE 754 pode ser processada com as mesmas comparações de inteiros para acelerar a ordenação dos números de ponto flutuante.<br /> O IEEE 754 é sem dúvida um padrão muito consistente e eficiente e vêm sendo mantido por sua confiabilidade. Além das propriedades descritas aqui, ainda há algumas outras que vale a pena conhecer. Por exemplo, o padrão já prevê um símbolo padrão para operações que geram erros, utilizado por “baixo dos panos” no envio de sinal para o programa tratar uma exceção. Uma leitura altamente recomendada deste padrão está no livro &#8220;Computer Organization and Design&#8221;, do Patterson.
                              </p>
                              
                              <p style="text-align: center;">
                                <h2>
                                  4.InvSqrt
                                </h2>
                                
                                <p>
                                  Começando pela primeira linha do algoritmo, pode-se adiantar que xhalf equivale ao produto (0.5*x) da expressão obtida no ítem 2.1:
                                </p>
                                
                                <p style="text-align: center;">
                                  <img class="aligncenter size-full wp-image-283" title="fig11__19" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__19.gif" alt="fig11__19" width="143" height="20" />
                                </p>
                                
                                <pre lang="”c”">float xhalf = 0.5f*x;// equivalente a expressao acima</pre>
                                
                                <p>
                                  este valor é salvo em uma nova variável (xhalf) porque a variável x será reaproveitada para guardar o valor de raiz (chamada de y nas demonstrações). Como visto anteriormente, a variável x (das expressões) só aparece na última expressão (0.5*x).<br /> Na linha seguinte:
                                </p>
                                
                                <pre lang="”c”">int i = *(int*)&x;</pre>
                                
                                <p>
                                  temos um casting de ponteiros que é a alma deste código. Internamente, o que ocorre é uma mudança na significância dos bits.<br /> Enquanto x é uma variável de ponto flutuante de 32 bits, com a significância para os bits do padrão 754 (1 bit de sinal, 8 para o expoente e 23 para a base), a variável i é uma variável inteira, onde todos os bits possuem a mesma significância. Todavia, como tanto o tipo de <em>x</em> quanto de <em>i</em> possuem o mesmo tamanho em palavra – 32 bits – é possível armazenar ambas em um mesmo espaço. Isso é o que faz esse código ser possível.<br /> As operações com ponteiros utilizada aqui deve ser lida de trás pra frente. A ordem diz que:
                                </p>
                                
                                <p style="text-align: center;">
                                  <p>
                                    &#8211; &x: passe o endereço do espaço de memória onde x ocupa (4 palavras de memoria, ou 32 bits), que suporta tipos de ponto flutuante.
                                  </p>
                                  
                                  <p style="text-align: center;">
                                    <p>
                                      &#8211; (int *): converta este espaço de memória para suportar tipos de dados inteiros simples (também 32 bits)
                                    </p>
                                    
                                    <p style="text-align: center;">
                                      <p>
                                        &#8211; *: retorne o valor armazenado lá como inteiro.
                                      </p>
                                      
                                      <p style="text-align: center;">
                                        <img class="aligncenter size-full wp-image-286" title="fig11_22" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_22.jpg" alt="fig11_22" width="700" height="415" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_22.jpg 700w, http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_22-300x177.jpg 300w" sizes="(max-width: 700px) 100vw, 700px" />
                                      </p>
                                      
                                      <p>
                                        Na próxima linha,
                                      </p>
                                      
                                      <pre lang="”c”">i = 0x5f3759df – (i&gt;&gt;1);</pre>
                                      
                                      <p>
                                        têm-se a estimativa inicial para y[n] = y[0]. Note que a operação (i >> 1), deslocamento de bits à direita, equivale à divisão por 2. O uso desta operação é a justificativa para a conversão da representação de float para int.<br /> Veja que realizando o deslocamento de bits em todo o vetor de bits, também se tira a raíz do expoente. Por exemplo, o deslocamento da representação por inteiro de um valor qualquer:
                                      </p>
                                      
                                      <p style="text-align: center;">
                                        BIN(01100110101111100010110101010101) = DEC(3447478954)
                                      </p>
                                      
                                      <p>
                                        apenas deslocando os bits à direita 1 vez, ( 01100110101111100010110101010101 >> 1) têm-se que:
                                      </p>
                                      
                                      <p style="text-align: center;">
                                        BIN(00110011010111110001011010101010) = DEC(1723739477)
                                      </p>
                                      
                                      <p>
                                        onde se vê claramente que 1723739477 = 3447478954/2.<br /> Mas isso não tem nada de excepcional. Contudo, analisando levando em conta a reserva de bits para sinal, base e expoente, da norma IEEE 754 para essa mesma seqüência, vê-se no exemplo:
                                      </p>
                                      
                                      <p style="text-align: center;">
                                        <img class="aligncenter size-full wp-image-287" title="fig11_23" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_23.jpg" alt="fig11_23" width="644" height="83" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_23.jpg 644w, http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_23-300x38.jpg 300w" sizes="(max-width: 644px) 100vw, 644px" />
                                      </p>
                                      
                                      <p>
                                        quando é aplicada o deslocamento de bits à direita, têm-se:
                                      </p>
                                      
                                      <p style="text-align: center;">
                                        <img class="aligncenter size-full wp-image-288" title="fig11_24" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_24.jpg" alt="fig11_24" width="643" height="81" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_24.jpg 643w, http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11_24-300x37.jpg 300w" sizes="(max-width: 643px) 100vw, 643px" />
                                      </p>
                                      
                                      <p>
                                        observe que o expoente é exatamente a metade inteira do valor antes do deslocamento dos bits. Da segunda linha das tabelas, no valor decimal, $$(int) 102.5 == 102 == (int)205/2 $$. Portanto, o motivo do autor do código de converter os bits de uma variável float para uma inteira e deslocar o bits é justamente para dividir o expoente por 2, que obviamente equivale à tirar a raiz. Em seguida, quando o autor reconverte o valor para ponto flutuante,
                                      </p>
                                      
                                      <pre lang="c">x = *(float*)&i;</pre>
                                      
                                      <p>
                                        ele simplesmente recoloca os bits na forma interpretada pelo processador como sendo um float do IEEE 754.
                                      </p>
                                      
                                      <p>
                                        Sendo assim, após já tirar a raíz do valor de entrada, o método de Newton é aplicado na última linha antes do retorno da função, para convergir ao valor da raiz quadrada:
                                      </p>
                                      
                                      <pre lang="c">x = x * (1.5f – xhalf * x * x);
// xhalf = 0.5x e x = y, nas demonstracoes</pre>
                                      
                                      <p>
                                        conforme demonstrado, o Método de Newton para raiz quadrada inversa:
                                      </p>
                                      
                                      <p style="text-align: center;">
                                        <img class="aligncenter size-full wp-image-283" title="fig11__19" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/03/fig11__19.gif" alt="fig11__19" width="143" height="20" />
                                      </p>
                                      
                                      <p style="text-align: center;">
                                        <h2>
                                          5.Conclusões
                                        </h2>
                                        
                                        <p>
                                          O código da InvSqrt quando foi desenvolvido, rodava supostamente 4 vezes mais rápido que utilizando (float) 1/sqrt(x), da biblioteca padrão e o erro relativo está por volta de 10^-4. O que tornava o código muito útil.<br /> Com o avanço das otimizações dos compiladores e dos circuitos de multiplicação dos processadores, a função nativa consegue ser mais eficiente. Contudo, conhecer esta função, seu funcionamento e o algoritmo utilizado é engrandecedor para qualquer programador.<br /> A importância desta função foi tamanha que muita discussão foi gerada em torno dela. Inclusive modificações, melhorias e até alguns artigos sobre ela.<br /> Um exemplo disso foi a pesquisa de Chris Lomont (www.math.purdue.edu/~clomont) sobre o melhor valor a ser usado como y[0] no número mágico para que a primeira aproximação tenha convergência mais rápida. Segundo ele, a melhor constante para melhoria da performance seria 0x5f375a86, uma pequena diferença de 167 em relação ao original.
                                        </p>
                                        
                                        <h2>
                                          6.Referencias
                                        </h2>
                                        
                                        <ul>
                                          <li>
                                            Finney, Ross L. CÁLCULO DE GEORGE B. THOMAS JR. , volume 1. Tradução de Paulo Buschcov. Addison Wesley, 2002. Páginas 301-305. “O MÉTODO DE NEWTON”.
                                          </li>
                                          <li>
                                            Chris Lomont, www.math.purdue.edu/~clomont, “FAST INVERT SQUARE ROOT”.
                                          </li>
                                          <li>
                                            IEEE 754, grouper.ieee.org/groups/754
                                          </li>
                                          <li>
                                            Patterson, David A. COMPUTER ORGANIZATION AND DESIGN. 3rd ed. Elsevier, 2005.
                                          </li>
                                        </ul>
