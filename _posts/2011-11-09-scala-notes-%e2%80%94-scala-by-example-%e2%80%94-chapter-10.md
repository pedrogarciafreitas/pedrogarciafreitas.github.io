---
id: 1453
title: Scala by Example — Chapter 10
date: 2011-11-09T08:36:29+00:00
author: CKPYT
excerpt: "Exercises solutions of the book 'Scala by Example'."
layout: post
guid: http://www.sawp.com.br/blog/?p=1453
permalink: p=1453
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:5446:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 10.1.1 Write the function
    *
    * def isSafe(col: Int, queens: List[Int], delta: Int): Boolean
    *
    * which tests whether a queen in the given column col is safe with respect to
    * the queens already placed. Here, delta is the difference between the row of
    * the queen to be placed and the row of the first queen in the list.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> queens<span style="color: #F78811;">&#40;</span>n<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> placeQueens<span style="color: #F78811;">&#40;</span>k<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>k <span style="color: #000080;">==</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> List<span style="color: #F78811;">&#40;</span>List<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#123;</span>queens <span style="color: #000080;">&lt;</span> - placeQueens<span style="color: #F78811;">&#40;</span>k - <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    column <span style="color: #000080;">&lt;</span>- List.<span style="color: #000000;">range</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span>, n + <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> isSafe<span style="color: #F78811;">&#40;</span>column, queens, <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> column <span style="color: #000080;">::</span> queens
    placeQueens<span style="color: #F78811;">&#40;</span>n<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> isSafe<span style="color: #F78811;">&#40;</span>col<span style="color: #000080;">:</span> Int, queens<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span>, delta<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> queens <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> h <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> <span style="color: #000080;">!</span><span style="color: #F78811;">&#40;</span>h <span style="color: #000080;">==</span> col<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&amp;&amp;</span> abs<span style="color: #F78811;">&#40;</span>h - col<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&amp;&amp;</span> ifSafe<span style="color: #F78811;">&#40;</span>col, t, delta + <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 10.1.1 Write the function
    *
    * def isSafe(col: Int, queens: List[Int], delta: Int): Boolean
    *
    * which tests whether a queen in the given column col is safe with respect to
    * the queens already placed. Here, delta is the difference between the row of
    * the queen to be placed and the row of the first queen in the list.
    */
    
    def queens(n: Int): List[List[Int]] = {
    def placeQueens(k: Int): List[List[Int]] =
    if (k == 0) List(List())
    else
    for {queens &lt; - placeQueens(k - 1)
    column &lt;- List.range(1, n + 1)
    if isSafe(column, queens, 1) } yield column :: queens
    placeQueens(n)
    }
    
    def isSafe(col: Int, queens: List[Int], delta: Int): Boolean = queens match {
    case Nil    =&gt; true
    case h :: t =&gt; !(h == col) &amp;&amp; abs(h - col) &amp;&amp; ifSafe(col, t, delta + 1)
    }</p></div>
    ;i:2;s:1589:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 10.3.1 Define the following function in terms of for.
    *
    * def flatten[A](xss: List[List[A]]): List[A] =
    *   (xss :\ (Nil: List[A])) ((xs, ys) =&gt; xs ::: ys)
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> flatten<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>xss<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>List<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&lt;</span> - xss<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> x</pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 10.3.1 Define the following function in terms of for.
    *
    * def flatten[A](xss: List[List[A]]): List[A] =
    *   (xss :\ (Nil: List[A])) ((xs, ys) =&gt; xs ::: ys)
    */
    def flatten[A](xss: List[List[A]]): List[A] =
    for (x &lt; - xss) yield x</p></div>
    ;i:3;s:4642:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 10.3.2 Translate
    *
    * for (b &lt; - books; a &lt;- b.authors if a startsWith &quot;Bird&quot;) yield b.title
    * for (b &lt;- books if (b.title indexOf &quot;Program&quot;) &gt;= 0) yield b.title
    *
    * to higher-order functions.
    */</span>
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/*
    supose class Book(title: String, authors: String*)
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> filterBirds<span style="color: #F78811;">&#40;</span>books<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Book<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> books <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span> Nil
    <span style="color: #0000ff; font-weight: bold;">case</span> h <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>h.<span style="color: #000000;">authors</span> startsWith <span style="color: #6666FF;">&quot;Bird&quot;</span><span style="color: #F78811;">&#41;</span>
    h.<span style="color: #000000;">title</span> <span style="color: #000080;">::</span> filterBirds<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span>
    filterBirds<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> filterProgramBooks<span style="color: #F78811;">&#40;</span>books<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Book<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> books <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span> Nil
    <span style="color: #0000ff; font-weight: bold;">case</span> h <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>h.<span style="color: #000000;">title</span> indexOf <span style="color: #6666FF;">&quot;Program&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&gt;=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    h.<span style="color: #000000;">title</span> <span style="color: #000080;">::</span> filterProgramBooks<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span>
    filterProgramBooks<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 10.3.2 Translate
    *
    * for (b &lt; - books; a &lt;- b.authors if a startsWith &quot;Bird&quot;) yield b.title
    * for (b &lt;- books if (b.title indexOf &quot;Program&quot;) &gt;= 0) yield b.title
    *
    * to higher-order functions.
    */
    
    /*
    supose class Book(title: String, authors: String*)
    */
    
    def filterBirds(books: List[Book]): List[String] = books match {
    case Nil    =&gt; Nil
    case h :: t =&gt;
    if (h.authors startsWith &quot;Bird&quot;)
    h.title :: filterBirds(t)
    else
    filterBirds(t)
    }
    
    def filterProgramBooks(books: List[Book]): List[String] = books match {
    case Nil    =&gt; Nil
    case h :: t =&gt;
    if ((h.title indexOf &quot;Program&quot;) &gt;= 0)
    h.title :: filterProgramBooks(t)
    else
    filterProgramBooks(t)
    }</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 10.1.1 Write the function
 *
 * def isSafe(col: Int, queens: List[Int], delta: Int): Boolean
 *
 * which tests whether a queen in the given column col is safe with respect to
 * the queens already placed. Here, delta is the difference between the row of
 * the queen to be placed and the row of the first queen in the list.
 */

