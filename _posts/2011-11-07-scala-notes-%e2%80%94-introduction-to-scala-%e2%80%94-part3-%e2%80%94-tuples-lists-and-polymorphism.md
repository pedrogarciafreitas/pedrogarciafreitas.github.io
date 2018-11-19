---
id: 1399
title: Introduction To Scala — Part3 — Tuples, Lists and Polymorphism
date: 2011-11-07T16:00:47+00:00
author: CKPYT
excerpt: "Exercises of the book 'Introduction to Objective Caml' solved in Scala."
layout: post
guid: http://www.sawp.com.br/blog/?p=1399
permalink: /p=1399
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:12367:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 3.1 Suppose you are implementing a relational employee database,
    * where the database is a list of tuples name * phone * salary:
    *
    * val db = (&quot;John&quot;, &quot;x3456&quot;, 50.1) :: (&quot;Jane&quot;, &quot;x1234&quot;, 107.3) ::
    (&quot;Joan&quot;, &quot;unlisted&quot;, 12.7) :: Nil
    *
    * 1. Write a function find_salary : string -&gt; float that returns the salary
    * of an employee, given the name.
    *
    * 2. Write a general function
    *
    * select : (string * string * float -&gt; bool) -&gt; (string * string * float) list
    *
    * that returns a list of all the tuples that match the predicate. For example
    * the expression select (fun (_, _, salary) -&gt; salary &lt; 100.0) would return
    * the tuples for John and Joan.
    *
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> db <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;John&quot;</span>, <span style="color: #6666FF;">&quot;x3456&quot;</span>, <span style="color: #F78811;">50.1</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Jane&quot;</span>, <span style="color: #6666FF;">&quot;x1234&quot;</span>, <span style="color: #F78811;">107.3</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span>
    <span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Joan&quot;</span>, <span style="color: #6666FF;">&quot;unlisted&quot;</span>, <span style="color: #F78811;">12.7</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> Nil
    &nbsp;
    <span style="color: #008000; font-style: italic;">// to sintetise the code</span>
    <span style="color: #0000ff; font-weight: bold;">type</span> listOfTuples <span style="color: #000080;">=</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>String, String, Double<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// 1 Write a function find_salary : string -&gt; float that returns the salary</span>
    <span style="color: #008000; font-style: italic;">// of an employee, given the name.</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> find<span style="color: #000080;">_</span>salary<span style="color: #F78811;">&#40;</span>name<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> search<span style="color: #F78811;">&#40;</span>t<span style="color: #000080;">:</span> listOfTuples<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Double <span style="color: #000080;">=</span> t <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>name<span style="color: #000080;">_</span>, <span style="color: #000080;">_</span>, salary<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> t <span style="color: #0000ff; font-weight: bold;">if</span> name <span style="color: #000080;">==</span> name<span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> salary
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> search<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span>
    <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Invalid Argument in find_salary&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    search<span style="color: #F78811;">&#40;</span>db<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// Write a general function</span>
    <span style="color: #008000; font-style: italic;">// select : (string * string * float -&gt; bool) -&gt; (string * string * float) list</span>
    <span style="color: #008000; font-style: italic;">// that returns a list of all the tuples that match the predicate. For example</span>
    <span style="color: #008000; font-style: italic;">// the expression select (fun (_, _, salary) -&gt; salary &lt; 100.0) would return</span>
    <span style="color: #008000; font-style: italic;">// the tuples for John and Joan.</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> select<span style="color: #F78811;">&#40;</span>pred<span style="color: #000080;">:</span> <span style="color: #F78811;">&#40;</span>String, String, Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> Boolean<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> search<span style="color: #F78811;">&#40;</span>found<span style="color: #000080;">:</span> listOfTuples<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> listOfTuples <span style="color: #000080;">=</span> found <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>p1, p2, p3<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> t <span style="color: #0000ff; font-weight: bold;">if</span> pred<span style="color: #F78811;">&#40;</span>p1, p2, p3<span style="color: #F78811;">&#41;</span>  <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#40;</span>p1, p2, p3<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> search<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #F78811;">&#40;</span>p1, p2, p3<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> t <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #000080;">!</span>pred<span style="color: #F78811;">&#40;</span>p1, p2, p3<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> search<span style="color: #F78811;">&#40;</span>t<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil <span style="color: #000080;">=&gt;</span> Nil
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Invalid Argument in select function&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    search<span style="color: #F78811;">&#40;</span>db<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #008000; font-style: italic;">// tests</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Searching the salary of 'Joan' at db: &quot;</span> + find<span style="color: #000080;">_</span>salary<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Joan&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;&quot;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> predicate <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span><span style="color: #000080;">_:</span>String, <span style="color: #000080;">_:</span>String, salary<span style="color: #000080;">:</span>Double<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span> <span style="color: #F78811;">&#40;</span>salary <span style="color: #000080;">&lt;</span> <span style="color: #F78811;">100.0</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;All employees that match with predicate 'salary &lt; 100.0': &quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\t</span>&quot;</span> + select<span style="color: #F78811;">&#40;</span>predicate<span style="color: #F78811;">&#41;</span> + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 3.1 Suppose you are implementing a relational employee database,
    * where the database is a list of tuples name * phone * salary:
    *
    * val db = (&quot;John&quot;, &quot;x3456&quot;, 50.1) :: (&quot;Jane&quot;, &quot;x1234&quot;, 107.3) ::
    (&quot;Joan&quot;, &quot;unlisted&quot;, 12.7) :: Nil
    *
    * 1. Write a function find_salary : string -&gt; float that returns the salary
    * of an employee, given the name.
    *
    * 2. Write a general function
    *
    * select : (string * string * float -&gt; bool) -&gt; (string * string * float) list
    *
    * that returns a list of all the tuples that match the predicate. For example
    * the expression select (fun (_, _, salary) -&gt; salary &lt; 100.0) would return
    * the tuples for John and Joan.
    *
    */
    
    val db = (&quot;John&quot;, &quot;x3456&quot;, 50.1) :: (&quot;Jane&quot;, &quot;x1234&quot;, 107.3) ::
    (&quot;Joan&quot;, &quot;unlisted&quot;, 12.7) :: Nil
    
    // to sintetise the code
    type listOfTuples = List[(String, String, Double)]
    
    // 1 Write a function find_salary : string -&gt; float that returns the salary
    // of an employee, given the name.
    def find_salary(name: String) = {
    def search(t: listOfTuples): Double = t match {
    case (name_, _, salary) :: t if name == name_ =&gt; salary
    case _ :: t =&gt; search(t)
    case Nil    =&gt;
    throw new Exception(&quot;Invalid Argument in find_salary&quot;)
    }
    search(db)
    }
    
    
    // Write a general function
    // select : (string * string * float -&gt; bool) -&gt; (string * string * float) list
    // that returns a list of all the tuples that match the predicate. For example
    // the expression select (fun (_, _, salary) -&gt; salary &lt; 100.0) would return
    // the tuples for John and Joan.
    def select(pred: (String, String, Double) =&gt; Boolean) = {
    def search(found: listOfTuples): listOfTuples = found match {
    case (p1, p2, p3) :: t if pred(p1, p2, p3)  =&gt; (p1, p2, p3) :: search(t)
    case (p1, p2, p3) :: t if !pred(p1, p2, p3) =&gt; search(t)
    case Nil =&gt; Nil
    case _ =&gt; throw new Exception(&quot;Invalid Argument in select function&quot;)
    }
    search(db)
    }
    
    
    // tests
    println(&quot;Searching the salary of 'Joan' at db: &quot; + find_salary(&quot;Joan&quot;))
    println(&quot;&quot;)
    
    val predicate = (_:String, _:String, salary:Double) =&gt; (salary &lt; 100.0)
    println(&quot;All employees that match with predicate 'salary &lt; 100.0': &quot;)
    println(&quot;\t&quot; + select(predicate) + &quot;\n&quot;)</p></div>
    ;i:2;s:6390:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 3.2 The function append : ’a list -&gt; ’a list -&gt; ’a list appends two
    * lists. It can be defined as follows:
    *
    * def append(l1: List[A], l2: List[A]): List[A] = l1 match {
    *   case h :: t =&gt; h :: append(t, l2)
    *   case Nil    =&gt; l2
    * }
    *
    * Write a tail-recursive version of append.
    */</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> append<span style="color: #F78811;">&#40;</span>l1<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span>, l2<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> l1 <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> h <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> h <span style="color: #000080;">::</span> append<span style="color: #F78811;">&#40;</span>t, l2<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil    <span style="color: #000080;">=&gt;</span> l2
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> appendTR<span style="color: #F78811;">&#40;</span>l1<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span>, l2<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>l<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span>, ll<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #000080;">_</span><span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> ll <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> h <span style="color: #000080;">::</span> ll <span style="color: #000080;">=&gt;</span> iter<span style="color: #F78811;">&#40;</span>h <span style="color: #000080;">::</span> l, ll<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Nil     <span style="color: #000080;">=&gt;</span> l
    <span style="color: #F78811;">&#125;</span>
    iter<span style="color: #F78811;">&#40;</span>l2, l1.<span style="color: #000000;">reverse</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic;">// tests</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> l1 <span style="color: #000080;">=</span> <span style="color: #F78811;">1</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">2</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">3</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">4</span> <span style="color: #000080;">::</span> Nil
    <span style="color: #0000ff; font-weight: bold;">val</span> l2 <span style="color: #000080;">=</span> <span style="color: #F78811;">6</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">7</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">8</span> <span style="color: #000080;">::</span> Nil
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Append of &quot;</span> + l1 + <span style="color: #6666FF;">&quot; + &quot;</span> + l2 + <span style="color: #6666FF;">&quot; = &quot;</span> + append<span style="color: #F78811;">&#40;</span>l1, l2<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Tail Recursive of &quot;</span> + l1 + <span style="color: #6666FF;">&quot; + &quot;</span> + l2 + <span style="color: #6666FF;">&quot; = &quot;</span> + appendTR<span style="color: #F78811;">&#40;</span>l1, l2<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 3.2 The function append : ’a list -&gt; ’a list -&gt; ’a list appends two
    * lists. It can be defined as follows:
    *
    * def append(l1: List[A], l2: List[A]): List[A] = l1 match {
    *   case h :: t =&gt; h :: append(t, l2)
    *   case Nil    =&gt; l2
    * }
    *
    * Write a tail-recursive version of append.
    */
    def append(l1: List[_], l2: List[_]): List[_] = l1 match {
    case h :: t =&gt; h :: append(t, l2)
    case Nil    =&gt; l2
    }
    
    def appendTR(l1: List[_], l2: List[_]) = {
    def iter(l: List[_], ll: List[_]): List[_] = ll match {
    case h :: ll =&gt; iter(h :: l, ll)
    case Nil     =&gt; l
    }
    iter(l2, l1.reverse)
    }
    
    // tests
    val l1 = 1 :: 2 :: 3 :: 4 :: Nil
    val l2 = 6 :: 7 :: 8 :: Nil
    
    println(&quot;Append of &quot; + l1 + &quot; + &quot; + l2 + &quot; = &quot; + append(l1, l2))
    println(&quot;Tail Recursive of &quot; + l1 + &quot; + &quot; + l2 + &quot; = &quot; + appendTR(l1, l2))</p></div>
    ;i:3;s:4710:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 3.3. It is known that a welfare crook lives in Los Angeles.
    * You are given lists for
    *
    * 1) people receiving welfare,
    * 2) Hollywood actors, and
    * 3) residents of Beverly Hills.
    *
    * The names in each list are sorted alphabetically (by &lt; ). A welfare crook is
    * someone who appears in all three lists. Write an algorithm to find at least
    * one crook.
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> findCrook<span style="color: #F78811;">&#40;</span>people<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span>, actors<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span>,
    residents<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span>
    <span style="color: #F78811;">&#40;</span>people, actors, residents<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>ph <span style="color: #000080;">::</span> pt<span style="color: #F78811;">&#41;</span>, <span style="color: #F78811;">&#40;</span>ah <span style="color: #000080;">::</span> at<span style="color: #F78811;">&#41;</span>, <span style="color: #F78811;">&#40;</span>rh <span style="color: #000080;">::</span> rt<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=&gt;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>ph <span style="color: #000080;">&lt;</span> ah || ph <span style="color: #000080;">&lt;</span> rh<span style="color: #F78811;">&#41;</span> findCrook<span style="color: #F78811;">&#40;</span>pt, ah, rh<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>ah <span style="color: #000080;">&lt;</span> ph || ah <span style="color: #000080;">&lt;</span> rh<span style="color: #F78811;">&#41;</span> findCrook<span style="color: #F78811;">&#40;</span>ph, at, rh<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>rh <span style="color: #000080;">&lt;</span> ph || rh <span style="color: #000080;">&lt;</span> ah<span style="color: #F78811;">&#41;</span> findCrook<span style="color: #F78811;">&#40;</span>ph, ag, rt<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span> ph
    <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Invalid Argument in findCrook&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 3.3. It is known that a welfare crook lives in Los Angeles.
    * You are given lists for
    *
    * 1) people receiving welfare,
    * 2) Hollywood actors, and
    * 3) residents of Beverly Hills.
    *
    * The names in each list are sorted alphabetically (by &lt; ). A welfare crook is
    * someone who appears in all three lists. Write an algorithm to find at least
    * one crook.
    */
    
    def findCrook(people: List[String], actors: List[String],
    residents: List[String]): List[String] =
    (people, actors, residents) match {
    ((ph :: pt), (ah :: at), (rh :: rt)) =&gt;
    if (ph &lt; ah || ph &lt; rh) findCrook(pt, ah, rh)
    else if (ah &lt; ph || ah &lt; rh) findCrook(ph, at, rh)
    else if (rh &lt; ph || rh &lt; ah) findCrook(ph, ag, rt)
    else ph
    _ =&gt; throw new Exception(&quot;Invalid Argument in findCrook&quot;)
    }</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 3.1 Suppose you are implementing a relational employee database,
 * where the database is a list of tuples name * phone * salary:
 *
 * val db = ("John", "x3456", 50.1) :: ("Jane", "x1234", 107.3) ::
            ("Joan", "unlisted", 12.7) :: Nil
 *
 * 1. Write a function find_salary : string -> float that returns the salary
 * of an employee, given the name.
 *
 * 2. Write a general function
 *
 * select : (string * string * float -> bool) -> (string * string * float) list
 *
 * that returns a list of all the tuples that match the predicate. For example
 * the expression select (fun (_, _, salary) -> salary &lt; 100.0) would return
 * the tuples for John and Joan.
 *
 */

