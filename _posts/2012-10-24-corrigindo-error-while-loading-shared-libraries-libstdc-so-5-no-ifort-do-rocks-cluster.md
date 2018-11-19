---
id: 1853
title: 'Corrigindo &#8220;error while loading shared libraries: libstdc++.so.5&#8221; no ifort do Rocks Cluster'
date: 2012-10-24T15:21:15+00:00
author: SAWP
excerpt: |
  Corrigindo:
  /opt/intel/Compiler/11.1/069/bin/intel64/fortcom: error while loading shared libraries: libstdc++.so.5: cannot open shared object file: No such file or directory
  ifort: error #10273: Fatal error in /opt/intel/Compiler/11.1/069/bin/intel64/fortcom, terminated by 0x7f
layout: post
guid: http://www.sawp.com.br/blog/?p=1853
permalink: p=1853
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:400:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">-bash-3.2$ </span>ifort test.f90 <span style="color: #660033;">-o</span> <span style="color: #7a0874; font-weight: bold;">test</span></pre></td></tr></table><p class="theCode" style="display:none;">-bash-3.2$ ifort test.f90 -o test</p></div>
    ;i:2;s:1413:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">wget</span> www.sawp.com.br<span style="color: #000000; font-weight: bold;">/</span>share<span style="color: #000000; font-weight: bold;">/</span>rocks<span style="color: #000000; font-weight: bold;">/</span>libstdc++.so.5.0.7
    <span style="color: #c20cb9; font-weight: bold;">mv</span> libstdc++.so.5.0.7 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>lib64<span style="color: #000000; font-weight: bold;">/</span>libstdc++.so.5.0.7
    <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-s</span> <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>lib64<span style="color: #000000; font-weight: bold;">/</span>libstdc++.so.5.0.7 <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>lib64<span style="color: #000000; font-weight: bold;">/</span>libstdc++.so.5</pre></td></tr></table><p class="theCode" style="display:none;">wget www.sawp.com.br/share/rocks/libstdc++.so.5.0.7
    mv libstdc++.so.5.0.7 /usr/lib64/libstdc++.so.5.0.7
    ln -s /usr/lib64/libstdc++.so.5.0.7 /usr/lib64/libstdc++.so.5</p></div>
    ";}
categories:
  - Rocks Cluster for Nubis
---
Após instalado o ifort, ao compilar um código-fonte,

<pre lang="bash">-bash-3.2$ ifort test.f90 -o test</pre>

nos deparamos com o seguinte erro:

> `<br />
/opt/intel/Compiler/11.1/069/bin/intel64/fortcom: error while loading shared libraries: libstdc++.so.5: cannot open shared object file: No such file or directory<br />
ifort: error #10273: Fatal error in /opt/intel/Compiler/11.1/069/bin/intel64/fortcom, terminated by 0x7f`

Isso ocorre porque a versão do cpp instalado é mais nova do que a requerida pelo ifort. Para usar o ifort, basta baixar a versão requerida e colocar no diretório correto:

<pre lang="bash">wget www.sawp.com.br/share/rocks/libstdc++.so.5.0.7
mv libstdc++.so.5.0.7 /usr/lib64/libstdc++.so.5.0.7
ln -s /usr/lib64/libstdc++.so.5.0.7 /usr/lib64/libstdc++.so.5</pre>
