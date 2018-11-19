---
id: 131
title: Técnicas AntiCracking – Parte I
date: 2008-08-08T18:10:54+00:00
author: SAWP
excerpt: 'Quando disassemblamos um binário para crackearmos, muitas vezes nos deparamos com um código que parece não fazer sentido. Isso ocorre por que o programa possivelmente foi implantado com alguma proteção contra engenharia reversa. '
layout: post
guid: http://www.sawp.com.br/blog/?p=131
permalink: /p=131
categories:
  - Programming Internals
tags:
  - cracking ofuscação código reverse cracker
---
## 1. Introdução</p> 

Quando disassemblamos um binário para crackearmos, muitas vezes nos deparamos com um código que parece não fazer sentido. Isso ocorre por que o programa possivelmente foi implantado com alguma proteção contra engenharia reversa. 

São muitos os casos em que se deseja criar softwares com proteção contra reversão. Desde criadores de vírus, que desejam dificultar o trabalho das empresas de antígenos, até as grandes corporações desenvolvedoras de software e jogos, que desejam atrasar a ação de crackers.

Veremos aqui as técnicas usadas para tornar o código compilado mais imune à ação de reversers e as conseqüências adversas que sua implementação trás, contribuindo para a perda de desempenho e aumento da complexidade do sistema.

&nbsp;

## 2. Anticracking? Para que?</p> 

Com o começo da comercialização dos computadores pessoais, ainda na década de 70, houve uma grande mudança na importância dada ao software. Ele deixou de ser visto como a simples &#8220;interface de operação&#8221; da máquina para se tornar o produto de uma industria própria.

Sendo mais do que um mero componente de um sistema computacional, uma grande parcela dos softwares produzidos se tornou um produto de comercialização, com todas as características que um bem de consumo possui. 

Desta indústria surgida com os sistemas de softwares também vieram as empresas tomar propriedade sobre seus produtos. E como toda indústria que sobrevive de suas patentes e fórmulas secretas, surge também a proteção do código fechado, através das técnicas anticracking.

Foi no contexto dos softwares proprietários que surgiram as atividades de cracking. Programadores que utilizavam sistemas das empresas, com recursos limitados, começaram a modificar estes programas para melhorá-los. Como na época a maioria dos softwares não eram de código aberto, os programadores precisavam alterar o próprio executável, já que não possuíam o fonte original.

Também foi nesse entrecho que se desenvolveram as técnicas anticracking. Constatada as alterações dos programas originais, as empresas começaram a proteger mais os seus &#8220;produtos&#8221;. 

Todavia, algumas aplicações realmente precisam de técnicas de anticracking. As plataformas JAVA e .NET geram um código executável com estrutura muito próxima da representação de linguagem. Por isso, há um esforço grande para o desenvolvimento de métodos de proteção de código para estas plataformas.

&nbsp;

## 3. Métodos de Anticracking</p> 

São várias as abordagens que podemos tomar para proteger um código. Cada uma delas possui suas próprias vantagens e desvantagens. Normalmente as aplicações utilizam uma combinação das técnicas que veremos para minimizar a produtividade do trabalho dos crackers. 

Contudo, deve-se escolher bem as técnicas a serem usadas de acordo com a tecnologia empregada, ambiente de execução, tamanho do programa e padrões de projetos, de forma minimizar os efeitos adversos que surgem pelo anticracking.

Os métodos abordados para antricracking são: Eliminação de Informação Simbólica, Técnicas Ativas de AntiDebugging, Confundir Disassemblers, Encriptação e Ofuscação de Código e Transformações no Controle de Fluxo.

&nbsp;

### 3.1 Eliminação de Informação Simbólica (Eliminating Symbolic Information &#8211; ESI)</p> 

A abordagem mais óbvia para confundir quem está lendo diretamente um código disassemblado é eliminar toda e qualquer informação textual do programa. 

No post em que demonstrei como se crackear um executável ( A Formula do Crack ) , utilizei como referência as informações textuais para localizar quais trechos de código são responsáveis por quais ações.

Se as strings no código assembly não estivessem transparentes, ou seja, se fossem diferentes da forma como vemos no programa em execução, o trabalho seria realmente bem mais difícil e demorado. 