val db = ("John", "x3456", 50.1) :: ("Jane", "x1234", 107.3) ::
         ("Joan", "unlisted", 12.7) :: Nil

// to sintetise the code
type listOfTuples = List[(String, String, Double)]

// 1 Write a function find_salary : string -> float that returns the salary
// of an employee, given the name.
def find_salary(name: String) = {
  def search(t: listOfTuples): Double = t match {
    case (name_, _, salary) :: t if name == name_ => salary
    case _ :: t => search(t)
    case Nil    =>
      throw new Exception("Invalid Argument in find_salary")
  }
  search(db)
}


// Write a general function
// select : (string * string * float -> bool) -> (string * string * float) list
// that returns a list of all the tuples that match the predicate. For example
// the expression select (fun (_, _, salary) -> salary &lt; 100.0) would return
// the tuples for John and Joan.
def select(pred: (String, String, Double) => Boolean) = {
  def search(found: listOfTuples): listOfTuples = found match {
    case (p1, p2, p3) :: t if pred(p1, p2, p3)  => (p1, p2, p3) :: search(t)
    case (p1, p2, p3) :: t if !pred(p1, p2, p3) => search(t)
    case Nil => Nil
    case _ => throw new Exception("Invalid Argument in select function")
  }
  search(db)
}


// tests
println("Searching the salary of 'Joan' at db: " + find_salary("Joan"))
println("")

