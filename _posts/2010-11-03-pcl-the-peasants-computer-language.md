---
id: 828
title: 'PCL &#8211; The Peasant&#8217;s Computer Language'
date: 2010-11-03T08:39:54+00:00
author: SAWP
excerpt: "Veja aqui as especificações da PCL: The Peasant's Computer Language"
layout: post
guid: http://www.sawp.com.br/blog/?p=828
permalink: p=828
categories:
  - Miscellaneous
---
## Introdução

Com a crescente demanda por treinamento em alta tecnologia, a equipe do Laboratório de Cálculos Científicos da Universidade de Brasília desenvolveu um sistema de simulação baseada em software para ensino de linguagens de computação em alto e baixo nível. 

O projeto da linguagem surgiu para unificação de projetos experimentais – tais como PAPC (Projeto Assembly para Crianças) e AFOP (_ASM For Old People_) –, que tinham características relevantes, mas não apresentavam uma solução auto-suficiente. 

Foi com o intuito de fornecer uma forma didática e fácil de ensinar linguagens de computação que surgiu a PCL (Peasant&#8217;s Computer Language) para aprendizagem de baixo nível, e  acessível para qualquer peão. Esta linguagem foi criada para ser compatível com o bytecode SAPECO (Singular Assembly PEão COde). 

## Características Técnicas

O código de instruções consiste em uma ISA virtualizada, com um conjunto reduzido de instruções, que permite a execução em um espaço de memória controlado pelo software EnXADA (Environment of eXtended Access Dynamic Assembler). 

O programa é executado na LAJE (Large Array Jumper Environment), que é a máquina virtual responsável pelo monitoramento e interpretação do bytecode SAPECO. 

A LAJE consiste em uma memória que armazena os programas com seus dados; uma fila de espera, na qual processos podem ser administrados; um registrador; uma unidade de execução para operações aritméticas e lógicas de cada instrução SAPECO; uma unidade de controle que prepara a próxima instrução (fila de controle); e a fila de espera (queue) &#8211; uma memória de dados composta por uma sequência de componentes de dados (Modelo FIFO). 

A LAJE faz comunicação externa através de algumas instruções específicas para leitura e saída de dados e só executa um programa por vez. 

Todas as operações realizadas na LAJE são feitas no registrador, onde as informações são colocadas e manipuladas. Todas as informações são tradas por palavras, que geram instruções de tamanho fixo. Uma palavra têm um número de tamanho fixo (4 dígitos decimais). 

Para armazenamento de dados, a LAJE é equipada com uma memória de 100 palavras, que são referenciadas de 00 à 99. 

OBS: os projetistas prevem uma extensão de 10000 palavras de armazenamento na segunda versão do bytecode. Na verdade, a LAJE já possui espaço de dados reservado para as 10000 palavras, contudo, como o bytecode atualmente só possui instruções de 2 dígitos decimais para referência e dados, somente 100 espaços são endereçáveis. O aumento dos dígitos para endereçamento previsto no padrão é denominado _PUSHADINHO_ pelos próprios criadores. 

O programa é carregado e começa a executar na posição 00. 

Cada instrução escrita em SAPECO ocupa uma palavra de memória da LAJE. A instrução SAPECO consiste em 4 dígitos, conforme dito. Os 2 primeiros dígitos consistem no código da operação e os últimos 2 dígitos consistem consistem nos operandos. 

É importante salientar que os operandos das instruções não equivalem à operandos matemáticos, como acontece em muitas ISAs. Os operandos de instruções são endereços de posição de memória contendo a palavra à qual a operação se aplica. 

As operações matemáticas são sempre feitas entre acumulador e memória. Dessa forma, as instruções de operações matemáticas possuem apenas 1 operando, que é o da memória. 

### Abaixo segue o conjunto de instruções SAPECO:

<center>
  </p> 
  
  <table border="1" cellspacing="0" cellpadding="4" width="670">
    <tr>
      <td width="206" bgcolor="#000000">
        <strong>NOME</strong>
      </td>
      
      <td width="97" bgcolor="#000000">
        <strong>MNEMÔNICO</strong>
      </td>
      
      <td width="154" bgcolor="#000000">
        <strong>OPCODE</strong>
      </td>
      
      <td width="179" bgcolor="#000000">
        <strong>DESCRIÇÃO</strong>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Bota Pá Nois aê</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">BPN *</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">10</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Lê uma palavra do teclado para uma posição específica.</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Mostra Pá Nóis Aê</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">MPN *</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">11</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Escreve na tela uma palavra de uma posição de memória.</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Traz Pá Nois aê</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">TPN</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">20</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Carrega da memória para o acumulador</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Guarda Pá Nóis aê</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">GPN</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">21</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Salva na memória o valor do acumulador</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Soma aê</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">SOM **</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">30</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Adiciona uma palavra de uma posição à palavra salva no acumulador</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Tira Essa Porra</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">TEP **</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">31</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Efetua a subtração de uma posição de memória pelo valor do registrador</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Divide</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">DIV **</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">32</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Divide o valor salvo na posição especificada pelo valor salvo no registrador.</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Multiplica</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">MUL **</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">33</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Multiplica a palavra de uma posição específica pelo acumulador.</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Quebra Pá Área</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">QPA</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">40</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Desvia para uma posição específica na memória.</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Vaza se Tiver Zerado</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">VTZ</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">41</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Sai para uma posição específica da memória se o acumulador estiver zerado.</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Quebra o Zé Ninguém</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">QZN</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">42</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Desvia para uma posição se o acumulador for negativo.</span></span>
      </td>
    </tr>
    
    <tr>
      <td width="206">
        <span style="font-size: x-small;"><strong>Capa o Gato</strong></span>
      </td>
      
      <td width="97">
        <span style="font-size: x-small;"><span style="font-size: x-small;">COG</span></span>
      </td>
      
      <td width="154">
        <span style="font-size: x-small;"><span style="font-size: x-small;">43</span></span>
      </td>
      
      <td width="179">
        <span style="font-size: x-small;"><span style="font-size: x-small;">Suspende todo o programa.</span></span>
      </td>
    </tr>
  </table>
  
  <p>
    </center>
  </p>
  
  <p>
    <span style="font-size: x-small;">* Obs: A instrução MPN e BPN não são comuns em arquiteturas reais. Contudo, arquiteturas interpretadas costumam ter instruções de baixo nível com operações diretas de IO padrão.</span>
  </p>
  
  <p>
    <span style="font-size: x-small;">** Após a operação o valor é salvo no acumulador.</span>
  </p>
  
  <h3>
    Exemplo utilizando todas matemáticas instruções SAPECO:
  </h3>
  
  <p>
    <center>
      </p> 
      
      <table border="1" cellspacing="0" cellpadding="4" width="670">
        <tr>
          <td width="51" bgcolor="#000000">
            <strong>POSIÇÃO</strong>
          </td>
          
          <td width="121" bgcolor="#000000">
            <strong>CÓDIGO</strong>
          </td>
          
          <td width="132" bgcolor="#000000">
            <strong>ASM</strong>
          </td>
          
          <td width="332" bgcolor="#000000">
            <strong>COMENTÁRIO</strong>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">00</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">1007</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">MPN 07</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># equivale à scanf(&M[7]), supondo que tenha digitado valor 10</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">01</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">1008</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">MPN 08</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># scanf(&M[8]), supondo que tenha digitado valor 8</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">02</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">2007</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">TPN 07</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># $registrador = M[7], ou seja, $registrador = 10</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">03</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">3008</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">SOM 08</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># $registrador = $registrador + M[8], $registrador = 10 + 8 = 18</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">04</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">3107</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">TEP 07</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># $registrador = $registrador – M[7], $registrador = 18 – 10 = 8</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">05</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">3307</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">MUL 07</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># $registrador = $registrador * M[7], $registrador = 8*10=80</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">06</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">3208</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">DIV 08</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># $registrador = $registrador / M[8], $registrador = 80/8=10</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">07</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">0010 **</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">&#8211;</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># Variável A</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">08</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">0008 **</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">&#8211;</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># Variavel B</span></span>
          </td>
        </tr>
        
        <tr>
          <td width="51">
            <span style="font-size: x-small;"><span style="font-size: x-small;">09</span></span>
          </td>
          
          <td width="121">
            <span style="font-size: x-small;"><span style="font-size: x-small;">4300</span></span>
          </td>
          
          <td width="132">
            <span style="font-size: x-small;"><span style="font-size: x-small;">COG</span></span>
          </td>
          
          <td width="332">
            <span style="font-size: x-small;"><span style="font-size: x-small;"># sai do &#8220;pograma&#8221;. Note que a LAJE ignora endereços de dados (00 nos 2 primeiros algarismos, seção de instrução)</span></span>
          </td>
        </tr>
      </table>
      
      <p>
        </center>
      </p>
      
      <p>
        <span style="font-size: x-small;">* M[] é o vetor que representa a memória usada na LAJE</span><br /> <span style="font-size: x-small;">** Veja que o código 00 nos 2 primeiros indica que aquela posição armazena um DADO, não uma instrução.</span>
      </p>
      
      <h2>
        Implementação da LAJE
      </h2>
      
      <p>
        Uma simples implementação compatível com as especificações acima pode ser obtida no endereço: <a href="http://www.sawp.com.br/code/general/LAJE.cc" target="_blank">http://www.sawp.com.br/code/general/LAJE.cc</a>
      </p>
      
      <h2>
        Considerações Finais
      </h2>
      
      <p>
        Este documento foi criado em meados de 2009, sendo uma compilação de várias ideias surgidas durante uma bebedeira promovida no Centro Acadêmico de Física da Universidade de Brasília. Portanto, pedimos que os leitores sóbrios não considerem tal conteúdo.
      </p></p> 
      
      <p>
        &nbsp;
      </p>
      
      <div align="right">
        Pedro Garcia
      </div>
