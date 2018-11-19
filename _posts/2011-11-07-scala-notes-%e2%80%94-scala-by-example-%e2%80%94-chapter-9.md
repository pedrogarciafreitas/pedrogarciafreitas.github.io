---
id: 1446
title: Scala by Example — Chapter 09
date: 2011-11-07T21:09:37+00:00
author: CKPYT
excerpt: "Exercises solutions of the book 'Scala by Example'."
layout: post
guid: http://www.sawp.com.br/blog/?p=1446
permalink: /p=1446
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:4552:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 9.1.1 Provide an implementation of the missing function insert.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> isort<span style="color: #F78811;">&#40;</span>xs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>xs.<span style="color: #000000;">isEmpty</span><span style="color: #F78811;">&#41;</span> Nil
    <span style="color: #0000ff; font-weight: bold;">else</span> insert<span style="color: #F78811;">&#40;</span>xs.<span style="color: #000000;">head</span>, isort<span style="color: #F78811;">&#40;</span>xs.<span style="color: #000000;">tail</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> insert<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> Int, xs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> xs <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil     <span style="color: #000080;">=&gt;</span> List<span style="color: #F78811;">&#40;</span>x<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> t <span style="color: #000080;">::</span> ts <span style="color: #000080;">=&gt;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">&lt;</span> <span style="color: #000080;">=</span> t<span style="color: #F78811;">&#41;</span>
    x <span style="color: #000080;">::</span> xs
    <span style="color: #0000ff; font-weight: bold;">else</span>
    t <span style="color: #000080;">::</span> insert<span style="color: #F78811;">&#40;</span>x, ts<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> testList <span style="color: #000080;">=</span> <span style="color: #F78811;">9</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">3</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">10</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">12</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">1</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">37</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">2</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">200</span> <span style="color: #000080;">::</span> Nil
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Original: &quot;</span> + testList<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Sorted: &quot;</span> + isort<span style="color: #F78811;">&#40;</span>testList<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 9.1.1 Provide an implementation of the missing function insert.
    */
    
    def isort(xs: List[Int]): List[Int] =
    if (xs.isEmpty) Nil
    else insert(xs.head, isort(xs.tail))
    
    def insert(x: Int, xs: List[Int]): List[Int] = xs match {
    case Nil     =&gt; List(x)
    case t :: ts =&gt;
    if (x &lt; = t)
    x :: xs
    else
    t :: insert(x, ts)
    }
    
    val testList = 9 :: 3 :: 10 :: 12 :: 1 :: 37 :: 2 :: 200 :: Nil
    
    println(&quot;Original: &quot; + testList)
    println(&quot;Sorted: &quot; + isort(testList))</p></div>
    ;i:2;s:3420:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 9.2.1 Design a tail-recursive version of length.
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> length<span style="color: #F78811;">&#40;</span>list<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>l<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span>, accumulator<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> l <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span> accumulator
    <span style="color: #0000ff; font-weight: bold;">case</span> h <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> iter<span style="color: #F78811;">&#40;</span>t, accumulator + <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>list, <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// test</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> testList <span style="color: #000080;">=</span>  <span style="color: #F78811;">9</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">3</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">10</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">12</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">1</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">37</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">2</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">200</span> <span style="color: #000080;">::</span> Nil
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Size of list: &quot;</span> + length<span style="color: #F78811;">&#40;</span>testList<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 9.2.1 Design a tail-recursive version of length.
    */
    def length(list: List[Int]): Int = {
    def iter(l: List[Int], accumulator: Int): Int = l match {
    case Nil    =&gt; accumulator
    case h :: t =&gt; iter(t, accumulator + 1)
    }
    iter(list, 0)
    }
    
    
    // test
    val testList =  9 :: 3 :: 10 :: 12 :: 1 :: 37 :: 2 :: 200 :: Nil
    
    println(&quot;Size of list: &quot; + length(testList))</p></div>
    ;i:3;s:3016:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 9.4.1 Consider a function which squares all elements of a list
    * and returns a list with the results. Complete the following two equivalent
    * definitions of squareList.
    *
    *    def squareList(xs: List[Int]): List[Int] = xs match {
    *      case List() =&gt; ??
    *      case y :: ys =&gt; ??
    *    }
    *
    *    def squareList(xs: List[Int]): List[Int] = xs map ??
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> squareList<span style="color: #F78811;">&#40;</span>xs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> xs <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> List<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>  <span style="color: #000080;">=&gt;</span> Nil
    <span style="color: #0000ff; font-weight: bold;">case</span> y <span style="color: #000080;">::</span> ys <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#40;</span>y <span style="color: #000080;">*</span> y<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> ys
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> squareList<span style="color: #F78811;">&#40;</span>xs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> xs map <span style="color: #F78811;">&#40;</span>x <span style="color: #000080;">=&gt;</span> x <span style="color: #000080;">*</span> x<span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 9.4.1 Consider a function which squares all elements of a list
    * and returns a list with the results. Complete the following two equivalent
    * definitions of squareList.
    *
    *    def squareList(xs: List[Int]): List[Int] = xs match {
    *      case List() =&gt; ??
    *      case y :: ys =&gt; ??
    *    }
    *
    *    def squareList(xs: List[Int]): List[Int] = xs map ??
    */
    
    def squareList(xs: List[Int]): List[Int] = xs match {
    case List()  =&gt; Nil
    case y :: ys =&gt; (y * y) :: ys
    }
    
    
    def squareList(xs: List[Int]): List[Int] = xs map (x =&gt; x * x)</p></div>
    ;i:4;s:4585:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 9.4.2 Consider the problem of writing a function flatten, which
    * takes a list of element lists as arguments. The result of flatten should be
    * the concatenation of all element lists into a single list. Here is an
    * implementation of this method in terms of :\.
    *
    * def flatten[A](xs: List[List[A]]): List[A] =
    *   (xs :\ (Nil: List[A])) {(x, xs) =&gt; x ::: xs}
    *
    * Consider replacing the body of flatten by
    *
    *        ((Nil: List[A]) /: xs) ((xs, x) =&gt; xs ::: x)
    *
    * What would be the difference in asymptotic complexity between the two
    * versions of flatten?
    *
    * In fact flatten is predefined together with a set of other userful function
    * in an object called List in the standatd Scala library. It can be accessed
    * from user program by calling List.flatten. Note that flatten is not a method
    * of class List - it would not make sense there, since it applies only to
    * lists of lists, not to all lists in general.
    */</span>
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/*
    In fact, the use of {} vs () doesn't make sintatic or semantic difference.
    In curry model of Scala, both the foldLeft /: and foldRight :\ methods
    define the function as second curry parammeter. So, the version of function
    that use /: can be writen like :\
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> flattenRight<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>xs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>List<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #F78811;">&#40;</span>xs <span style="color: #000080;">:</span>\ <span style="color: #F78811;">&#40;</span>Nil<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span><span style="color: #F78811;">&#40;</span>x, xs<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> x <span style="color: #000080;">:::</span> xs<span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/*
    Note that is the same function, just changing the application of flatten
    function. So, there's no difference in asymptotic complexity between the
    two implementation.
    */</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 9.4.2 Consider the problem of writing a function flatten, which
    * takes a list of element lists as arguments. The result of flatten should be
    * the concatenation of all element lists into a single list. Here is an
    * implementation of this method in terms of :\.
    *
    * def flatten[A](xs: List[List[A]]): List[A] =
    *   (xs :\ (Nil: List[A])) {(x, xs) =&gt; x ::: xs}
    *
    * Consider replacing the body of flatten by
    *
    *        ((Nil: List[A]) /: xs) ((xs, x) =&gt; xs ::: x)
    *
    * What would be the difference in asymptotic complexity between the two
    * versions of flatten?
    *
    * In fact flatten is predefined together with a set of other userful function
    * in an object called List in the standatd Scala library. It can be accessed
    * from user program by calling List.flatten. Note that flatten is not a method
    * of class List - it would not make sense there, since it applies only to
    * lists of lists, not to all lists in general.
    */
    
    /*
    In fact, the use of {} vs () doesn't make sintatic or semantic difference.
    In curry model of Scala, both the foldLeft /: and foldRight :\ methods
    define the function as second curry parammeter. So, the version of function
    that use /: can be writen like :\
    */
    def flattenRight[A](xs: List[List[A]]): List[A] =
    (xs :\ (Nil: List[A])) {(x, xs) =&gt; x ::: xs}
    
    /*
    Note that is the same function, just changing the application of flatten
    function. So, there's no difference in asymptotic complexity between the
    two implementation.
    */</p></div>
    ;i:5;s:3291:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 9.4.3 Fill in the missing expressions to complete the following
    * definitions of some basic list-manipulation operations as fold operations.
    *
    * def mapFun[A, B](xs: List[A], f: A =&gt; B): List[B] =
    *   (xs :\ List[B]()){ ?? }
    *
    * def lengthFun[A](xs: List[A]): int =
    *   (0 /: xs){ ?? }
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> mapFun<span style="color: #F78811;">&#91;</span>A, B<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>xs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span>, f<span style="color: #000080;">:</span> A <span style="color: #000080;">=&gt;</span> B<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>B<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #F78811;">&#40;</span>xs <span style="color: #000080;">:</span>\ List<span style="color: #F78811;">&#91;</span>B<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span><span style="color: #F78811;">&#40;</span>x, fx<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> f<span style="color: #F78811;">&#40;</span>x<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> xs<span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> lengthFun<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>xs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>A<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span>
    <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span> /<span style="color: #000080;">:</span> xs<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span><span style="color: #F78811;">&#40;</span>acc, <span style="color: #000080;">_</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> acc + <span style="color: #F78811;">1</span><span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 9.4.3 Fill in the missing expressions to complete the following
    * definitions of some basic list-manipulation operations as fold operations.
    *
    * def mapFun[A, B](xs: List[A], f: A =&gt; B): List[B] =
    *   (xs :\ List[B]()){ ?? }
    *
    * def lengthFun[A](xs: List[A]): int =
    *   (0 /: xs){ ?? }
    */
    
    def mapFun[A, B](xs: List[A], f: A =&gt; B): List[B] =
    (xs :\ List[B]()){(x, fx) =&gt; f(x) :: xs}
    
    def lengthFun[A](xs: List[A]): Int =
    (0 /: xs){(acc, _) =&gt; acc + 1}</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 9.1.1 Provide an implementation of the missing function insert.
 */

