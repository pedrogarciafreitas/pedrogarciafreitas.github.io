---
id: 1409
title: Introduction To Scala — Part4 — Types and Case-classes
date: 2011-11-07T16:11:47+00:00
author: CKPYT
excerpt: "Exercises of the book 'Introduction to Objective Caml' solved in Scala."
layout: post
guid: http://www.sawp.com.br/blog/?p=1409
permalink: p=1409
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:10205:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.1 Suppose you are given the following definition of a list type.
    *
    *    type 'a mylist = Nil | Cons of 'a * 'a mylist
    *
    * 1. Write a function map : ('a -&gt; 'b) -&gt; 'a mylist -&gt; 'b mylist, where
    *
    *    map f [x0 ; x1 ; ...; xn ] = [f x0 ; f x1 ; ...; f xn ].
    *
    * 2. Write a function append : 'a mylist -&gt; 'a mylist -&gt; 'a mylist, where
    *
    *    append [x1 ;...; xn ] [xn+1 ; ...; xn+m ] = [x1 ; ...; xn+m ].
    */</span>
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Cons<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>h<span style="color: #000080;">:</span> T, v<span style="color: #000080;">:</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Nil<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 1. This is a non-tail-recursive version of map</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> map<span style="color: #F78811;">&#91;</span>U, T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>l<span style="color: #000080;">:</span> MyList<span style="color: #F78811;">&#91;</span>U<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#40;</span>f<span style="color: #000080;">:</span> U <span style="color: #000080;">=&gt;</span> T<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> l <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>      <span style="color: #000080;">=&gt;</span> Nil<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Cons<span style="color: #F78811;">&#40;</span>h, t<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> Cons<span style="color: #F78811;">&#40;</span>f<span style="color: #F78811;">&#40;</span>h<span style="color: #F78811;">&#41;</span>, map<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span>f<span style="color: #F78811;">&#125;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 2. This is a not-tail-recursive append</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> append<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>l1<span style="color: #000080;">:</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>, l2<span style="color: #000080;">:</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> MyList<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> l1 <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> l2
    <span style="color: #0000ff; font-weight: bold;">case</span> Cons<span style="color: #F78811;">&#40;</span>h, t<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> Cons<span style="color: #F78811;">&#40;</span>h, append<span style="color: #F78811;">&#40;</span>t, l2<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// Test map</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> lst1 <span style="color: #000080;">=</span> Cons<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">12</span>, Cons<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">100</span>, Cons<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">17</span>, Cons<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">8</span>, Nil<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> lst2 <span style="color: #000080;">=</span> Cons<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">9</span>, Cons<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">4</span>, Cons<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2</span>, Nil<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> mapped1 <span style="color: #000080;">=</span> map<span style="color: #F78811;">&#40;</span>lst1<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span>x <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">1.0</span> <span style="color: #000080;">*</span> x <span style="color: #000080;">*</span> x<span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> mapped2 <span style="color: #000080;">=</span> map<span style="color: #F78811;">&#40;</span>lst2<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span>x <span style="color: #000080;">=&gt;</span> math.<span style="color: #000000;">sqrt</span><span style="color: #F78811;">&#40;</span>x<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#125;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;List1: &quot;</span> + lst1<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Not tail-recursive mapping: &quot;</span> + mapped1<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>List2: &quot;</span> + lst2<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Not tail-recursive mapping: &quot;</span> + mapped2<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>Concatenation of Lis1 and Lis2: &quot;</span> + append<span style="color: #F78811;">&#40;</span>lst1, lst2<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.1 Suppose you are given the following definition of a list type.
    *
    *    type 'a mylist = Nil | Cons of 'a * 'a mylist
    *
    * 1. Write a function map : ('a -&gt; 'b) -&gt; 'a mylist -&gt; 'b mylist, where
    *
    *    map f [x0 ; x1 ; ...; xn ] = [f x0 ; f x1 ; ...; f xn ].
    *
    * 2. Write a function append : 'a mylist -&gt; 'a mylist -&gt; 'a mylist, where
    *
    *    append [x1 ;...; xn ] [xn+1 ; ...; xn+m ] = [x1 ; ...; xn+m ].
    */
    sealed abstract class MyList[T]
    case class Cons[T](h: T, v: MyList[T]) extends MyList[T]
    case class Nil[T]() extends MyList[T]
    
    // 1. This is a non-tail-recursive version of map
    def map[U, T](l: MyList[U])(f: U =&gt; T): MyList[T] = l match {
    case Nil()      =&gt; Nil()
    case Cons(h, t) =&gt; Cons(f(h), map(t){f})
    }
    
    // 2. This is a not-tail-recursive append
    def append[T](l1: MyList[T], l2: MyList[T]): MyList[T] = l1 match {
    case Nil() =&gt; l2
    case Cons(h, t) =&gt; Cons(h, append(t, l2))
    }
    
    
    // Test map
    val lst1 = Cons(12, Cons(100, Cons(17, Cons(8, Nil()))))
    val lst2 = Cons(9, Cons(4, Cons(2, Nil())))
    val mapped1 = map(lst1){x =&gt; 1.0 * x * x}
    val mapped2 = map(lst2){x =&gt; math.sqrt(x)}
    println(&quot;List1: &quot; + lst1)
    println(&quot;Not tail-recursive mapping: &quot; + mapped1)
    println(&quot;\nList2: &quot; + lst2)
    println(&quot;Not tail-recursive mapping: &quot; + mapped2)
    println(&quot;\nConcatenation of Lis1 and Lis2: &quot; + append(lst1, lst2))</p></div>
    ;i:2;s:9838:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.2 A type of unary (base-1) natural numbers can be defined as
    * follows,
    *
    *    type unary_number = Z | S of unary_number
    *
    * where Z represents the number zero, and if i is a unary number, then S i
    * is i + 1. For example, the number 5 would be represented as
    * S (S (S (S (S Z)))).
    *
    * 1. Write a function to add two unary numbers. What is the complexity of your
    * function?
    *
    * 2. Write a function to multiply two unary numbers.
    */</span>
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Unary
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Z<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Unary
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> S<span style="color: #F78811;">&#40;</span>counter<span style="color: #000080;">:</span> Unary<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Unary
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 1. Write a function to add two unary numbers. What is the complexity of your</span>
    <span style="color: #008000; font-style: italic;">// function?</span>
    <span style="color: #008000; font-style: italic;">// The complexity of an expression add(m, n) is O(n)</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> add<span style="color: #F78811;">&#40;</span>m<span style="color: #000080;">:</span> Unary, n<span style="color: #000080;">:</span> Unary<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Unary <span style="color: #000080;">=</span> n <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> S<span style="color: #F78811;">&#40;</span>n<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> add<span style="color: #F78811;">&#40;</span>S<span style="color: #F78811;">&#40;</span>m<span style="color: #F78811;">&#41;</span>, n<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Z<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>  <span style="color: #000080;">=&gt;</span> m
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 2. Write a function to multiply two unary numbers.</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> multiply<span style="color: #F78811;">&#40;</span>m<span style="color: #000080;">:</span> Unary, n<span style="color: #000080;">:</span> Unary<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Unary <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>i<span style="color: #000080;">:</span> Unary, acc<span style="color: #000080;">:</span> Unary<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Unary <span style="color: #000080;">=</span> i <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Z<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>  <span style="color: #000080;">=&gt;</span> acc
    <span style="color: #0000ff; font-weight: bold;">case</span> S<span style="color: #F78811;">&#40;</span>n<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> iter<span style="color: #F78811;">&#40;</span>n, add<span style="color: #F78811;">&#40;</span>acc, m<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>n, Z<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// test of functions</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> u5 <span style="color: #000080;">=</span> S<span style="color: #F78811;">&#40;</span>S <span style="color: #F78811;">&#40;</span>S <span style="color: #F78811;">&#40;</span>S <span style="color: #F78811;">&#40;</span>S<span style="color: #F78811;">&#40;</span>Z<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> u4 <span style="color: #000080;">=</span> S<span style="color: #F78811;">&#40;</span>S <span style="color: #F78811;">&#40;</span>S <span style="color: #F78811;">&#40;</span>S<span style="color: #F78811;">&#40;</span>Z<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> zero <span style="color: #000080;">=</span> Z<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;5 + 4 = 9, in unary is: &quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>u5 + <span style="color: #6666FF;">&quot; + &quot;</span> + u4 + <span style="color: #6666FF;">&quot; = &quot;</span> + add<span style="color: #F78811;">&#40;</span>u5, u4<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>5 + 0 = 5, in unary is: &quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>u5 + <span style="color: #6666FF;">&quot; + &quot;</span> + zero + <span style="color: #6666FF;">&quot; = &quot;</span> + add<span style="color: #F78811;">&#40;</span>u5, zero<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>5 * 0 = 0, in unary is: &quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>u5 + <span style="color: #6666FF;">&quot; * &quot;</span> + zero + <span style="color: #6666FF;">&quot; = &quot;</span> + multiply<span style="color: #F78811;">&#40;</span>u5, zero<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>5 * 4 = 20, in unary is: &quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>u5 + <span style="color: #6666FF;">&quot; * &quot;</span> + u4 + <span style="color: #6666FF;">&quot; = &quot;</span> + multiply<span style="color: #F78811;">&#40;</span>u5, u4<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.2 A type of unary (base-1) natural numbers can be defined as
    * follows,
    *
    *    type unary_number = Z | S of unary_number
    *
    * where Z represents the number zero, and if i is a unary number, then S i
    * is i + 1. For example, the number 5 would be represented as
    * S (S (S (S (S Z)))).
    *
    * 1. Write a function to add two unary numbers. What is the complexity of your
    * function?
    *
    * 2. Write a function to multiply two unary numbers.
    */
    sealed abstract class Unary
    case class Z() extends Unary
    case class S(counter: Unary) extends Unary
    
    // 1. Write a function to add two unary numbers. What is the complexity of your
    // function?
    // The complexity of an expression add(m, n) is O(n)
    def add(m: Unary, n: Unary): Unary = n match {
    case S(n) =&gt; add(S(m), n)
    case Z()  =&gt; m
    }
    
    // 2. Write a function to multiply two unary numbers.
    def multiply(m: Unary, n: Unary): Unary = {
    def iter(i: Unary, acc: Unary): Unary = i match {
    case Z()  =&gt; acc
    case S(n) =&gt; iter(n, add(acc, m))
    }
    iter(n, Z())
    }
    
    // test of functions
    val u5 = S(S (S (S (S(Z())))))
    val u4 = S(S (S (S(Z()))))
    val zero = Z()
    println(&quot;5 + 4 = 9, in unary is: &quot;)
    println(u5 + &quot; + &quot; + u4 + &quot; = &quot; + add(u5, u4))
    println(&quot;\n5 + 0 = 5, in unary is: &quot;)
    println(u5 + &quot; + &quot; + zero + &quot; = &quot; + add(u5, zero))
    println(&quot;\n5 * 0 = 0, in unary is: &quot;)
    println(u5 + &quot; * &quot; + zero + &quot; = &quot; + multiply(u5, zero))
    println(&quot;\n5 * 4 = 20, in unary is: &quot;)
    println(u5 + &quot; * &quot; + u4 + &quot; = &quot; + multiply(u5, u4))</p></div>
    ;i:3;s:14811:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.3 Suppose we have the following definition for a type of small
    * numbers.
    *
    *      type small = Four | Three | Two | One
    *
    * The builtin comparison (&lt; ) orders the numbers in reverse order.
    *
    * scala&gt; Four &lt; Three
    * res6: Boolean = false
    *
    * 1. Write a function lt_small : small -&gt; small -&gt; bool that orders the
    * numbers in the normal way.
    *
    * 2. Suppose the type small defines n small integers. How does the size of
    * your code depend on n?
    */</span>
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> SmallNumbers
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> SmallNumbers
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> SmallNumbers
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> SmallNumbers
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> SmallNumbers
    &nbsp;
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> lt<span style="color: #000080;">_</span>small<span style="color: #F78811;">&#40;</span>n1<span style="color: #000080;">:</span> SmallNumbers, n2<span style="color: #000080;">:</span> SmallNumbers<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>n1, n2<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> | Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 2. Suppose the type small defines n small integers. How does the size of</span>
    <span style="color: #008000; font-style: italic;">// your code depend on n?</span>
    <span style="color: #008000; font-style: italic;">// R. Using lt_small, the code grows in $O(n^2)$. To reduce the code size,</span>
    <span style="color: #008000; font-style: italic;">// transform the number in integers and uses Scala's native operators for</span>
    <span style="color: #008000; font-style: italic;">// comparison.</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> smallNumbersToInt<span style="color: #F78811;">&#40;</span>number<span style="color: #000080;">:</span> SmallNumbers<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> number <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>   <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">1</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>   <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">2</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">3</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>  <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">4</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> lt<span style="color: #000080;">_</span>small<span style="color: #000080;">_</span>smarty<span style="color: #F78811;">&#40;</span>n1<span style="color: #000080;">:</span> SmallNumbers, n2<span style="color: #000080;">:</span> SmallNumbers<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Boolean <span style="color: #000080;">=</span>
    smallNumbersToInt<span style="color: #F78811;">&#40;</span>n1<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span> smallNumbersToInt<span style="color: #F78811;">&#40;</span>n2<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// test cases</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Naive lt_small: &quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;One &lt; Two? &quot;</span> + lt<span style="color: #000080;">_</span>small<span style="color: #F78811;">&#40;</span>One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Four &lt; Three? &quot;</span> + lt<span style="color: #000080;">_</span>small<span style="color: #F78811;">&#40;</span>Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Two &lt; Two? &quot;</span> + lt<span style="color: #000080;">_</span>small<span style="color: #F78811;">&#40;</span>Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>Not so naive lt_small&quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;One &lt; Two? &quot;</span> + lt<span style="color: #000080;">_</span>small<span style="color: #000080;">_</span>smarty<span style="color: #F78811;">&#40;</span>One<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Four &lt; Three? &quot;</span> + lt<span style="color: #000080;">_</span>small<span style="color: #000080;">_</span>smarty<span style="color: #F78811;">&#40;</span>Four<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Three<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Two &lt; Two? &quot;</span> + lt<span style="color: #000080;">_</span>small<span style="color: #000080;">_</span>smarty<span style="color: #F78811;">&#40;</span>Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Two<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.3 Suppose we have the following definition for a type of small
    * numbers.
    *
    *      type small = Four | Three | Two | One
    *
    * The builtin comparison (&lt; ) orders the numbers in reverse order.
    *
    * scala&gt; Four &lt; Three
    * res6: Boolean = false
    *
    * 1. Write a function lt_small : small -&gt; small -&gt; bool that orders the
    * numbers in the normal way.
    *
    * 2. Suppose the type small defines n small integers. How does the size of
    * your code depend on n?
    */
    sealed abstract class SmallNumbers
    case class One() extends SmallNumbers
    case class Two() extends SmallNumbers
    case class Three() extends SmallNumbers
    case class Four() extends SmallNumbers
    
    
    def lt_small(n1: SmallNumbers, n2: SmallNumbers): Boolean = (n1, n2) match {
    case (One(), Two() | Three() | Four()) =&gt; true
    case (Two(), Three() | Four()) =&gt; true
    case (Three(), Four()) =&gt; true
    case (One(), One()) =&gt; false
    case (Two(), One() | Two()) =&gt; false
    case (Three(), One() | Two() | Three()) =&gt; false
    case (Four(), One() | Two() | Three() | Four()) =&gt; false
    }
    
    
    // 2. Suppose the type small defines n small integers. How does the size of
    // your code depend on n?
    // R. Using lt_small, the code grows in $O(n^2)$. To reduce the code size,
    // transform the number in integers and uses Scala's native operators for
    // comparison.
    def smallNumbersToInt(number: SmallNumbers): Int = number match {
    case One()   =&gt; 1
    case Two()   =&gt; 2
    case Three() =&gt; 3
    case Four()  =&gt; 4
    }
    def lt_small_smarty(n1: SmallNumbers, n2: SmallNumbers): Boolean =
    smallNumbersToInt(n1) &lt; smallNumbersToInt(n2)
    
    // test cases
    println(&quot;Naive lt_small: &quot;)
    println(&quot;One &lt; Two? &quot; + lt_small(One(), Two()))
    println(&quot;Four &lt; Three? &quot; + lt_small(Four(), Three()))
    println(&quot;Two &lt; Two? &quot; + lt_small(Two(), Two()))
    
    println(&quot;\nNot so naive lt_small&quot;)
    println(&quot;One &lt; Two? &quot; + lt_small_smarty(One(), Two()))
    println(&quot;Four &lt; Three? &quot; + lt_small_smarty(Four(), Three()))
    println(&quot;Two &lt; Two? &quot; + lt_small_smarty(Two(), Two()))</p></div>
    ;i:4;s:10043:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.4 We can define a data type for simple arithmetic expressions as
    * follows.
    *
    *    type unop = Neg
    *    type binop = Add | Sub | Mul | Div
    *    type exp =
    *      Constant of int
    *      | Unary of unop * exp
    *      | Binary of exp * binop * exp
    *
    * Write a function eval : exp -&gt; int to evaluate an expression, performing
    * the calculation to produce an integer result.
    */</span>
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> UnOp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Neg<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> UnOp
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> BinOp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Add<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> BinOp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Sub<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> BinOp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Mul<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> BinOp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Div<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> BinOp
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Exp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Constant<span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Exp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Unary<span style="color: #F78811;">&#40;</span>unop<span style="color: #000080;">:</span> UnOp, expr<span style="color: #000080;">:</span> Exp<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Exp
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Binary<span style="color: #F78811;">&#40;</span>expr1<span style="color: #000080;">:</span> Exp, binop<span style="color: #000080;">:</span> BinOp, expr2<span style="color: #000080;">:</span> Exp<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Exp
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> eval<span style="color: #F78811;">&#40;</span>e<span style="color: #000080;">:</span> Exp<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Int <span style="color: #000080;">=</span> e <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Constant<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span>        <span style="color: #000080;">=&gt;</span> i
    <span style="color: #0000ff; font-weight: bold;">case</span> Unary<span style="color: #F78811;">&#40;</span>Neg<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, e<span style="color: #F78811;">&#41;</span>    <span style="color: #000080;">=&gt;</span> -<span style="color: #F78811;">1</span> <span style="color: #000080;">*</span> eval<span style="color: #F78811;">&#40;</span>e<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Binary<span style="color: #F78811;">&#40;</span>e1, op, e2<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> <span style="color: #F78811;">&#40;</span>el, er<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>eval<span style="color: #F78811;">&#40;</span>e1<span style="color: #F78811;">&#41;</span>, eval<span style="color: #F78811;">&#40;</span>e2<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> ret <span style="color: #000080;">=</span> op <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Add<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> el + er
    <span style="color: #0000ff; font-weight: bold;">case</span> Sub<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> el - er
    <span style="color: #0000ff; font-weight: bold;">case</span> Mul<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> el <span style="color: #000080;">*</span> er
    <span style="color: #0000ff; font-weight: bold;">case</span> Div<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> el / er
    <span style="color: #F78811;">&#125;</span>
    ret
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// Test</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> b1 <span style="color: #000080;">=</span> Binary<span style="color: #F78811;">&#40;</span>Constant<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">12</span><span style="color: #F78811;">&#41;</span>, Add<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Constant<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">15</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> u1 <span style="color: #000080;">=</span> Unary<span style="color: #F78811;">&#40;</span>Neg<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Constant<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">10</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> express <span style="color: #000080;">=</span> Binary<span style="color: #F78811;">&#40;</span>b1, Sub<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, u1<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Evaluation of (12 + 15) - (-10) = 37: &quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>express + <span style="color: #6666FF;">&quot; = &quot;</span> + eval<span style="color: #F78811;">&#40;</span>express<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.4 We can define a data type for simple arithmetic expressions as
    * follows.
    *
    *    type unop = Neg
    *    type binop = Add | Sub | Mul | Div
    *    type exp =
    *      Constant of int
    *      | Unary of unop * exp
    *      | Binary of exp * binop * exp
    *
    * Write a function eval : exp -&gt; int to evaluate an expression, performing
    * the calculation to produce an integer result.
    */
    sealed abstract class UnOp
    case class Neg() extends UnOp
    
    sealed abstract class BinOp
    case class Add() extends BinOp
    case class Sub() extends BinOp
    case class Mul() extends BinOp
    case class Div() extends BinOp
    
    sealed abstract class Exp
    case class Constant(value: Int) extends Exp
    case class Unary(unop: UnOp, expr: Exp) extends Exp
    case class Binary(expr1: Exp, binop: BinOp, expr2: Exp) extends Exp
    
    def eval(e: Exp): Int = e match {
    case Constant(i)        =&gt; i
    case Unary(Neg(), e)    =&gt; -1 * eval(e)
    case Binary(e1, op, e2) =&gt; {
    val (el, er) = (eval(e1), eval(e2))
    val ret = op match {
    case Add() =&gt; el + er
    case Sub() =&gt; el - er
    case Mul() =&gt; el * er
    case Div() =&gt; el / er
    }
    ret
    }
    }
    
    
    // Test
    val b1 = Binary(Constant(12), Add(), Constant(15))
    val u1 = Unary(Neg(), Constant(10))
    val express = Binary(b1, Sub(), u1)
    println(&quot;Evaluation of (12 + 15) - (-10) = 37: &quot;)
    println(express + &quot; = &quot; + eval(express))</p></div>
    ;i:5;s:11305:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.5. A way to implement a dictionary is with tree, where each
    * node in the tree has a label and a value.
    *
    * 1. Implement a polymorphic dictionary, (’key, ’value) dictionary, as a tree
    * with the three dictionary operations.
    *
    *    empty: (’key, ’value) dict
    *    add: (’key, ’value) dict -&gt; ’key -&gt; ’value -&gt; (’key, ’value) dict
    *    find : (’key, ’value) dict -&gt; ’key -&gt; ’value
    *
    */</span>
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Dict<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Node<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>no<span style="color: #000080;">:</span>Tuple2<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span>, l<span style="color: #000080;">:</span> Dict<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span>, r<span style="color: #000080;">:</span> Dict<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">extends</span> Dict<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Leaf<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Dict<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> empty <span style="color: #000080;">=</span> Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> add<span style="color: #F78811;">&#91;</span>T <span style="color: #000080;">&lt;</span> <span style="color: #000080;">%</span> Ordered<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>,U<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>dict<span style="color: #000080;">:</span> Dict<span style="color: #F78811;">&#91;</span>T, U<span style="color: #F78811;">&#93;</span>, key<span style="color: #000080;">:</span> T, value<span style="color: #000080;">:</span> U<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Dict<span style="color: #F78811;">&#91;</span>T,U<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    dict <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span>
    Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>key, value<span style="color: #F78811;">&#41;</span>, Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> key <span style="color: #000080;">&lt;</span> k <span style="color: #000080;">=&gt;</span>
    Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, add<span style="color: #F78811;">&#40;</span>left, key, value<span style="color: #F78811;">&#41;</span>, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> key <span style="color: #000080;">&gt;</span> k <span style="color: #000080;">=&gt;</span>
    Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, left, add<span style="color: #F78811;">&#40;</span>right, key, value<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> key <span style="color: #000080;">==</span> k <span style="color: #000080;">=&gt;</span>
    Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>key, value<span style="color: #F78811;">&#41;</span>, left, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Invalid Argument in add dict.&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> find<span style="color: #F78811;">&#91;</span>T <span style="color: #000080;">&lt;</span> <span style="color: #000080;">%</span> Ordered<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>,U<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>dict<span style="color: #000080;">:</span> Dict<span style="color: #F78811;">&#91;</span>T, U<span style="color: #F78811;">&#93;</span>, key<span style="color: #000080;">:</span> T<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> U <span style="color: #000080;">=</span>
    dict <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Not Found.&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> key <span style="color: #000080;">&lt;</span> k <span style="color: #000080;">=&gt;</span> find<span style="color: #F78811;">&#40;</span>left, key<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> key <span style="color: #000080;">&gt;</span> k <span style="color: #000080;">=&gt;</span> find<span style="color: #F78811;">&#40;</span>right, key<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>k, v<span style="color: #F78811;">&#41;</span>, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">if</span> key <span style="color: #000080;">==</span> k <span style="color: #000080;">=&gt;</span> v
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Invalid Argument in add dict.&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.5. A way to implement a dictionary is with tree, where each
    * node in the tree has a label and a value.
    *
    * 1. Implement a polymorphic dictionary, (’key, ’value) dictionary, as a tree
    * with the three dictionary operations.
    *
    *    empty: (’key, ’value) dict
    *    add: (’key, ’value) dict -&gt; ’key -&gt; ’value -&gt; (’key, ’value) dict
    *    find : (’key, ’value) dict -&gt; ’key -&gt; ’value
    *
    */
    sealed abstract class Dict[T,U]
    case class Node[T,U](no:Tuple2[T,U], l: Dict[T,U], r: Dict[T,U])
    extends Dict[T,U]
    case class Leaf[T,U]() extends Dict[T,U]
    
    def empty = Leaf()
    
    def add[T &lt; % Ordered[T],U](dict: Dict[T, U], key: T, value: U): Dict[T,U] =
    dict match {
    case Leaf() =&gt;
    Node((key, value), Leaf(), Leaf())
    case Node((k, v), left, right) if key &lt; k =&gt;
    Node((k, v), add(left, key, value), right)
    case Node((k, v), left, right) if key &gt; k =&gt;
    Node((k, v), left, add(right, key, value))
    case Node((k, v), left, right) if key == k =&gt;
    Node((key, value), left, right)
    case _ =&gt; throw new Exception(&quot;Invalid Argument in add dict.&quot;)
    }
    
    def find[T &lt; % Ordered[T],U](dict: Dict[T, U], key: T): U =
    dict match {
    case Leaf() =&gt; throw new Exception(&quot;Not Found.&quot;)
    case Node((k, v), left, right) if key &lt; k =&gt; find(left, key)
    case Node((k, v), left, right) if key &gt; k =&gt; find(right, key)
    case Node((k, v), left, right) if key == k =&gt; v
    case _ =&gt; throw new Exception(&quot;Invalid Argument in add dict.&quot;)
    }</p></div>
    ;i:6;s:10383:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.6 Consider the function insert for unbalanced, ordered, binary
    * trees. One potential implementation problem is when uses the builtin
    * comparison (&lt; ). Rewrite the definition so the it is parameterized by a
    * comparison function that, given two elements, returns on of three values
    *
    *    type comparison = LessThan | Equal | GreaterThan.
    *
    * The expression insert compare x tree inserts an element x into the tree
    * tree. The type is
    *
    *    insert : (’a -&gt; ’a -&gt; comparison) -&gt; ’a -&gt; ’a tree -&gt; ’a tree.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Leaf<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Node<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>v<span style="color: #000080;">:</span> T, left<span style="color: #000080;">:</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>, right<span style="color: #000080;">:</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Comparison
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> LessThan<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Comparison
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Equal<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Comparison
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> GreaterThan<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Comparison
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> insert<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> T, tree<span style="color: #000080;">:</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#40;</span>comp<span style="color: #000080;">:</span> Comparison<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    tree <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> Node<span style="color: #F78811;">&#40;</span>value, Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>, Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>v, left, right<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span>
    comp <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Equal<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> Node<span style="color: #F78811;">&#40;</span>v, left, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> LessThan<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> Node<span style="color: #F78811;">&#40;</span>v, insert<span style="color: #F78811;">&#40;</span>value, left<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span>comp<span style="color: #F78811;">&#125;</span>, right<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> GreaterThan<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> Node<span style="color: #F78811;">&#40;</span>v, left, insert<span style="color: #F78811;">&#40;</span>value, right<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span>comp<span style="color: #F78811;">&#125;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> listToTree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>l<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Tree<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> l <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span> Leaf<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> h <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> insert<span style="color: #F78811;">&#40;</span>h, listToTree<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#123;</span>LessThan<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// Tests</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> list <span style="color: #000080;">=</span> List<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">7</span>, <span style="color: #F78811;">5</span>, <span style="color: #F78811;">9</span>, <span style="color: #F78811;">11</span>, <span style="color: #F78811;">3</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> tree <span style="color: #000080;">=</span> listToTree<span style="color: #F78811;">&#40;</span>list<span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Convert list: &quot;</span> + list + <span style="color: #6666FF;">&quot; into tree: &quot;</span> + tree<span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.6 Consider the function insert for unbalanced, ordered, binary
    * trees. One potential implementation problem is when uses the builtin
    * comparison (&lt; ). Rewrite the definition so the it is parameterized by a
    * comparison function that, given two elements, returns on of three values
    *
    *    type comparison = LessThan | Equal | GreaterThan.
    *
    * The expression insert compare x tree inserts an element x into the tree
    * tree. The type is
    *
    *    insert : (’a -&gt; ’a -&gt; comparison) -&gt; ’a -&gt; ’a tree -&gt; ’a tree.
    */
    
    sealed abstract class Tree[T]
    case class Leaf[T]() extends Tree[T]
    case class Node[T](v: T, left: Tree[T], right: Tree[T]) extends Tree[T]
    
    sealed abstract class Comparison
    case class LessThan() extends Comparison
    case class Equal() extends Comparison
    case class GreaterThan() extends Comparison
    
    def insert[T](value: T, tree: Tree[T]) (comp: Comparison): Tree[T] =
    tree match {
    case Leaf() =&gt; Node(value, Leaf(), Leaf())
    case Node(v, left, right) =&gt;
    comp match {
    case Equal() =&gt; Node(v, left, right)
    case LessThan() =&gt; Node(v, insert(value, left){comp}, right)
    case GreaterThan() =&gt; Node(v, left, insert(value, right){comp})
    }
    }
    
    def listToTree[T](l: List[T]): Tree[T] = l match {
    case Nil    =&gt; Leaf()
    case h :: t =&gt; insert(h, listToTree(t)){LessThan()}
    }
    
    
    // Tests
    val list = List(7, 5, 9, 11, 3)
    val tree = listToTree(list)
    
    println(&quot;Convert list: &quot; + list + &quot; into tree: &quot; + tree)</p></div>
    ;i:7;s:17734:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 4.7 A heap of integers is a data structure supporting the
    * following operations.
    *
    *   makeheap: int -&gt; heap: create a heap containing a single element,
    *
    *   insert: heap -&gt; int -&gt; heap: add an element to a heap; duplicates are
    *            alowed,
    *
    *   findmin: heap -&gt; int: return the smallest element of the heap.
    *
    *   deletemin: heap -&gt; heap: return a new heap that is the same as the
    *               original, without the smallest element.
    *
    *   meld: heap -&gt; heap -&gt; heap: join two heaps into a new heap containing the
    *         elements of both.
    *
    * A heap can be represented as a binary tree, where for any node a, if b is a
    * child node of a, then label(a) &lt; = label(b). The order of children does not
    * matter. A pairing heap is a particular implementation where the operations
    * are performed as follows.
    *
    *    makeheap i: produce a single-node tree with i at the root.
    *
    *    insert h i = meld h (makeheap i).
    *
    *    findmin h: return the root label.
    *
    *    deletemin h: remove the root, and meld the subtrees.
    *
    *    meld h1 h2: compare the roots, and make the heap with the larger element
    *    a subtree of the other.
    *
    * 1. Define a type heap and implement the five operations.
    *
    * 2. A heap sort is performed by inserting the elements to be sorted into a
    *    heap, then the values are extracted from smallest to largest. Write a
    *    function heap_sort : int list -&gt; int list that performs a heap sort,
    *    where the result is sorted from largest to smallest.
    */</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 1. Define a type heap and implement the five operations.</span>
    <span style="color: #0000ff; font-weight: bold;">type</span> T <span style="color: #000080;">=</span> Int
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">sealed</span> <span style="color: #0000ff; font-weight: bold;">abstract</span> <span style="color: #0000ff; font-weight: bold;">class</span> Heap
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #0000ff; font-weight: bold;">class</span> Node<span style="color: #F78811;">&#40;</span>value<span style="color: #000080;">:</span> T, l<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Heap
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> makeheap<span style="color: #F78811;">&#40;</span>i<span style="color: #000080;">:</span> T<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> Node<span style="color: #F78811;">&#40;</span>i, Nil<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> meld<span style="color: #F78811;">&#40;</span>h1<span style="color: #000080;">:</span> Node, h2<span style="color: #000080;">:</span> Node<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Node <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>h1, h2<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>Node<span style="color: #F78811;">&#40;</span>hh1<span style="color: #000080;">:</span> T, t1<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span>, Node<span style="color: #F78811;">&#40;</span>hh2<span style="color: #000080;">:</span> T, t2<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>hh1 <span style="color: #000080;">&gt;</span> hh2<span style="color: #F78811;">&#41;</span> Node<span style="color: #F78811;">&#40;</span>hh1, h2 <span style="color: #000080;">::</span> t1<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> Node<span style="color: #F78811;">&#40;</span>hh2, h1 <span style="color: #000080;">::</span> t2<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> insert<span style="color: #F78811;">&#40;</span>h<span style="color: #000080;">:</span> Node, i<span style="color: #000080;">:</span> T<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Node <span style="color: #000080;">=</span>
    meld<span style="color: #F78811;">&#40;</span>h, makeheap<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> findmin<span style="color: #F78811;">&#40;</span>h<span style="color: #000080;">:</span> Node<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> T <span style="color: #000080;">=</span> h <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>i<span style="color: #000080;">:</span> T, <span style="color: #000080;">_</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> i
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> deletemin<span style="color: #F78811;">&#40;</span>h<span style="color: #000080;">:</span> Node<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Node <span style="color: #000080;">=</span> h <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #000080;">_</span>, h <span style="color: #000080;">::</span> t<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>h<span style="color: #000080;">:</span> Node, acc<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Node <span style="color: #000080;">=</span> acc <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> x <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> iter<span style="color: #F78811;">&#40;</span>meld<span style="color: #F78811;">&#40;</span>h, x<span style="color: #F78811;">&#41;</span>, t<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span> h
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>h, t<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #000080;">_</span>, List<span style="color: #F78811;">&#40;</span>h<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> h
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span><span style="color: #000080;">_</span>, Nil<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Invalid Argument in deletemin.&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 2. heapsort</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> heap<span style="color: #000080;">_</span>sort<span style="color: #F78811;">&#40;</span>l<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> l <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil <span style="color: #000080;">=&gt;</span> Nil
    <span style="color: #0000ff; font-weight: bold;">case</span> x <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> insertList<span style="color: #F78811;">&#40;</span>h<span style="color: #000080;">:</span> Node, l<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Node <span style="color: #000080;">=</span> l <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil <span style="color: #000080;">=&gt;</span> h
    <span style="color: #0000ff; font-weight: bold;">case</span> x <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> insertList<span style="color: #F78811;">&#40;</span>insert<span style="color: #F78811;">&#40;</span>h, x<span style="color: #F78811;">&#41;</span>, t<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>sorted<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span>, h<span style="color: #000080;">:</span> Node<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>T<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> h <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Node<span style="color: #F78811;">&#40;</span>x, Nil<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> x <span style="color: #000080;">::</span> sorted
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> iter<span style="color: #F78811;">&#40;</span>findmin<span style="color: #F78811;">&#40;</span>h<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> sorted, deletemin<span style="color: #F78811;">&#40;</span>h<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>Nil, insertList<span style="color: #F78811;">&#40;</span>makeheap<span style="color: #F78811;">&#40;</span>x<span style="color: #F78811;">&#41;</span>, t<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// tests</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> h <span style="color: #000080;">=</span> makeheap<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">12</span><span style="color: #F78811;">&#41;</span>
    h <span style="color: #000080;">=</span> insert<span style="color: #F78811;">&#40;</span>h, <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    h <span style="color: #000080;">=</span> insert<span style="color: #F78811;">&#40;</span>h, <span style="color: #F78811;">17</span><span style="color: #F78811;">&#41;</span>
    h <span style="color: #000080;">=</span> insert<span style="color: #F78811;">&#40;</span>h, <span style="color: #F78811;">200</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> l <span style="color: #000080;">=</span> List<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">5</span>, <span style="color: #F78811;">7</span>, <span style="color: #F78811;">8</span>, <span style="color: #F78811;">10</span>, <span style="color: #F78811;">11</span>, <span style="color: #F78811;">0</span>, <span style="color: #F78811;">101</span>, <span style="color: #F78811;">112</span>, <span style="color: #F78811;">99</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;heap: &quot;</span> + h<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>l + <span style="color: #6666FF;">&quot; sorted &quot;</span> + heap<span style="color: #000080;">_</span>sort<span style="color: #F78811;">&#40;</span>l<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 4.7 A heap of integers is a data structure supporting the
    * following operations.
    *
    *   makeheap: int -&gt; heap: create a heap containing a single element,
    *
    *   insert: heap -&gt; int -&gt; heap: add an element to a heap; duplicates are
    *            alowed,
    *
    *   findmin: heap -&gt; int: return the smallest element of the heap.
    *
    *   deletemin: heap -&gt; heap: return a new heap that is the same as the
    *               original, without the smallest element.
    *
    *   meld: heap -&gt; heap -&gt; heap: join two heaps into a new heap containing the
    *         elements of both.
    *
    * A heap can be represented as a binary tree, where for any node a, if b is a
    * child node of a, then label(a) &lt; = label(b). The order of children does not
    * matter. A pairing heap is a particular implementation where the operations
    * are performed as follows.
    *
    *    makeheap i: produce a single-node tree with i at the root.
    *
    *    insert h i = meld h (makeheap i).
    *
    *    findmin h: return the root label.
    *
    *    deletemin h: remove the root, and meld the subtrees.
    *
    *    meld h1 h2: compare the roots, and make the heap with the larger element
    *    a subtree of the other.
    *
    * 1. Define a type heap and implement the five operations.
    *
    * 2. A heap sort is performed by inserting the elements to be sorted into a
    *    heap, then the values are extracted from smallest to largest. Write a
    *    function heap_sort : int list -&gt; int list that performs a heap sort,
    *    where the result is sorted from largest to smallest.
    */
    
    // 1. Define a type heap and implement the five operations.
    type T = Int
    
    sealed abstract class Heap
    case class Node(value: T, l: List[Node]) extends Heap
    
    def makeheap(i: T) = Node(i, Nil)
    
    def meld(h1: Node, h2: Node): Node = (h1, h2) match {
    case (Node(hh1: T, t1: List[Node]), Node(hh2: T, t2: List[Node])) =&gt;
    if (hh1 &gt; hh2) Node(hh1, h2 :: t1)
    else Node(hh2, h1 :: t2)
    }
    
    def insert(h: Node, i: T): Node =
    meld(h, makeheap(i))
    
    def findmin(h: Node): T = h match {
    case Node(i: T, _) =&gt; i
    }
    
    def deletemin(h: Node): Node = h match {
    case Node(_, h :: t) =&gt; {
    def iter(h: Node, acc: List[Node]): Node = acc match {
    case x :: t =&gt; iter(meld(h, x), t)
    case Nil    =&gt; h
    }
    iter(h, t)
    }
    case Node(_, List(h)) =&gt; h
    case Node(_, Nil) =&gt; throw new Exception(&quot;Invalid Argument in deletemin.&quot;)
    }
    
    // 2. heapsort
    
    def heap_sort(l: List[T]): List[T] = l match {
    case Nil =&gt; Nil
    case x :: t =&gt; {
    def insertList(h: Node, l: List[T]): Node = l match {
    case Nil =&gt; h
    case x :: t =&gt; insertList(insert(h, x), t)
    }
    def iter(sorted: List[T], h: Node): List[T] = h match {
    case Node(x, Nil) =&gt; x :: sorted
    case _ =&gt; iter(findmin(h) :: sorted, deletemin(h))
    }
    iter(Nil, insertList(makeheap(x), t))
    }
    }
    
    // tests
    var h = makeheap(12)
    h = insert(h, 1)
    h = insert(h, 17)
    h = insert(h, 200)
    val l = List(5, 7, 8, 10, 11, 0, 101, 112, 99)
    println(&quot;heap: &quot; + h)
    println(l + &quot; sorted &quot; + heap_sort(l))</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 4.1 Suppose you are given the following definition of a list type.
 *
 *    type 'a mylist = Nil | Cons of 'a * 'a mylist
 *
 * 1. Write a function map : ('a -> 'b) -> 'a mylist -> 'b mylist, where
 *
 *    map f [x0 ; x1 ; ...; xn ] = [f x0 ; f x1 ; ...; f xn ].
 *
 * 2. Write a function append : 'a mylist -> 'a mylist -> 'a mylist, where
 *
 *    append [x1 ;...; xn ] [xn+1 ; ...; xn+m ] = [x1 ; ...; xn+m ].
 */
