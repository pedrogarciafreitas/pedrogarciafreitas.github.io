---
id: 1530
title: 'Full Example — Fermat&#8217;s factorization method'
date: 2012-05-10T00:26:36+00:00
author: CKPYT
excerpt: "Scala implementation of Fermat's factorization method, named after Pierre de Fermat, is based on the representation of an odd integer as the difference of two squares."
layout: post
guid: http://www.sawp.com.br/blog/?p=1530
permalink: /p=1530
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:7996:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #000080;">#!</span>/bin/sh
    exec scala <span style="color: #6666FF;">&quot;$0&quot;</span> <span style="color: #6666FF;">&quot;$@&quot;</span>
    <span style="color: #000080;">!#</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> decomposeInPrimes<span style="color: #F78811;">&#40;</span>t<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Set<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> factors <span style="color: #000080;">=</span> Set<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> isqrt<span style="color: #F78811;">&#40;</span>number<span style="color: #000080;">:</span> Float<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> squareroot<span style="color: #000080;">:</span>Int <span style="color: #000080;">=</span> Math.<span style="color: #000000;">sqrt</span><span style="color: #F78811;">&#40;</span>number<span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    squareroot
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> fermat<span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> number <span style="color: #000080;">=</span> n
    <span style="color: #0000ff; font-weight: bold;">while</span><span style="color: #F78811;">&#40;</span>number <span style="color: #000080;">%</span> <span style="color: #F78811;">2</span> <span style="color: #000080;">==</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    number /<span style="color: #000080;">=</span> <span style="color: #F78811;">2</span>
    factors +<span style="color: #000080;">=</span> <span style="color: #F78811;">2</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>number <span style="color: #000080;">==</span> <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">return</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> r <span style="color: #000080;">=</span> isqrt<span style="color: #F78811;">&#40;</span>number<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> is<span style="color: #000080;">_</span>prime <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>r <span style="color: #000080;">&lt;</span> <span style="color: #F78811;">&#40;</span>number + <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span> / <span style="color: #F78811;">2</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> m <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>r <span style="color: #000080;">*</span> r<span style="color: #F78811;">&#41;</span> -  number<span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toFloat</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>m <span style="color: #000080;">&gt;=</span> <span style="color: #F78811;">0</span> <span style="color: #000080;">&amp;&amp;</span> Math.<span style="color: #000000;">sqrt</span><span style="color: #F78811;">&#40;</span>m<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">==</span> Math.<span style="color: #000000;">floor</span><span style="color: #F78811;">&#40;</span>Math.<span style="color: #000000;">sqrt</span><span style="color: #F78811;">&#40;</span>m<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> s <span style="color: #000080;">=</span> isqrt<span style="color: #F78811;">&#40;</span>m<span style="color: #F78811;">&#41;</span>
    fermat<span style="color: #F78811;">&#40;</span>r - s<span style="color: #F78811;">&#41;</span>
    fermat<span style="color: #F78811;">&#40;</span>r + s<span style="color: #F78811;">&#41;</span>
    is<span style="color: #000080;">_</span>prime <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">return</span>
    <span style="color: #F78811;">&#125;</span>
    r +<span style="color: #000080;">=</span> <span style="color: #F78811;">1</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>is<span style="color: #000080;">_</span>prime <span style="color: #000080;">==</span> <span style="color: #0000ff; font-weight: bold;">true</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    factors +<span style="color: #000080;">=</span> number
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    fermat<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    factors
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> test <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    println<span style="color: #F78811;">&#40;</span>decomposeInPrimes<span style="color: #F78811;">&#40;</span>test<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!/bin/sh
    exec scala &quot;$0&quot; &quot;$@&quot;
    !#
    
    def decomposeInPrimes(t: Int): Set[Int] = {
    var factors = Set[Int]()
    
    def isqrt(number: Float): Int = {
    val squareroot:Int = Math.sqrt(number).toInt
    squareroot
    }
    
    def fermat(n: Int) {
    var number = n
    while(number % 2 == 0) {
    number /= 2
    factors += 2
    }
    if (number == 1) {
    return
    }
    var r = isqrt(number)
    var is_prime = true
    while (r &lt; (number + 1) / 2) {
    val m = ((r * r) -  number).toFloat
    if (m &gt;= 0 &amp;&amp; Math.sqrt(m) == Math.floor(Math.sqrt(m))) {
    val s = isqrt(m)
    fermat(r - s)
    fermat(r + s)
    is_prime = false
    return
    }
    r += 1
    }
    if (is_prime == true) {
    factors += number
    }
    }
    fermat(t)
    factors
    }
    
    val test = args(0).toInt
    println(decomposeInPrimes(test))</p></div>
    ;i:2;s:329:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">.<span style="color: #000000; font-weight: bold;">/</span>fermat.sh <span style="color: #000000;">9941</span></pre></td></tr></table><p class="theCode" style="display:none;">./fermat.sh 9941</p></div>
    ";}
categories:
  - Scala Notes
---
Fermat&#8217;s factorization method, named after Pierre de Fermat, is based on the representation of an odd integer as the difference of two squares. See more in <a href="http://en.wikipedia.org/wiki/Fermat's_factorization_method" target="_blank">Wikipedia</a>.

<pre lang="scala">#!/bin/sh
exec scala "$0" "$@"
!#

def decomposeInPrimes(t: Int): Set[Int] = {
  var factors = Set[Int]()

  def isqrt(number: Float): Int = {
    val squareroot:Int = Math.sqrt(number).toInt
    squareroot
  }

  def fermat(n: Int) {
    var number = n
    while(number % 2 == 0) {
      number /= 2
      factors += 2
    }
    if (number == 1) {
      return
    }
    var r = isqrt(number)
    var is_prime = true
    while (r &lt; (number + 1) / 2) {
      val m = ((r * r) -  number).toFloat
      if (m >= 0 && Math.sqrt(m) == Math.floor(Math.sqrt(m))) {
        val s = isqrt(m)
        fermat(r - s)
        fermat(r + s)
        is_prime = false
        return
      }
      r += 1
    }
    if (is_prime == true) {
      factors += number
    }
  }
  fermat(t)
  factors
}

val test = args(0).toInt
println(decomposeInPrimes(test))</pre></p> 



To run this program as script, save as &#8220;fermat.sh&#8221; and execute:

<pre lang="bash">./fermat.sh 9941</pre></p>
