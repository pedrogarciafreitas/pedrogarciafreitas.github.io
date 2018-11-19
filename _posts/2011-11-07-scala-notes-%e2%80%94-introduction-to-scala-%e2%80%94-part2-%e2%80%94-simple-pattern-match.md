---
id: 1393
title: Introduction To Scala — Part2 — Simple Pattern Match
date: 2011-11-07T15:55:16+00:00
author: CKPYT
excerpt: "Exercises of the book 'Introduction to Objective Caml' solved in Scala."
layout: post
guid: http://www.sawp.com.br/blog/?p=1393
permalink: p=1393
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:6433:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * Exercise 2.1 Suppose we have a crypto-system based on the following
    * substitution cipher, where each plain letter is encrypted according to the
    * following table.
    *
    *    |   Plain   | Encrypted |
    *    |     A     |     C     |
    *    |     B     |     A     |
    *    |     C     |     D     |
    *    |     D     |     B     |
    *
    * For example, the string BAD would be encrypted as ACB.
    * Write a function check that, given a plaintext string s1 and a ciphertext
    * string s2, returns true if, and only if, s2 is the ciphertext for s1.
    * Your function should raise an exception if s1 is not a plaintext string.
    * How does your code scale as the alphabet gets larger?
    *
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> encryptSingleChar<span style="color: #F78811;">&#40;</span>c<span style="color: #000080;">:</span> Char<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> c <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #6666FF;">'A'</span> <span style="color: #000080;">=&gt;</span> <span style="color: #6666FF;">'C'</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #6666FF;">'B'</span> <span style="color: #000080;">=&gt;</span> <span style="color: #6666FF;">'A'</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #6666FF;">'C'</span> <span style="color: #000080;">=&gt;</span> <span style="color: #6666FF;">'D'</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #6666FF;">'D'</span> <span style="color: #000080;">=&gt;</span> <span style="color: #6666FF;">'B'</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span>   <span style="color: #000080;">=&gt;</span>
    <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Invalid Argument &quot;</span> + c + <span style="color: #6666FF;">&quot; in encryptSingleChar&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> encryptString<span style="color: #F78811;">&#40;</span>s<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> iter<span style="color: #F78811;">&#40;</span>i<span style="color: #000080;">:</span> Int, acc<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> String <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">==</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> encryptSingleChar<span style="color: #F78811;">&#40;</span>s<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> + acc
    <span style="color: #0000ff; font-weight: bold;">else</span> iter<span style="color: #F78811;">&#40;</span>i - <span style="color: #F78811;">1</span>, encryptSingleChar<span style="color: #F78811;">&#40;</span>s<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> + acc<span style="color: #F78811;">&#41;</span>
    iter<span style="color: #F78811;">&#40;</span>s.<span style="color: #000000;">length</span> - <span style="color: #F78811;">1</span>, <span style="color: #6666FF;">&quot;&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> compare<span style="color: #F78811;">&#40;</span>s1<span style="color: #000080;">:</span> String, s2<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    encryptString<span style="color: #F78811;">&#40;</span>s1<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">==</span> s2
    &nbsp;
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;The 'BAD' string encrypted is &quot;</span> + encryptString<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;BAD&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Exercise 2.1 Suppose we have a crypto-system based on the following
    * substitution cipher, where each plain letter is encrypted according to the
    * following table.
    *
    *    |   Plain   | Encrypted |
    *    |     A     |     C     |
    *    |     B     |     A     |
    *    |     C     |     D     |
    *    |     D     |     B     |
    *
    * For example, the string BAD would be encrypted as ACB.
    * Write a function check that, given a plaintext string s1 and a ciphertext
    * string s2, returns true if, and only if, s2 is the ciphertext for s1.
    * Your function should raise an exception if s1 is not a plaintext string.
    * How does your code scale as the alphabet gets larger?
    *
    */
    
    def encryptSingleChar(c: Char) = c match {
    case 'A' =&gt; 'C'
    case 'B' =&gt; 'A'
    case 'C' =&gt; 'D'
    case 'D' =&gt; 'B'
    case _   =&gt;
    throw new Exception(&quot;Invalid Argument &quot; + c + &quot; in encryptSingleChar&quot;)
    }
    
    def encryptString(s: String) = {
    def iter(i: Int, acc: String): String =
    if (i == 0) encryptSingleChar(s(i)) + acc
    else iter(i - 1, encryptSingleChar(s(i)) + acc)
    iter(s.length - 1, &quot;&quot;)
    }
    
    def compare(s1: String, s2: String) =
    encryptString(s1) == s2
    
    
    println(&quot;The 'BAD' string encrypted is &quot; + encryptString(&quot;BAD&quot;))</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">/**
 * Exercise 2.1 Suppose we have a crypto-system based on the following
 * substitution cipher, where each plain letter is encrypted according to the
 * following table.
 *
 *    |   Plain   | Encrypted |
 *    |     A     |     C     |
 *    |     B     |     A     |
 *    |     C     |     D     |
 *    |     D     |     B     |
 *
 * For example, the string BAD would be encrypted as ACB.
 * Write a function check that, given a plaintext string s1 and a ciphertext
 * string s2, returns true if, and only if, s2 is the ciphertext for s1. 
 * Your function should raise an exception if s1 is not a plaintext string.
 * How does your code scale as the alphabet gets larger?
 *
 */

def encryptSingleChar(c: Char) = c match {
  case 'A' => 'C'
  case 'B' => 'A'
  case 'C' => 'D'
  case 'D' => 'B'
  case _   =>
    throw new Exception("Invalid Argument " + c + " in encryptSingleChar")
}

def encryptString(s: String) = {
  def iter(i: Int, acc: String): String = 
    if (i == 0) encryptSingleChar(s(i)) + acc
    else iter(i - 1, encryptSingleChar(s(i)) + acc)
  iter(s.length - 1, "")
}

def compare(s1: String, s2: String) = 
  encryptString(s1) == s2


println("The 'BAD' string encrypted is " + encryptString("BAD"))</pre>