sealed abstract class MyList[T]
 case class Cons[T](h: T, v: MyList[T]) extends MyList[T]
 case class Nil[T]() extends MyList[T]

// 1. This is a non-tail-recursive version of map
def map[U, T](l: MyList[U])(f: U => T): MyList[T] = l match {
  case Nil()      => Nil()
  case Cons(h, t) => Cons(f(h), map(t){f})
}

// 2. This is a not-tail-recursive append
def append[T](l1: MyList[T], l2: MyList[T]): MyList[T] = l1 match {
  case Nil() => l2
  case Cons(h, t) => Cons(h, append(t, l2))
}


// Test map
val lst1 = Cons(12, Cons(100, Cons(17, Cons(8, Nil()))))
val lst2 = Cons(9, Cons(4, Cons(2, Nil())))
val mapped1 = map(lst1){x => 1.0 * x * x}
val mapped2 = map(lst2){x => math.sqrt(x)}
println("List1: " + lst1)
println("Not tail-recursive mapping: " + mapped1)
println("\nList2: " + lst2)
println("Not tail-recursive mapping: " + mapped2)
println("\nConcatenation of Lis1 and Lis2: " + append(lst1, lst2))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 4.2 A type of unary (base-1) natural numbers can be defined as
 * follows,
 *
 *    type unary_number = Z | S of unary_number
 *
 * where Z represents the number zero, and if i is a unary number, then S i
 * is i + 1. For example, the number 5 would be represented as
 * S (S (S (S (S Z)))).
 *
 * 1. Write a function to add two unary numbers. What is the complexity of your
 * function?
 *
 * 2. Write a function to multiply two unary numbers.
 */
