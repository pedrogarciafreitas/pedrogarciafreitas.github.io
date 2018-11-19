---
id: 1458
title: Scala by Example — Chapter 11
date: 2011-11-09T08:40:26+00:00
author: CKPYT
excerpt: "Exercises solutions of the book 'Scala by Example'."
layout: post
guid: http://www.sawp.com.br/blog/?p=1458
permalink: p=1458
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:2624:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 11.2.1 Write a function repeatLoop, which should be applied as follows:
    *
    *    repeatLoop { command } ( condition )
    *
    * Is there also a way to obtain a loop syntax like the following?
    *
    *    repeatLoop { command } until ( condition )
    */</span>
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/*
    The repeatLoop is implemented as
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> repeatLoop<span style="color: #F78811;">&#40;</span>command<span style="color: #000080;">:</span> <span style="color: #000080;">=&gt;</span> Unit<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>condition<span style="color: #000080;">:</span> <span style="color: #000080;">=&gt;</span> Boolen<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>condition<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    command
    repeatLoop <span style="color: #F78811;">&#40;</span>command<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#40;</span>condition<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/*
    We can extend this command with until command
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> until<span style="color: #F78811;">&#40;</span>condition<span style="color: #000080;">:</span> <span style="color: #000080;">=&gt;</span> Boolean<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #000080;">!</span>condition</pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 11.2.1 Write a function repeatLoop, which should be applied as follows:
    *
    *    repeatLoop { command } ( condition )
    *
    * Is there also a way to obtain a loop syntax like the following?
    *
    *    repeatLoop { command } until ( condition )
    */
    
    /*
    The repeatLoop is implemented as
    */
    def repeatLoop(command: =&gt; Unit)(condition: =&gt; Boolen) =
    if (condition) {
    command
    repeatLoop (command) (condition)
    }
    
    /*
    We can extend this command with until command
    */
    def until(condition: =&gt; Boolean): Boolean = !condition</p></div>
    ;i:2;s:2133:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 11.3.1 Write the implementation of orGate.
    */</span>
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/*
    Following the style of andGate, we have
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> orGate<span style="color: #F78811;">&#40;</span>a1<span style="color: #000080;">:</span> Wire, a2<span style="color: #000080;">:</span> Wire, output<span style="color: #000080;">:</span> Wire<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> orAction<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> a1Sig <span style="color: #000080;">=</span> a1.<span style="color: #000000;">getSignal</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> a2Sig <span style="color: #000080;">=</span> a2.<span style="color: #000000;">getSignal</span>
    afterDelay<span style="color: #F78811;">&#40;</span>orGateDelay<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    output setSignal <span style="color: #F78811;">&#40;</span>a1Sig | a2Sig<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    a1 addAction orAction
    a2 addAction orAction
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 11.3.1 Write the implementation of orGate.
    */
    
    /*
    Following the style of andGate, we have
    */
    def orGate(a1: Wire, a2: Wire, output: Wire) {
    def orAction() {
    val a1Sig = a1.getSignal
    val a2Sig = a2.getSignal
    afterDelay(orGateDelay) {
    output setSignal (a1Sig | a2Sig)
    }
    }
    a1 addAction orAction
    a2 addAction orAction
    }</p></div>
    ;i:3;s:1707:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 11.3.2 Another way is to define an or-gate by a combination of
    * inverters and and gates. Define a function orGate in terms of andGate and
    * inverter. What is the delay time of this function?
    */</span>
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/*
    The book define the inverter function. So, we can use the De Morgan theorem
    to make a orGate in terms of andGate:
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> orGate<span style="color: #F78811;">&#40;</span>a1<span style="color: #000080;">:</span> Wire, a2<span style="color: #000080;">:</span> Wire, output<span style="color: #000080;">:</span> Wire<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    inverter<span style="color: #F78811;">&#40;</span>a1, output<span style="color: #F78811;">&#41;</span>
    andGate<span style="color: #F78811;">&#40;</span>a1, a2, output<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 11.3.2 Another way is to define an or-gate by a combination of
    * inverters and and gates. Define a function orGate in terms of andGate and
    * inverter. What is the delay time of this function?
    */
    
    /*
    The book define the inverter function. So, we can use the De Morgan theorem
    to make a orGate in terms of andGate:
    */
    def orGate(a1: Wire, a2: Wire, output: Wire) {
    inverter(a1, output)
    andGate(a1, a2, output)
    }</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 11.2.1 Write a function repeatLoop, which should be applied as follows:
 *
 *    repeatLoop { command } ( condition )
 * 
 * Is there also a way to obtain a loop syntax like the following?
 * 
 *    repeatLoop { command } until ( condition )
*/

/*
  The repeatLoop is implemented as
*/
def repeatLoop(command: => Unit)(condition: => Boolen) =
  if (condition) {
    command
    repeatLoop (command) (condition)
  }

/*
  We can extend this command with until command
*/
def until(condition: => Boolean): Boolean = !condition</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 11.3.1 Write the implementation of orGate.
 */

/*
  Following the style of andGate, we have
*/
def orGate(a1: Wire, a2: Wire, output: Wire) {
  def orAction() {
    val a1Sig = a1.getSignal
    val a2Sig = a2.getSignal
    afterDelay(orGateDelay) {
      output setSignal (a1Sig | a2Sig)
    }
  }
  a1 addAction orAction
  a2 addAction orAction
}</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 11.3.2 Another way is to define an or-gate by a combination of
 * inverters and and gates. Define a function orGate in terms of andGate and
 * inverter. What is the delay time of this function?
 */

/*
  The book define the inverter function. So, we can use the De Morgan theorem
  to make a orGate in terms of andGate:
*/
def orGate(a1: Wire, a2: Wire, output: Wire) {
  inverter(a1, output)
  andGate(a1, a2, output)
}</pre>
