---
id: 1441
title: Scala by Example — Chapter 06
date: 2011-11-07T20:40:44+00:00
author: CKPYT
excerpt: "Exercises solutions of the book 'Scala by Example'."
layout: post
guid: http://www.sawp.com.br/blog/?p=1441
permalink: /p=1441
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:9133:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 6.0.1 Write methods union and intersection to form the union and
    * intersection between two sets.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">trait</span> IntSet <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> incl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet
    <span style="color: #0000ff; font-weight: bold;">def</span> contains<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean
    <span style="color: #0000ff; font-weight: bold;">def</span> union<span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet
    <span style="color: #0000ff; font-weight: bold;">def</span> intersect<span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">class</span> EmptySet <span style="color: #0000ff; font-weight: bold;">extends</span> IntSet <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> contains<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> incl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>x, <span style="color: #0000ff; font-weight: bold;">new</span> EmptySet, <span style="color: #0000ff; font-weight: bold;">new</span> EmptySet<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> union<span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> other
    <span style="color: #0000ff; font-weight: bold;">def</span> intersect<span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">class</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem<span style="color: #000080;">:</span> Int, left<span style="color: #000080;">:</span> IntSet, right<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> IntSet <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> contains<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&lt;</span> elem<span style="color: #F78811;">&#41;</span> left contains x
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&gt;</span> elem<span style="color: #F78811;">&#41;</span> right contains x
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> incl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&lt;</span> elem<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem, left incl x, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&gt;</span> elem<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem, left, right incl x<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> + <span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> Intset<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> newSet <span style="color: #000080;">=</span> left + right + other
    newSet incl elem
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> union<span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">this</span> + other
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> intersect<span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> rght <span style="color: #000080;">=</span> right intersect other
    <span style="color: #0000ff; font-weight: bold;">val</span> lft <span style="color: #000080;">=</span> left intersect other
    <span style="color: #0000ff; font-weight: bold;">val</span> newSet <span style="color: #000080;">=</span> lft union rght
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>other contains elem<span style="color: #F78811;">&#41;</span>
    s incl elem
    <span style="color: #0000ff; font-weight: bold;">else</span>
    s
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 6.0.1 Write methods union and intersection to form the union and
    * intersection between two sets.
    */
    
    trait IntSet {
    def incl(x: Int): IntSet
    def contains(x: Int): Boolean
    def union(other: IntSet): IntSet
    def intersect(other: IntSet): IntSet
    }
    
    class EmptySet extends IntSet {
    def contains(x: Int): Boolean = false
    def incl(x: Int): IntSet = new NonEmptySet(x, new EmptySet, new EmptySet)
    def union(other: IntSet): IntSet = other
    def intersect(other: IntSet): IntSet = this
    }
    
    class NonEmptySet(elem: Int, left: IntSet, right: IntSet) extends IntSet {
    def contains(x: Int): Boolean =
    if (x &lt; elem) left contains x
    else if (x &gt; elem) right contains x
    else true
    def incl(x: Int): IntSet =
    if (x &lt; elem) new NonEmptySet(elem, left incl x, right)
    else if (x &gt; elem) new NonEmptySet(elem, left, right incl x)
    else this
    def + (other: Intset): IntSet = {
    val newSet = left + right + other
    newSet incl elem
    }
    
    def union(other: IntSet): IntSet = this + other
    
    def intersect(other: IntSet): IntSet = {
    val rght = right intersect other
    val lft = left intersect other
    val newSet = lft union rght
    
    if (other contains elem)
    s incl elem
    else
    s
    }
    }</p></div>
    ;i:2;s:9072:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 6.0.2 Add a method
    *    def excl(x: Int)
    * to return the given set without the element x. To accomplish this, it is
    * useful to also implement a test method
    *    def isEmpty: Boolean
    * for sets.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">trait</span> IntSet <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> incl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet
    <span style="color: #0000ff; font-weight: bold;">def</span> contains<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean
    <span style="color: #0000ff; font-weight: bold;">def</span> excl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet
    <span style="color: #0000ff; font-weight: bold;">def</span> isEmpty<span style="color: #000080;">:</span> Boolean
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">class</span> EmptySet <span style="color: #0000ff; font-weight: bold;">extends</span> IntSet <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> contains<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> incl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>x, <span style="color: #0000ff; font-weight: bold;">new</span> EmptySet, <span style="color: #0000ff; font-weight: bold;">new</span> EmptySet<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> excl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> isEmpty<span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">class</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem<span style="color: #000080;">:</span> Int, left<span style="color: #000080;">:</span> IntSet, right<span style="color: #000080;">:</span> IntSet<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> IntSet <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> contains<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&lt;</span> elem<span style="color: #F78811;">&#41;</span> left contains x
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&gt;</span> elem<span style="color: #F78811;">&#41;</span> right contains x
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> incl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&lt;</span> elem<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem, left incl x, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&gt;</span> elem<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem, left, right incl x<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> + <span style="color: #F78811;">&#40;</span>other<span style="color: #000080;">:</span> Intset<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> newSet <span style="color: #000080;">=</span> left + right + other
    newSet incl elem
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> isEmpty<span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> excl<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> IntSet <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&lt;</span> elem<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem, left excl x, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&gt;</span> elem<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> NonEmptySet<span style="color: #F78811;">&#40;</span>elem, left, right excl x<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span>
    left append right
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 6.0.2 Add a method
    *    def excl(x: Int)
    * to return the given set without the element x. To accomplish this, it is
    * useful to also implement a test method
    *    def isEmpty: Boolean
    * for sets.
    */
    
    trait IntSet {
    def incl(x: Int): IntSet
    def contains(x: Int): Boolean
    def excl(x: Int): IntSet
    def isEmpty: Boolean
    }
    
    class EmptySet extends IntSet {
    def contains(x: Int): Boolean = false
    def incl(x: Int): IntSet = new NonEmptySet(x, new EmptySet, new EmptySet)
    def excl(x: Int): IntSet = this
    def isEmpty: Boolean = true
    }
    
    class NonEmptySet(elem: Int, left: IntSet, right: IntSet) extends IntSet {
    def contains(x: Int): Boolean =
    if (x &lt; elem) left contains x
    else if (x &gt; elem) right contains x
    else true
    
    def incl(x: Int): IntSet =
    if (x &lt; elem) new NonEmptySet(elem, left incl x, right)
    else if (x &gt; elem) new NonEmptySet(elem, left, right incl x)
    else this
    
    def + (other: Intset): IntSet = {
    val newSet = left + right + other
    newSet incl elem
    }
    
    def isEmpty: Boolean = false
    
    def excl(x: Int): IntSet =
    if (x &lt; elem)
    new NonEmptySet(elem, left excl x, right)
    else if (x &gt; elem)
    new NonEmptySet(elem, left, right excl x)
    else
    left append right
    }</p></div>
    ;i:3;s:9851:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 6.0.3 Write an implementation Integer of integer numbers The
    * implementation should support all operations of class Nat while adding two
    * methods.
    *
    *      def isPositive: Boolean
    *      def negate: Integer
    *
    * The first method should return true if the number is positive. The second
    * method should negate the number. Do not use any of Scala’s standard numeric
    * classes in your implementation. (Hint: There are two possible ways to
    * implement Integer. One can either make use the existing implementation of
    * Nat, representing an integer as a natural number and a sign. Or one can
    * generalize the given implementation of Nat to Integer, using the three
    * subclasses Zero for 0, Succ for positive numbers and Pred for negative
    * numbers.)
    */</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// APENAS REESCREVE AS FUNÇÕES, SEGUINDO O PADRÃO DE NAT</span>
    <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Nat <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> isZero<span style="color: #000080;">:</span> Boolean
    <span style="color: #0000ff; font-weight: bold;">def</span> predecessor<span style="color: #000080;">:</span> Nat
    <span style="color: #0000ff; font-weight: bold;">def</span> successor<span style="color: #000080;">:</span> Nat
    <span style="color: #0000ff; font-weight: bold;">def</span> + <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> Nat<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Nat
    <span style="color: #0000ff; font-weight: bold;">def</span> - <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> Nat<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Nat
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Integer <span style="color: #0000ff; font-weight: bold;">extends</span> Nat <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">protected</span> <span style="color: #0000ff; font-weight: bold;">val</span> sign<span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> isPositive <span style="color: #000080;">=</span> sign
    <span style="color: #0000ff; font-weight: bold;">def</span> negate <span style="color: #000080;">=</span> <span style="color: #000080;">!</span>sign
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// exemplo de uso da definição</span>
    <span style="color: #0000ff; font-weight: bold;">class</span> Succ<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Nat<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Nat <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> isZero<span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> predecessor<span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> x
    <span style="color: #0000ff; font-weight: bold;">def</span> successor<span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Succ<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">this</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> + <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> Nat<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> x + that.<span style="color: #000000;">successor</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> - <span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> Nat<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>that.<span style="color: #000000;">isZero</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> x - that.<span style="color: #000000;">predecessor</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">object</span> ZeroInteger <span style="color: #0000ff; font-weight: bold;">extends</span> Integer <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> isZero<span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> predecessor<span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">new</span> Succ<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">this</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">negate</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> successor<span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Succ<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">this</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> +<span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> Nat<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> that
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> -<span style="color: #F78811;">&#40;</span>that<span style="color: #000080;">:</span> Nat<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> that.<span style="color: #000000;">negate</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> isPositive<span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> negate<span style="color: #000080;">:</span> Nat <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">this</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 6.0.3 Write an implementation Integer of integer numbers The
    * implementation should support all operations of class Nat while adding two
    * methods.
    *
    *      def isPositive: Boolean
    *      def negate: Integer
    *
    * The first method should return true if the number is positive. The second
    * method should negate the number. Do not use any of Scala’s standard numeric
    * classes in your implementation. (Hint: There are two possible ways to
    * implement Integer. One can either make use the existing implementation of
    * Nat, representing an integer as a natural number and a sign. Or one can
    * generalize the given implementation of Nat to Integer, using the three
    * subclasses Zero for 0, Succ for positive numbers and Pred for negative
    * numbers.)
    */
    
    // APENAS REESCREVE AS FUNÇÕES, SEGUINDO O PADRÃO DE NAT
    abstract class Nat {
    def isZero: Boolean
    def predecessor: Nat
    def successor: Nat
    def + (that: Nat): Nat
    def - (that: Nat): Nat
    }
    
    abstract class Integer extends Nat {
    protected val sign: Boolean = true
    def isPositive = sign
    def negate = !sign
    }
    
    // exemplo de uso da definição
    class Succ(x: Nat) extends Nat {
    def isZero: Boolean = false
    def predecessor: Nat = x
    def successor: Nat = new Succ(this)
    def + (that: Nat): Nat = x + that.successor
    def - (that: Nat): Nat = if (that.isZero) this
    else x - that.predecessor
    }
    
    object ZeroInteger extends Integer {
    override def isZero: Boolean = true
    override def predecessor: Nat = (new Succ(this)).negate
    override def successor: Nat = new Succ(this)
    override def +(that: Nat): Nat = that
    override def -(that: Nat): Nat = that.negate
    override def isPositive: Boolean = true
    override def negate: Nat = this
    }</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 6.0.1 Write methods union and intersection to form the union and
 * intersection between two sets.
 */

