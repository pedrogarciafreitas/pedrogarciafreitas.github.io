---
id: 128
title: NestedVM – ASM MIPS para JAVA
date: 2008-08-07T19:03:24+00:00
author: SAWP
excerpt: |
  Veremos aqui sobre a NestedVM, conversor de Assembly MIPS para bytecode JAVA, “cross-compilation” para compilarmos de C++ para ASM MIPS, permitindo assim, em conjunto com o NestedVM, converter todo um sistema para JAVA. E comentaremos sobre alguns métodos alternativos e mais populares para integração de sistemas já prontos com o JAVA, como o JNI, Jazillian, c2j etc. E porquê esses sistemas ficam aquém ao NestedVm.
layout: post
guid: http://www.sawp.com.br/blog/?p=128
permalink: /p=128
wp-syntax-cache-content:
  - |
    a:19:{i:1;s:703:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="asm" style="font-family:monospace;"><span style="color: #339933;">//</span> lw v0<span style="color: #339933;">,</span> <span style="color: #ff0000;">20</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #46aa03; font-weight: bold;">sp</span><span style="color: #009900; font-weight: bold;">&#41;</span> <span style="color: #666666; font-style: italic;">; # carreg uma palavra de 4 bytes em sp+20, sp(stack pointer)</span></pre></td></tr></table><p class="theCode" style="display:none;">// lw v0, 20(sp) ; # carreg uma palavra de 4 bytes em sp+20, sp(stack pointer)</p></div>
    ;i:2;s:928:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">v0 <span style="color: #339933;">=</span> memory<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#40;</span>sp<span style="color: #339933;">+</span><span style="color: #cc66cc;">20</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">&gt;&gt;&gt;</span><span style="color: #cc66cc;">16</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#40;</span>sp<span style="color: #339933;">+</span><span style="color: #cc66cc;">20</span><span style="color: #009900;">&#41;</span>0xffff<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">v0 = memory[(sp+20)&gt;&gt;&gt;16][(sp+20)0xffff];</p></div>
    ;i:3;s:2106:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="asm" style="font-family:monospace;">string<span style="color: #339933;">:</span> <span style="color: #339933;">.</span>asciiz <span style="color: #7f007f;">&quot;Hello World \n&quot;</span>        <span style="color: #666666; font-style: italic;">; # string é um label</span>
    li        <span style="color: #0000ff; font-weight: bold;">$</span>v0<span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span>                                <span style="color: #666666; font-style: italic;">; # código da chamada do sistema</span>
    la        <span style="color: #0000ff; font-weight: bold;">$</span>a0<span style="color: #339933;">,</span> string                        <span style="color: #666666; font-style: italic;">; # carrega e coloca em $a0</span>
    <span style="color: #00007f; font-weight: bold;">syscall</span>                                        <span style="color: #666666; font-style: italic;">; # faz a chamada de sistema</span>
    # REFERENCIA <span style="color: #0000ff; font-weight: bold;">DO</span> SYSTEMCALL
    # http<span style="color: #339933;">://</span>www<span style="color: #339933;">.</span>doc<span style="color: #339933;">.</span>ic<span style="color: #339933;">.</span>ac<span style="color: #339933;">.</span>uk<span style="color: #339933;">/</span>lab<span style="color: #339933;">/</span>secondyear<span style="color: #339933;">/</span>spim<span style="color: #339933;">/</span>node8<span style="color: #339933;">.</span>html</pre></td></tr></table><p class="theCode" style="display:none;">string: .asciiz &quot;Hello World \n&quot;        ; # string é um label
    li        $v0, 4                                ; # código da chamada do sistema
    la        $a0, string                        ; # carrega e coloca em $a0
    syscall                                        ; # faz a chamada de sistema
    # REFERENCIA DO SYSTEMCALL
    # http://www.doc.ic.ac.uk/lab/secondyear/spim/node8.html</p></div>
    ;i:4;s:664:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="asm" style="font-family:monospace;">v0 = <span style="color: #00007f; font-weight: bold;">syscall</span><span style="color: #009900; font-weight: bold;">&#40;</span>v0<span style="color: #339933;">,</span>a0<span style="color: #339933;">,</span>a1<span style="color: #339933;">,</span>a2<span style="color: #339933;">,</span>a3<span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #666666; font-style: italic;">; // syscall</span></pre></td></tr></table><p class="theCode" style="display:none;">v0 = syscall(v0,a0,a1,a2,a3); // syscall</p></div>
    ;i:5;s:2252:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">/* Aqui o método syscall() executa uma operação baseada no
    número-código de referencia */</span>
    &nbsp;
    <span style="color: #000066; font-weight: bold;">int</span> syscall<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> sc, <span style="color: #000066; font-weight: bold;">int</span> a, <span style="color: #000066; font-weight: bold;">int</span> b, <span style="color: #000066; font-weight: bold;">int</span> c, <span style="color: #000066; font-weight: bold;">int</span> d<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">switch</span><span style="color: #009900;">&#40;</span>sc<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">case</span> SYS_write<span style="color: #339933;">:</span> <span style="color: #000000; font-weight: bold;">return</span> sys_write<span style="color: #009900;">&#40;</span>a,b,c,d<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">case</span> SYS_open<span style="color: #339933;">:</span> <span style="color: #000000; font-weight: bold;">return</span> sys_open<span style="color: #009900;">&#40;</span>a,b,c,d<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ....
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/* Aqui o método syscall() executa uma operação baseada no
    número-código de referencia */
    
    int syscall(int sc, int a, int b, int c, int d) {
    switch(sc) {
    case SYS_write: return sys_write(a,b,c,d);
    case SYS_open: return sys_open(a,b,c,d);
    ....
    }
    }</p></div>
    ;i:6;s:677:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">$ <span style="color: #7a0874; font-weight: bold;">cd</span> ~
    &nbsp;
    $  <span style="color: #c20cb9; font-weight: bold;">wget</span> http:<span style="color: #000000; font-weight: bold;">//</span>www.sawp.com.br<span style="color: #000000; font-weight: bold;">/</span>nestedvm<span style="color: #000000; font-weight: bold;">/</span>nestedvm-<span style="color: #000000;">2008</span>-08-06.tar.gz</pre></td></tr></table><p class="theCode" style="display:none;">$ cd ~
    
    $  wget http://www.sawp.com.br/nestedvm/nestedvm-2008-08-06.tar.gz</p></div>
    ;i:7;s:689:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $ <span style="color: #c20cb9; font-weight: bold;">tar</span> <span style="color: #660033;">-xfz</span> nestedvm-<span style="color: #000000;">2008</span>-08-06.tar.gz
    &nbsp;
    $ <span style="color: #7a0874; font-weight: bold;">cd</span> nestedvm-<span style="color: #000000;">2008</span>-08-06
    &nbsp;
    $ <span style="color: #c20cb9; font-weight: bold;">make</span></pre></td></tr></table><p class="theCode" style="display:none;">        $ tar -xfz nestedvm-2008-08-06.tar.gz
    
    $ cd nestedvm-2008-08-06
    
    $ make</p></div>
    ;i:8;s:354:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $ <span style="color: #c20cb9; font-weight: bold;">make</span> <span style="color: #7a0874; font-weight: bold;">test</span></pre></td></tr></table><p class="theCode" style="display:none;">        $ make test</p></div>
    ;i:9;s:5156:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        Constructor<span style="color: #000000; font-weight: bold;">!</span>
    &nbsp;
    Entered main<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    <span style="color: #000000;">16777215</span>
    &nbsp;
    <span style="color: #000000;">16777215</span>
    &nbsp;
    <span style="color: #000000;">16777215</span>
    &nbsp;
    <span style="color: #000000;">16777215</span>
    &nbsp;
    argv<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">0</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> = <span style="color: #ff0000;">&quot;tests.Test&quot;</span>
    &nbsp;
    argv<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> = <span style="color: #ff0000;">&quot;arg 1&quot;</span>
    &nbsp;
    argv<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">2</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> = <span style="color: #ff0000;">&quot;arg 2&quot;</span>
    &nbsp;
    argv<span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #000000;">3</span><span style="color: #7a0874; font-weight: bold;">&#93;</span> = <span style="color: #ff0000;">&quot;arg 3&quot;</span>
    &nbsp;
    getenv<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">&quot;USER&quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> = <span style="color: #ff0000;">&quot;(null)&quot;</span>
    &nbsp;
    getenv<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">&quot;HOME&quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> = <span style="color: #ff0000;">&quot;(null)&quot;</span>
    &nbsp;
    getenv<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">&quot;TZ&quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> = <span style="color: #ff0000;">&quot;(null)&quot;</span>
    &nbsp;
    GMT GMT <span style="color: #000000;">0</span>
    &nbsp;
    Running ctime
    &nbsp;
    ctime returned: 0x2b958
    &nbsp;
    Current time: Wed Aug  <span style="color: #000000;">6</span> <span style="color: #000000;">14</span>:<span style="color: #000000;">39</span>:<span style="color: #000000;">37</span> <span style="color: #000000;">2008</span>
    &nbsp;
    Trying to open <span style="color: #000000; font-weight: bold;">/</span>nonexistent
    &nbsp;
    open: No such <span style="color: #c20cb9; font-weight: bold;">file</span> or directory
    &nbsp;
    Tyring to <span style="color: #c20cb9; font-weight: bold;">mkdir</span> .mkdirtest
    &nbsp;
    Attempted to use a UnixRuntime syscall <span style="color: #000000; font-weight: bold;">in</span> Runtime <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #000000;">18</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    mkdir: Function not implemented
    &nbsp;
    Trying to opendir .
    &nbsp;
    opendir: No such <span style="color: #c20cb9; font-weight: bold;">file</span> or directory
    &nbsp;
    1.574000e+00
    &nbsp;
    -4.315000e+01l
    &nbsp;
    <span style="color: #660033;">-43</span>
    &nbsp;
    -4.315000e+01
    &nbsp;
    4.315000e+01
    &nbsp;
    Hello, World
    &nbsp;
    7F
    &nbsp;
    fabs<span style="color: #7a0874; font-weight: bold;">&#40;</span>-<span style="color: #000000;">2.24</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> = <span style="color: #000000;">2.34</span>
    &nbsp;
    Destructor<span style="color: #000000; font-weight: bold;">!</span></pre></td></tr></table><p class="theCode" style="display:none;">        Constructor!
    
    Entered main()
    
    16777215
    
    16777215
    
    16777215
    
    16777215
    
    argv[0] = &quot;tests.Test&quot;
    
    argv[1] = &quot;arg 1&quot;
    
    argv[2] = &quot;arg 2&quot;
    
    argv[3] = &quot;arg 3&quot;
    
    getenv(&quot;USER&quot;) = &quot;(null)&quot;
    
    getenv(&quot;HOME&quot;) = &quot;(null)&quot;
    
    getenv(&quot;TZ&quot;) = &quot;(null)&quot;
    
    GMT GMT 0
    
    Running ctime
    
    ctime returned: 0x2b958
    
    Current time: Wed Aug  6 14:39:37 2008
    
    Trying to open /nonexistent
    
    open: No such file or directory
    
    Tyring to mkdir .mkdirtest
    
    Attempted to use a UnixRuntime syscall in Runtime (18)
    
    mkdir: Function not implemented
    
    Trying to opendir .
    
    opendir: No such file or directory
    
    1.574000e+00
    
    -4.315000e+01l
    
    -43
    
    -4.315000e+01
    
    4.315000e+01
    
    Hello, World
    
    7F
    
    fabs(-2.24) = 2.34
    
    Destructor!</p></div>
    ;i:10;s:416:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $ <span style="color: #c20cb9; font-weight: bold;">make</span> env.sh
    &nbsp;
    $ <span style="color: #7a0874; font-weight: bold;">source</span> env.sh</pre></td></tr></table><p class="theCode" style="display:none;">        $ make env.sh
    
    $ source env.sh</p></div>
    ;i:11;s:878:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $ <span style="color: #c20cb9; font-weight: bold;">wget</span> http:<span style="color: #000000; font-weight: bold;">//</span>www.sawp.com.br<span style="color: #000000; font-weight: bold;">/</span>nestedvm<span style="color: #000000; font-weight: bold;">/</span>test.c
    &nbsp;
    $ <span style="color: #c20cb9; font-weight: bold;">wget</span> http:<span style="color: #000000; font-weight: bold;">//</span>www.sawp.com.br<span style="color: #000000; font-weight: bold;">/</span>nestedvm<span style="color: #000000; font-weight: bold;">/</span>test2.c</pre></td></tr></table><p class="theCode" style="display:none;">        $ wget http://www.sawp.com.br/nestedvm/test.c
    
    $ wget http://www.sawp.com.br/nestedvm/test2.c</p></div>
    ;i:12;s:498:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $  mips-unknown-elf-cpp <span style="color: #660033;">-o</span> test.mips test.c
    &nbsp;
    $  mips-unknown-elf-cpp <span style="color: #660033;">-o</span> test2.mips test2.c</pre></td></tr></table><p class="theCode" style="display:none;">        $  mips-unknown-elf-cpp -o test.mips test.c
    
    $  mips-unknown-elf-cpp -o test2.mips test2.c</p></div>
    ;i:13;s:831:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $  mips-unknown-elf-cpp <span style="color: #660033;">-S</span> test.c         <span style="color: #7a0874; font-weight: bold;">&#40;</span>test.s em MIPS<span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    <span style="color: #007800;">$gcc</span> <span style="color: #660033;">-S</span> test.c        <span style="color: #7a0874; font-weight: bold;">&#40;</span>test.s na arquitetura da máquina<span style="color: #7a0874; font-weight: bold;">&#41;</span>.</pre></td></tr></table><p class="theCode" style="display:none;">        $  mips-unknown-elf-cpp -S test.c         (test.s em MIPS)
    
    $gcc -S test.c        (test.s na arquitetura da máquina).</p></div>
    ;i:14;s:453:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $ <span style="color: #c20cb9; font-weight: bold;">java</span> org.ibex.nestedvm.Compiler <span style="color: #660033;">-outfile</span> Test1.class Test1 test.mips</pre></td></tr></table><p class="theCode" style="display:none;">        $ java org.ibex.nestedvm.Compiler -outfile Test1.class Test1 test.mips</p></div>
    ;i:15;s:350:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $ <span style="color: #c20cb9; font-weight: bold;">java</span> Test1
    &nbsp;
    Hello World</pre></td></tr></table><p class="theCode" style="display:none;">        $ java Test1
    
    Hello World</p></div>
    ;i:16;s:2476:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">$ <span style="color: #c20cb9; font-weight: bold;">java</span> org.ibex.nestedvm.Compiler <span style="color: #660033;">-outfile</span> Test2.class Test2 test2.mips
    &nbsp;
    $ <span style="color: #c20cb9; font-weight: bold;">java</span> Test2
    &nbsp;
    <span style="color: #000000;">100</span> <span style="color: #666666; font-style: italic;">#digite um inteiro</span>
    &nbsp;
    <span style="color: #000000;">2</span>
    &nbsp;
    <span style="color: #000000;">3</span>
    &nbsp;
    <span style="color: #000000;">5</span>
    &nbsp;
    <span style="color: #000000;">7</span>
    &nbsp;
    <span style="color: #000000;">11</span>
    &nbsp;
    <span style="color: #000000;">13</span>
    &nbsp;
    <span style="color: #000000;">17</span>
    &nbsp;
    <span style="color: #000000;">19</span>
    &nbsp;
    <span style="color: #000000;">23</span>
    &nbsp;
    <span style="color: #000000;">29</span>
    &nbsp;
    <span style="color: #000000;">31</span>
    &nbsp;
    <span style="color: #000000;">37</span>
    &nbsp;
    <span style="color: #000000;">41</span>
    &nbsp;
    <span style="color: #000000;">43</span>
    &nbsp;
    <span style="color: #000000;">47</span>
    &nbsp;
    <span style="color: #000000;">53</span>
    &nbsp;
    <span style="color: #000000;">59</span>
    &nbsp;
    <span style="color: #000000;">61</span>
    &nbsp;
    <span style="color: #000000;">67</span>
    &nbsp;
    <span style="color: #000000;">71</span>
    &nbsp;
    <span style="color: #000000;">73</span>
    &nbsp;
    <span style="color: #000000;">79</span>
    &nbsp;
    <span style="color: #000000;">83</span>
    &nbsp;
    <span style="color: #000000;">89</span>
    &nbsp;
    <span style="color: #000000;">97</span></pre></td></tr></table><p class="theCode" style="display:none;">$ java org.ibex.nestedvm.Compiler -outfile Test2.class Test2 test2.mips
    
    $ java Test2
    
    100 #digite um inteiro
    
    2
    
    3
    
    5
    
    7
    
    11
    
    13
    
    17
    
    19
    
    23
    
    29
    
    31
    
    37
    
    41
    
    43
    
    47
    
    53
    
    59
    
    61
    
    67
    
    71
    
    73
    
    79
    
    83
    
    89
    
    97</p></div>
    ;i:17;s:978:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $  <span style="color: #c20cb9; font-weight: bold;">wget</span> http:<span style="color: #000000; font-weight: bold;">//</span>www.sawp.com.br<span style="color: #000000; font-weight: bold;">/</span>nestedvm<span style="color: #000000; font-weight: bold;">/</span>redpill.c
    &nbsp;
    $ mips-unknown-elf-gcc <span style="color: #660033;">-o</span> redpill.mips redpill.c
    &nbsp;
    $ <span style="color: #c20cb9; font-weight: bold;">java</span> org.ibex.nestedvm.Compiler <span style="color: #660033;">-outfile</span> Redpill.class Redpill redpill.mips</pre></td></tr></table><p class="theCode" style="display:none;">        $  wget http://www.sawp.com.br/nestedvm/redpill.c
    
    $ mips-unknown-elf-gcc -o redpill.mips redpill.c
    
    $ java org.ibex.nestedvm.Compiler -outfile Redpill.class Redpill redpill.mips</p></div>
    ;i:18;s:306:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">        $  <span style="color: #c20cb9; font-weight: bold;">java</span> Redpill</pre></td></tr></table><p class="theCode" style="display:none;">        $  java Redpill</p></div>
    ;i:19;s:3078:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">org.ibex.nestedvm.Runtime$</span>ExecutionException: Jumped to invalid address <span style="color: #000000; font-weight: bold;">in</span> trampoline <span style="color: #7a0874; font-weight: bold;">&#40;</span>r2: <span style="color: #000000;">268435376</span> pc: <span style="color: #000000;">268435376</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> at <span style="color: #7a0874; font-weight: bold;">&#40;</span>unknown<span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at Redpill.trampoline<span style="color: #7a0874; font-weight: bold;">&#40;</span>redpill.mips<span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at Redpill._execute<span style="color: #7a0874; font-weight: bold;">&#40;</span>redpill.mips<span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at org.ibex.nestedvm.Runtime.__execute<span style="color: #7a0874; font-weight: bold;">&#40;</span>Runtime.java:<span style="color: #000000;">506</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at org.ibex.nestedvm.Runtime.execute<span style="color: #7a0874; font-weight: bold;">&#40;</span>Runtime.java:<span style="color: #000000;">523</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at org.ibex.nestedvm.Runtime.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>Runtime.java:<span style="color: #000000;">545</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at org.ibex.nestedvm.Runtime.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>Runtime.java:<span style="color: #000000;">538</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at org.ibex.nestedvm.Runtime.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>Runtime.java:<span style="color: #000000;">537</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    &nbsp;
    at Redpill.main<span style="color: #7a0874; font-weight: bold;">&#40;</span>redpill.mips<span style="color: #7a0874; font-weight: bold;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">org.ibex.nestedvm.Runtime$ExecutionException: Jumped to invalid address in trampoline (r2: 268435376 pc: 268435376) at (unknown)
    
    at Redpill.trampoline(redpill.mips)
    
    at Redpill._execute(redpill.mips)
    
    at org.ibex.nestedvm.Runtime.__execute(Runtime.java:506)
    
    at org.ibex.nestedvm.Runtime.execute(Runtime.java:523)
    
    at org.ibex.nestedvm.Runtime.run(Runtime.java:545)
    
    at org.ibex.nestedvm.Runtime.run(Runtime.java:538)
    
    at org.ibex.nestedvm.Runtime.run(Runtime.java:537)
    
    at Redpill.main(redpill.mips)</p></div>
    ";}
categories:
  - Virtualization
tags:
  - cross-compiler
  - java
  - nestedvm
  - Virtualization
---
## 1. Introdução

Linguagens de alto nível como FORTRAN, C, C++ e Pascal foram inicialmente desenvolvidas para terem certa portabilidade e serem independentes de arquiteturas. Contudo, são dependentes de compilação, ou seja, o mesmo sistema precisa ser recompilado várias vezes, para cada arquitetura.

Por outro lado, linguagens como JAVA e C# foram construídas para permitirem que os programas escritos nestas tecnologias possam correr em qualquer arquitetura e sistema operacional com a mesma compilação.

O que permite esta independência de plataforma é o código objeto em &#8220;bytecodes&#8221;.

Ao invés de compilar para instruções de máquina o programa executará em uma Máquina Virtual. Assim, o programador se preocupa com a compatibilidade entre seu programa e a MV – enquanto a MV interpreta as instruções na máquina.

Desta forma, além de aprimorar a portabilidade do programa, permite a construção de um código mais seguro, pois não permite execução de instruções inválidas, nem acesso à regiões arbitrárias de memória.

Linguagens consideradas seguras como JAVA são relativamente novas, comparadas com o tempo de vida das linguagens compiladas, como o C. Sendo assim, existe no mercado vasto número de bibliotecas e programas escritos nessas linguagens.

Por isso, podemos nos deparar com a necessidade de utilizar um código escrito em C num sistema em desenvolvimento na linguagem JAVA.

Logo, há uma grande motivação para a conversão de programas e bibliotecas em C para JAVA.

Como exemplo pensar nos inúmeros aplicativos escritos para *NIX que poderiam ser facilmente portados para Windows, e vice-versa, sem a necessidade de diferentes compilações.

Veremos aqui sobre a NestedVM, montador que converte o Assembly MIPS para o bytecode JAVA.

Discutiremos também o processo de “cross-compilation”. Pois precisaremos compilar um código em C++ para um executável da arquitetura MIPS. Será o objeto desta compilação que converteremos para um .class JAVA.

Comentaremos também sobre alguns métodos alternativos e mais populares para integração de sistemas já prontos com o JAVA, como o JNI, Jazillian, c2j etc. E porquê esses sistemas ficam aquém à NestedVm.

&nbsp;

## 2. JAVA Native Interface: JNI

A JNI é uma &#8220;ponte&#8221; entre uma Java Virtual Machine (JVM) e o código compilado em uma linguagem dependente de plataforma, chamado de &#8220;código nativo&#8221;.

A JNI permite que aplicativos escritos em JAVA interajam com código nativo. Isso resolve, em parte, o problema de reutilização de software, pois permite que bibliotecas já escritas em uma linguagem &#8220;conversem&#8221; com o programa JAVA.

Contudo, isso acaba com a portabilidade do JAVA, pois as bibliotecas de código nativo continuaram dependentes da plataforma para qual foram compiladas.

O uso de JNI também não resolve o problema de segurança. A JVM não terá controle sobre o código nativo, permitindo assim a execução das instruções herdadas, inseguras e suscetíveis (como buffer overflow e heaps corruptions).

O reaproveitamento de software também não é total pois alguns ambientes JAVA (Applets e Servlets) não são compatíveis com JNI.

Normalmente JNI são utilizadas para aproveitar alguns drivers que não são acessíveis pela JVM.

Saiba mais:

<a href="http://en.wikipedia.org/wiki/Java_Native_Interface" target="_blank">http://en.wikipedia.org/wiki/Java_Native_Interface</a>

<a href="http://java.sun.com/developer/onlineTraining/Programming/JDCBook/jni.html" target="_blank">http://java.sun.com/developer/onlineTraining/Programming/JDCBook/jni.html</a>

<a href="http://java.sun.com/docs/books/jni/html/intro.html#1811" target="_blank">http://java.sun.com/docs/books/jni/html/intro.html#1811</a>

<a href="http://today.java.net/pub/a/today/2006/10/19/invoking-assembly-language-from-java.html" target="_blank">http://today.java.net/pub/a/today/2006/10/19/invoking-assembly-language-from-java.html</a>

<a href="http://ringlord.com/publications/jni-howto/" target="_blank">http://ringlord.com/publications/jni-howto/</a>

&nbsp;

## 3. Soluções Portáveis

Considere o diagrama abaixo: 

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-244" title="p3f1" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f1.jpg" alt="p3f1" width="400" height="200" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f1.jpg 400w, http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f1-300x150.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

<p style="text-align: center;">
  <p>
    Observe os 4 objetos: 2 são códigos-fontes e 2 são códigos-objetos. Os destacados de vermelho são os diferentes compiladores, responsáveis em transformar códigos-fontes em códigos de máquina.
  </p>
  
  <p>
    O que estamos querendo encontrar aqui é o caminho que saia do código .c e gere um .class, compatível com as JVM.
  </p>
  
  <h3>
    3.1. Tradução Fonte-para-Fonte (Source-to-Source)
  </h3>
  
  <p>
    Baseado no diagrama da Figura 01, este método realiza as conversões representadas abaixo:
  </p>
  
  <p style="text-align: center;">
    <p style="text-align: center;">
      <img class="aligncenter size-full wp-image-245" title="p3f2" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f2.jpg" alt="p3f2" width="400" height="200" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f2.jpg 400w, http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f2-300x150.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />
    </p>
    
    <p>
      As ferramentas que utilizam esta técnica de tradução são ainda divididas em: tradução parcial (que converte somente partes de código seguras, mas precisam ser completadas pelo programador) e as que fazem a tradução total (e geram erros e conflitos ). Segue abaixo o comentário de algumas soluções.
    </p>
    
    <p>
      <strong>Jazillian</strong> é uma ferramenta de tradução parcial que produz código JAVA altamente legível a partir de um fonte C.
    </p>
    
    <p>
      Contudo, traduz somente uma parte da linguagem C e é utilizado principalmente pela sua inteligência na análise sintática do código para evitar conflitos.
    </p>
    
    <p>
      Uma vantagem é que ao invés de converter apenas de linguagem para linguagem, converte para algumas APIs do JAVA. Por exemplo, na tradução de arrays de char, do C legado, converte para classe String, do JAVA. &#8220;char string1[] = strcpy(string2); &#8221; vira &#8220;String string1 = string2;&#8221;
    </p>
    
    <p>
      Infelizmente, Jazillian não produz toda conversão de código e costuma gerar erros quando converte bibliotecas que possuem código ASM embutido, como as de IO.
    </p>
    
    <p>
      É boa para se ter &#8220;um norte&#8221; quando estiver reprogramando alguma biblioteca de C para o JAVA.
    </p>
    
    <p>
      Uma segunda ferramenta de conversão parcial de código, semelhante ao Jazillian, é o <strong>Mocha-JAVA</strong>. Ela trabalha da mesma forma que o Jazillian, contudo, converte C++ em JAVA.
    </p>
    
    <p>
      Outras ferramentas, tais como, o <strong>c2j</strong>, <strong>c2j++</strong>, <strong>Cappuccino</strong> e <strong>Ephedra</strong>, permitem uma tradução completa de código C/C++ para JAVA. Cada uma das quatro mencionadas acima suportam uma grande parte de código convertida, contudo, costumam gerar alguns erros de E/S.
    </p>
    
    <p>
      Porém, a conversão de código-para-código não são satisfatórias devido ao fato de haver diferentes recursos entre o C/C++ e o JAVA.
    </p>
    
    <p>
      O erro mais comum encontrado na transcrição de código é relacionado às operações de entrada e saída. Muitas bibliotecas do C são dependentes de plataforma, pois possuem código _asm embutido.
    </p>
    
    <p>
      Outro fator de incompatibilidade se dá por que o JAVA não têm recursos &#8211; no nível da linguagem &#8211; que permitem aritmética de ponteiros (inclusive pelo projeto da linguagem).
    </p>
    
    <p>
      Associado à isso, o C/C++ também encontra recursos como structs, unions, casting de tipos dinâmicos, classes amigas, interfaces (que difere do conceito de interface do java), e outros elementos de código que não estão presentes na linguagem JAVA.
    </p>
    
    <p>
      Logo, pode-se dizer que a forma menos eficiente de se portar um código para java é com a transcrição código para código.
    </p>
    
    <h3>
      3.2 Tradução Fonte-para-Bytecode ( source &#8211; to &#8211; bytecode )
    </h3>
    
    <p>
      Este caso envolve o processo direto de compilação de uma linguagem para um bytecode.
    </p>
    
    <p style="text-align: center;">
      <p style="text-align: center;">
        <img class="aligncenter size-full wp-image-246" title="p3f3" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f3.jpg" alt="p3f3" width="400" height="200" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f3.jpg 400w, http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f3-300x150.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />
      </p>
      
      <p>
        Há uma versão experimental do gcc, atualmente conhecido como egcs-jvm, que tenta converter o código C para bytecode ao invés de instruções de máquina.
      </p>
      
      <p>
        Existe também um compilador conhecido como lcc-java.
      </p>
      
      <p>
        Em ambos compiladores há um sério problema de compatibilidade, pois ainda não resolveram totalmente os problemas com as aritméticas e manipulações de ponteiros.
      </p>
      
      <p>
        Outro grande problema se dá devido ao modelo de gerência de memória empregado por estes compiladores. A gerencia de memória deveria ficar toda para a JVM, e não para o ambiente, levando a existência de conflitos quando o programa necessitar acessar algumas regiões da memória.
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <h2>
        4. NestedVM
      </h2>
      
      <p>
        Diferente dos métodos mencionados até aqui, a NestedVM não converte diretamente um código de alto nível (C ou C++) em um outro código na linguagem JAVA e também não compila este código para bytecode.
      </p>
      
      <p>
        Na verdade, a abordagem escolhida consiste em traduzir um arquivo compilado em um bytecode.
      </p>
      
      <p>
        O processo de conversão do NestedVM é realmente interessante: utilizamos um compilador a parte para converter o código C para ASM MIPS. Em seguida utilizamos o NestedVM para interpretar este assembly e transformar em bytecode.
      </p>
      
      <p>
        Entretanto, ainda há a opção do NestedVm realizar uma decompilação, transformando o código assembly em um código-fonte JAVA. Chamamos este processo de binary-to-source.
      </p>
      
      <p>
        A forma de trabalho do NestedVM traz uma série de vantagens. A primeira delas é que a NestedVM não irá precisar se preocupar com os processos de compilação, deixando este trabalho a cargo do compilador.
      </p>
      
      <p>
        Como o NestedVM trabalha com o código assembly, é possível converter em JAVA o código escrito em qualquer linguagem (e não só em C, embora seja a linguagem que mais estamos mencionando aqui). Basta que o compilador possa traduzir a linguagem em ASM MIPS.
      </p>
      
      <p>
        Ou seja, o mesmo compilador que gera o código nativo, é o que gera o assembly utilizado pelo NestedVm. Assim, Makefiles, cabeçalhos, estruturas complexas, fica tudo compatível.
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <h3>
        4.1 Por quê MIPS?
      </h3>
      
      <p>
        Segundo os criadores do NestedVM, a escolha pelo MIPS se dá por 3 motivos:
      </p>
      
      <p>
        1. MIPS é uma arquitetura muito conhecida no meio da ciência da computação. Foi uma das primeiras arquiteturas RISC e muitas outras arquiteturas se basearam em seus conceitos. Sendo assim, há uma quantidade muito grande de ferramentas e compiladores para MIPS.
      </p>
      
      <p>
        2. O MIPS ISA é muito mais simples que o x86.
      </p>
      
      <p>
        3. A criadora do JAVA, Sun Microsystems, possui uma tecnologia de processadores baseada no MIPS: o SPARC. Provavelmente por isso a ISA (Instruction Set Architeture) da JVM seja parecida com do conjunto de instruções do SPARC. E, portanto, tão semelhante com a ISA MIPS.
      </p>
      
      <p>
        A “GNU Compile Colection” (GCC) é capaz de compilar C, C++, JAVA, FORTRAN, Objective C e Pascal para a arquitetura MIPS. Portanto, é possível converter qualquer programa escrito nessas linguagens para JAVA.
      </p>
      
      <p>
        Outra grande vantagem do MIPS é que, assim como o JAVA, ele possui a maioria das instruções com o tamanho fixo de 32 bits. Sendo assim, tanto o MIPS quanto o JAVA conseguem endereçar a mesma quantidade de memória.
      </p>
      
      <p>
        Isso supera os problemas mencionados nos casos de compilação direta para o bytecode JAVA.
      </p>
      
      <p>
        O NestedVM pode representar a memória como um array int[ ][ ] no JAVA. Ele indexa por pagina os primeiro n bits como sendo de endereço e os bits restantes como sendo os valores.
      </p>
      
      <p>
        Logo, quebrando a memória em páginas, torna-se possível alocar dinamicamente espaço na memória da JVM, permitindo uma compatibilidade com comandos new, delete, malloc e free do C/C++ &#8211; funções problemáticas para os outros meios de conversão que comentamos.
      </p>
      
      <p>
        Veja uma instrução de acesso à memória MIPS convertida em JAVA:
      </p>
      
      <p>
        MIPS:
      </p>
      
      <pre lang="asm">// lw v0, 20(sp) ; # carreg uma palavra de 4 bytes em sp+20, sp(stack pointer)</pre>
      
      <p>
        JAVA:
      </p>
      
      <pre lang="java">v0 = memory[(sp+20)>>>16][(sp+20)0xffff];</pre>
      
      <p>
        Além do tamanho das instruções de manipulação de memória, o tamanho das instruções aritméticas também são semelhantes. O MIPS r2000 permite instruções de multiplicar e dividir como sendo de única ou dupla precisão de unidade de ponto flutuante. Esse conjunto de instruções também é encontrado na JVM. Ou seja, a maioria das instruções MIPS é semelhante às instruções do bytecode.
      </p>
      
      <h3>
        4.2 Binary &#8211; to &#8211; Source
      </h3>
      
      <p>
        O primeiro modo operacional do NestedVM é a tradução binary-to-source. Deste modo, NVM traduz o binário MIPS em um código fonte JAVA e só então compila em um bytecode.
      </p>
      
      <p>
        Veja o esquema abaixo:
      </p>
      
      <p style="text-align: center;">
        <a class="thickbox" href="http://www.sawp.com.br/blog/wp-content/uploads/post3_nestedvm/p3f4.jpg"><img class="aligncenter size-full wp-image-247" title="p3f4" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f4.jpg" alt="p3f4" width="400" height="200" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f4.jpg 400w, http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f4-300x150.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" /><br /> </a>
      </p>
      
      <p>
        O processo de tradução segue 4 etapas: 1 &#8211; código fonte C é compilado e feito todo processo de linkagem. 2 &#8211; NestedVM é usado para emitir o arquivo .java (fonte JAVA). 3 &#8211; O arquivo resultante .java é compilado em um bytecode .class via javac. 4 &#8211; em tempo de execução a JVM invoca o método run() na geração da classe, isso irá equivaler à entrada da função main() do C.
      </p>
      
      <h3>
        4.3 Binary &#8211; to &#8211; Binary
      </h3>
    </p>
    
    <p style="text-align: center;">
      <p style="text-align: center;">
        <img class="aligncenter size-full wp-image-248" title="p3f5" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f5.jpg" alt="p3f5" width="400" height="200" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f5.jpg 400w, http://www.sawp.com.br/blog/wp-content/uploads/2008/08/p3f5-300x150.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />
      </p>
      
      <p>
        Este modo é mais recomendado e possui algumas vantagens.
      </p>
      
      <p>
        Gerando o bytecode diretamente do MIPS há chance de gerar código que não seria compatível se transformássemos em um source .java. Algumas operações com ponteiros, permissão de acesso e operações específicas da linguagem inicial poderiam não ter estruturas no fonte .java.
      </p>
      
      <p>
        Gerando .class diretamente eliminamos o tempo de compilação do javac .
      </p>
      
      <p>
        Compilação direta para arquivos .class permitem tradução dos binários MIPS com o carregamento via ClassLoader.fromBytes() , eliminando a necessidade de compilar um programa que carrega todos seus módulos de uma vez na memoria.
      </p>
      
      <h3>
        4.4 Chamadas ao sistema &#8211; syscalls
      </h3>
      
      <p>
        Sabemos que um programa, quando compilado, além de dependente de arquitetura se torna dependente de sistema operacional.
      </p>
      
      <p>
        Isso acontece por que o sistema operacional deveria ser o responsável pelo gerenciamento dos dispositivos de hardware e nosso programa deve interagir com o SO para solicitar os recursos de entrada e saída.
      </p>
      
      <p>
        Em um nível mais baixo, a comunicação entre aplicativo e SO é feita através de códigos associados à instrução MIPS chamada syscall.
      </p>
      
      <p>
        Funciona assim: o programa envia um valor relacionado à um recurso do sistema operacional. O controle do programa naquele ponto é transferido para o Kernel do SO. Então, o kernel verifica se o código equivale á uma operação válida e decide o que fazer. Feita a operação, retorna a execução do programa.
      </p>
      
      <p>
        Um exemplo com um &#8220;Hello World&#8221; em ASM MIPS:
      </p>
      
      <pre lang="asm">string: .asciiz "Hello World \n"        ; # string é um label
        li        $v0, 4                                ; # código da chamada do sistema
        la        $a0, string                        ; # carrega e coloca em $a0
        syscall                                        ; # faz a chamada de sistema
        # REFERENCIA DO SYSTEMCALL
        # http://www.doc.ic.ac.uk/lab/secondyear/spim/node8.html
</pre>
      
      <p>
        É importante discutir sobre esta comunicação pois o NestedVM têm ainda que converter chamadas do sistema em chamadas para a JVM.
      </p>
      
      <h3>
        4.5 NestedVM Runtime
      </h3>
      
      <p>
        Na hora da tradução o NestedVM embute um código que simula as syscalls nas comunicações com o aplicativo. Ele trabalha como o kernel real, mantendo as informações de estados por processos: tabela descritora de arquivos, caching, diretório atual, etc.
      </p>
      
      <p>
        A responsável por controlar as solicitações de recursos e atuar como o SO é uma classe chamada Runtime, que faz parte do NestedVM. Para cada interação via syscall temos uma nova instância da Runtime.
      </p>
      
      <p>
        Por exemplo, uma instrução syscall, do java, mapeada como uma método chamado syscall:
      </p>
      
      <pre lang="asm">v0 = syscall(v0,a0,a1,a2,a3); // syscall</pre>
      
      <p>
        Exemplo: Implementando em JAVA a chamada syscall
      </p>
      
      <pre lang="java">/* Aqui o método syscall() executa uma operação baseada no 
                número-código de referencia */

        int syscall(int sc, int a, int b, int c, int d) {
          switch(sc) {
                  case SYS_write: return sys_write(a,b,c,d);
                  case SYS_open: return sys_open(a,b,c,d);
                  ....
          }
        }
</pre>
      
      <p>
        Há duas implementações do NVM Runtime, uma simples com suporte mínimo de instruções requeridas para compilar código ANSI C e outra mais sofisticada, que emula grande parte das systemcalls da implementação POSIX.
      </p>
      
      <h4>
        4.5.1 ANSI C Runtime
      </h4>
      
      <p>
        O ANSI C Runtime oferece operações tipicas de entrada e saída tais como, open(), read(), write(), close() e seek().
      </p>
      
      <p>
        Os descritores de arquivos são implementados da mesma forma como são nos kernels dos SO.
      </p>
      
      <p>
        A tabela de arquivos é mantida e os descritores agem como índices desta tabela.
      </p>
      
      <p>
        Cada descritor de arquivo é representado como uma classe Java RandomAccessFile .
      </p>
      
      <p>
        O gerenciamento de memória no nível de processos é feito através da syscall sbrk() que extende o heap do processo adicionando mais páginas à tabela de memória.
      </p>
      
      <p>
        Operações de cópia e liberação de memória pode ser feita com os métodos memset() e memcpy(), que invocam os métodos System.arraycopy() do Java.
      </p>
      
      <p>
        A chamada exit() realiza a saída do processo e libera o controle para a JVM.
      </p>
      
      <h4>
        4.5.2 POSIX Runtime
      </h4>
      
      <p>
        POSIX (Portable Operating System Interface), como o próprio nome sugere, é um conjunto de normas (padrão IEEE 1003) criada para manter a portabilidade entre sistemas diferentes que implementam esta mesma norma.
      </p>
      
      <p>
        É usada pela NestedVM para garantir a portabilidade entre as máquinas virtuais do sistema traduzido.
      </p>
      
      <p>
        A implementação POSIX estende a ANSI C nos modelos de E/S – incluindo um sistema de arquivos e nós de dispositivos – tratando dispositivos como arquivos com interface de programação idênticas.
      </p>
      
      <p>
        O uso de uma classe que simula a implementação POSIX como interface de acesso à JVM permite um isolamento da camada de tratamento de dispositivos pelo JAVA.
      </p>
      
      <p>
        Para o acesso cada sistema de arquivos é implementado em uma classe Java, que poderia, por exemplo, acessar um host do sistema e executar operações tais como: state(), lstat(), mkdir(), unlink(), o conteúdo de um arquivo compactado ou até mesmo a resposta de um servidor externo.
      </p>
      
      <p>
        A chamada fork() é implementada no Java pelo uso de um método clone() ( herdado da classe Object ). Uma nova instancia é adicionado à tabela de processos para facilitar a comunicação entre eles.
      </p>
      
      <p>
        O metodo exec(), que carrega o binário MIPS do sistema de arquivos, se valida da classe Class.loadBytes() para a conversão MIPS  to  bytecode .
      </p>
      
      <p>
        A API waitpid() permite, que um processo pai bloqueie a execução de um processo filho, é modelado pelo uso do processo wait() do JAVA.
      </p>
      
      <p>
        Já a chamada de sistema pipe(), que permite a comunicação entre processos pai e filho, é emulada todo controle de escalonamento e deadlock dentro da JVM, exatamente como nos sistemas UNIX.
      </p>
      
      <p>
        O suporte à rede também é tratado com socket. É provido pelos métodos opensocket(), close(), listensocket() e accept().
      </p>
      
      <p>
        Assim, todo o sistema fica isolado do mundo externo pelas syscalls emuladas pelas implementações do Java.
      </p>
      
      <h2>
        5. Cross-Compile
      </h2>
      
      <p>
        Segundo a Wikipédia: &#8220;Um cross compile é a capacidade de um compilador de criar códigos executáveis para uma plataforma diferente da plataforma em que se está sendo compilada.
      </p>
      
      <p>
        &#8220;Geralmente são usadas para gerar executáveis para sistemas embutidos ou multi-plataformas&#8221;.
      </p>
      
      <p>
        Veja mais em: <a href="http://en.wikipedia.org/wiki/Cross_compile" target="_blank">http://en.wikipedia.org/wiki/Cross_compile</a>
      </p>
      
      <h3>
        5.1 Cross-compile e NestedVM
      </h3>
      
      <p>
        Como o NestedVM utiliza o código asm MIPS, utilizamos uma &#8220;cross compilation&#8221; para transformar o código da linguagem inicial (C, FORTRAN, Pascal) em um código compilado ASM.
      </p>
      
      <p>
        Para isso, utilizamos a &#8220;NewLib&#8221; ( <a href="http://sourceware.org/newlib/" target="_blank">http://sourceware.org/newlib/</a> ), biblioteca escrita em C mantida pela Red Hat e usada para compilar fontes para sistemas embutidos.
      </p>
      
      <p>
        Quando compilamos o NestedVM fornecido pelo autor ( <a href="http://nestedvm.ibex.org/" target="_blank">http://nestedvm.ibex.org/</a> ), o arquivo Makefile faz o download de todas as dependências necessárias. Contudo, há alguns arquivos que estão com os links quebrados. O que pode acarretar em uma falha ao compilar.
      </p>
      
      <p>
        Contudo, há uma versão alternativa do Make, que calcula as dependências e baixa os arquivos necessários. Para conseguir a versão do nosso site faça o download do arquivo em <a href="http://www.sawp.com.br/nestedvm/nestedvm-2008-08-06.tar.gz" target="_blank">http://www.sawp.com.br/nestedvm/nestedvm-2008-08-06.tar.gz</a> .
      </p>
      
      <h2>
        6. Instalando NestedVM
      </h2>
      
      <p>
        O tutorial aqui é utilizando o fonte do nosso site [ <a href="http://www.sawp.com.br" target="_blank">http://www.sawp.com.br</a> ], que possui as correções de dependência, além de possuir todos os pré-requisitos para compilação no próprio site.
      </p>
      
      <h3>
        6.1 instalando no UNIX
      </h3>
      
      <p>
        Abra um shell e digite os passos abaixo:
      </p>
      
      <pre lang="bash">$ cd ~

$  wget http://www.sawp.com.br/nestedvm/nestedvm-2008-08-06.tar.gz</pre>
      
      <p>
        Após o download do arquivo, descompacte o tarball:
      </p>
      
      <pre lang="bash">        $ tar -xfz nestedvm-2008-08-06.tar.gz

        $ cd nestedvm-2008-08-06

        $ make
</pre>
      
      <p>
        Provavelmente irá compilar com sucesso. Após a compilação, você pode verificar a instalação:
      </p>
      
      <pre lang="bash">        $ make test</pre>
      
      <p>
        Se o NestedVM for compilado com sucesso, algo como o resultado abaixo deve aparecer:
      </p>
      
      <pre lang="bash">
        Constructor!

        Entered main()

        16777215

        16777215

        16777215

        16777215

        argv[0] = "tests.Test"

        argv[1] = "arg 1"

        argv[2] = "arg 2"

        argv[3] = "arg 3"

        getenv("USER") = "(null)"

        getenv("HOME") = "(null)"

        getenv("TZ") = "(null)"

        GMT GMT 0

        Running ctime

        ctime returned: 0x2b958

        Current time: Wed Aug  6 14:39:37 2008

        Trying to open /nonexistent

        open: No such file or directory

        Tyring to mkdir .mkdirtest

        Attempted to use a UnixRuntime syscall in Runtime (18)

        mkdir: Function not implemented

        Trying to opendir .

        opendir: No such file or directory

        1.574000e+00

        -4.315000e+01l

        -43

        -4.315000e+01

        4.315000e+01

        Hello, World

        7F

        fabs(-2.24) = 2.34

        Destructor!</pre>
      
      <p>
        Se você chegou neste ponto, provavelmente já está com as ferramentas necessárias instaladas para compilar binários em MIPS (gcc, red hat newlib e binutils).
      </p>
      
      <p>
        Caso haja algum problema durante a compilação, por favor, relatar via e-mail: <a href="mailto:sawp@sawp.com.br" target="_blank">sawp@sawp.com.br</a>
      </p>
      
      <h3>
        6.2 Compilando de C para MIPS
      </h3>
      
      <p>
        Agora, adicione o ambiente de cross-compilation à variavel de CLASSPATH:
      </p>
      
      <pre lang="bash">        $ make env.sh

        $ source env.sh</pre>
      
      <p>
        Feito esses passos, agora iremos demonstrar os passos e como proceder para compilar um código .c, .cpp, .pas ou .f para um .class java.
      </p>
      
      <p>
        Para isso, faça o download de 2 arquivos de teste no nosso site:
      </p>
      
      <pre lang="bash">        $ wget http://www.sawp.com.br/nestedvm/test.c

        $ wget http://www.sawp.com.br/nestedvm/test2.c</pre>
      
      <p>
        Agora, iremos compilar os arquivos em um binário MIPS:
      </p>
      
      <pre lang="bash">        $  mips-unknown-elf-cpp -o test.mips test.c

        $  mips-unknown-elf-cpp -o test2.mips test2.c</pre>
      
      <p>
        Pronto! Acabamos de compilar em código objeto MIPS.
      </p>
      
      <p>
        Para visualizar a diferença entre o assembly da sua máquina e o assembly MIPS, execute:
      </p>
      
      <pre lang="bash">        $  mips-unknown-elf-cpp -S test.c         (test.s em MIPS)

        $gcc -S test.c        (test.s na arquitetura da máquina).</pre>
      
      <h3>
        6.3 Convertendo de MIPS para bytecode JAVA
      </h3>
      
      <p>
        Até aqui temos um código objeto que executaria perfeitamente em uma arquitetura MIPS. Agora, para converter para JAVA execute:
      </p>
      
      <pre lang="bash">        $ java org.ibex.nestedvm.Compiler -outfile Test1.class Test1 test.mips</pre>
      
      <p>
        Se tudo correr bem, nada aparecerá. Para testar, digite:
      </p>
      
      <pre lang="bash">
        $ java Test1

        Hello World</pre>
      
      <p>
        O segundo exemplo, testa a entrada de dados. Para isso, digite um valor de entrada para o programa:
      </p>
      
      <pre lang="bash">$ java org.ibex.nestedvm.Compiler -outfile Test2.class Test2 test2.mips

        $ java Test2

        100 #digite um inteiro

        2 

        3 

        5 

        7 

        11

        13 

        17 

        19 

        23 

        29 

        31 

        37 

        41 

        43 

        47 

        53 

        59 

        61 

        67 

        71 

        73 

        79 

        83 

        89 

        97</pre>
      
      <p>
        Se tudo estiver ok, o programa mostrará todos primos de 2 até o valor de entrada.
      </p>
      
      <h3>
        6.4 Observações
      </h3>
      
      <p>
        Tentaremos, agora, compilar o Código da Pílula Vermelha:
      </p>
      
      <pre lang="bash">        $  wget http://www.sawp.com.br/nestedvm/redpill.c

        $ mips-unknown-elf-gcc -o redpill.mips redpill.c

        $ java org.ibex.nestedvm.Compiler -outfile Redpill.class Redpill redpill.mips</pre>
      
      <p>
        Se o NestedVM estiver instalado corretamente na máquina, tudo dará certo até aqui. Contudo, quando executarmos o executável Java:
      </p>
      
      <pre lang="bash">        $  java Redpill</pre>
      
      <p>
        Provavelmente teremos o erro:
      </p>
      
      <pre lang="bash">org.ibex.nestedvm.Runtime$ExecutionException: Jumped to invalid address in trampoline (r2: 268435376 pc: 268435376) at (unknown)

                at Redpill.trampoline(redpill.mips)

                at Redpill._execute(redpill.mips)

                at org.ibex.nestedvm.Runtime.__execute(Runtime.java:506)

                at org.ibex.nestedvm.Runtime.execute(Runtime.java:523)

                at org.ibex.nestedvm.Runtime.run(Runtime.java:545)

                at org.ibex.nestedvm.Runtime.run(Runtime.java:538)

                at org.ibex.nestedvm.Runtime.run(Runtime.java:537)

                at Redpill.main(redpill.mips)</pre>
      
      <p>
        Isso ocorre porque o código C continha instruções assembly de outra arquitetura embutidas. Note que a operação de desvio não foi reconhecida, por isso não pode ser emulada.
      </p>
      
      <p>
        Para o NestedVM funcionar corretamente é preciso que o código seja escrito de forma mais portável possível, sem utilizar instruções ou recursos dependentes de plataforma.
      </p>
      
      <p>
        Operações bit-a-bit, como shift left (<<), embutir blocos _asm{} e códigos de baixo nível inviabilizam o uso do NestedVM, pois inserem no código objeto instruções "não-MIPS". Sendo assim, é importante possui o código original mais independente possível de arquitetura, referenciando-se somente na linguagem.
      </p>