sealed abstract class Unary
  case class Z() extends Unary
  case class S(counter: Unary) extends Unary

// 1. Write a function to add two unary numbers. What is the complexity of your
// function?
// The complexity of an expression add(m, n) is O(n)
def add(m: Unary, n: Unary): Unary = n match {
  case S(n) => add(S(m), n)
  case Z()  => m
}

// 2. Write a function to multiply two unary numbers.
def multiply(m: Unary, n: Unary): Unary = {
  def iter(i: Unary, acc: Unary): Unary = i match {
    case Z()  => acc
    case S(n) => iter(n, add(acc, m))
  }
  iter(n, Z())
}

// test of functions
val u5 = S(S (S (S (S(Z())))))
val u4 = S(S (S (S(Z()))))
val zero = Z()
println("5 + 4 = 9, in unary is: ")
println(u5 + " + " + u4 + " = " + add(u5, u4))
println("\n5 + 0 = 5, in unary is: ")
println(u5 + " + " + zero + " = " + add(u5, zero))
println("\n5 * 0 = 0, in unary is: ")
println(u5 + " * " + zero + " = " + multiply(u5, zero))
println("\n5 * 4 = 20, in unary is: ")
println(u5 + " * " + u4 + " = " + multiply(u5, u4))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 4.3 Suppose we have the following definition for a type of small
 * numbers.
 *
 *      type small = Four | Three | Two | One
 *
 * The builtin comparison (&lt; ) orders the numbers in reverse order.
 * 
 * scala> Four &lt; Three
 * res6: Boolean = false
 *
 * 1. Write a function lt_small : small -> small -> bool that orders the
 * numbers in the normal way.
 *
 * 2. Suppose the type small defines n small integers. How does the size of
 * your code depend on n?
 */
