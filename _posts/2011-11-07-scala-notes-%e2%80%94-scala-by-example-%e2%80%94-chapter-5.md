---
id: 1431
title: Scala by Example — Chapter 05
date: 2011-11-07T20:05:57+00:00
author: CKPYT
excerpt: "Exercises solutions of the book 'Scala by Example'."
layout: post
guid: http://www.sawp.com.br/blog/?p=1431
permalink: /p=1431
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:3614:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 5.2.1 1. The sum function uses a linear recursion. Can you write a
    * tail-recursive one by filling in the ??’s?
    *
    * def sum(f: Int =&gt; Int)(a: Int, b: Int): Int = {
    *   def iter(a: Int, result: Int): Int = {
    *     if (??) ??
    *     else iter(??, ??)
    *   }
    *   iter(??, ??)
    * }
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> sum<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> Int <span style="color: #000080;">=&gt;</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> Int, b<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> Int, result<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>a <span style="color: #000080;">&gt;</span> b<span style="color: #F78811;">&#41;</span>
    result
    <span style="color: #0000ff; font-weight: bold;">else</span>
    iter<span style="color: #F78811;">&#40;</span>a + <span style="color: #F78811;">1</span>, f<span style="color: #F78811;">&#40;</span>a<span style="color: #F78811;">&#41;</span> + result<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>a, <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span>sum<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>sum<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #000080;">*</span>x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 5.2.1 1. The sum function uses a linear recursion. Can you write a
    * tail-recursive one by filling in the ??’s?
    *
    * def sum(f: Int =&gt; Int)(a: Int, b: Int): Int = {
    *   def iter(a: Int, result: Int): Int = {
    *     if (??) ??
    *     else iter(??, ??)
    *   }
    *   iter(??, ??)
    * }
    */
    
    def sum(f: Int =&gt; Int)(a: Int, b: Int): Int = {
    def iter(a: Int, result: Int): Int = {
    if (a &gt; b)
    result
    else
    iter(a + 1, f(a) + result)
    }
    iter(a, 0)
    }
    
    println(sum(x =&gt; x)(1, 30))
    println(sum(x =&gt; x*x)(1, 30))</p></div>
    ;i:2;s:3371:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 5.2.2 Write a function product that computes the product of the
    * values of functions at points over a given range.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> product<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=&gt;</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, b<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, result<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>a <span style="color: #000080;">&gt;</span> b<span style="color: #F78811;">&#41;</span>
    result
    <span style="color: #0000ff; font-weight: bold;">else</span>
    iter<span style="color: #F78811;">&#40;</span>a + <span style="color: #F78811;">1</span>, f<span style="color: #F78811;">&#40;</span>a<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">*</span> result<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>a, <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span>product<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>product<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #000080;">*</span>x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 5.2.2 Write a function product that computes the product of the
    * values of functions at points over a given range.
    */
    
    def product(f: BigInt =&gt; BigInt)(a: BigInt, b: BigInt): BigInt = {
    def iter(a: BigInt, result: BigInt): BigInt = {
    if (a &gt; b)
    result
    else
    iter(a + 1, f(a) * result)
    }
    iter(a, 1)
    }
    
    println(product(x =&gt; x)(1, 30))
    println(product(x =&gt; x*x)(1, 30))</p></div>
    ;i:3;s:3633:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 5.2.3 Write factorial in terms of product.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> product<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=&gt;</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, b<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, result<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>a <span style="color: #000080;">&gt;</span> b<span style="color: #F78811;">&#41;</span>
    result
    <span style="color: #0000ff; font-weight: bold;">else</span>
    iter<span style="color: #F78811;">&#40;</span>a + <span style="color: #F78811;">1</span>, f<span style="color: #F78811;">&#40;</span>a<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">*</span> result<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>a, <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> factorial<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> product<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, x<span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span>factorial<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">5</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>factorial<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">10</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>factorial<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">100</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 5.2.3 Write factorial in terms of product.
    */
    
    def product(f: BigInt =&gt; BigInt)(a: BigInt, b: BigInt): BigInt = {
    def iter(a: BigInt, result: BigInt): BigInt = {
    if (a &gt; b)
    result
    else
    iter(a + 1, f(a) * result)
    }
    iter(a, 1)
    }
    
    def factorial(x: BigInt) = product(x =&gt; x)(1, x)
    
    println(factorial(5))
    println(factorial(10))
    println(factorial(100))</p></div>
    ;i:4;s:6699:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 5.2.4 Can you write an even more general function which
    * generalizes both sum and product?
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> general<span style="color: #F78811;">&#40;</span>op<span style="color: #000080;">:</span> <span style="color: #F78811;">&#40;</span>BigInt, BigInt<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=&gt;</span> BigInt<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, b<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, result<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>a <span style="color: #000080;">&gt;</span> b<span style="color: #F78811;">&#41;</span>
    result
    <span style="color: #0000ff; font-weight: bold;">else</span>
    iter<span style="color: #F78811;">&#40;</span>a + <span style="color: #F78811;">1</span>, op<span style="color: #F78811;">&#40;</span>f<span style="color: #F78811;">&#40;</span>a<span style="color: #F78811;">&#41;</span>, result<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>a, <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> sum<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=&gt;</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, b<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span>
    general<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>x, y<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> x + y<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>f<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>a, b<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> product<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=&gt;</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>a<span style="color: #000080;">:</span> BigInt, b<span style="color: #000080;">:</span> BigInt<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> BigInt <span style="color: #000080;">=</span>
    general<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>x, y<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> x <span style="color: #000080;">*</span> y<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>f<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>a, b<span style="color: #F78811;">&#41;</span>
    &nbsp;
    &nbsp;
    println<span style="color: #F78811;">&#40;</span>sum<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>sum<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #000080;">*</span>x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span>product<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>product<span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x<span style="color: #000080;">*</span>x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, <span style="color: #F78811;">30</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 5.2.4 Can you write an even more general function which
    * generalizes both sum and product?
    */
    
    def general(op: (BigInt, BigInt) =&gt; BigInt)(f: BigInt =&gt; BigInt)
    (a: BigInt, b: BigInt): BigInt = {
    def iter(a: BigInt, result: BigInt): BigInt = {
    if (a &gt; b)
    result
    else
    iter(a + 1, op(f(a), result))
    }
    iter(a, 1)
    }
    
    def sum(f: BigInt =&gt; BigInt)(a: BigInt, b: BigInt): BigInt =
    general((x, y) =&gt; x + y)(f)(a, b)
    
    def product(f: BigInt =&gt; BigInt)(a: BigInt, b: BigInt): BigInt =
    general((x, y) =&gt; x * y)(f)(a, b)
    
    
    println(sum(x =&gt; x)(1, 30))
    println(sum(x =&gt; x*x)(1, 30))
    
    println(product(x =&gt; x)(1, 30))
    println(product(x =&gt; x*x)(1, 30))</p></div>
    ;i:5;s:6194:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 5.3.1 Write a function for cube roots using fixedPoint and
    * averageDamp.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> abs<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&gt;=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> x <span style="color: #0000ff; font-weight: bold;">else</span> -x
    <span style="color: #0000ff; font-weight: bold;">val</span> tolerance <span style="color: #000080;">=</span> 2.2250738585072014E-308
    <span style="color: #0000ff; font-weight: bold;">def</span> isCloseEnough<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Double, y<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> abs<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>x - y<span style="color: #F78811;">&#41;</span> / x<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">=</span> tolerance
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> fixedPoint<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> Double <span style="color: #000080;">=&gt;</span> Double<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>firstGuess<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iterate<span style="color: #F78811;">&#40;</span>guess<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Double <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> next <span style="color: #000080;">=</span> f<span style="color: #F78811;">&#40;</span>guess<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>isCloseEnough<span style="color: #F78811;">&#40;</span>guess, next<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> next
    <span style="color: #0000ff; font-weight: bold;">else</span> iterate<span style="color: #F78811;">&#40;</span>next<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iterate<span style="color: #F78811;">&#40;</span>firstGuess<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> averageDamp<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> Double <span style="color: #000080;">=&gt;</span> Double<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>x + f<span style="color: #F78811;">&#40;</span>x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> / <span style="color: #F78811;">2</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> cube<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> fixedPoint<span style="color: #F78811;">&#40;</span>averageDamp<span style="color: #F78811;">&#40;</span>y <span style="color: #000080;">=&gt;</span> x/<span style="color: #F78811;">&#40;</span>y <span style="color: #000080;">*</span> y<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1.0</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    &nbsp;
    println<span style="color: #F78811;">&#40;</span>cube<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">8</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>cube<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">27</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>cube<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">64</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>cube<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">125</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 5.3.1 Write a function for cube roots using fixedPoint and
    * averageDamp.
    */
    
    def abs(x: Double) = if (x &gt;= 0) x else -x
    val tolerance = 2.2250738585072014E-308
    def isCloseEnough(x: Double, y: Double) = abs((x - y) / x) &lt; = tolerance
    
    def fixedPoint(f: Double =&gt; Double)(firstGuess: Double) = {
    def iterate(guess: Double): Double = {
    val next = f(guess)
    if (isCloseEnough(guess, next)) next
    else iterate(next)
    }
    iterate(firstGuess)
    }
    
    def averageDamp(f: Double =&gt; Double)(x: Double) = (x + f(x)) / 2
    
    def cube(x: Double) = fixedPoint(averageDamp(y =&gt; x/(y * y)))(1.0)
    
    
    println(cube(8))
    println(cube(27))
    println(cube(64))
    println(cube(125))</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 5.2.1 1. The sum function uses a linear recursion. Can you write a
 * tail-recursive one by filling in the ??’s?
 *
 * def sum(f: Int => Int)(a: Int, b: Int): Int = {
 *   def iter(a: Int, result: Int): Int = {
 *     if (??) ??
 *     else iter(??, ??)
 *   }
 *   iter(??, ??)
 * }
 */

