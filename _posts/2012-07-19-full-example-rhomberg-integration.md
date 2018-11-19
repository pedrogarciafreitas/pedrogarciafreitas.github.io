---
id: 1650
title: 'Full Example &#8212; Rhomberg Integration'
date: 2012-07-19T13:02:45+00:00
author: CKPYT
excerpt: Romberg integration is a powerful numerical integration technique which ises k refinaments of the extened trapezoidal rule to remove errors.
layout: post
guid: http://www.sawp.com.br/blog/?p=1650
permalink: p=1650
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:7427:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">import</span> math.<span style="color: #000000;">pow</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> romberg<span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> Double <span style="color: #000080;">=&gt;</span> Double, a<span style="color: #000080;">:</span> Double, b<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Double <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> R<span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int, m<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Double <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>n, m<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span>, <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #F78811;">0.5</span> <span style="color: #000080;">*</span> <span style="color: #F78811;">&#40;</span>b - a<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">*</span> <span style="color: #F78811;">&#40;</span>f<span style="color: #F78811;">&#40;</span>a<span style="color: #F78811;">&#41;</span> + f<span style="color: #F78811;">&#40;</span>b<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span><span style="color: #000080;">_</span>, <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> hn <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>b - a<span style="color: #F78811;">&#41;</span> / pow<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2.0</span>, n<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> s <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>k <span style="color: #000080;">&lt;</span> - <span style="color: #F78811;">1</span> until pow<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2</span>, n-<span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span>
    f<span style="color: #F78811;">&#40;</span>a + hn <span style="color: #000080;">*</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2.0</span> <span style="color: #000080;">*</span> k - <span style="color: #F78811;">1.0</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">0.5</span> <span style="color: #000080;">*</span> R<span style="color: #F78811;">&#40;</span>n - <span style="color: #F78811;">1</span>, <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> + hn <span style="color: #000080;">*</span> s.<span style="color: #000000;">sum</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span><span style="color: #000080;">_</span>, <span style="color: #000080;">_</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> q4m <span style="color: #000080;">=</span> pow<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">4.0</span>, m<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> frac <span style="color: #000080;">=</span> <span style="color: #F78811;">1.0</span> / <span style="color: #F78811;">&#40;</span>q4m - <span style="color: #F78811;">1.0</span><span style="color: #F78811;">&#41;</span>
    frac <span style="color: #000080;">*</span> <span style="color: #F78811;">&#40;</span>q4m <span style="color: #000080;">*</span> R<span style="color: #F78811;">&#40;</span>n, m - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span> - R<span style="color: #F78811;">&#40;</span>n - <span style="color: #F78811;">1</span>, m - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    R<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">20</span>, <span style="color: #F78811;">5</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> f<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Double<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Double <span style="color: #000080;">=</span> x <span style="color: #000080;">*</span> x + <span style="color: #F78811;">2</span> <span style="color: #000080;">*</span> x + <span style="color: #F78811;">1</span>
    &nbsp;
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> r <span style="color: #000080;">=</span> romberg<span style="color: #F78811;">&#40;</span>f, <span style="color: #F78811;">0</span>, <span style="color: #F78811;">5</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Integral de x * x + 2 * x + 1 em [0, 5] = &quot;</span> + r<span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">import math.pow
    
    def romberg(f: Double =&gt; Double, a: Double, b: Double): Double = {
    def R(n: Int, m: Int): Double = (n, m) match {
    case (0, 0) =&gt; {
    0.5 * (b - a) * (f(a) + f(b))
    }
    case (_, 0) =&gt; {
    val hn = (b - a) / pow(2.0, n)
    val s = for (k &lt; - 1 until pow(2, n-1).toInt) yield
    f(a + hn * (2.0 * k - 1.0))
    0.5 * R(n - 1, 0) + hn * s.sum
    }
    case (_, _) =&gt; {
    val q4m = pow(4.0, m)
    val frac = 1.0 / (q4m - 1.0)
    frac * (q4m * R(n, m - 1) - R(n - 1, m - 1))
    }
    }
    R(20, 5)
    }
    
    def f(x: Double): Double = x * x + 2 * x + 1
    
    
    val r = romberg(f, 0, 5)
    println(&quot;Integral de x * x + 2 * x + 1 em [0, 5] = &quot; + r)</p></div>
    ";}
categories:
  - Scala Notes
---
In numerical analysis, Romberg&#8217;s method (Romberg 1955) is a numerical approach used to estimate the definite integral \(\int_a^b f(x) dx\).

<pre lang="scala">import math.pow

def romberg(f: Double => Double, a: Double, b: Double): Double = {
  def R(n: Int, m: Int): Double = (n, m) match {
    case (0, 0) => {
      0.5 * (b - a) * (f(a) + f(b))
    }
    case (_, 0) => {
      val hn = (b - a) / pow(2.0, n)
      val s = for (k &lt; - 1 until pow(2, n-1).toInt) yield 
        f(a + hn * (2.0 * k - 1.0))
      0.5 * R(n - 1, 0) + hn * s.sum
    }
    case (_, _) => {
      val q4m = pow(4.0, m)
      val frac = 1.0 / (q4m - 1.0)
      frac * (q4m * R(n, m - 1) - R(n - 1, m - 1))
    }
  }
  R(20, 5)
}

def f(x: Double): Double = x * x + 2 * x + 1 


val r = romberg(f, 0, 5)
println("Integral de x * x + 2 * x + 1 em [0, 5] = " + r)</pre>