sealed abstract class SmallNumbers
  case class One() extends SmallNumbers
  case class Two() extends SmallNumbers
  case class Three() extends SmallNumbers
  case class Four() extends SmallNumbers


def lt_small(n1: SmallNumbers, n2: SmallNumbers): Boolean = (n1, n2) match {
  case (One(), Two() | Three() | Four()) => true
  case (Two(), Three() | Four()) => true
  case (Three(), Four()) => true
  case (One(), One()) => false
  case (Two(), One() | Two()) => false
  case (Three(), One() | Two() | Three()) => false
  case (Four(), One() | Two() | Three() | Four()) => false
}


// 2. Suppose the type small defines n small integers. How does the size of
// your code depend on n?
// R. Using lt_small, the code grows in $O(n^2)$. To reduce the code size,
// transform the number in integers and uses Scala's native operators for
// comparison.
def smallNumbersToInt(number: SmallNumbers): Int = number match {
  case One()   => 1
  case Two()   => 2
  case Three() => 3
  case Four()  => 4
}
def lt_small_smarty(n1: SmallNumbers, n2: SmallNumbers): Boolean =
  smallNumbersToInt(n1) &lt; smallNumbersToInt(n2)

// test cases
println("Naive lt_small: ")
println("One &lt; Two? " + lt_small(One(), Two()))
println("Four &lt; Three? " + lt_small(Four(), Three()))
println("Two &lt; Two? " + lt_small(Two(), Two()))