def sum(f: Int => Int)(a: Int, b: Int): Int = {
  def iter(a: Int, result: Int): Int = {
    if (a > b)
      result 
    else
      iter(a + 1, f(a) + result)
  }
  iter(a, 0)
}

println(sum(x => x)(1, 30))
println(sum(x => x*x)(1, 30))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 5.2.2 Write a function product that computes the product of the
 * values of functions at points over a given range.
 */

def product(f: BigInt => BigInt)(a: BigInt, b: BigInt): BigInt = {
  def iter(a: BigInt, result: BigInt): BigInt = {
    if (a > b)
      result 
    else
      iter(a + 1, f(a) * result)
  }
  iter(a, 1)
}

println(product(x => x)(1, 30))
println(product(x => x*x)(1, 30))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 5.2.3 Write factorial in terms of product.
 */

def product(f: BigInt => BigInt)(a: BigInt, b: BigInt): BigInt = {
  def iter(a: BigInt, result: BigInt): BigInt = {
    if (a > b)
      result 
    else
      iter(a + 1, f(a) * result)
  }
  iter(a, 1)
}

def factorial(x: BigInt) = product(x => x)(1, x)

println(factorial(5))
println(factorial(10))
println(factorial(100))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 5.2.4 Can you write an even more general function which
 * generalizes both sum and product?
 */

