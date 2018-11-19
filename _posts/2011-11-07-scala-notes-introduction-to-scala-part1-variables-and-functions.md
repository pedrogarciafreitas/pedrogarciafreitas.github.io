---
id: 1359
title: Introduction To Scala — Part1 — Variables and Functions
date: 2011-11-07T15:00:32+00:00
author: CKPYT
excerpt: "Exercises of the book 'Introduction to Objective Caml' solved in Scala."
layout: post
guid: http://www.sawp.com.br/blog/?p=1359
permalink: /p=1359
wp-syntax-cache-content:
  - |
    a:9:{i:1;s:3756:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">def</span> sum<span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int, m<span style="color: #000080;">:</span> Int, f<span style="color: #000080;">:</span> Int <span style="color: #000080;">=&gt;</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>n <span style="color: #000080;">&gt;</span> m<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> f<span style="color: #F78811;">&#40;</span>n<span style="color: #F78811;">&#41;</span> + sum<span style="color: #F78811;">&#40;</span>n +<span style="color: #F78811;">1</span>, m, f<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> sumTailRecursive<span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int, m<span style="color: #000080;">:</span> Int, f<span style="color: #000080;">:</span> Int <span style="color: #000080;">=&gt;</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>i<span style="color: #000080;">:</span> Int, acc<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">&gt;</span> m<span style="color: #F78811;">&#41;</span> acc
    <span style="color: #0000ff; font-weight: bold;">else</span> iter <span style="color: #F78811;">&#40;</span>i + <span style="color: #F78811;">1</span>, f<span style="color: #F78811;">&#40;</span>i + acc<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    iter<span style="color: #F78811;">&#40;</span>n, <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Sum not tail recursive: &quot;</span> + sum<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">10</span>, x <span style="color: #000080;">=&gt;</span> x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Sum tail recursive: &quot;</span> + sumTailRecursive<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">10</span>, x <span style="color: #000080;">=&gt;</span> x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def sum(n: Int, m: Int, f: Int =&gt; Int): Int =
    if (n &gt; m) 0
    else f(n) + sum(n +1, m, f)
    
    def sumTailRecursive(n: Int, m: Int, f: Int =&gt; Int) = {
    def iter(i: Int, acc: Int): Int =
    if (i &gt; m) acc
    else iter (i + 1, f(i + acc))
    iter(n, 0)
    }
    
    println(&quot;Sum not tail recursive: &quot; + sum(1, 10, x =&gt; x))
    println(&quot;Sum tail recursive: &quot; + sumTailRecursive(1, 10, x =&gt; x))</p></div>
    ;i:2;s:998:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;">gcd<span style="color: #a52a2a;">&#40;</span>n, m<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">while</span> m <span style="color: #a52a2a;">=</span> <span style="color: #c6c;">0</span>
    <span style="color: #06c; font-weight: bold;">if</span> n <span style="color: #a52a2a;">&gt;</span> m
    n <span style="color: #a52a2a;">&lt;</span> <span style="color: #a52a2a;">-</span> n <span style="color: #a52a2a;">-</span> m
    <span style="color: #06c; font-weight: bold;">else</span>
    m <span style="color: #a52a2a;">&lt;-</span> m <span style="color: #a52a2a;">-</span> n
    return n</pre></td></tr></table><p class="theCode" style="display:none;">gcd(n, m) =
    while m = 0
    if n &gt; m
    n &lt; - n - m
    else
    m &lt;- m - n
    return n</p></div>
    ;i:3;s:6165:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> IntWithGCD<span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> value <span style="color: #000080;">=</span> n
    <span style="color: #0000ff; font-weight: bold;">def</span> <span style="color: #000080;">%%</span> <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> IntWithGCD<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntWithGCD <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>that <span style="color: #000080;">==</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">this</span> <span style="color: #000080;">&gt;</span> that<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">this</span> - that<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">%%</span> that
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">this</span> <span style="color: #000080;">%%</span> <span style="color: #F78811;">&#40;</span>that - <span style="color: #0000ff; font-weight: bold;">this</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> <span style="color: #000080;">&lt;</span> <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> IntWithGCD<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">this</span>.<span style="color: #000000;">value</span> <span style="color: #000080;">&lt;</span> that.<span style="color: #000000;">value</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> <span style="color: #000080;">&gt;</span> <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> IntWithGCD<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    that <span style="color: #000080;">&lt;</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> <span style="color: #000080;">==</span> <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> IntWithGCD<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    that.<span style="color: #000000;">value</span> <span style="color: #000080;">==</span> <span style="color: #0000ff; font-weight: bold;">this</span>.<span style="color: #000000;">value</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> <span style="color: #000080;">==</span> <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    that <span style="color: #000080;">==</span> <span style="color: #0000ff; font-weight: bold;">this</span>.<span style="color: #000000;">value</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> - <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> IntWithGCD<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> IntWithGCD<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">this</span>.<span style="color: #000000;">value</span> - that.<span style="color: #000000;">value</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> toString <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">this</span>.<span style="color: #000000;">value</span>.<span style="color: #000000;">toString</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">implicit</span> <span style="color: #0000ff; font-weight: bold;">def</span> intToIntWithGCD<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> IntWithGCD<span style="color: #F78811;">&#40;</span>x<span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;GCD 4 and 8: &quot;</span> + <span style="color: #F78811;">8</span> <span style="color: #000080;">%%</span> <span style="color: #F78811;">4</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">class IntWithGCD(n: Int) {
    val value = n
    def %% (that: IntWithGCD): IntWithGCD =
    if (that == 0) this
    else if (this &gt; that) (this - that) %% that
    else this %% (that - this)
    
    def &lt; (that: IntWithGCD) =
    this.value &lt; that.value
    
    def &gt; (that: IntWithGCD) =
    that &lt; this
    
    def == (that: IntWithGCD) =
    that.value == this.value
    
    def == (that: Int) =
    that == this.value
    
    def - (that: IntWithGCD) =
    new IntWithGCD(this.value - that.value)
    
    override def toString = this.value.toString
    }
    
    implicit def intToIntWithGCD(x: Int) = new IntWithGCD(x)
    
    println(&quot;GCD 4 and 8: &quot; + 8 %% 4)</p></div>
    ;i:4;s:5632:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #008000; font-style: italic;">// A simple O(n) tail-recursive implementation</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> search <span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> Int <span style="color: #000080;">=&gt;</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>i<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>f<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&gt;=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> i
    <span style="color: #0000ff; font-weight: bold;">else</span> iter<span style="color: #F78811;">&#40;</span>i+<span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    iter<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// A faster O(log(n)) tail-recursive implementation</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> search2 <span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> Int <span style="color: #000080;">=&gt;</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>i<span style="color: #000080;">:</span> Int, acc<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">&lt;</span> acc - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> k <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>i + acc<span style="color: #F78811;">&#41;</span> / <span style="color: #F78811;">2</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>f<span style="color: #F78811;">&#40;</span>k<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&gt;=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> iter<span style="color: #F78811;">&#40;</span>i, k<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> iter<span style="color: #F78811;">&#40;</span>k, acc<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">else</span>
    acc
    iter<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span>, n<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Search O(n): &quot;</span> + search <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">10</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Search Log(n): &quot;</span> + search2 <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">10</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">// A simple O(n) tail-recursive implementation
    def search (n: Int) (f: Int =&gt; Int): Int = {
    def iter(i: Int): Int =
    if (f(i) &gt;= 0) i
    else iter(i+1)
    iter(0)
    }
    
    // A faster O(log(n)) tail-recursive implementation
    def search2 (n: Int) (f: Int =&gt; Int): Int = {
    def iter(i: Int, acc: Int): Int =
    if (i &lt; acc - 1) {
    val k = (i + acc) / 2
    if (f(k) &gt;= 0) iter(i, k)
    else iter(k, acc)
    } else
    acc
    iter(0, n)
    }
    
    println(&quot;Search O(n): &quot; + search (10) (x =&gt; x - 1))
    println(&quot;Search Log(n): &quot; + search2 (10) (x =&gt; x - 1))</p></div>
    ;i:5;s:1275:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;">empty <span style="color: #a52a2a;">=</span> key <span style="color: #a52a2a;">-&gt;</span> <span style="color: #c6c;">0</span>
    add<span style="color: #a52a2a;">&#40;</span>dict, key, v<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">=</span> key<span style="color: #a52a2a;">'</span> <span style="color: #a52a2a;">-&gt;</span> <span style="color: #06c; font-weight: bold;">if</span> <span style="color: #a52a2a;">&#40;</span>key<span style="color: #a52a2a;">'</span> <span style="color: #a52a2a;">=</span> key<span style="color: #a52a2a;">&#41;</span> v <span style="color: #06c; font-weight: bold;">else</span> dict<span style="color: #a52a2a;">&#40;</span>key<span style="color: #a52a2a;">&#41;</span>
    find<span style="color: #a52a2a;">&#40;</span>dict, key<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">=</span> dict<span style="color: #a52a2a;">&#40;</span>key<span style="color: #a52a2a;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">empty = key -&gt; 0
    add(dict, key, v) = key' -&gt; if (key' = key) v else dict(key)
    find(dict, key) = dict(key)</p></div>
    ;i:6;s:1154:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">let</span> dict1 <span style="color: #a52a2a;">=</span> add empty <span style="color: #3cb371;">&quot;x&quot;</span> <span style="color: #c6c;">1</span>
    <span style="color: #06c; font-weight: bold;">let</span> dict2 <span style="color: #a52a2a;">=</span> add dict1 <span style="color: #3cb371;">&quot;y&quot;</span> <span style="color: #c6c;">2</span>
    <span style="color: #06c; font-weight: bold;">let</span> dict3 <span style="color: #a52a2a;">=</span> add dict2 <span style="color: #3cb371;">&quot;x&quot;</span> <span style="color: #c6c;">3</span>
    <span style="color: #06c; font-weight: bold;">let</span> dict4 <span style="color: #a52a2a;">=</span> add dict3 <span style="color: #3cb371;">&quot;y&quot;</span> <span style="color: #c6c;">4</span></pre></td></tr></table><p class="theCode" style="display:none;">let dict1 = add empty &quot;x&quot; 1
    let dict2 = add dict1 &quot;y&quot; 2
    let dict3 = add dict2 &quot;x&quot; 3
    let dict4 = add dict3 &quot;y&quot; 4</p></div>
    ;i:7;s:6724:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #008000; font-style: italic;">// 1 Implement the dictionary in Scala.</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> empty <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>key<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> add<span style="color: #F78811;">&#40;</span>dict<span style="color: #000080;">:</span> String <span style="color: #000080;">=&gt;</span> Int, key<span style="color: #000080;">:</span> String, v<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #F78811;">&#40;</span>keyl<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>keyl <span style="color: #000080;">==</span> key<span style="color: #F78811;">&#41;</span> v <span style="color: #0000ff; font-weight: bold;">else</span> dict<span style="color: #F78811;">&#40;</span>key<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> find<span style="color: #F78811;">&#40;</span>dict<span style="color: #000080;">:</span> String <span style="color: #000080;">=&gt;</span> Int, key<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> dict<span style="color: #F78811;">&#40;</span>key<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 2. What are the values associated with &quot;x&quot; and &quot;y&quot; in each of the four</span>
    <span style="color: #008000; font-style: italic;">// dictionaries?</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> dict1 <span style="color: #000080;">=</span> add<span style="color: #F78811;">&#40;</span>empty, <span style="color: #6666FF;">&quot;x&quot;</span>, <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> dict2 <span style="color: #000080;">=</span> add<span style="color: #F78811;">&#40;</span>dict1, <span style="color: #6666FF;">&quot;y&quot;</span>, <span style="color: #F78811;">2</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> dict3 <span style="color: #000080;">=</span> add<span style="color: #F78811;">&#40;</span>dict2, <span style="color: #6666FF;">&quot;x&quot;</span>, <span style="color: #F78811;">3</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> dict4 <span style="color: #000080;">=</span> add<span style="color: #F78811;">&#40;</span>dict3, <span style="color: #6666FF;">&quot;y&quot;</span>, <span style="color: #F78811;">4</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict1['x'] = &quot;</span> + dict1<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;x&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict2['x'] = &quot;</span> + dict2<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;x&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict3['x'] = &quot;</span> + dict3<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;x&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict4['x'] = &quot;</span> + dict4<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;x&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict1['y'] = &quot;</span> + dict1<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;y&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict2['y'] = &quot;</span> + dict2<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;y&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict3['y'] = &quot;</span> + dict3<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;y&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;dict4['y'] = &quot;</span> + dict4<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;y&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">// 1 Implement the dictionary in Scala.
    def empty = (key: String) =&gt; 0
    def add(dict: String =&gt; Int, key: String, v: Int) =
    (keyl: String) =&gt; if (keyl == key) v else dict(key)
    def find(dict: String =&gt; Int, key: String) = dict(key)
    
    // 2. What are the values associated with &quot;x&quot; and &quot;y&quot; in each of the four
    // dictionaries?
    val dict1 = add(empty, &quot;x&quot;, 1)
    val dict2 = add(dict1, &quot;y&quot;, 2)
    val dict3 = add(dict2, &quot;x&quot;, 3)
    val dict4 = add(dict3, &quot;y&quot;, 4)
    
    println(&quot;dict1['x'] = &quot; + dict1(&quot;x&quot;))
    println(&quot;dict2['x'] = &quot; + dict2(&quot;x&quot;))
    println(&quot;dict3['x'] = &quot; + dict3(&quot;x&quot;))
    println(&quot;dict4['x'] = &quot; + dict4(&quot;x&quot;))
    println(&quot;dict1['y'] = &quot; + dict1(&quot;y&quot;))
    println(&quot;dict2['y'] = &quot; + dict2(&quot;y&quot;))
    println(&quot;dict3['y'] = &quot; + dict3(&quot;y&quot;))
    println(&quot;dict4['y'] = &quot; + dict4(&quot;y&quot;))</p></div>
    ;i:8;s:814:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"> <span style="color: #06c; font-weight: bold;">let</span> f x <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">let</span> z <span style="color: #a52a2a;">=</span> g<span style="color: #a52a2a;">&#40;</span>x<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">fun</span> y <span style="color: #a52a2a;">-&gt;</span> h<span style="color: #a52a2a;">&#40;</span>z, y<span style="color: #a52a2a;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;"> let f x =
    let z = g(x) in
    fun y -&gt; h(z, y)</p></div>
    ;i:9;s:3565:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">def</span> r<span style="color: #F78811;">&#40;</span>b<span style="color: #000080;">:</span> Double, c<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> <span style="color: #F78811;">&#40;</span>Double <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#40;</span>Double, Double<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> bMinus <span style="color: #000080;">=</span> -b
    <span style="color: #0000ff; font-weight: bold;">val</span> bTimesb <span style="color: #000080;">=</span> b <span style="color: #000080;">*</span> b
    <span style="color: #0000ff; font-weight: bold;">val</span> fourC <span style="color: #000080;">=</span> <span style="color: #F78811;">4.0</span> <span style="color: #000080;">*</span> c
    <span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>bMinus + math.<span style="color: #000000;">sqrt</span><span style="color: #F78811;">&#40;</span>bTimesb - fourC <span style="color: #000080;">*</span> a<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> / <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2.0</span> <span style="color: #000080;">*</span> a<span style="color: #F78811;">&#41;</span>,
    <span style="color: #F78811;">&#40;</span>bMinus - math.<span style="color: #000000;">sqrt</span><span style="color: #F78811;">&#40;</span>bTimesb - fourC <span style="color: #000080;">*</span> a<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> / <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2.0</span> <span style="color: #000080;">*</span> a<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> baskara <span style="color: #000080;">=</span> r<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">5.0</span>, <span style="color: #F78811;">1.0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> x <span style="color: #000080;">=</span> baskara<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2.0</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Solution of 2x^2 + 5x + 1 = 0 is &quot;</span> + x<span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def r(b: Double, c: Double): (Double =&gt; (Double, Double)) = {
    val bMinus = -b
    val bTimesb = b * b
    val fourC = 4.0 * c
    (a: Double) =&gt; ((bMinus + math.sqrt(bTimesb - fourC * a)) / (2.0 * a),
    (bMinus - math.sqrt(bTimesb - fourC * a)) / (2.0 * a))
    }
    
    def baskara = r(5.0, 1.0)
    val x = baskara(2.0)
    
    println(&quot;Solution of 2x^2 + 5x + 1 = 0 is &quot; + x)</p></div>
    ";}