def isort(xs: List[Int]): List[Int] =
  if (xs.isEmpty) Nil
  else insert(xs.head, isort(xs.tail))

def insert(x: Int, xs: List[Int]): List[Int] = xs match {
  case Nil     => List(x)
  case t :: ts => 
    if (x &lt; = t)
      x :: xs
    else
      t :: insert(x, ts)
}

val testList = 9 :: 3 :: 10 :: 12 :: 1 :: 37 :: 2 :: 200 :: Nil

println("Original: " + testList)
println("Sorted: " + isort(testList))
</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 9.2.1 Design a tail-recursive version of length.
 */
def length(list: List[Int]): Int = {
  def iter(l: List[Int], accumulator: Int): Int = l match {
    case Nil    => accumulator
    case h :: t => iter(t, accumulator + 1)
  }
  iter(list, 0)
}


// test
val testList =  9 :: 3 :: 10 :: 12 :: 1 :: 37 :: 2 :: 200 :: Nil

println("Size of list: " + length(testList))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 9.4.1 Consider a function which squares all elements of a list
 * and returns a list with the results. Complete the following two equivalent
 * definitions of squareList.
 *
 *    def squareList(xs: List[Int]): List[Int] = xs match {
 *      case List() => ??
 *      case y :: ys => ??
 *    }
 *
 *    def squareList(xs: List[Int]): List[Int] = xs map ??
 */