Em um binário executável que acessa diretamente o hardware, não-bytecode, podemos simplesmente esconder toda a informação do programa. Já em programas baseados em bytecodes os executáveis muitas vezes contém uma grande quantidade de informação simbólica, como nome de classes, nome de membro de classes e a tabela de objetos instanciados. Estas informações podem ser extremamente úteis para quem disassemblar o código pois com base nelas é possível localizar pontos-chave do código. 

&nbsp;

### 3.2 Ofuscação e Encriptação de Código (Code Obfuscation and Encryption &#8211; COE) </p> 

Encriptação e ofuscação são técnicas utilizadas para reduzir a vulnerabilidade de crackear programas. Normalmente são utilizadas quando a ESI não é suficiente para proteção anticracking.

Consiste em modificar o layout do programa, a lógica e os dados de forma que reorganize o código, tornando-o menos legível, mas mantendo a funcionalidade para o usuário final.

COE difere-se da Eliminação Simbólica por alterar a estrutura do código em sí e não dos nomes dos componentes constantes.

&nbsp;

### 3.3 Técnicas Ativas de Antidebuggin (Active AntiDebugger Techniques  AADT)</p> 

Considerando que as atividades de cracking são feitas em grande parte com o uso de debuggers a possibilidade de incorporar no programa algum código que complique o processo de depuração é desejável para o aumento na proteção do código.

Técnicas AADT são altamente efetivas quando combinadas com encriptação de código. Pois, ao encriptar o programa, força os crackers executá-lo dentro de um debugger e o código AADT não permite sua depuração.

Existem dezenas de truques utilizados para antidebuggin. Mas quase todos são dependentes de plataforma ou altamente dependente de sistemas operacionais.

As implementações de AADT oferecem alguns riscos e algumas vezes costumam gerar exceções não tratáveis e causar mal funcionamento do programa quando detecta um debugger no sistema, mesmo se o programa não estiver anexado ao debugger.

&nbsp;

### 3.4 Confundindo Disassemblers (Confusing Disassemblers &#8211; CD)</p> 

Enganar disassemblers para inibir a atividade de crackers não é uma forma muito resistente de antireversing. Entretanto, é a mais popular.

A estratégia é simples: Nas arquiteturas de processadores que usam instruções de tamanho variável (como IA-32) é possível enganar o disassembler inserindo dados impróprios no começo da instrução. Isto faz com que o disassembler perca a sincronização e disassemble o resto do código incorretamente (colocando 1 bit a direita ou a esquerda, o conjunto de bits seguintes implicarão na perda da instrução).

&nbsp;

### 3.5 Transformações no Controle de Fluxo (Control Flow Transformations &#8211; CFT)</p> 

Transformações no controle de fluxo consistem em alterar a ordem e o fluxo de um programa para reduzir a legibilidade do código ao gerar assembly. Podendo ser definida em 3 categorias: computação de transformações, agregação de transformações e ordenação de transformações.

A Computação de Transformações modifica a estrutura de fluxo original para trazer uma funcionalidade equivalente ao usuário final, mas tornando mais difícil de se reverter o código. Isso pode ser feito removendo o fluxo de informação do programa e adicionando outra declaração de controle de fluxo que complicaria o entendimento para quem for ler o código em baixo nível.

A Agregação de Transformações destrói a estrutura de alto nível do programa, quebrando a abstração de linguagem de alto nível em tempo de programação. A idéia básica é desfazer essa abstração de modo que após a compilação ser feita a funcionalidade do programa se mantenha, mas quando o código seja desassemblado a estrutura pareça absurda.

Por fim Ordenação de Transformadas são as menos poderosas e consistem em randomizar a ordem das operações em um programa na esperança de reduzir a legibilidade do programa.

&nbsp;

### 3.6 Transformações de Dados ( Data Transformations &#8211; DT )</p> 

Transformações de dados focam em encriptar tanto os dados quanto a estrutura do programa. Essa associação é interessante pois identificar uma importante estrutura de dados é um dos passos fundamentais para entender como o programa funciona. 

&nbsp;

## 4. Conclusão</p> 

Como vimos aqui, existem algumas opções disponíveis para os desenvolvedores de software que precisem atrasar o trabalho dos crackers. Neste tópico comentamos sobre as abordagens mais comuns que iremos discutir mais detalhadamente em outros artigos.