categories:
  - Scala Notes
---
**Exercise 1.1:** Write a function sum that, given two integer bounds $$n$$ and $$m$$ and a function $$f$$, computes a summation.
  


<center>
  <br /> $$ sum ~ n ~ m ~ f = \sum_{i=n}^{m} f(i) $$<br />
</center>

<pre lang="scala">def sum(n: Int, m: Int, f: Int => Int): Int = 
  if (n > m) 0
  else f(n) + sum(n +1, m, f)

def sumTailRecursive(n: Int, m: Int, f: Int => Int) = {
  def iter(i: Int, acc: Int): Int = 
    if (i > m) acc
    else iter (i + 1, f(i + acc))
  iter(n, 0)
}

println("Sum not tail recursive: " + sum(1, 10, x => x))
println("Sum tail recursive: " + sumTailRecursive(1, 10, x => x))</pre>

&nbsp;

**Exercise 1.2:** Euclid&#8217;s algorithm computes the greatest common divisor (GCD) of two integers. It is one of the oldest known algorithms, appearing in Euclid&#8217;s Elements in roughly 300 BC. It can be defined in pseudo-code as follows, where < - represents assignment. 

<pre lang="ocaml">gcd(n, m) = 
  while m = 0
     if n > m
       n &lt; - n - m
     else
       m &lt;- m - n
   return n</pre>

