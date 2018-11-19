---
id: 1959
title: Modificação das interfaces de rede
date: 2013-03-11T20:33:34+00:00
author: SAWP
excerpt: Como fazer o Rocks reconhecer novas interfaces de rede instaladas.
layout: post
guid: http://www.sawp.com.br/blog/?p=1959
permalink: /p=1959
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:404:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">dmesg</span> <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">grep</span> eth</pre></td></tr></table><p class="theCode" style="display:none;">dmesg | grep eth</p></div>
    ";}
categories:
  - Rocks Cluster for Nubis
---
Ao modificar as interfaces de rede, o Rocks não irá detectar o novo dispositivo. Se você quiser simplesmente substituir as interfaces de rede por algum motivo (tal como trocar por um modelo mais veloz), será necessário atualizar os endereços MACs nas configurações do _frontend_. Portanto, primeiramente descubra o MAC da(s) nova(s) interfaces instaladas. Isso pode ser feito utilizando-se o comando

<pre lang="bash">dmesg | grep eth</pre>

Isso deve produzir uma saída parecida com

> `<br />
eth0: RealTek RTL8139 at 0xffffc2000002cc00, 00:08:54:21:ba:31, IRQ 16<br />
eth0:  Identified 8139 chip type 'RTL-8100B/8139D'<br />
eth0: link up, 100Mbps, full-duplex, lpa 0xC5E1<br />
eth0: no IPv6 routers present<br />
` 

Onde **00:08:54:21:ba:31** é o MAC do dispositivo instalado. 

Em seguida, edite o arquivo **/etc/sysconfig/network-scripts/ifcfg-eth0** e substitua o valor da variável **HWADDR** pelo endereço MAC da interface instalada. Note que nesse caso foi atualizada a interface que desejamos herdar as configurações para eth0. Se você substituir outras interfaces, modifique o arquivo ifcfg-eth_ apropriado.
