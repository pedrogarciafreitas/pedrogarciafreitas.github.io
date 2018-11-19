---
id: 1841
title: 'Corrigindo o erro &#8220;ifort: error #10001: could not find directory in which g++ resides&#8221; no Rocks'
date: 2012-10-08T19:49:33+00:00
author: SAWP
excerpt: Correção dos erros de compilação do ifort e outros problemas causados pela falta de espaço no /var
layout: post
guid: http://www.sawp.com.br/blog/?p=1841
permalink: p=1841
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1685:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">unlink</span> <span style="color: #000000; font-weight: bold;">/</span>tmp
    <span style="color: #c20cb9; font-weight: bold;">rm</span> <span style="color: #660033;">-rf</span> <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>tmp
    <span style="color: #c20cb9; font-weight: bold;">mkdir</span> <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition1<span style="color: #000000; font-weight: bold;">/</span>tmp
    <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition<span style="color: #000000; font-weight: bold;">/</span>tmp <span style="color: #000000; font-weight: bold;">/</span>tmp
    <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition<span style="color: #000000; font-weight: bold;">/</span>tmp <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>tmp</pre></td></tr></table><p class="theCode" style="display:none;">unlink /tmp
    rm -rf /var/tmp
    mkdir /state/partition1/tmp
    ln -s /state/partition/tmp /tmp
    ln -s /state/partition/tmp /var/tmp</p></div>
    ;i:2;s:499:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">rm</span> <span style="color: #660033;">-rf</span> <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>log<span style="color: #000000; font-weight: bold;">/*</span></pre></td></tr></table><p class="theCode" style="display:none;">rm -rf /var/log/*</p></div>
    ";}
categories:
  - Rocks Cluster for Nubis
---
Se, ao compilar, o ifort fornece o seguinte erro:
  


<center>
  <code>ifort: error #10001: could not find directory in which g++ resides</code>
</center>


  
Isso ocorre porque não há espaço suficiente no **/var/tmp**. Para resolver isso, dê os seguintes comandos:

<pre lang="bash">unlink /tmp
rm -rf /var/tmp
mkdir /state/partition1/tmp
ln -s /state/partition/tmp /tmp
ln -s /state/partition/tmp /var/tmp</pre>

Isso deve bastar para arrumar este erro. Contudo, esse e outros erros decorrentes do **/var** sem espaço, basta limpar a pasta de logs:

<pre lang="bash">rm -rf /var/log/*</pre>