Write an Scala function %% that computes the GCD using Euclid&#8217;s algorithm (so n %% m is the GCD of the integers n and m). You should define it without assignment, as recursive function. [Note, this is Euclid&#8217;s original definition of the algorithm. More modern versions usually use a modulus operation instead of subtraction.

<pre lang="scala">class IntWithGCD(n: Int) {
  val value = n
  def %% (that: IntWithGCD): IntWithGCD =
    if (that == 0) this
    else if (this > that) (this - that) %% that
    else this %% (that - this)

  def &lt; (that: IntWithGCD) = 
    this.value &lt; that.value

  def > (that: IntWithGCD) =
    that &lt; this

  def == (that: IntWithGCD) =
    that.value == this.value

  def == (that: Int) =
    that == this.value

  def - (that: IntWithGCD) = 
    new IntWithGCD(this.value - that.value)

  override def toString = this.value.toString
}

implicit def intToIntWithGCD(x: Int) = new IntWithGCD(x)

println("GCD 4 and 8: " + 8 %% 4)</pre>

&nbsp;

**Exercise 1.3:** Suppose you have a function on integers $$f : int -> int$$ that is monotonically increasing over some range of arguments from $$0$$ up to $$n$$. That is, $$f (i) < f (i + 1)[/latex] for any [latex]0 \leq i < n[/latex]. In addition [latex]f(0) < 0[/latex] and [latex]f(n) > 0$$. Write a function search $$f$$ $$n$$ that finds the smallest argument $$i$$ where $$f(i) \geq 0$$.

