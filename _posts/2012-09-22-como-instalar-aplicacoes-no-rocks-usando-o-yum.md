---
id: 1787
title: Como Instalar Aplicações no Rocks Usando o yum
date: 2012-09-22T11:32:38+00:00
author: SAWP
excerpt: Como instalar aplicações no Rocks usando gerenciador de pacotes o yum, usado no CentOS. Note que essas aplicações podem funcionar somente no frontend.
layout: post
guid: http://www.sawp.com.br/blog/?p=1787
permalink: p=1787
categories:
  - Rocks Cluster for Nubis
---
O primeiro passo é fazer o download de todas OS rolls da versão do Rocks instalado. Isto é, se você instalou o Rocks 5.3, vá em 

<center>
  <strong>DOWNLOADS → Older downloads → Download Rolled Tacos (5.3) for Linux</strong> <br /> (ou acesse esse endereço: <a href="http://www.rocksclusters.org/ftp-site/pub/rocks/" target=_blank>http://www.rocksclusters.org/ftp-site/pub/rocks/)</a>
</center>

Desça até a opção de CDs e faça o download de todos os discos OS Rolls (os arquivos estão nomeados como **os-[versão].[arquitetura].disk[i].iso**). 

No diretório em que os CDs foram baixados, como root, digite:

> `<br />
# rocks add roll os*iso<br />
` 

e finalmente faça um rebuild da distribuição:

> `<br />
# cd /export/rocks/install<br />
# rocks create distro<br />
` 

Agora é possível instalar vários pacotes direto pelo yum através do comando

> `<br />
# yum install [package]<br />
` 

Para instalar o gnuplot:

> `<br />
# yum clean<br />
# yum install gnuplot<br />
`