val predicate = (_:String, _:String, salary:Double) => (salary &lt; 100.0)
println("All employees that match with predicate 'salary &lt; 100.0': ")
println("\t" + select(predicate) + "\n")</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 3.2 The function append : ’a list -> ’a list -> ’a list appends two
 * lists. It can be defined as follows:
 *
 * def append(l1: List[A], l2: List[A]): List[A] = l1 match {
 *   case h :: t => h :: append(t, l2)
 *   case Nil    => l2
 * }
 *
 * Write a tail-recursive version of append.
*/
def append(l1: List[_], l2: List[_]): List[_] = l1 match {
  case h :: t => h :: append(t, l2)
  case Nil    => l2
}

def appendTR(l1: List[_], l2: List[_]) = {
  def iter(l: List[_], ll: List[_]): List[_] = ll match {
    case h :: ll => iter(h :: l, ll)
    case Nil     => l
  }
  iter(l2, l1.reverse)
}

// tests
val l1 = 1 :: 2 :: 3 :: 4 :: Nil
val l2 = 6 :: 7 :: 8 :: Nil

println("Append of " + l1 + " + " + l2 + " = " + append(l1, l2))
println("Tail Recursive of " + l1 + " + " + l2 + " = " + appendTR(l1, l2))</pre>

&nbsp;

&nbsp;

<pre lang="scala">/**
 * Exercise 3.3. It is known that a welfare crook lives in Los Angeles.
 * You are given lists for
 *
 * 1) people receiving welfare,
 * 2) Hollywood actors, and
 * 3) residents of Beverly Hills.
 *
 * The names in each list are sorted alphabetically (by &lt; ). A welfare crook is
 * someone who appears in all three lists. Write an algorithm to find at least
 * one crook.
 */

def findCrook(people: List[String], actors: List[String],
              residents: List[String]): List[String] =
  (people, actors, residents) match {
    ((ph :: pt), (ah :: at), (rh :: rt)) =>
      if (ph &lt; ah || ph &lt; rh) findCrook(pt, ah, rh)
      else if (ah &lt; ph || ah &lt; rh) findCrook(ph, at, rh)
      else if (rh &lt; ph || rh &lt; ah) findCrook(ph, ag, rt)
      else ph
    _ => throw new Exception("Invalid Argument in findCrook")
  }</pre>