trait IntSet {
  def incl(x: Int): IntSet
  def contains(x: Int): Boolean
  def union(other: IntSet): IntSet
  def intersect(other: IntSet): IntSet
}

class EmptySet extends IntSet {
  def contains(x: Int): Boolean = false
  def incl(x: Int): IntSet = new NonEmptySet(x, new EmptySet, new EmptySet)
  def union(other: IntSet): IntSet = other
  def intersect(other: IntSet): IntSet = this
}

class NonEmptySet(elem: Int, left: IntSet, right: IntSet) extends IntSet {
  def contains(x: Int): Boolean =
    if (x &lt; elem) left contains x
    else if (x > elem) right contains x
    else true
  def incl(x: Int): IntSet =
    if (x &lt; elem) new NonEmptySet(elem, left incl x, right)
    else if (x > elem) new NonEmptySet(elem, left, right incl x)
    else this
  def + (other: Intset): IntSet = {
    val newSet = left + right + other
    newSet incl elem
  }

  def union(other: IntSet): IntSet = this + other

  def intersect(other: IntSet): IntSet = {
    val rght = right intersect other
    val lft = left intersect other
    val newSet = lft union rght

    if (other contains elem)
      s incl elem
    else
      s
  }
}</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 6.0.2 Add a method
 *    def excl(x: Int)
 * to return the given set without the element x. To accomplish this, it is
 * useful to also implement a test method
 *    def isEmpty: Boolean
 * for sets.
 */