<pre lang="scala">// A simple O(n) tail-recursive implementation
def search (n: Int) (f: Int => Int): Int = {
  def iter(i: Int): Int = 
    if (f(i) >= 0) i
    else iter(i+1)
  iter(0)
}

// A faster O(log(n)) tail-recursive implementation
def search2 (n: Int) (f: Int => Int): Int = {
  def iter(i: Int, acc: Int): Int =
    if (i &lt; acc - 1) {
      val k = (i + acc) / 2
      if (f(k) >= 0) iter(i, k)
      else iter(k, acc)
    } else
      acc
  iter(0, n)
}

println("Search O(n): " + search (10) (x => x - 1))
println("Search Log(n): " + search2 (10) (x => x - 1))</pre>

&nbsp;

**Exercise 1.4:** A dictionary is a data structure that represents a map from keys to values. A dictionary has three operations:

  *  `empty : dictionary` 
  *  `add   : dictionary -> key -> value -> dictionary` 
  *  `find  : dictionary -> key -> value` 

The value empty is an empty dictionary; the expression add dict key value takes an existing dictionary dict and augments it with a new binding $$key -> value;$$ and the expression find dict key fetches the value in the dictionary dict associated with the key.

One way to implement a dictionary is to represent it as a function from keys to values. Let&#8217;s assume we are building a dictionary where the key type is string, the value type is int, and the empty dictionary maps every key to zero. This dictionary can be implemented abstractly as follows, where we write $$->$$ for the map from keys to values.

