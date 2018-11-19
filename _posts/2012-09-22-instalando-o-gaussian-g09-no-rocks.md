---
id: 1813
title: Instalando o Gaussian (G09) no Rocks
date: 2012-09-22T14:46:45+00:00
author: SAWP
excerpt: Instruções para a Instalação do Gaussian.
layout: post
guid: http://www.sawp.com.br/blog/?p=1813
permalink: /p=1813
wp-syntax-cache-content:
  - |
    a:8:{i:1;s:703:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># cd /etc</span>
    <span style="color: #666666; font-style: italic;"># cp -p group group.bak</span>
    <span style="color: #666666; font-style: italic;"># cp -p gshadow gshadow.bak</span>
    <span style="color: #666666; font-style: italic;"># grep 499 group</span>
    <span style="color: #666666; font-style: italic;"># groupadd -g 499 gaussian</span></pre></td></tr></table><p class="theCode" style="display:none;"># cd /etc
    # cp -p group group.bak
    # cp -p gshadow gshadow.bak
    # grep 499 group
    # groupadd -g 499 gaussian</p></div>
    ;i:2;s:373:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;"># </span>usermod <span style="color: #660033;">-a</span> <span style="color: #660033;">-G</span> gaussian dasf</pre></td></tr></table><p class="theCode" style="display:none;"># usermod -a -G gaussian dasf</p></div>
    ;i:3;s:691:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># cd /export/apps/</span>
    <span style="color: #666666; font-style: italic;"># wget http://www.sawp.com.br/share/rocks/E64_930X.TGZ</span>
    <span style="color: #666666; font-style: italic;"># tar -zxvf E64_930X.TGZ </span>
    <span style="color: #666666; font-style: italic;"># chown -R root:gaussian g09</span></pre></td></tr></table><p class="theCode" style="display:none;"># cd /export/apps/
    # wget http://www.sawp.com.br/share/rocks/E64_930X.TGZ
    # tar -zxvf E64_930X.TGZ
    # chown -R root:gaussian g09</p></div>
    ;i:4;s:828:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;"># </span><span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>export<span style="color: #000000; font-weight: bold;">/</span>rocks<span style="color: #000000; font-weight: bold;">/</span>install<span style="color: #000000; font-weight: bold;">/</span>site-profiles<span style="color: #000000; font-weight: bold;">/</span><span style="color: #000000;">5.3</span><span style="color: #000000; font-weight: bold;">/</span>nodes<span style="color: #000000; font-weight: bold;">/</span></pre></td></tr></table><p class="theCode" style="display:none;"># cd /export/rocks/install/site-profiles/5.3/nodes/</p></div>
    ;i:5;s:369:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;"># </span><span style="color: #c20cb9; font-weight: bold;">cp</span> skeleton.xml extend-compute.xml</pre></td></tr></table><p class="theCode" style="display:none;"># cp skeleton.xml extend-compute.xml</p></div>
    ;i:6;s:1528:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #000000; font-weight: bold;">!</span> <span style="color: #660033;">-d</span> <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition1<span style="color: #000000; font-weight: bold;">/</span>scratch <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
    <span style="color: #c20cb9; font-weight: bold;">mkdir</span> <span style="color: #660033;">-p</span> <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition1<span style="color: #000000; font-weight: bold;">/</span>scratch
    <span style="color: #c20cb9; font-weight: bold;">chmod</span> <span style="color: #000000;">777</span> <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition1<span style="color: #000000; font-weight: bold;">/</span>scratch
    <span style="color: #000000; font-weight: bold;">fi</span></pre></td></tr></table><p class="theCode" style="display:none;">if [ ! -d /state/partition1/scratch ]; then
    mkdir -p /state/partition1/scratch
    chmod 777 /state/partition1/scratch
    fi</p></div>
    ;i:7;s:283:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;"># </span>rocks create distro</pre></td></tr></table><p class="theCode" style="display:none;"># rocks create distro</p></div>
    ;i:8;s:1392:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">module load intel
    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #000000; font-weight: bold;">!</span> <span style="color: #660033;">-d</span> <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition1<span style="color: #000000; font-weight: bold;">/</span>scratch<span style="color: #000000; font-weight: bold;">/</span><span style="color: #007800;">$USER</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
    <span style="color: #c20cb9; font-weight: bold;">mkdir</span>  <span style="color: #000000; font-weight: bold;">/</span>state<span style="color: #000000; font-weight: bold;">/</span>partition1<span style="color: #000000; font-weight: bold;">/</span>scratch<span style="color: #000000; font-weight: bold;">/</span><span style="color: #007800;">$USER</span>
    <span style="color: #000000; font-weight: bold;">fi</span></pre></td></tr></table><p class="theCode" style="display:none;">module load intel
    if [ ! -d /state/partition1/scratch/$USER ]; then
    mkdir  /state/partition1/scratch/$USER
    fi</p></div>
    ";}
categories:
  - Rocks Cluster for Nubis
---
Crie um grupo para os usuários do programa

<pre lang="bash"># cd /etc
# cp -p group group.bak
# cp -p gshadow gshadow.bak
# grep 499 group
# groupadd -g 499 gaussian
</pre>

Depois de criado o grupo, deve-se adicionar os usuários que tem permissão para usar o Gaussian ao grupo

<pre lang="bash"># usermod -a -G gaussian dasf</pre>

Agora, é preciso instalar o Gaussian de fato:

<pre lang="bash"># cd /export/apps/
# wget http://www.sawp.com.br/share/rocks/E64_930X.TGZ
# tar -zxvf E64_930X.TGZ 
# chown -R root:gaussian g09
</pre>

Até então, o ambiente já possui o programa, mas ainda falta configurá-lo para que ele esteja acessível em todos os nós. Primeiramente, deve-se ir para o diretório **cd /export/rocks/install/site-profiles/[rocks_version]/nodes/**. Por exemplo, no Rocks 5.3 o diretório é

<pre lang="bash"># cd /export/rocks/install/site-profiles/5.3/nodes/
</pre>

Copie agora o arquivo **skeleton.xml** para **extend-compute.xml**:

<pre lang="bash"># cp skeleton.xml extend-compute.xml
</pre>

Neste novo arquivo, o conteúdo delimitado pelas tags **<post>** deve ser substituído por

<pre lang="bash">if [ ! -d /state/partition1/scratch ]; then
    mkdir -p /state/partition1/scratch
    chmod 777 /state/partition1/scratch
fi
</pre>

Então, deve-se executar no prompt o seguinte comando:

<pre lang="bash"># rocks create distro
</pre>

Pronto, o programa está instalado. Se for para disponibilizar para todos os usuários, é preciso alterar o arquivo **/etc/bashrc**, adicionando ao final do arquivo as seguintes linhas:

<pre lang="bash">module load intel
if [ ! -d /state/partition1/scratch/$USER ]; then
    mkdir  /state/partition1/scratch/$USER
fi
</pre>
