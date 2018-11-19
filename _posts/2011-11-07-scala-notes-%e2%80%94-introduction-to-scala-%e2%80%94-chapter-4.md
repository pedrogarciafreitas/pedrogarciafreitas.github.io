---
id: 1428
title: Scala by Example — Chapter 04
date: 2011-11-07T20:01:21+00:00
author: CKPYT
excerpt: "Exercises solutions of the book 'Scala by Example'."
layout: post
guid: http://www.sawp.com.br/blog/?p=1428
permalink: p=1428
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:3094:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.4.1
    * The isGoodEnough test is not very precise for small numbers
    * and might lead to non-termination for very large ones (why?). Design a
    * different version of isGoodEnough which does not have these problems.
    *
    * OBS: in the book isGoodEnough is
    * def isGoodEnough(guess: Double, x: Double) =
    *   abs(square(guess) - x) &lt; 0.001
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> sqrtIter<span style="color: #F78811;">&#40;</span>guess<span style="color: #000080;">:</span> Double, x<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Double <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>isGoodEnough<span style="color: #F78811;">&#40;</span>guess, x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> guess
    <span style="color: #0000ff; font-weight: bold;">else</span> sqrtIter<span style="color: #F78811;">&#40;</span>improve<span style="color: #F78811;">&#40;</span>guess, x<span style="color: #F78811;">&#41;</span>, x<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> sqrt<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> sqrtIter<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1.0</span>, x<span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span>sqrt<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.0001</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>sqrt<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">9</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>sqrt<span style="color: #F78811;">&#40;</span>1e308<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.4.1
    * The isGoodEnough test is not very precise for small numbers
    * and might lead to non-termination for very large ones (why?). Design a
    * different version of isGoodEnough which does not have these problems.
    *
    * OBS: in the book isGoodEnough is
    * def isGoodEnough(guess: Double, x: Double) =
    *   abs(square(guess) - x) &lt; 0.001
    */
    
    def sqrtIter(guess: Double, x: Double): Double =
    if (isGoodEnough(guess, x)) guess
    else sqrtIter(improve(guess, x), x)
    
    def sqrt(x: Double) = sqrtIter(1.0, x)
    
    println(sqrt(0.0001))
    println(sqrt(9))
    println(sqrt(1e308))</p></div>
    ;i:2;s:3431:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.6.1 Design a tail-recursive version of factorial.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> factorial<span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> factLoop<span style="color: #F78811;">&#40;</span>accumulator<span style="color: #000080;">:</span> BigInt, i<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">==</span> <span style="color: #F78811;">0</span> || i <span style="color: #000080;">==</span> <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    accumulator
    <span style="color: #0000ff; font-weight: bold;">else</span>
    factLoop<span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">*</span> accumulator, i - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    factLoop<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, n<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;fat(5) = &quot;</span> + factorial<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">5</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;fat(10) = &quot;</span> + factorial<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">10</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;fat(100) = &quot;</span> + factorial<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">100</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;fat(500) = &quot;</span> + factorial<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">500</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.6.1 Design a tail-recursive version of factorial.
    */
    
    def factorial(n: BigInt): BigInt = {
    def factLoop(accumulator: BigInt, i: BigInt): BigInt =
    if (i == 0 || i == 1)
    accumulator
    else
    factLoop(i * accumulator, i - 1)
    factLoop(1, n)
    }
    
    
    println(&quot;fat(5) = &quot; + factorial(5))
    println(&quot;fat(10) = &quot; + factorial(10))
    println(&quot;fat(100) = &quot; + factorial(100))
    println(&quot;fat(500) = &quot; + factorial(500))</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 4.4.1
 * The isGoodEnough test is not very precise for small numbers
 * and might lead to non-termination for very large ones (why?). Design a
 * different version of isGoodEnough which does not have these problems.
 *
 * OBS: in the book isGoodEnough is
 * def isGoodEnough(guess: Double, x: Double) =
 *   abs(square(guess) - x) &lt; 0.001
 */

def sqrtIter(guess: Double, x: Double): Double =
  if (isGoodEnough(guess, x)) guess
  else sqrtIter(improve(guess, x), x)

def sqrt(x: Double) = sqrtIter(1.0, x)

println(sqrt(0.0001))
println(sqrt(9))
println(sqrt(1e308))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 4.6.1 Design a tail-recursive version of factorial.
 */

def factorial(n: BigInt): BigInt = {
  def factLoop(accumulator: BigInt, i: BigInt): BigInt =
    if (i == 0 || i == 1)
      accumulator
    else
      factLoop(i * accumulator, i - 1)
  factLoop(1, n)
}


println("fat(5) = " + factorial(5))
println("fat(10) = " + factorial(10))
println("fat(100) = " + factorial(100))
println("fat(500) = " + factorial(500))</pre>
