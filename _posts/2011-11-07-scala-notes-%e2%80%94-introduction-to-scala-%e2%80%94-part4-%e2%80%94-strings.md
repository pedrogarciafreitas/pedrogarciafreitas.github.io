---
id: 1422
title: Introduction To Scala — Part5 — Strings
date: 2011-11-07T19:42:19+00:00
author: CKPYT
excerpt: "Exercises of the book 'Introduction to Objective Caml' solved in Scala."
layout: post
guid: http://www.sawp.com.br/blog/?p=1422
permalink: /p=1422
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4514:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 5.1.
    * Write a function string_reverse : string -&gt; unit to reverse a
    * string in-place.
    *
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> string<span style="color: #000080;">_</span>reverse<span style="color: #F78811;">&#40;</span>s<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> String <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> len <span style="color: #000080;">=</span> s.<span style="color: #000000;">length</span> / <span style="color: #F78811;">2</span> - <span style="color: #F78811;">1</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> sb <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> StringBuilder<span style="color: #F78811;">&#40;</span>s<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">&lt;</span> - <span style="color: #F78811;">0</span> to len<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> c <span style="color: #000080;">=</span> sb<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span>
    sb<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> sb<span style="color: #F78811;">&#40;</span>s.<span style="color: #000000;">length</span> -i - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    sb<span style="color: #F78811;">&#40;</span>s.<span style="color: #000000;">length</span> - i - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> c
    <span style="color: #F78811;">&#125;</span>
    sb.<span style="color: #000000;">toString</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// Test</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> stringTest1 <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;Aleksandr Dugin&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> stringTest2 <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;Olavo de Carvalho&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> rev1 <span style="color: #000080;">=</span> string<span style="color: #000080;">_</span>reverse<span style="color: #F78811;">&#40;</span>stringTest1<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> rev2 <span style="color: #000080;">=</span> string<span style="color: #000080;">_</span>reverse<span style="color: #F78811;">&#40;</span>stringTest2<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Original: &quot;</span> + stringTest1 + <span style="color: #6666FF;">&quot;    reversed: &quot;</span> + rev1<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Original: &quot;</span> + stringTest2 + <span style="color: #6666FF;">&quot;    reversed: &quot;</span> + rev2<span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 5.1.
    * Write a function string_reverse : string -&gt; unit to reverse a
    * string in-place.
    *
    */
    def string_reverse(s: String): String = {
    val len = s.length / 2 - 1
    val sb = new StringBuilder(s)
    for (i &lt; - 0 to len) {
    val c = sb(i)
    sb(i) = sb(s.length -i - 1)
    sb(s.length - i - 1) = c
    }
    sb.toString
    }
    
    
    // Test
    val stringTest1 = &quot;Aleksandr Dugin&quot;
    val stringTest2 = &quot;Olavo de Carvalho&quot;
    val rev1 = string_reverse(stringTest1)
    val rev2 = string_reverse(stringTest2)
    println(&quot;Original: &quot; + stringTest1 + &quot;    reversed: &quot; + rev1)
    println(&quot;Original: &quot; + stringTest2 + &quot;    reversed: &quot; + rev2)</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 5.1.
 * Write a function string_reverse : string -> unit to reverse a
 * string in-place.
 *
 */
def string_reverse(s: String): String = {
  val len = s.length / 2 - 1
  val sb = new StringBuilder(s)
  for (i &lt; - 0 to len) {
    val c = sb(i)
    sb(i) = sb(s.length -i - 1)
    sb(s.length - i - 1) = c
  }
  sb.toString
}


// Test
val stringTest1 = "Aleksandr Dugin"
val stringTest2 = "Olavo de Carvalho"
val rev1 = string_reverse(stringTest1)
val rev2 = string_reverse(stringTest2)
println("Original: " + stringTest1 + "    reversed: " + rev1)
println("Original: " + stringTest2 + "    reversed: " + rev2)</pre>
