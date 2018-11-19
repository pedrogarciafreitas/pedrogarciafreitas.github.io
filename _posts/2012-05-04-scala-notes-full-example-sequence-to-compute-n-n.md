---
id: 1505
title: 'Full Example — Sequence to Compute n * n'
date: 2012-05-04T01:32:00+00:00
author: SAWP
excerpt: Calculating square using sums.
layout: post
guid: http://www.sawp.com.br/blog/?p=1505
permalink: p=1505
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3357:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">def</span> square<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> sq<span style="color: #F78811;">&#40;</span>y<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> y <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">0</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">1</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">1</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">val</span> y2 <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span> to <span style="color: #F78811;">&#40;</span>y - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">reduceLeft</span><span style="color: #F78811;">&#40;</span> <span style="color: #000080;">_</span> + <span style="color: #000080;">_</span> <span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    y + y2 + y2
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> z <span style="color: #000080;">=</span> Math.<span style="color: #000000;">abs</span><span style="color: #F78811;">&#40;</span>x<span style="color: #F78811;">&#41;</span>
    sq<span style="color: #F78811;">&#40;</span>z<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">&lt;</span> - -<span style="color: #F78811;">20</span> to <span style="color: #F78811;">20</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span>square<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">def square(x: Int): Int = {
    def sq(y: Int): Int = y match {
    case 0 =&gt; 0
    case 1 =&gt; 1
    case _ =&gt; val y2 = ((1 to (y - 1)).reduceLeft( _ + _ ))
    y + y2 + y2
    }
    val z = Math.abs(x)
    sq(z)
    }
    
    for (i &lt; - -20 to 20) {
    println(square(i))
    }</p></div>
    ";}
categories:
  - Scala Notes
---
The square \(n*n\) can be computed using the following sequence:
  


<center>
  <br /> \( n^2 = n + 2 \sum_{i=0}^{n-1} i\)<br />
</center>

In scala:

<pre lang="scala">def square(x: Int): Int = {
  def sq(y: Int): Int = y match {
    case 0 => 0
    case 1 => 1
    case _ => val y2 = ((1 to (y - 1)).reduceLeft( _ + _ ))
              y + y2 + y2
  }
  val z = Math.abs(x)
  sq(z)
}

for (i &lt; - -20 to 20) {
  println(square(i))
}</pre>
