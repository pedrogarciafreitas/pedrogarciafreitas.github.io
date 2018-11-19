---
id: 225
title: 'Técnicas AntiCracking – Parte VII &#8211; Conclusão'
date: 2009-01-16T12:25:53+00:00
author: SAWP
excerpt: O programa ficará mais lento quão maior for o descuido na implantação dessas técnicas devido aos efeitos adversos, tais como o uso excessivo da CPU com instruções que não tem funcionalidade nenhuma para o usuário, o aumento significativo do código e a perda de desempenho no sistema. Todavia, ao implementar este tipo de proteção devemos usar as técnicas de forma que as reações colaterais sejam minimizadas. Neste artigo, discutimos quais são os custos ao se implementar uma técnica que desfavoreça a engenharia reversa, o nível de proteção máximo que se pode ser obtido e qual preço desta segurança.
layout: post
guid: http://www.sawp.com.br/blog/?p=225
permalink: p=225
categories:
  - Programming Internals
tags:
  - cracking ofuscação código reverse cracker
---
Vimos ser impossível criar-se um código imune ao cracking. O que é se faz é esconder, mascarar, enganar e obstruir o programa para que ele se torne lento demais, detecte alguma ferramenta de cracking instalada no sistema, ou faça o código gerado ser um tormento para um leitor humano.

Espero que tenha ficado claro que é possível se criar códigos extremamente difíceis de se crackear, desde que se pague um preço por isso. E a maior penalidade sofrida é a queda de performance em tempo de execução.

O programa ficará mais lerdo quão maior for o descuido na implantação dessas técnicas devido aos efeitos adversos, tais como o uso excessivo da CPU com instruções que não tem funcionalidade nenhuma para o usuário, o aumento significativo do código e a perda de desempenho no sistema.

Todavia, as pessoas que implementam este tipo de proteção combinam as técnicas de forma que as reações colaterais sejam minimizadas. Uma das formas de se fazer isto é colocando um pré-requisito de hardware superior ao que seria necessário para rodar as funcionalidades do programa sem anticracking.

Como exemplo disso, podemos pensar nas empresas desenvolvedoras de jogos. Sabendo que o hardware necessário para execução de um jogo normalmente possui requisitos específicos – como um conjunto restrito de placas de vídeo, processadores e quantidade de RAM –, estas empresas podem usar as técnicas anticracking em pontos do programa que necessitam mais de segurança do que eficiência – como as checagens de serial, registro, validade de instalação etc. Assim, o usuário não percebe a queda de eficiência relativa para a funcionalidade que foi protegida, afinal possui um hardware potente suficiente que compensa esta perda.

Do estudo que tivemos sobre as técnicas anticracking podemos ver que surge uma vantagem sobre os programas que possuem código aberto. Como estes sistemas já disponibilizam o código-fonte, não há necessidade de protegê-lo com os métodos contra-reversão. Isso faz com que a perda de desempenho pelo uso das técnicas não seja inserida no sistema.

Entre outras características que distinguem software proprietário e livre, nota-se que os sistemas abertos costumam ter eficiência computacional superior se compararmos programas com fins semelhantes. Uma das possíveis razões para isso se dá justamente pela inserção de meios que impedem a reversão no sistema proprietário, e que consome recursos que poderiam estar disponíveis para as necessidades do usuário.

Por fim, gostaria de agradecer à Christian Collberg e Clark Thomborson que desenvolveram um extenso estudo sobre as transformações no controle de fluxo e suas aplicações em anticracking. [1]
  
Para saber mais consulte a bibliografia que utilizei para desenvolver estes artigos.

&nbsp;

## Bibliografia

  * [1] “Manufacturing Cheap, Resilient, and Stealthy Opaque Constructs” &#8211; <a href="http://www.cs.arizona.edu/~collberg/Research/Publications/CollbergThomborsonLow98a/index.html" target="_blank">http://www.cs.arizona.edu/~collberg/Research/Publications/CollbergThomborsonLow98a/index.html</a>
  * <a href="http://www.cs.arizona.edu/~collberg/" target="_blank">http://www.cs.arizona.edu/~collberg/</a>
  * WROBLEWSKI, Gregory. General Method of Program Code Obfuscation.
  * THOMBORSON, C; LOW, Douglas; COLLBERG, C. A taxonomy of Obfuscating Transformations.
  * HYDE, Randall. The Art of Assembly Language.
  * CARTER, Paul. PC Assembly Language.
  * CALONI A. Engenharia reversa para principiantes. Google Docs. <a href="http://docs.google.com/Present?docid=ddd3j862_29grq4sx&fs=true" target="_blank">http://docs.google.com/Present?docid=ddd3j862_29grq4sx&fs=true</a>