def general(op: (BigInt, BigInt) => BigInt)(f: BigInt => BigInt)
           (a: BigInt, b: BigInt): BigInt = {
  def iter(a: BigInt, result: BigInt): BigInt = {
    if (a > b)
      result 
    else
      iter(a + 1, op(f(a), result))
  }
  iter(a, 1)
}

def sum(f: BigInt => BigInt)(a: BigInt, b: BigInt): BigInt =
  general((x, y) => x + y)(f)(a, b)

def product(f: BigInt => BigInt)(a: BigInt, b: BigInt): BigInt =
  general((x, y) => x * y)(f)(a, b)


println(sum(x => x)(1, 30))
println(sum(x => x*x)(1, 30))

println(product(x => x)(1, 30))
println(product(x => x*x)(1, 30))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 5.3.1 Write a function for cube roots using fixedPoint and
 * averageDamp.
 */

def abs(x: Double) = if (x >= 0) x else -x
val tolerance = 2.2250738585072014E-308 
def isCloseEnough(x: Double, y: Double) = abs((x - y) / x) &lt; = tolerance

def fixedPoint(f: Double => Double)(firstGuess: Double) = {
  def iterate(guess: Double): Double = {
    val next = f(guess)
    if (isCloseEnough(guess, next)) next
    else iterate(next)
  }
  iterate(firstGuess)
}

def averageDamp(f: Double => Double)(x: Double) = (x + f(x)) / 2

def cube(x: Double) = fixedPoint(averageDamp(y => x/(y * y)))(1.0)


println(cube(8))
println(cube(27))
println(cube(64))
println(cube(125))</pre>