<pre lang="ocaml">empty = key -> 0
add(dict, key, v) = key' -> if (key' = key) v else dict(key)
find(dict, key) = dict(key)</pre>

**1.** Implement the dictionary in Scala.
  
**2.** Suppose we have constructed several dictionaries as follows.

<pre lang="ocaml">let dict1 = add empty "x" 1
let dict2 = add dict1 "y" 2
let dict3 = add dict2 "x" 3
let dict4 = add dict3 "y" 4 </pre>

What are the values associated with &#8220;x&#8221; and &#8220;y&#8221; in each of the four dictionaries?

<pre lang="scala">// 1 Implement the dictionary in Scala.
def empty = (key: String) => 0
def add(dict: String => Int, key: String, v: Int) = 
  (keyl: String) => if (keyl == key) v else dict(key)
def find(dict: String => Int, key: String) = dict(key)

// 2. What are the values associated with "x" and "y" in each of the four
// dictionaries?
val dict1 = add(empty, "x", 1)
val dict2 = add(dict1, "y", 2)
val dict3 = add(dict2, "x", 3)
val dict4 = add(dict3, "y", 4)

println("dict1['x'] = " + dict1("x"))
println("dict2['x'] = " + dict2("x"))
println("dict3['x'] = " + dict3("x"))
println("dict4['x'] = " + dict4("x"))
println("dict1['y'] = " + dict1("y"))
println("dict2['y'] = " + dict2("y"))
println("dict3['y'] = " + dict3("y"))
println("dict4['y'] = " + dict4("y"))</pre>