println("\nNot so naive lt_small")
println("One &lt; Two? " + lt_small_smarty(One(), Two()))
println("Four &lt; Three? " + lt_small_smarty(Four(), Three()))
println("Two &lt; Two? " + lt_small_smarty(Two(), Two()))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 4.4 We can define a data type for simple arithmetic expressions as
 * follows.
 *
 *    type unop = Neg
 *    type binop = Add | Sub | Mul | Div
 *    type exp =
 *      Constant of int
 *      | Unary of unop * exp
 *      | Binary of exp * binop * exp
 *
 * Write a function eval : exp -> int to evaluate an expression, performing
 * the calculation to produce an integer result.
 */
sealed abstract class UnOp
  case class Neg() extends UnOp

sealed abstract class BinOp
  case class Add() extends BinOp
  case class Sub() extends BinOp
  case class Mul() extends BinOp
  case class Div() extends BinOp

sealed abstract class Exp
  case class Constant(value: Int) extends Exp
  case class Unary(unop: UnOp, expr: Exp) extends Exp
  case class Binary(expr1: Exp, binop: BinOp, expr2: Exp) extends Exp

def eval(e: Exp): Int = e match {
  case Constant(i)        => i
  case Unary(Neg(), e)    => -1 * eval(e)
  case Binary(e1, op, e2) => {
    val (el, er) = (eval(e1), eval(e2))
    val ret = op match {
      case Add() => el + er
      case Sub() => el - er
      case Mul() => el * er
      case Div() => el / er
    }
    ret
  }
}


