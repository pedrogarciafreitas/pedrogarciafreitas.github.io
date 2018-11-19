---
id: 1829
title: Gerador de Strings Aleatórias em Bash (one liner)
date: 2012-09-22T17:23:59+00:00
author: CKPYT
excerpt: One liner password generator em Bash para propósitos gerais...
layout: post
guid: http://www.sawp.com.br/blog/?p=1829
permalink: /p=1829
categories:
  - Quick Tips For Networking
---
Esse script de geração de strings aleatórias tem me sido muito útil para geração de senhas para os usuários. Basta criar um arquivo em **/usr/local/bin/password-generator** com permissão de execução e inserir este conteúdo:
  


<center>
  <code>dd if=/dev/urandom count=1 2> /dev/null | uuencode -m - | sed -ne 2p | cut -c-12</code>
</center>
