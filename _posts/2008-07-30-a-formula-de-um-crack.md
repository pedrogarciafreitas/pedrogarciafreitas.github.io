---
id: 105
title: A Fórmula de um Crack
date: 2008-07-30T16:24:06+00:00
author: SAWP
excerpt: Crackear qualquer sistema é impossível sem as ferramentas certas. Abaixo iremos discutir as diferenças entre as existentes. E de posse do conhecimento destas, iremos desenvolver um exemplo suficientemente completo para se entender como crackear um executável.
layout: post
guid: http://www.sawp.com.br/blog/?p=105
permalink: p=105
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:3928:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #ff0000; font-style: italic;">/*
    * HelloWorld.h
    *
    *  Created on: 14/07/2008
    *      Author: SAWP
    */</span>
    <span style="color: #339900;">#include</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #007788;">string</span><span style="color: #008080;">;</span>
    <span style="color: #339900;">#ifndef HELLOWORLD_H_</span>
    <span style="color: #339900;">#define HELLOWORLD_H_</span>
    <span style="color: #0000ff;">class</span> HelloWorld <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
    HelloWorld<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">virtual</span> ~HelloWorld<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">void</span> digitSerial<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span> <span style="color: #666666;">// The program continue if user serial is valid,</span>
    <span style="color: #0000ff;">else</span> will lock in <span style="color: #0000dd;">this</span> function
    <span style="color: #0000ff;">private</span><span style="color: #008080;">:</span>
    <span style="color: #0000ff;">void</span> startProgram<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span><span style="color: #008080;">;</span> <span style="color: #666666;">// program starter: licensed, execute</span>
    <span style="color: #0000ff;">bool</span> hadPass<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span><span style="color: #008080;">;</span> <span style="color: #666666;">//Check if user serial is valid </span>
    <span style="color: #008000;">&#40;</span>equals factory serial<span style="color: #008000;">&#41;</span>
    <span style="color: #0000ff;">const</span> string serial<span style="color: #008080;">;</span> <span style="color: #666666;">// The serial that come from factory that </span>
    We will crack
    string userserial<span style="color: #008080;">;</span> <span style="color: #666666;">// The serial that must be insert by user</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    <span style="color: #339900;">#endif /* HELLOWORLD_H_ */</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
    * HelloWorld.h
    *
    *  Created on: 14/07/2008
    *      Author: SAWP
    */
    #include
    using std::string;
    #ifndef HELLOWORLD_H_
    #define HELLOWORLD_H_
    class HelloWorld {
    public:
    HelloWorld();
    virtual ~HelloWorld();
    void digitSerial(void); // The program continue if user serial is valid,
    else will lock in this function
    private:
    void startProgram(void) const; // program starter: licensed, execute
    bool hadPass(void) const; //Check if user serial is valid
    (equals factory serial)
    const string serial; // The serial that come from factory that
    We will crack
    string userserial; // The serial that must be insert by user
    };
    #endif /* HELLOWORLD_H_ */</p></div>
    ;i:2;s:11282:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #ff0000; font-style: italic;">/*
    * HelloWorld.cpp
    *
    *  Created on: 14/07/2008
    *      Author: SAWP
    */</span>
    <span style="color: #339900;">#include</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #007788;">string</span><span style="color: #008080;">;</span>
    <span style="color: #339900;">#include &quot;HelloWorld.h&quot;</span>
    <span style="color: #339900;">#include</span>
    &nbsp;
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cout</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cin</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #007788;">endl</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">//const starter, this serial simulate the generator</span>
    HelloWorld<span style="color: #008080;">::</span><span style="color: #007788;">HelloWorld</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008080;">:</span> serial<span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;1234567890&quot;</span><span style="color: #008000;">&#41;</span>  <span style="color: #008000;">&#123;</span>
    this<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span> digitSerial<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    HelloWorld<span style="color: #008080;">::</span>~HelloWorld<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// TODO Auto-generated destructor stub</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">bool</span> HelloWorld<span style="color: #008080;">::</span><span style="color: #007788;">hadPass</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span>this<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span> userserial <span style="color: #000080;">==</span> this<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span> serial<span style="color: #008000;">&#41;</span> <span style="color: #666666;">//detect the serial from user</span>
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">else</span>
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #0000ff;">void</span> HelloWorld<span style="color: #008080;">::</span><span style="color: #007788;">startProgram</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;*************************************************************<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;Congratulations! Now, you are a licensed guy!<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;Here is a program functionality: Hello World&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;*************************************************************<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">int</span> temp<span style="color: #008080;">;</span> <span style="color: #666666;">// while not digited</span>
    <span style="color: #0000dd;">cout</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> <span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>&gt; &gt;  Something to continue.. &gt; &gt; <span style="color: #000099; font-weight: bold;">\r</span>&quot;</span><span style="color: #008000;">&#41;</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> endl<span style="color: #008080;">;</span>
    <span style="color: #0000dd;">cin</span> <span style="color: #000080;">&gt;</span> <span style="color: #000080;">&gt;</span>  temp<span style="color: #008080;">;</span>
    <span style="color: #0000dd;">exit</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">EXIT_SUCCESS</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #0000ff;">void</span> HelloWorld<span style="color: #008080;">::</span><span style="color: #007788;">digitSerial</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;&gt; &gt; Please, digit a valid serial &gt; &gt;  &quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">cin</span>.<span style="color: #007788;">clear</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span> <span style="color: #666666;">// clear the input</span>
    <span style="color: #0000dd;">cin</span> <span style="color: #000080;">&gt;</span> <span style="color: #000080;">&gt;</span>  this<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span> userserial<span style="color: #008080;">;</span> <span style="color: #666666;">// read from prompt the user serial</span>
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span>hadPass<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span> <span style="color: #666666;">//if is a valid serial, execute the program</span>
    this<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span> startProgram<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #0000ff;">else</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">cout</span>.<span style="color: #007788;">clear</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    digitSerial<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span> <span style="color: #666666;">// this recursive block the program while a </span>
    valid serial is <span style="color: #0000ff;">not</span> detected
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
    * HelloWorld.cpp
    *
    *  Created on: 14/07/2008
    *      Author: SAWP
    */
    #include
    using std::string;
    #include &quot;HelloWorld.h&quot;
    #include
    
    using std::cout;
    using std::cin;
    using std::endl;
    
    //const starter, this serial simulate the generator
    HelloWorld::HelloWorld() : serial(&quot;1234567890&quot;)  {
    this-&gt; digitSerial();
    }
    
    HelloWorld::~HelloWorld() {
    // TODO Auto-generated destructor stub
    }
    
    bool HelloWorld::hadPass() const{
    if(this-&gt; userserial == this-&gt; serial) //detect the serial from user
    return true;
    else
    return false;
    }
    
    
    void HelloWorld::startProgram() const{
    puts(&quot;\n\n\n&quot;);
    puts(&quot;*************************************************************\n&quot;);
    puts(&quot;Congratulations! Now, you are a licensed guy!\n\n&quot;);
    puts(&quot;Here is a program functionality: Hello World&quot;);
    puts(&quot;*************************************************************\n&quot;);
    int temp; // while not digited
    cout &lt; &lt; (&quot;\n\n&gt; &gt;  Something to continue.. &gt; &gt; \r&quot;) &lt; &lt; endl;
    cin &gt; &gt;  temp;
    exit(EXIT_SUCCESS);
    }
    void HelloWorld::digitSerial(){
    puts(&quot;\n&quot;);
    puts(&quot;&gt; &gt; Please, digit a valid serial &gt; &gt;  &quot;);
    cin.clear(); // clear the input
    cin &gt; &gt;  this-&gt; userserial; // read from prompt the user serial
    if(hadPass()){ //if is a valid serial, execute the program
    this-&gt; startProgram();
    }else {
    cout.clear();
    digitSerial(); // this recursive block the program while a
    valid serial is not detected
    }
    }</p></div>
    ;i:3;s:3537:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #666666;">//========================================================</span>
    <span style="color: #666666;">// Name        : post1.cpp</span>
    <span style="color: #666666;">// Author      : SAWP</span>
    <span style="color: #666666;">// Version     :</span>
    <span style="color: #666666;">// Copyright   : Copyright 2008, Licensed by Creative Commons</span>
    <span style="color: #666666;">// Description : Hello World with a serial checker in C++, Ansi-style</span>
    <span style="color: #666666;">//========================================================</span>
    <span style="color: #339900;">#include</span>
    <span style="color: #0000ff;">using</span> <span style="color: #0000ff;">namespace</span> std<span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cout</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cin</span><span style="color: #008080;">;</span>
    <span style="color: #339900;">#include </span>
    <span style="color: #339900;">#include &quot;HelloWorld.h&quot;</span>
    <span style="color: #0000ff;">int</span> main<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;##############################################&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>Welcome to sample<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;##############################################&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    HelloWorld teste<span style="color: #008080;">;</span>
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">EXIT_SUCCESS</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//========================================================
    // Name        : post1.cpp
    // Author      : SAWP
    // Version     :
    // Copyright   : Copyright 2008, Licensed by Creative Commons
    // Description : Hello World with a serial checker in C++, Ansi-style
    //========================================================
    #include
    using namespace std;
    using std::cout;
    using std::cin;
    #include
    #include &quot;HelloWorld.h&quot;
    int main(){
    puts(&quot;##############################################&quot;);
    puts(&quot;\n\nWelcome to sample\n\n&quot;);
    puts(&quot;##############################################&quot;);
    HelloWorld teste;
    return EXIT_SUCCESS;
    }</p></div>
    ";}
categories:
  - Programming Internals
tags:
  - Programming Internals
---
<p style="text-align: center;">
  <a class="thickbox" href="http://www.sawp.com.br/blog/wp-content/uploads/aformuladocrack/ac_124_13.jpg"><img class="ngg-singlepic ngg-center aligncenter" title="Crack" src="http://www.sawp.com.br/blog/wp-content/uploads/aformuladocrack/ac_124_13.jpg" alt="Crack" width="300" height="200" /></a>
</p>

## 1. Introdução

Crackear qualquer sistema é impossível sem as ferramentas certas. Abaixo iremos discutir as diferenças entre as existentes. E de posse do conhecimento destas, iremos desenvolver um exemplo suficientemente completo para se entender como crackear um executável.

Saber escolher as ferramentas certas para cada “ocasião” é o que diferenciará o fracasso do sucesso de seu experimento, o tempo necessário para encontrar os códigos necessários, etc.

A escolha de qual ferramenta usar dependerá das muitas diferenças que encontramos entre arquiteturas, compiladores, código gerado, plataforma que está sendo executada e em qual plataforma foi gerada.

Estudaremos utilizando as ferramentas e um programa em linguagem assembly IA-32. Porém, algumas ferramentas são tão completas que servem para a maioria das arquiteturas e sistemas, bem como os métodos a serem seguidos.

Quando abrimos um executável observamos, testamos e utilizamos mais de uma ferramenta aqui apresentada. Tudo vale para se encontrar a informação que se está buscando.

Geralmente certo tipo de ferramenta facilitará algum dos dois tipos fundamentais de metodologias de análise: online ou análise offline. Também deveremos utilizar aquela que oferece melhor compatibilidade para os tipos de aplicação: user-mode ou kernel-mode.

## 2. Métodos de Análise

### 2.1 Análise Offline (DeadListing)

A análise offline de um código ocorre quando pegamos um arquivo binário executável e o desassemblamos para convertê-lo na linguagem assembly (normalmente da arquitetura em que ele foi compilado) sem observarmos como o código se comporta durante a execução.

A reversão é feita manualmente a partir da leitura de parte do código obtido.

No processo de estudo de um arquivo para o crackeamento a maior parte do trabalho é feito com uma análise offline do código, visto que buscamos quase sempre certos pedaços de código que queremos retirar.

Também é a técnica de análise mais utilizada porque é mais fácil procurar em um código linhas do programa e funções específicas que estamos interessados.

Esta análise torna a visualização mais parecida com a programação original, pois observamos apenas código e não a alteração do fluxo de dados durante a execução.

### 2.2 Análise Online

Graças à vários fatores relacionados à técnicas “anti-cracking”, existem programas em que a análise offline de código não é suficiente para entendermos o funcionamento do programa.

Há casos em que o código está compilado com uso de técnicas de empacotamento, códigos encriptados ou comprimidos de forma que as instruções são decriptadas ou descomprimidas em tempo de execução. Nestes casos, somente a análise de código offline torna impossível o entendimento da estrutura do programa.

A observação e análise de um código ativo, em execução, nos permite descobrir como o programa se comporta. É desta forma que recriamos (ou supostamente recriamos) aqueles pedaços de códigos não compreensíveis pela análise offline. Quando mesclamos o código original com algum outro produzido por nos fica possível refazermos um programa que atenda nossas necessidades.

É observando o comportamento de um programa ativo que fica possível encontrar os dados internos do programa – não observáveis pela leitura estática – , além de tornar visível o fluxo de controle.

Assim, encontramos quais variáveis contém quais valores e o que ocorre quando o programa lê ou modifica os dados.

## 3. Ferramentas

### 3.1 Disassemblers

Disassemblers são as ferramentas primordiais, fundamentais e as mais importantes dentre quaisquer outras utilizadas para a análise offline do código.

São os desassemblers que decodificam o código binário de máquina (0101010 e, as vezes, 2) em código assembly, mais legíveis.

O assembly é uma linguagem de programação primitiva, onde cada comando equivale à uma instrução do processador.

O programa responsável por converter a linguagem assembly na representação compreensível pela máquina se chama montador. É o montador que transforma a representação textual das instruções em instruções binárias.

Um desassemblador apenas faz o trabalho inverso dos montadores, decodificando cada instrução binária em uma representação textual.

A escolha de um desassemblador requer estudo de alguns requisitos. Cada arquitetura de computador possui sua própria linguagem assembly. Devido aos diferentes sets de instruções e aos diferentes tipos de registradores. Por isso, a escolha da ferramenta deverá levar em conta o suporte que ela dá para desmontar determinado assembly.

### 3.2 Debuggers

Debbugers são utilizados vastamente por desenvolvedores de software para auxiliar na localização e correção de erros em tempo de execução dos programas. Contudo, se bem usados, podem ser uma grande “mão-na-roda” como ferramenta para “outros fins”.

Os debuggers analisam o código e permitem uma visão desassemblada do programa rodando. Permitem também, durante a execução, que possamos observar comportamento dos dados na memória, na CPU [registradores] e na pilha de execução.

Ou seja, enquanto os disassemblers são ideais para uma visão do código desassemblado de forma estática, os debuggers são feitos para observamos o programa em tempo de execução. Resumindo: disassemblers são usados para análise offline, debuggers, análise online.

Os debuggers são ainda divididos de acordo com seu modo de operação:

#### 3.2.1 Debuggers – User-mode

Debuggers que operam em modo usuário são os mais comuns de serem encontrados. São usados pelos desenvolvedores de software para testar seus programas.

Eles operam com mais restrição dentro do sistema operacional, são executados como uma aplicação normal (em modo-usuário) e podem ser usados para debugar aplicações comuns (que também obedecem às restrições do usuário).

Seu funcionamento é simples: anexam outro processo (que está debugando) e toma controle sobre ele. Têm a vantagem de ser simples de operar, já que é apenas outro programa correndo dentro do sistema operacional.

Os debuggers de user mode só podem analisar um processo por vez (step-by-step). E é aí que está a beleza da coisa: analisando um processo por vez aumenta a chance de encontrarmos exatamente o processo que queremos.

Por exemplo, suponhamos que queremos encontrar qual processo que verifica a presença de um registro no sistema. Ao descobrirmos a localização do processo, podemos verificar quais as posições das devidas instruções no código são responsáveis por ele. De posse dessas posições, retiramos as instruções. Remontamos. Resultado: teremos um executável funcionando sem este pedido de autenticação. “Crackeado”.

Como o nome sugere, debuggers que atuam no modo usuário não agem e nem acessam componentes de sistema operacional, tarefas administrativas ou componentes que requerem drivers (programas que acessam dispositivos: gravadores de cd/DVD, discadores, etc).

Logo, cada ferramenta é utilizada para um caso especifico. Seria um desperdício de energia, paciência e tempo debugar um programa com um debugger em kernel mode se sua análise não exigir. É bem mais produtivo debugá-lo em modo usuário, se assim for possível.

Todavia, em casos em que há chamadas ao sistema operacional, uso de dispositivos de hardware, chamadas de bibliotecas dinâmicas (DLL) ou sistemas de processamento paralelo, os debuggers de modo usuário não seriam suficientes.

#### 3.2.2 Debuggers – Kernel Mode

Os debuggers que atual em modo kernel, são bem mais poderosos pois permitem um controle ilimitado sobre o binário estudado e também proporcionam uma visão geral de tudo que acontece no sistema (aplicação ou SO).

São eles que utilizamos quando devemos sair do escopo (ou das limitações) de um único processo para visualizar o sistema como um todo. Diferentemente do modo usuário são mais do que uma aplicação executando dentro do sistema operacional, são como componentes do kernel.

Os principais usuários destes debuggers são desenvolvedores e programadores de sistemas operacionais. Pessoas que precisam trabalhar no nível do kernel ou próximos à ele: desenvolvedores de drivers, componentes de SO, extensões de sistema, antivírus etc.

A utilização de debuggers em kernel mode para atividades de crackerismo é muito rara. Contudo, há alguns casos: quebras de bloqueios do IPHONE, analistas de keymakers (temos aí vista bruteforce) e afins.

Um exemplo da aplicação de debuggers em kernel mode aparece quando estamos analisando como um programa utiliza uma chamada (da API) do sistema. Se o sistema estiver utilizando uma biblioteca do tipo window.h e queremos encontrar o código responsável pela integração entre a API e o programa em estudo, devemos utilizar um debugger que consiga ver esse conjunto de chamadas. Somente um debugger em kernel mode poderia oferecer uma solução viável para este caso.

Porém, com maiores poderes, temos mais responsabilidades [e dificuldades].

Como nesta atividade tendemos à destruir e corromper o sistema em estudo, recomendo sempre manter cópias dos originais. A quantidade de erros fatais nessa atividade é realmente alta. Basta a inserção uma única instrução errada para acabar com um programa inteiro.

Os debuggers em kernel-mode tendem a desestabilizar todo o sistema que estão anexados. Por isso é recomendável manter cópias do sistema operacional. E manter um sistema operacional dedicado só para os experimentos.

Devido à seus inconvenientes, a utilização dos debuggers em kernel-mode é indicada somente em casos em que eles são realmente necessários. Inclusive porque eles são piores de se trabalhar: a sua menor simplicidade promove menor produtividade.

Quando precisar trabalhar com eles, mantenha sempre cópias e mais cópias do sistema operacional “sadio”. Recomendo Virtual Box!

### 3.3 OllyDbg

Pessoalmente, tenho um carinho todo especial por este brinquedinho. É um debugger que de quebra tem um montador e uma “patching engine”.

Com ele é possível reescrever o código assembly em qualquer área do programa e depois remontá-lo com um clique. Isso é perfeito durante o “desenvolvimento” do crack, pois permite reescrever, reprogramar e executar tudo como se estivesse brincando com um interpretador.

O OllyDBG foi escrito por Oleh Yuschuk é o melhor debugger existente. Muito leve, permite uma ótima análise de código, bem organizado, escrito exatamente para estudos que exigem reversão.

Sua organização, combinada com o analisador de código, pode identificar blocos de instruções dos loops, desvios, jumps e estruturas de código

Possui também uma grande variedade de visões (incluindo listas de importação e exportação de módulos), bibliotecas, etc.

Atua em modo usuário e é a melhor ferramenta para análise online de código, além de ser completamente gratuito.

<p style="text-align: center;">
  <img class="aligncenter size-medium wp-image-235" title="ollydbg3" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg3-300x187.png" alt="ollydbg3" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg3-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg3-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg3.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
</p>

<p style="text-align: center;">
  <img class="aligncenter size-medium wp-image-234" title="ollydbg2" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg2-300x187.png" alt="ollydbg2" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg2-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg2-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg2.png 1280w" sizes="(max-width: 300px) 100vw, 300px" /><img class="aligncenter size-medium wp-image-233" title="ollydbg1" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg1-300x187.png" alt="ollydbg1" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg1-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg1-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/ollydbg1.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
</p>

### 3.4 WinDbg

É um debugger distribuído pela MS e o mais utilizado pelos desenvolvedores que utilizam Windows (http://www.microsoft.com/whdc/devtools/debuggin/default.mspx).

Pessoalmente, acho que tem uma interface péssima. Algo entre GUI e uma interface texto. O disassembler dele é um tanto limitado e já me ocorreram muitos erros (travamentos, incapacidade de voltar para a janela do programa que estava querendo desassemblar etc) usando ele. Não obtive boa experiencia com esta ferramenta.

O WinDbg tenta ser um debugger de propósito multi-modo. Ele pode trabalhar tanto como em user-mode como em kernel-mode. Porém, em kernel-mode a execução do WinDbg deve ser em um computador remoto ou em um sistema separado.

Ele é um pouco limitado e pouco flexível. Talvez porque eu use mais recursos em modo usuário, prefiro outras ferramentas. Mas a interface de usuário do WinDbg é muito limitada e um tanto desconfortável em modo usuário (breakpoints sempre dão problemas, não tem alteração online do código, péssimo para “brincar”).

<p style="text-align: center;">
  <p style="text-align: center;">
    <img class="aligncenter size-medium wp-image-236" title="windbg" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/windbg-300x187.png" alt="windbg" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/windbg-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/windbg-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/windbg.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
  </p>
  
  <h3>
    3.5 Interactive Disassembler – IDA PRO
  </h3>
  
  <p>
    Esse sim pode ser chamado orgulhosamente de disassembler. É o verdadeiro canivete suíço para as atividades que envolvem cracking, pois é uma ferramenta construída e projetada exatamente para fins de engenharia reversa.
  </p>
  
  <p>
    Há uma grande quantidade de ferramentas e sua interface se assemelha muito com uma IDE. Provavelmente tudo que precisarmos para crackear um binário encontraremos implementado no IDA PRO.
  </p>
  
  <p>
    É extremamente flexível, tem um excelente disassembler e algumas propriedades – que só encontrei nele até hoje – auxiliam muito na busca de código e facilitam as atividades de cracking.
  </p>
  
  <p>
    O IDA PRO é capaz de produzir excelentes aproximações de estruturas de controle. O que o torna extremamente produtivo ao cracking.
  </p>
  
  <p>
    Há uma ferramenta neste programa chamado “graph” que nos permite observar o fluxo de dados e as chamadas de função. Isso facilita muito a busca do código desejado. O IDA analisa as condições de desvio e, baseada nas instruções encontradas, implementa todo um fluxograma de execução.
  </p>
  
  <p>
    Como isso já não bastasse, as janelas básicas do programa são: IDA View-A (que resume o código disassemblado e alguns trechos do fluxo de dados); Hex View, exports, imports, names, functions, strings, strutures e enums, que exibem o que os nomes sugerem.
  </p>
  
  <p>
    Outro recurso do IDA é que ele possui destaque de funções e instruções. Se selecionamos uma instrução, função ou trecho de código, o IDA PRO destaca todas ocorrências idênticas às destacadas. Por exemplo, quando selecionamos a instrução MOVZX, todas as instancias dessa pseudoinstrução serão destacada.
  </p>
  
  <p>
    Infelizmente esta ferramenta não é gratuita. Muito menos barata. Mas é fundamental.
  </p>
  
  <p>
    Ela é produzida pela DataRescue ( http://www.datarescue.com ), empresa que também produz vários outros programas interessantes. Contudo, quem estiver interessado em se dedicar à atividades de reversão, vale a pena investir no IDA PRO.
  </p>
  
  <p>
    IDA também possui suporte a uma variedade de arquiteturas que vai de IA32 à embarcados. Então, para quem se interessar por GamingCrack, o IDA PRO tem um excelente suporte para os formatos XBE, do XBOX.
  </p>
  
  <p style="text-align: center;">
    <img class="aligncenter size-medium wp-image-242" title="figura9" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura9-300x187.png" alt="figura9" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura9-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura9-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura9.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
  </p>
  
  <p style="text-align: center;">
    <img class="aligncenter size-medium wp-image-241" title="figura8" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura8-300x187.png" alt="figura8" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura8-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura8-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura8.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
  </p>
  
  <p style="text-align: center;">
    <img class="aligncenter size-medium wp-image-240" title="figura7" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura7-300x187.png" alt="figura7" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura7-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura7-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura7.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
  </p>
  
  <p style="text-align: center;">
    <img class="aligncenter size-medium wp-image-238" title="figura4" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura4-300x187.png" alt="figura4" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura4-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura4-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/figura4.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
  </p>
  
  <p style="text-align: center;">
    <h3>
      3.6 Syser Debugger
    </h3>
    
    <p>
      Baseado no antigo SoftIce, é um excelente debugger que atua em Kernel Mode. Para quem desenvolve drivers é altamente recomendado.
    </p>
    
    <h3>
      3.7 Máquinas Virtuais
    </h3>
    
    <p>
      Debugar em Kernel Mode trava e potencialmente desestabiliza o sistema operacional. Sendo assim, é altamente recomendável usar um sistema operacional dedicado para kernel debugger e não usar o kernel debugger em seu sistema de trabalho.
    </p>
    
    <p>
      Porém, nem todo o mundo tem a seu dispor computadores extras para usar como hosts. Sendo assim, a solução é utilizar um sistema com um hardware mais parrudo e simular em um único hardware diferentes computadores com maquinas virtuais (MV).
    </p>
    
    <p>
      MV são perfeitas para debugar em kernel mode, pois permitem o isolamento e a execução paralela de sistemas num mesmo ambiente de trabalho.
    </p>
    
    <p>
      Como os sistemas instalados em uma máquina virtual ficam todos simulados em arquivos (normalmente 1 arquivo que simula o hardware e outro com as configurações), facilita muito fazer os backups do sistema cliente – bastando copiar e colar – favorecendo a replicação.
    </p>
    
    <p>
      A maioria das MV suportam drivers próprios. Graças à isso permitem mais compatibilidade com alguns sistemas que seriam incompatíveis se instalados diretamente no hardware.
    </p>
    
    <p>
      Esta propriedade também torna as MV perfeitas para quem se interessar pelo estudo de vírus e desenvolvimento de softwares maliciosos. Já que se o sistema virtualizado é ambiente de teste para algum malware, ele não acessará os recursos diretos do hardware, nem irá corromper arquivos do sistema que hospeda a MV.
    </p>
    
    <p>
      Algumas MV atuais simulam processadores (veremos sobre SPIM), o que permite emularmos sistemas ou plataformas.
    </p>
    
    <h2>
      4. Um Exemplo Prático
    </h2>
    
    <p>
      Agora faremos nosso crack. O programa para este experimento terá apenas uma funcionalidade prática: imprimir um “Hello World” na tela. Bom, também alguns outros caracteres e frescuras.
    </p>
    
    <p>
      Antes de atingir sua funcionalidade primordial, nosso programa exige que o usuário entre com uma chave para ativar o programa. O intuito disso é simular o bloqueio dos programas comerciais que exigem números seriais de ativação.
    </p>
    
    <p>
      Segue abaixo o código do programa a ser crackeado:
    </p>
    
    <pre lang="cpp">/*
 * HelloWorld.h
 *
 *  Created on: 14/07/2008
 *      Author: SAWP
 */
#include
using std::string;
#ifndef HELLOWORLD_H_
#define HELLOWORLD_H_
class HelloWorld {
  public:
        HelloWorld();
        virtual ~HelloWorld();
        void digitSerial(void); // The program continue if user serial is valid,
                                       else will lock in this function
  private:
          void startProgram(void) const; // program starter: licensed, execute
          bool hadPass(void) const; //Check if user serial is valid 
                                        (equals factory serial)
          const string serial; // The serial that come from factory that 
                                        We will crack
          string userserial; // The serial that must be insert by user
};
#endif /* HELLOWORLD_H_ */</pre>
    
    <pre lang="cpp">/*
 * HelloWorld.cpp
 *
 *  Created on: 14/07/2008
 *      Author: SAWP
 */
#include
using std::string;
#include "HelloWorld.h"
#include

using std::cout;
using std::cin;
using std::endl;

//const starter, this serial simulate the generator
HelloWorld::HelloWorld() : serial("1234567890")  {
        this-> digitSerial();
}

HelloWorld::~HelloWorld() {
        // TODO Auto-generated destructor stub
}

bool HelloWorld::hadPass() const{
        if(this-> userserial == this-> serial) //detect the serial from user
                return true;
        else
                return false;
}


void HelloWorld::startProgram() const{
        puts("\n\n\n");
        puts("*************************************************************\n");
        puts("Congratulations! Now, you are a licensed guy!\n\n");
        puts("Here is a program functionality: Hello World");
        puts("*************************************************************\n");
        int temp; // while not digited
        cout &lt; &lt; ("\n\n> >  Something to continue.. > > \r") &lt; &lt; endl;
        cin > >  temp;
        exit(EXIT_SUCCESS);
}
void HelloWorld::digitSerial(){
        puts("\n");
        puts("> > Please, digit a valid serial > >  ");
        cin.clear(); // clear the input
        cin > >  this-> userserial; // read from prompt the user serial
        if(hadPass()){ //if is a valid serial, execute the program
                this-> startProgram();
        }else {
                cout.clear();
                digitSerial(); // this recursive block the program while a 
                                   valid serial is not detected
        }
}</pre>
    
    <pre lang="cpp">
//========================================================
// Name        : post1.cpp
// Author      : SAWP
// Version     :
// Copyright   : Copyright 2008, Licensed by Creative Commons
// Description : Hello World with a serial checker in C++, Ansi-style
//========================================================
#include
using namespace std;
using std::cout;
using std::cin;
#include 
#include "HelloWorld.h"
int main(){
        puts("##############################################");
        puts("\n\nWelcome to sample\n\n");
        puts("##############################################");
        HelloWorld teste;
        return EXIT_SUCCESS;
}</pre>
    
    <p>
      Compile e execute o programa. Observe bem as mensagens emitidas por ele. É baseada nessas mensagens que iremos buscar no código as instruções responsáveis pela solicitação/verificação do serial.
    </p>
    
    <p>
      Com o IDA PRO, abra o executável que acabamos de compilar. O IDA irá desassemblar automaticamente o arquivo.
    </p>
    
    <p>
      Com o programa já podendo ser visualizado em linguagem assembly, vá na aba “Names” e procure pela string “>>Please, digit a valid serial >>”, que por observação, nos sugere pertencer ao ponto de congelamento do sistema que exige o serial.
    </p>
    
    <p>
      Achado a respectiva string, clique duas vezes nela e um código poderá ser visualizado na aba “IDA View-A”. Note que o rótulo da string que acabamos de encontrar, bem como o endereço da atual instrução, pode ser visualizado.
    </p>
    
    <p>
      Note também que ao final da linha haverá um comentário com a forma “DATA XREF: &#8230;”. Este comentário é gerado pelo IDA PRO e serve para lincarmos com a função chamadora deste rótulo. Ao clicarmos na subrotina (de nome sub_algumNumero), iremos direto para o código da mesma.
    </p>
    
    <p>
      Já na respectiva subrotina, coloque o modo de visualização em gráficos. Se o leitor se guiou certo até o presente momento, provavelmente um diagrama &#8211; contendo um retangulo principal seguido por dois abaixo – irá aparecer.
    </p>
    
    <p>
      Este gráfico, na verdade, é um diagrama de fluxo de dados gerado pelo próprio IDA PRO com base nas instruções de desvio que ele encontra no código assembly. E este é um dos recursos mais fantásticos e úteis desse programa, além de tornar muito mais produtivo o trabalho de cracking.
    </p>
    
    <p>
      Como sabemos, estudar ou desenvolver um programa com o auxílio de diagramas aumenta muito mais a produtividade e reduz o tempo de [re] programação.
    </p>
    
    <p>
      Sendo assim, observe as chamadas das duas subdivisões que o IDA gerou da subrotina que estamos. Note que o quadro da direita possui uma chamada para a própria subrotina. Isso indica que seguindo este fluxo o programa entra num loop, até que a condição que leva ao quadro da esquerda seja satisfeita.
    </p>
    
    <p>
      Portanto, o quadro da esquerda é o que possui a chamada de subrotina que leva o programa para a próxima “fase” de instruções. E é exatamente esta função que possui a chamada para o inicializador do programa.
    </p>
    
    <p>
      Agora mude para a visualização em texto do código.
    </p>
    
    <p>
      Anote o endereço das instruções: chamada de subrotina inicializadora e inicio da rotina de verificação de serial (a que provavelmente o leitor estará).
    </p>
    
    <p>
      Agora, abra o OllyDbg. Com ele iremos modificar a instrução em tempo real. Ou seja, poderemos modificar as instruções na memória enquanto o programa estiver rodando. Isso é que torna o OllyDBG perfeito para “ambiente de desenvolvimento”, pois podemos abrir, mecher, remecher e testar como quisermos o programa, online.
    </p>
    
    <p>
      Com o OllyDbg, busque o endereço das instruções que queremos alterar. Altere cada uma delas, reassembly, teste, remonte em um executável e teremos o programa crackeado.
    </p>
    
    <p>
      Veja esses passos no vídeo abaixo:
    </p>
    
    <p style="text-align: center;">
    </p>
    
    <p style="text-align: center;">
      Download: <a class="wp-caption" title="Download" href="http://www.megaupload.com/pt/?d=UHAFMXAK" target="_blank">http://www.megaupload.com/pt/?d=UHAFMXAK</a>
    </p>
    
    <p>
      Obviamente, programas comerciais são um pouco mais complexos. Normalmente utilizam de 2 a 3 subrotinas para todo o processo de validação (busca no registro -> inserção pelo usuário -> validação de numero digitado/keychecker). Contudo, o princípio é o mesmo. Claro que com muito mais instruções. Mas o exemplo aqui abordado é um bom exercício para se familiarizar com as ferramentas e a busca.
    </p>
    
    <h2>
      5. Conclusão
    </h2>
    
    <p>
      Espero ter sido esclarecedor. Quaisquer dúvidas, críticas, sugestões ou reclamações: sawp@sawp.com.br
    </p>