// Test
val b1 = Binary(Constant(12), Add(), Constant(15))
val u1 = Unary(Neg(), Constant(10))
val express = Binary(b1, Sub(), u1)
println("Evaluation of (12 + 15) - (-10) = 37: ")
println(express + " = " + eval(express))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 4.5. A way to implement a dictionary is with tree, where each
 * node in the tree has a label and a value.
 *
 * 1. Implement a polymorphic dictionary, (’key, ’value) dictionary, as a tree
 * with the three dictionary operations.
 *
 *    empty: (’key, ’value) dict
 *    add: (’key, ’value) dict -> ’key -> ’value -> (’key, ’value) dict
 *    find : (’key, ’value) dict -> ’key -> ’value
 *
 */
sealed abstract class Dict[T,U]
  case class Node[T,U](no:Tuple2[T,U], l: Dict[T,U], r: Dict[T,U])
    extends Dict[T,U]
  case class Leaf[T,U]() extends Dict[T,U]

def empty = Leaf()

def add[T &lt; % Ordered[T],U](dict: Dict[T, U], key: T, value: U): Dict[T,U] =
  dict match {
    case Leaf() =>
      Node((key, value), Leaf(), Leaf())
    case Node((k, v), left, right) if key &lt; k =>
      Node((k, v), add(left, key, value), right)
    case Node((k, v), left, right) if key > k =>
      Node((k, v), left, add(right, key, value))
    case Node((k, v), left, right) if key == k =>
      Node((key, value), left, right)
    case _ => throw new Exception("Invalid Argument in add dict.")
  }