def queens(n: Int): List[List[Int]] = {
  def placeQueens(k: Int): List[List[Int]] =
    if (k == 0) List(List())
    else
      for {queens &lt; - placeQueens(k - 1)
           column &lt;- List.range(1, n + 1)
        if isSafe(column, queens, 1) } yield column :: queens
    placeQueens(n)
}

def isSafe(col: Int, queens: List[Int], delta: Int): Boolean = queens match {
  case Nil    => true
  case h :: t => !(h == col) && abs(h - col) && ifSafe(col, t, delta + 1)
}</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 10.3.1 Define the following function in terms of for.
 *
 * def flatten[A](xss: List[List[A]]): List[A] =
 *   (xss :\ (Nil: List[A])) ((xs, ys) => xs ::: ys)
 */
def flatten[A](xss: List[List[A]]): List[A] =
  for (x &lt; - xss) yield x</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 10.3.2 Translate
 *
 * for (b &lt; - books; a &lt;- b.authors if a startsWith "Bird") yield b.title
 * for (b &lt;- books if (b.title indexOf "Program") >= 0) yield b.title
 *
 * to higher-order functions.
 */

/*
 supose class Book(title: String, authors: String*)
*/

def filterBirds(books: List[Book]): List[String] = books match {
  case Nil    => Nil
  case h :: t =>
    if (h.authors startsWith "Bird")
      h.title :: filterBirds(t)
    else
      filterBirds(t)
}

def filterProgramBooks(books: List[Book]): List[String] = books match {
  case Nil    => Nil
  case h :: t =>
    if ((h.title indexOf "Program") >= 0)
      h.title :: filterProgramBooks(t)
    else
      filterProgramBooks(t)
}</pre>
