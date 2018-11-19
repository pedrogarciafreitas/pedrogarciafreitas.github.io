---
id: 1801
title: Instalando Compiladores da Intel no Rocks Cluster
date: 2012-09-22T13:24:43+00:00
author: SAWP
excerpt: Passo a passo para instalar o ifort no Rocks Cluster.
layout: post
guid: http://www.sawp.com.br/blog/?p=1801
permalink: p=1801
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:763:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># wget http://www.sawp.com.br/share/rocks/l_cprof_p_11.1.069_intel64.tgz</span>
    <span style="color: #666666; font-style: italic;"># tar -zxvf  l_cprof_p_11.1.069_intel64.tgz</span>
    <span style="color: #666666; font-style: italic;"># cd  l_cprof_p_11.1.069_intel64</span>
    <span style="color: #666666; font-style: italic;"># ./install.sh</span></pre></td></tr></table><p class="theCode" style="display:none;"># wget http://www.sawp.com.br/share/rocks/l_cprof_p_11.1.069_intel64.tgz
    # tar -zxvf  l_cprof_p_11.1.069_intel64.tgz
    # cd  l_cprof_p_11.1.069_intel64
    # ./install.sh</p></div>
    ;i:2;s:1295:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># wget http://rocks.stanford.edu/ISOS/ENVIRONMENT/modules-5.3/modules-5.3-1.x86_64.disk1.iso</span>
    <span style="color: #666666; font-style: italic;"># rocks add roll modules-5.3-1.x86_64.disk1.iso</span>
    <span style="color: #666666; font-style: italic;"># rocks enable roll modules</span>
    <span style="color: #666666; font-style: italic;"># cd /export/rocks/install</span>
    <span style="color: #666666; font-style: italic;"># rocks create distro</span>
    <span style="color: #666666; font-style: italic;"># rocks run roll modules | sh</span>
    <span style="color: #666666; font-style: italic;"># source /etc/profile</span>
    <span style="color: #666666; font-style: italic;"># tentakel /boot/kickstart/cluster-kickstart</span></pre></td></tr></table><p class="theCode" style="display:none;"># wget http://rocks.stanford.edu/ISOS/ENVIRONMENT/modules-5.3/modules-5.3-1.x86_64.disk1.iso
    # rocks add roll modules-5.3-1.x86_64.disk1.iso
    # rocks enable roll modules
    # cd /export/rocks/install
    # rocks create distro
    # rocks run roll modules | sh
    # source /etc/profile
    # tentakel /boot/kickstart/cluster-kickstart</p></div>
    ;i:3;s:1323:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># wget http://rocks.stanford.edu/ISOS/COMPILERS/intel-11-5.3/intel-11-5.3-1.x86_64.disk1.iso</span>
    <span style="color: #666666; font-style: italic;"># rocks add roll intel-11-5.3-1.x86_64.disk1.iso</span>
    <span style="color: #666666; font-style: italic;"># rocks enable roll intel-11</span>
    <span style="color: #666666; font-style: italic;"># cd /export/rocks/install</span>
    <span style="color: #666666; font-style: italic;"># rocks create distro</span>
    <span style="color: #666666; font-style: italic;"># rocks run roll intel-11 &gt;&gt; intel-11.sh</span>
    <span style="color: #666666; font-style: italic;"># sh intel-11.sh</span>
    <span style="color: #666666; font-style: italic;"># tentakel /boot/kickstart/cluster-kickstart</span></pre></td></tr></table><p class="theCode" style="display:none;"># wget http://rocks.stanford.edu/ISOS/COMPILERS/intel-11-5.3/intel-11-5.3-1.x86_64.disk1.iso
    # rocks add roll intel-11-5.3-1.x86_64.disk1.iso
    # rocks enable roll intel-11
    # cd /export/rocks/install
    # rocks create distro
    # rocks run roll intel-11 &gt;&gt; intel-11.sh
    # sh intel-11.sh
    # tentakel /boot/kickstart/cluster-kickstart</p></div>
    ";}
categories:
  - Rocks Cluster for Nubis
---
Os exemplos aqui seguem com o **ifort** (Intel Fortran Compiler) para arquitetura x86_64.

<pre lang="bash"># wget http://www.sawp.com.br/share/rocks/l_cprof_p_11.1.069_intel64.tgz
# tar -zxvf  l_cprof_p_11.1.069_intel64.tgz
# cd  l_cprof_p_11.1.069_intel64
# ./install.sh
</pre>

Durante a instalação, será requisitado o serial. Um número válido é **NB3L-PMHW76B8**.

O próximo passo é instalar os rolls dos módulos do kernel. Para isso, faça o download de acordo com a versão do Rocks instalada. A nomenclatura que segue dos links é **http://rocks.stanford.edu/ISOS/ENVIRONMENT/modules-[version]/modules-[version].x86_64.disk1.iso**. Por exemplo, no Rocks 5.3, siga os passos:

<pre lang="bash"># wget http://rocks.stanford.edu/ISOS/ENVIRONMENT/modules-5.3/modules-5.3-1.x86_64.disk1.iso
# rocks add roll modules-5.3-1.x86_64.disk1.iso
# rocks enable roll modules
# cd /export/rocks/install
# rocks create distro
# rocks run roll modules | sh
# source /etc/profile
# tentakel /boot/kickstart/cluster-kickstart
</pre>

Por último, é preciso instalar o roll da Intel. A ideia segue o mesmo padrão de nomenclatura dos módulos: **http://rocks.stanford.edu/ISOS/COMPILERS/intel-[compiler\_version]-[rocks\_version].x86_64.disk1.iso**. Por exemplo, para instalar no Rocks 5.3:

<pre lang="bash"># wget http://rocks.stanford.edu/ISOS/COMPILERS/intel-11-5.3/intel-11-5.3-1.x86_64.disk1.iso
# rocks add roll intel-11-5.3-1.x86_64.disk1.iso
# rocks enable roll intel-11
# cd /export/rocks/install
# rocks create distro
# rocks run roll intel-11 >> intel-11.sh
# sh intel-11.sh
# tentakel /boot/kickstart/cluster-kickstart</pre>