def find[T &lt; % Ordered[T],U](dict: Dict[T, U], key: T): U =
  dict match {
    case Leaf() => throw new Exception("Not Found.")
    case Node((k, v), left, right) if key &lt; k => find(left, key)
    case Node((k, v), left, right) if key > k => find(right, key)
    case Node((k, v), left, right) if key == k => v
    case _ => throw new Exception("Invalid Argument in add dict.")
  }</pre>

&nbsp;

&nbsp;

<pre lang="scala">/** 
 * Exercise 4.6 Consider the function insert for unbalanced, ordered, binary
 * trees. One potential implementation problem is when uses the builtin
 * comparison (&lt; ). Rewrite the definition so the it is parameterized by a
 * comparison function that, given two elements, returns on of three values
 *
 *    type comparison = LessThan | Equal | GreaterThan.
 *
 * The expression insert compare x tree inserts an element x into the tree
 * tree. The type is
 * 
 *    insert : (’a -> ’a -> comparison) -> ’a -> ’a tree -> ’a tree.
 */

sealed abstract class Tree[T]
  case class Leaf[T]() extends Tree[T]
  case class Node[T](v: T, left: Tree[T], right: Tree[T]) extends Tree[T]

sealed abstract class Comparison
  case class LessThan() extends Comparison
  case class Equal() extends Comparison
  case class GreaterThan() extends Comparison