def squareList(xs: List[Int]): List[Int] = xs match {
  case List()  => Nil
  case y :: ys => (y * y) :: ys
}


def squareList(xs: List[Int]): List[Int] = xs map (x => x * x)
</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 9.4.2 Consider the problem of writing a function flatten, which
 * takes a list of element lists as arguments. The result of flatten should be
 * the concatenation of all element lists into a single list. Here is an
 * implementation of this method in terms of :\.
 *
 * def flatten[A](xs: List[List[A]]): List[A] =
 *   (xs :\ (Nil: List[A])) {(x, xs) => x ::: xs}
 * 
 * Consider replacing the body of flatten by
 *
 *        ((Nil: List[A]) /: xs) ((xs, x) => xs ::: x)
 *
 * What would be the difference in asymptotic complexity between the two
 * versions of flatten?
 * 
 * In fact flatten is predefined together with a set of other userful function
 * in an object called List in the standatd Scala library. It can be accessed
 * from user program by calling List.flatten. Note that flatten is not a method
 * of class List - it would not make sense there, since it applies only to
 * lists of lists, not to all lists in general.
 */

/*
  In fact, the use of {} vs () doesn't make sintatic or semantic difference.
  In curry model of Scala, both the foldLeft /: and foldRight :\ methods
  define the function as second curry parammeter. So, the version of function
  that use /: can be writen like :\
*/
def flattenRight[A](xs: List[List[A]]): List[A] =
  (xs :\ (Nil: List[A])) {(x, xs) => x ::: xs}

/*
  Note that is the same function, just changing the application of flatten
  function. So, there's no difference in asymptotic complexity between the
  two implementation.
*/
</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 9.4.3 Fill in the missing expressions to complete the following
 * definitions of some basic list-manipulation operations as fold operations.
 *
 * def mapFun[A, B](xs: List[A], f: A => B): List[B] =
 *   (xs :\ List[B]()){ ?? }
 *
 * def lengthFun[A](xs: List[A]): int =
 *   (0 /: xs){ ?? }
 */

def mapFun[A, B](xs: List[A], f: A => B): List[B] =
  (xs :\ List[B]()){(x, fx) => f(x) :: xs}

def lengthFun[A](xs: List[A]): Int =
  (0 /: xs){(acc, _) => acc + 1}</pre>
