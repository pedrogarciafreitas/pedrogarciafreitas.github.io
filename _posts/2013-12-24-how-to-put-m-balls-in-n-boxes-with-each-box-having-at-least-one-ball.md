---
id: 2071
title: How to put m balls in n boxes with each box having at least one ball
date: 2013-12-24T09:46:26+00:00
author: SAWP
excerpt: 'If you have m balls and n boxes, with n<m, and you insert the balls into the boxes randomly, what is the probability that all the boxes have at least one ball in it?'
layout: post
guid: http://www.sawp.com.br/blog/?p=2071
permalink: p=2071
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:2396:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="haskell" style="font-family:monospace;">fact <span style="color: red;">0</span> <span style="color: #339933; font-weight: bold;">=</span> <span style="color: red;">1</span>
    fact <span style="color: red;">1</span> <span style="color: #339933; font-weight: bold;">=</span> <span style="color: red;">1</span>
    fact x <span style="color: #339933; font-weight: bold;">=</span> x <span style="color: #339933; font-weight: bold;">*</span> fact <span style="color: green;">&#40;</span>x <span style="color: #339933; font-weight: bold;">-</span> <span style="color: red;">1</span><span style="color: green;">&#41;</span>
    &nbsp;
    &nbsp;
    balls m <span style="color: red;">1</span> <span style="color: #339933; font-weight: bold;">=</span> <span style="color: red;">1</span>
    balls m n <span style="color: #339933; font-weight: bold;">|</span> m <span style="color: #339933; font-weight: bold;">&lt;</span> n <span style="color: #339933; font-weight: bold;">=</span> <span style="color: red;">0</span>
    balls m n <span style="color: #339933; font-weight: bold;">|</span> m <span style="color: #339933; font-weight: bold;">==</span> n <span style="color: #339933; font-weight: bold;">=</span> fact<span style="color: green;">&#40;</span>n<span style="color: green;">&#41;</span>
    balls m n <span style="color: #339933; font-weight: bold;">=</span> n <span style="color: #339933; font-weight: bold;">*</span> balls <span style="color: green;">&#40;</span>m <span style="color: #339933; font-weight: bold;">-</span><span style="color: red;">1</span><span style="color: green;">&#41;</span> n <span style="color: #339933; font-weight: bold;">+</span> n <span style="color: #339933; font-weight: bold;">*</span> balls <span style="color: green;">&#40;</span>m <span style="color: #339933; font-weight: bold;">-</span> <span style="color: red;">1</span><span style="color: green;">&#41;</span> <span style="color: green;">&#40;</span>n <span style="color: #339933; font-weight: bold;">-</span> <span style="color: red;">1</span><span style="color: green;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">fact 0 = 1
    fact 1 = 1
    fact x = x * fact (x - 1)
    
    
    balls m 1 = 1
    balls m n | m &lt; n = 0
    balls m n | m == n = fact(n)
    balls m n = n * balls (m -1) n + n * balls (m - 1) (n - 1)</p></div>
    ;i:2;s:985:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">$ ghci
    GHCi, version 7.6.3: http:<span style="color: #000000; font-weight: bold;">//</span>www.haskell.org<span style="color: #000000; font-weight: bold;">/</span>ghc<span style="color: #000000; font-weight: bold;">/</span>  :? <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #7a0874; font-weight: bold;">help</span>
    Loading package ghc-prim ... linking ... done.
    Loading package integer-gmp ... linking ... done.
    Loading package base ... linking ... done.
    Prelude<span style="color: #000000; font-weight: bold;">&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">$ ghci
    GHCi, version 7.6.3: http://www.haskell.org/ghc/  :? for help
    Loading package ghc-prim ... linking ... done.
    Loading package integer-gmp ... linking ... done.
    Loading package base ... linking ... done.
    Prelude&gt;</p></div>
    ;i:3;s:3273:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="haskell" style="font-family:monospace;">Prelude<span style="color: #339933; font-weight: bold;">&gt;</span> <span style="color: #339933; font-weight: bold;">:</span>l balls.hs
    <span style="color: green;">&#91;</span><span style="color: red;">1</span> <span style="color: #06c; font-weight: bold;">of</span> <span style="color: red;">1</span><span style="color: green;">&#93;</span> Compiling Main             <span style="color: green;">&#40;</span> balls.hs, interpreted <span style="color: green;">&#41;</span>
    Ok, modules loaded<span style="color: #339933; font-weight: bold;">:</span> Main.
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">12</span> <span style="color: red;">3</span>
    <span style="color: red;">519156</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">50</span> <span style="color: red;">2</span>
    <span style="color: red;">1125899906842622</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">2</span> <span style="color: red;">2</span>
    <span style="color: red;">2</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">3</span> <span style="color: red;">2</span>
    <span style="color: red;">6</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">4</span> <span style="color: red;">5</span>
    <span style="color: red;">0</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">5</span> <span style="color: red;">10</span>
    <span style="color: red;">0</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">10</span> <span style="color: red;">5</span>
    <span style="color: red;">5103000</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">10</span> <span style="color: red;">2</span>
    <span style="color: red;">1022</span>
    <span style="color: #339933; font-weight: bold;">*</span>Main<span style="color: #339933; font-weight: bold;">&gt;</span> balls <span style="color: red;">10</span> <span style="color: red;">9</span>
    <span style="color: red;">16329600</span></pre></td></tr></table><p class="theCode" style="display:none;">Prelude&gt; :l balls.hs
    [1 of 1] Compiling Main             ( balls.hs, interpreted )
    Ok, modules loaded: Main.
    *Main&gt; balls 12 3
    519156
    *Main&gt; balls 50 2
    1125899906842622
    *Main&gt; balls 2 2
    2
    *Main&gt; balls 3 2
    6
    *Main&gt; balls 4 5
    0
    *Main&gt; balls 5 10
    0
    *Main&gt; balls 10 5
    5103000
    *Main&gt; balls 10 2
    1022
    *Main&gt; balls 10 9
    16329600</p></div>
    ";}
categories:
  - Miscellaneous
---
The calculation for the number of ways of putting $m$ balls in $n$ boxes with each box having at **least one ball** in Haskell:

<pre lang="haskell">fact 0 = 1
fact 1 = 1
fact x = x * fact (x - 1)


balls m 1 = 1
balls m n | m &lt; n = 0
balls m n | m == n = fact(n)
balls m n = n * balls (m -1) n + n * balls (m - 1) (n - 1)</pre>

Testing:

<pre lang="bash">$ ghci
GHCi, version 7.6.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Prelude> </pre>

<pre lang="haskell">Prelude> :l balls.hs 
[1 of 1] Compiling Main             ( balls.hs, interpreted )
Ok, modules loaded: Main.
*Main> balls 12 3
519156
*Main> balls 50 2
1125899906842622
*Main> balls 2 2
2
*Main> balls 3 2
6
*Main> balls 4 5
0
*Main> balls 5 10
0
*Main> balls 10 5
5103000
*Main> balls 10 2
1022
*Main> balls 10 9
16329600
</pre>