def insert[T](value: T, tree: Tree[T]) (comp: Comparison): Tree[T] =
  tree match {
    case Leaf() => Node(value, Leaf(), Leaf())
    case Node(v, left, right) =>
      comp match {
        case Equal() => Node(v, left, right)
        case LessThan() => Node(v, insert(value, left){comp}, right)
        case GreaterThan() => Node(v, left, insert(value, right){comp})
      }
  }

def listToTree[T](l: List[T]): Tree[T] = l match {
  case Nil    => Leaf()
  case h :: t => insert(h, listToTree(t)){LessThan()}
}


// Tests
val list = List(7, 5, 9, 11, 3)
val tree = listToTree(list)

println("Convert list: " + list + " into tree: " + tree)</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 4.7 A heap of integers is a data structure supporting the
 * following operations.
 *
 *   makeheap: int -> heap: create a heap containing a single element,
 *
 *   insert: heap -> int -> heap: add an element to a heap; duplicates are
 *            alowed,
 * 
 *   findmin: heap -> int: return the smallest element of the heap.
 *
 *   deletemin: heap -> heap: return a new heap that is the same as the
 *               original, without the smallest element.
 *
 *   meld: heap -> heap -> heap: join two heaps into a new heap containing the
 *         elements of both.
 *
 * A heap can be represented as a binary tree, where for any node a, if b is a
 * child node of a, then label(a) &lt; = label(b). The order of children does not
 * matter. A pairing heap is a particular implementation where the operations
 * are performed as follows.
 *
 *    makeheap i: produce a single-node tree with i at the root.
 *
 *    insert h i = meld h (makeheap i).
 *
 *    findmin h: return the root label.
 *
 *    deletemin h: remove the root, and meld the subtrees.
 *
 *    meld h1 h2: compare the roots, and make the heap with the larger element
 *    a subtree of the other.
 *
 * 1. Define a type heap and implement the five operations.
 * 
 * 2. A heap sort is performed by inserting the elements to be sorted into a
 *    heap, then the values are extracted from smallest to largest. Write a
 *    function heap_sort : int list -> int list that performs a heap sort,
 *    where the result is sorted from largest to smallest.
 */

// 1. Define a type heap and implement the five operations.
type T = Int

sealed abstract class Heap
  case class Node(value: T, l: List[Node]) extends Heap

def makeheap(i: T) = Node(i, Nil)

def meld(h1: Node, h2: Node): Node = (h1, h2) match {
  case (Node(hh1: T, t1: List[Node]), Node(hh2: T, t2: List[Node])) => 
    if (hh1 > hh2) Node(hh1, h2 :: t1)
    else Node(hh2, h1 :: t2)
}

def insert(h: Node, i: T): Node =
  meld(h, makeheap(i))

def findmin(h: Node): T = h match {
  case Node(i: T, _) => i
}

def deletemin(h: Node): Node = h match {
  case Node(_, h :: t) => {
    def iter(h: Node, acc: List[Node]): Node = acc match {
      case x :: t => iter(meld(h, x), t)
      case Nil    => h
    }
    iter(h, t)
  }
  case Node(_, List(h)) => h
  case Node(_, Nil) => throw new Exception("Invalid Argument in deletemin.")
}

// 2. heapsort

def heap_sort(l: List[T]): List[T] = l match {
  case Nil => Nil
  case x :: t => {
    def insertList(h: Node, l: List[T]): Node = l match {
      case Nil => h
      case x :: t => insertList(insert(h, x), t)
    }
    def iter(sorted: List[T], h: Node): List[T] = h match {
      case Node(x, Nil) => x :: sorted
      case _ => iter(findmin(h) :: sorted, deletemin(h))
    }
    iter(Nil, insertList(makeheap(x), t))
  }
}

// tests
var h = makeheap(12)
h = insert(h, 1)
h = insert(h, 17)
h = insert(h, 200)
val l = List(5, 7, 8, 10, 11, 0, 101, 112, 99)
println("heap: " + h)
println(l + " sorted " + heap_sort(l))</pre>
