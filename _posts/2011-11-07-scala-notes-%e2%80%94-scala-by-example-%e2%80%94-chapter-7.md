---
id: 1444
title: Scala by Example — Chapter 07
date: 2011-11-07T21:01:05+00:00
author: CKPYT
excerpt: "Exercises solutions of the book 'Scala by Example'."
layout: post
guid: http://www.sawp.com.br/blog/?p=1444
permalink: p=1444
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:7136:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 7.2.2 Consider the following definitions representing trees of
    * integers. These definitions can be seen as an alternative representation of
    * IntSet:
    *
    *    abstract class IntTree
    *    case object EmptyTree extends IntTree
    *    case class Node(elem: Int, left: IntTree, right: IntTree) extends IntTree
    *
    * Complete the following implementations of function contains and insert for
    * IntTree's.
    *
    *    def contains(t: IntTree, v: Int): Boolean = t match {}
    *    def insert(t: IntTree, v: Int): IntTree = t match {}
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> IntTree
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">object</span> EmptyTree <span style="color: #0000ff; font-weight: bold;">extends</span> IntTree
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Node<span style="color: #F78811;">&#40;</span>elem<span style="color: #000080;">:</span> Int, left<span style="color: #000080;">:</span> IntTree, right<span style="color: #000080;">:</span> IntTree<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> IntTree
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> contains<span style="color: #F78811;">&#40;</span>t<span style="color: #000080;">:</span> IntTree, v<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> t <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> EmptyTree                           <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>elem, <span style="color: #000080;">_</span>, <span style="color: #000080;">_</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>elem <span style="color: #000080;">==</span> v<span style="color: #F78811;">&#41;</span>     <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>elem, left, <span style="color: #000080;">_</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>elem <span style="color: #000080;">&lt;</span> v<span style="color: #F78811;">&#41;</span>   <span style="color: #000080;">=&gt;</span> contains<span style="color: #F78811;">&#40;</span>left, v<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>elem, <span style="color: #000080;">_</span>, right<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>elem <span style="color: #000080;">&gt;</span> v<span style="color: #F78811;">&#41;</span>  <span style="color: #000080;">=&gt;</span> contains<span style="color: #F78811;">&#40;</span>right, v<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> insert<span style="color: #F78811;">&#40;</span>t<span style="color: #000080;">:</span> IntTree, v<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntTree <span style="color: #000080;">=</span> t <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> EmptyTree <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">new</span> Node<span style="color: #F78811;">&#40;</span>v, EmptyTree, EmptyTree<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>elem, left, <span style="color: #000080;">_</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>v <span style="color: #000080;">&lt;</span> elem<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">new</span> Node<span style="color: #F78811;">&#40;</span>elem, insert<span style="color: #F78811;">&#40;</span>left, v<span style="color: #F78811;">&#41;</span>, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>elem, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">new</span> Node<span style="color: #F78811;">&#40;</span>elem, left, insert<span style="color: #F78811;">&#40;</span>right, v<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 7.2.2 Consider the following definitions representing trees of
    * integers. These definitions can be seen as an alternative representation of
    * IntSet:
    *
    *    abstract class IntTree
    *    case object EmptyTree extends IntTree
    *    case class Node(elem: Int, left: IntTree, right: IntTree) extends IntTree
    *
    * Complete the following implementations of function contains and insert for
    * IntTree's.
    *
    *    def contains(t: IntTree, v: Int): Boolean = t match {}
    *    def insert(t: IntTree, v: Int): IntTree = t match {}
    */
    
    abstract class IntTree
    case object EmptyTree extends IntTree
    case class Node(elem: Int, left: IntTree, right: IntTree) extends IntTree
    
    def contains(t: IntTree, v: Int): Boolean = t match {
    case EmptyTree                           =&gt; false
    case Node(elem, _, _) if (elem == v)     =&gt; true
    case Node(elem, left, _) if (elem &lt; v)   =&gt; contains(left, v)
    case Node(elem, _, right) if (elem &gt; v)  =&gt; contains(right, v)
    }
    
    def insert(t: IntTree, v: Int): IntTree = t match {
    case EmptyTree =&gt; new Node(v, EmptyTree, EmptyTree)
    case Node(elem, left, _) if (v &lt; elem) =&gt; new Node(elem, insert(left, v), right)
    case Node(elem, left, right) =&gt; new Node(elem, left, insert(right, v))
    }</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 7.2.2 Consider the following definitions representing trees of
 * integers. These definitions can be seen as an alternative representation of
 * IntSet:
 *
 *    abstract class IntTree
 *    case object EmptyTree extends IntTree
 *    case class Node(elem: Int, left: IntTree, right: IntTree) extends IntTree
 *
 * Complete the following implementations of function contains and insert for
 * IntTree's.
 *
 *    def contains(t: IntTree, v: Int): Boolean = t match {}
 *    def insert(t: IntTree, v: Int): IntTree = t match {}
 */

abstract class IntTree
case object EmptyTree extends IntTree
case class Node(elem: Int, left: IntTree, right: IntTree) extends IntTree

def contains(t: IntTree, v: Int): Boolean = t match {
  case EmptyTree                           => false
  case Node(elem, _, _) if (elem == v)     => true
  case Node(elem, left, _) if (elem &lt; v)   => contains(left, v)
  case Node(elem, _, right) if (elem > v)  => contains(right, v)
}

def insert(t: IntTree, v: Int): IntTree = t match {
  case EmptyTree => new Node(v, EmptyTree, EmptyTree)
  case Node(elem, left, _) if (v &lt; elem) => new Node(elem, insert(left, v), right)
  case Node(elem, left, right) => new Node(elem, left, insert(right, v))
}</pre>
