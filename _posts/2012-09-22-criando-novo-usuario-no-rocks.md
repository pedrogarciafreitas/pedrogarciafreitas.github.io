---
id: 1827
title: Criando Novo Usuário no Rocks
date: 2012-09-22T16:42:50+00:00
author: CKPYT
excerpt: Detalhes para criar usuários e compartilhar com os nós.
layout: post
guid: http://www.sawp.com.br/blog/?p=1827
permalink: /p=1827
categories:
  - Rocks Cluster for Nubis
---
`<br />
# useradd -d /export/home/[username]<br />
# passwd [username]<br />
# usermod -a -G gaussian [username]<br />
# rocks sync users<br />
`