&nbsp;

**Exercise 1.5:** Partial application is sometimes used to improve the performance of a multi-argument function when the function is to be called repeatedly with one or more of its arguments fixed. Consider a function $$f(x, y)$$ that is to be called multiple times with $$x$$ fixed. First, the function must be written in a form $$f(x, y) = h(g(x), y)$$ from some functions $$g$$ and $$h$$, where $$g$$ represents the part of the computation that uses only the value $$x$$. We then write it in OCaml as follows.

<pre lang="ocaml">let f x =
      let z = g(x) in
        fun y -> h(z, y)</pre>

Calling f on its first argument computes $$g(x)$$ and returns a function that uses the value (without re-computing it).

Consider one root of a quadratic equation $$ax^2 + bx + c = 0$$ specified by the by the quadratic formula $$r(a, b, c) = \frac{-b + \sqrt{b^2 &#8211; 4ac}{2a}$$. Suppose we wish to to evaluate the quadratic formula for multiple values of $$a$$ with $$b$$ and $$c$$ fixed. Write a function to compute the formula efficiently.

<pre lang="scala">def r(b: Double, c: Double): (Double => (Double, Double)) = {
  val bMinus = -b
  val bTimesb = b * b
  val fourC = 4.0 * c
  (a: Double) => ((bMinus + math.sqrt(bTimesb - fourC * a)) / (2.0 * a),
                  (bMinus - math.sqrt(bTimesb - fourC * a)) / (2.0 * a))
}

def baskara = r(5.0, 1.0)
val x = baskara(2.0)

println("Solution of 2x^2 + 5x + 1 = 0 is " + x)</pre>