trait IntSet {
  def incl(x: Int): IntSet
  def contains(x: Int): Boolean
  def excl(x: Int): IntSet
  def isEmpty: Boolean
}

class EmptySet extends IntSet {
  def contains(x: Int): Boolean = false
  def incl(x: Int): IntSet = new NonEmptySet(x, new EmptySet, new EmptySet)
  def excl(x: Int): IntSet = this
  def isEmpty: Boolean = true
}

class NonEmptySet(elem: Int, left: IntSet, right: IntSet) extends IntSet {
  def contains(x: Int): Boolean =
    if (x &lt; elem) left contains x
    else if (x > elem) right contains x
    else true

  def incl(x: Int): IntSet =
    if (x &lt; elem) new NonEmptySet(elem, left incl x, right)
    else if (x > elem) new NonEmptySet(elem, left, right incl x)
    else this

  def + (other: Intset): IntSet = {
    val newSet = left + right + other
    newSet incl elem
  }

  def isEmpty: Boolean = false

  def excl(x: Int): IntSet = 
    if (x &lt; elem)
      new NonEmptySet(elem, left excl x, right)
    else if (x > elem)
      new NonEmptySet(elem, left, right excl x)
    else
      left append right
}</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 6.0.3 Write an implementation Integer of integer numbers The
 * implementation should support all operations of class Nat while adding two
 * methods.
 *
 *      def isPositive: Boolean
 *      def negate: Integer
 *
 * The first method should return true if the number is positive. The second
 * method should negate the number. Do not use any of Scala’s standard numeric
 * classes in your implementation. (Hint: There are two possible ways to
 * implement Integer. One can either make use the existing implementation of
 * Nat, representing an integer as a natural number and a sign. Or one can
 * generalize the given implementation of Nat to Integer, using the three
 * subclasses Zero for 0, Succ for positive numbers and Pred for negative 
 * numbers.)
 */

// APENAS REESCREVE AS FUNÇÕES, SEGUINDO O PADRÃO DE NAT
abstract class Nat {
  def isZero: Boolean
  def predecessor: Nat
  def successor: Nat
  def + (that: Nat): Nat
  def - (that: Nat): Nat
}

abstract class Integer extends Nat {
  protected val sign: Boolean = true
  def isPositive = sign
  def negate = !sign
}

// exemplo de uso da definição
class Succ(x: Nat) extends Nat {
  def isZero: Boolean = false
  def predecessor: Nat = x
  def successor: Nat = new Succ(this)
  def + (that: Nat): Nat = x + that.successor
  def - (that: Nat): Nat = if (that.isZero) this
                           else x - that.predecessor
}

object ZeroInteger extends Integer {
  override def isZero: Boolean = true
  override def predecessor: Nat = (new Succ(this)).negate
  override def successor: Nat = new Succ(this)
  override def +(that: Nat): Nat = that
  override def -(that: Nat): Nat = that.negate
  override def isPositive: Boolean = true
  override def negate: Nat = this
}</pre>
