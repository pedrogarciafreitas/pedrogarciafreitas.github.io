---
id: 201
title: 'Técnicas AntiCracking – Parte III – Ofuscação  e Encriptação de Código'
date: 2008-12-12T11:31:22+00:00
author: SAWP
excerpt: |
  Também conhecidas como Code Obfuscation and Encryption (COE), são técnicas utilizadas para prevenir a Análise Estática de Código. Diferente da Eliminação Simbólica (Eliminating Symbolic Information – ESI), a COE é aplicada após a compilação do programa, modificando o binário original antes de ser entregue ao cliente.
layout: post
guid: http://www.sawp.com.br/blog/?p=201
permalink: /p=201
categories:
  - Programming Internals
tags:
  - Programming Internals
---
Também conhecidas como Code Obfuscation and Encryption (COE), são técnicas utilizadas para prevenir a Análise Estática de Código. 

Diferente da Eliminação Simbólica (Eliminating Symbolic Information – ESI), a COE é aplicada após a compilação do programa, modificando o binário original antes de ser entregue ao cliente. 

A encriptação de código normalmente não cria muita dificuldades para os crackers mais experientes, pois os códigos necessários para a decriptação fica presente no próprio executável. Basta uma análise online para o cracker encontrar a lógica e chave da decriptação. 

Para descobrir a chave de decriptação é simples. Com um debugger, executa-se o binário encriptado e observa-se o fluxo de execução. Todas instruções que indicam ponteiros para funções passarão por um trecho de código antes da execução. Este código é o próprio responsável pela decriptação. De posse dele é possível reverter todo o programa. 

Ou seja, o programa precisa decriptar o código em tempo de execução. Isso significa que uma cópia do programa decriptografado &#8211; ou partes dele &#8211; ficarão na memória durante a execução. Se usarmos um aplicativo à parte que leia a memória (como o Cheat Engine), podemos obter o asm da cópia decriptada. 

Sendo assim, quando algum cracker descobre o código para decriptação de um código criptografado, costuma reprogramá-lo e criar um “patch” para distribuir à comunidade. Estes “patches” são pacotes que criam novos executáveis contendo o programa original sem a criptografia. 

Para impedir a criação dos patches ou que um terceiro programa decripte o executável, esconde-se a chave de criptografia de uma maneira em que ela tenha alguma relação com o programa original. 

Uma forma eficaz de se fazer isso é utilizar uma chave que é calculada em tempo de execução dentro do programa. Contudo, o algoritmo gerador de chaves pode também ser encontrado, mas certamente consumirá mais tempo de análise pelo cracker. 

Outra medida que se utiliza para esconder a chave é utilizar identificadores do programa original para se criar chaves secundárias tais como “hashes” de trechos do próprio executável. 

Estas chaves secundárias garantem ao algoritmo de decriptação que ele só irá extrair o código original se estiver sendo executando do binário correto. Isso faz com que as chaves também sirvam como assinaturas de integridade. Sem estas “assinaturas” um programa externo não consegue retirar o código original mesmo tendo o algoritmo de decriptografia. Ou seja, impossibilita a construção de um “patch”. 

Uma combinação das duas técnicas mencionadas acima consiste em manter várias variáveis globais, denominadas “sentinelas”, que são acessadas e modificadas por diferentes subrotinas do programa. Estas sentinelas são utilizadas pelo algoritmo de decriptação. Os valores dessas variáveis são ainda mantidas por uma composição matemática que criam uma espécie de “log de execução” (conferindo se segue o fluxo de execução original), garantindo que quem está modificando-as é o próprio programa. 

Conforme dito anteriormente, utilizando Análise Online, um cracker poderia facilmente obter o algoritmo e as chaves para decriptografia. Mas com as técnicas comentadas acima, nota-se que é muito mais complexo se obter o código original completo, pois impede que um “patch” de decriptografia automática obtenha êxito.

A ofuscação de código é um processo muito semelhante à encriptação. Contudo esta é aplicada à um executável compilado, de plataforma específica, com conjunto de instruções bem definido. Já aquela é utilizada em casos em que envolvem instruções para máquinas virtuais, linguagens de script ou compilações intermediárias, como o bytecode. 

Ofuscar um código real significa transformá-lo em outro menos legível para o ser humano, inserindo nele instruções irrelevantes, mas mantendo sua funcionalidade. 

Podemos então pensar que a Eliminação de Informação Simbólica (ESI\EIS) é uma forma de ofuscação. Mas isso não é bem verdade. Enquanto a EIS consiste em criptografar e modificar strings identificadoras, ou seja, trabalha no escopo dos dados, a Ofuscação atua na alteração da estrutura do código. 

Um conceito de “nível de complexidade” é inserido quando falamos de ofuscação de código e é medida pelas formas convencionais de mensuração de complexidade de softwares. Este “nível de complexidade”, além de ser medido pela lógica e aritmética aplicada, também recebe como variável a “resistência” &#8211; capacidade de evitar “anti-ofuscação”. Um algorítimo de ofuscação é tão bom quão for sua resistência. 

Como a Ofuscação de Código é dada por uma transformada, há a possibilidade de se criar uma transformada inversa que traz de volta o código original. A esta transformada inversa damos o nome de “deofuscador”.
	  
O deofuscador é o programa que implementa uma série de análises de fluxo de dados e de execução no código ofuscado até que possa retirar o código original, removendo instruções irrelevantes.

Se o leitor chegou até aqui com as Partes I e II lidas deve ter notado que a perda de eficiência é um ponto comum à todas técnicas anti-cracking. E como não poderia ser diferente, as COE também possuem alto custo associado. 

Na encriptação temos uma grande perda de performance graças ao alto consumo de memória necessária para se extrair o código original, associada à um alto overhead na chamada dos processos responsáveis pela decriptografia. 

Embora na ofuscação de código não gastar-se tempo de processamento com a transformação inversa em tempo de execução, obtemos um código muito maior que o original, repleto de instruções com funcionalidades nulas, gerando um aumento no tempo de execução, de memória e de espaço requerido no disco. 

&nbsp; 

Alguns sites de programas ofuscadores e encriptadores:

<center>
  http://www.strongbit.com (execcryptor. Encripta assembly ia32)
</center>


  


<center>
  http://www.star-force.com (starforcesuit)<br />
</center>
