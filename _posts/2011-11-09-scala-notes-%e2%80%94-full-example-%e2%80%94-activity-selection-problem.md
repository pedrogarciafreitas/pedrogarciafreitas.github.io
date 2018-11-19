---
id: 1466
title: Full Example — Activity Selection Problem
date: 2011-11-09T08:45:47+00:00
author: CKPYT
excerpt: An activity-selection is the problem of scheduling a resource among several competing activity.
layout: post
guid: http://www.sawp.com.br/blog/?p=1466
permalink: /p=1466
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8360:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/*
    * A greedy algorithm for activity selection
    *
    *
    * Author: Pedro Garcia Freitas [sawp@sawp.com.br&gt;]
    * Date: Aug, 2011
    *
    * [Ref] Cormen, Thomas H. &quot;Introduction to Algorithms&quot; -- 3rd ed.
    */</span>
    <span style="color: #0000ff; font-weight: bold;">import</span> scala.<span style="color: #000000;">collection</span>.<span style="color: #000000;">mutable</span>.<span style="color: #000000;">ListBuffer</span>
    &nbsp;
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">class</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">val</span> name<span style="color: #000080;">:</span> String, <span style="color: #0000ff; font-weight: bold;">val</span> start<span style="color: #000080;">:</span> Int, <span style="color: #0000ff; font-weight: bold;">val</span> finish<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> toString <span style="color: #000080;">=</span>
    name + <span style="color: #6666FF;">&quot;[&quot;</span> + start + <span style="color: #6666FF;">&quot;,&quot;</span> + finish + <span style="color: #6666FF;">&quot;]&quot;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> greedy<span style="color: #000080;">_</span>activity<span style="color: #000080;">_</span>selector<span style="color: #F78811;">&#40;</span>ac<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Activity<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Activity<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> k <span style="color: #000080;">=</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> A <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> ListBuffer<span style="color: #F78811;">&#91;</span>Activity<span style="color: #F78811;">&#93;</span>
    A +<span style="color: #000080;">=</span> ac<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>m <span style="color: #000080;">&lt;</span> - <span style="color: #F78811;">1</span> until ac.<span style="color: #000000;">length</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>ac<span style="color: #F78811;">&#40;</span>m<span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">start</span> <span style="color: #000080;">&gt;=</span> ac<span style="color: #F78811;">&#40;</span>k<span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">finish</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    A +<span style="color: #000080;">=</span> ac<span style="color: #F78811;">&#40;</span>m<span style="color: #F78811;">&#41;</span>
    k <span style="color: #000080;">=</span> m
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    A.<span style="color: #000000;">toList</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> activities <span style="color: #000080;">=</span> List<span style="color: #F78811;">&#40;</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Calculus&quot;</span>, <span style="color: #F78811;">1</span>, <span style="color: #F78811;">5</span><span style="color: #F78811;">&#41;</span>,
    <span style="color: #0000ff; font-weight: bold;">new</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Numerical Analysis&quot;</span>, <span style="color: #F78811;">2</span>, <span style="color: #F78811;">4</span><span style="color: #F78811;">&#41;</span>,
    <span style="color: #0000ff; font-weight: bold;">new</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Introduction to Computational Methods&quot;</span>, <span style="color: #F78811;">2</span>, <span style="color: #F78811;">7</span><span style="color: #F78811;">&#41;</span>,
    <span style="color: #0000ff; font-weight: bold;">new</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Physics&quot;</span>, <span style="color: #F78811;">4</span>, <span style="color: #F78811;">6</span><span style="color: #F78811;">&#41;</span>,
    <span style="color: #0000ff; font-weight: bold;">new</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Numerical Methods for Physics&quot;</span>, <span style="color: #F78811;">5</span>, <span style="color: #F78811;">6</span><span style="color: #F78811;">&#41;</span>,
    <span style="color: #0000ff; font-weight: bold;">new</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Algorithms 1&quot;</span>, <span style="color: #F78811;">6</span>, <span style="color: #F78811;">7</span><span style="color: #F78811;">&#41;</span>,
    <span style="color: #0000ff; font-weight: bold;">new</span> Activity<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Operating Systems&quot;</span>, <span style="color: #F78811;">7</span>, <span style="color: #F78811;">9</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>Activities: &quot;</span> + activities<span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span><span style="color: #6666ff; font-weight: bold;">\n</span>Possible Distribution of activities: &quot;</span> +
    greedy<span style="color: #000080;">_</span>activity<span style="color: #000080;">_</span>selector<span style="color: #F78811;">&#40;</span>activities<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
    * A greedy algorithm for activity selection
    *
    *
    * Author: Pedro Garcia Freitas [sawp@sawp.com.br&gt;]
    * Date: Aug, 2011
    *
    * [Ref] Cormen, Thomas H. &quot;Introduction to Algorithms&quot; -- 3rd ed.
    */
    import scala.collection.mutable.ListBuffer
    
    
    class Activity(val name: String, val start: Int, val finish: Int) {
    override def toString =
    name + &quot;[&quot; + start + &quot;,&quot; + finish + &quot;]&quot;
    }
    
    def greedy_activity_selector(ac: List[Activity]): List[Activity] = {
    var k = 0
    val A = new ListBuffer[Activity]
    A += ac(0)
    for (m &lt; - 1 until ac.length) {
    if (ac(m).start &gt;= ac(k).finish) {
    A += ac(m)
    k = m
    }
    }
    A.toList
    }
    
    val activities = List(
    new Activity(&quot;Calculus&quot;, 1, 5),
    new Activity(&quot;Numerical Analysis&quot;, 2, 4),
    new Activity(&quot;Introduction to Computational Methods&quot;, 2, 7),
    new Activity(&quot;Physics&quot;, 4, 6),
    new Activity(&quot;Numerical Methods for Physics&quot;, 5, 6),
    new Activity(&quot;Algorithms 1&quot;, 6, 7),
    new Activity(&quot;Operating Systems&quot;, 7, 9)
    )
    
    println(&quot;\nActivities: &quot; + activities)
    
    println(&quot;\n\nPossible Distribution of activities: &quot; +
    greedy_activity_selector(activities))</p></div>
    ";}
categories:
  - Scala Notes
---
An activity-selection is the problem of scheduling a resource among several competing activity.

<pre lang="scala">/*
 * A greedy algorithm for activity selection
 * 
 * 
 * Author: Pedro Garcia Freitas [sawp@sawp.com.br>]
 * Date: Aug, 2011
 *
 * [Ref] Cormen, Thomas H. "Introduction to Algorithms" -- 3rd ed.
 */
import scala.collection.mutable.ListBuffer


class Activity(val name: String, val start: Int, val finish: Int) {
  override def toString = 
    name + "[" + start + "," + finish + "]"
}

def greedy_activity_selector(ac: List[Activity]): List[Activity] = {
  var k = 0
  val A = new ListBuffer[Activity]
  A += ac(0)
  for (m &lt; - 1 until ac.length) {
    if (ac(m).start >= ac(k).finish) {
      A += ac(m)
      k = m
    }
  }
  A.toList
}

val activities = List(
  new Activity("Calculus", 1, 5),
  new Activity("Numerical Analysis", 2, 4),
  new Activity("Introduction to Computational Methods", 2, 7),
  new Activity("Physics", 4, 6),
  new Activity("Numerical Methods for Physics", 5, 6),
  new Activity("Algorithms 1", 6, 7),
  new Activity("Operating Systems", 7, 9)
)

println("\nActivities: " + activities)

println("\n\nPossible Distribution of activities: " +
  greedy_activity_selector(activities))</pre>
