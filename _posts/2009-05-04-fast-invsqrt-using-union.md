---
id: 305
title: Others InvSqrt implementations
date: 2009-05-04T18:50:30+00:00
author: SAWP
excerpt: Veja aqui algumas alternativas à implementação da Fast InvSqrt.
layout: post
guid: http://www.sawp.com.br/blog/?p=305
permalink: /p=305
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:2327:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #993333;">float</span> InvSqrt <span style="color: #009900;">&#40;</span><span style="color: #993333;">float</span> x<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #993333;">float</span> xhalf <span style="color: #339933;">=</span> <span style="color:#800080;">0.5f</span><span style="color: #339933;">*</span>x<span style="color: #339933;">;</span>
    <span style="color: #993333;">int</span> i <span style="color: #339933;">=</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span><span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">&amp;</span>x<span style="color: #339933;">;</span>
    i <span style="color: #339933;">=</span> <span style="color: #208080;">0x5f3759df</span> <span style="color: #339933;">-</span> <span style="color: #009900;">&#40;</span>i<span style="color: #339933;">&gt;&gt;</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    x <span style="color: #339933;">=</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span><span style="color: #993333;">float</span><span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">&amp;</span>i<span style="color: #339933;">;</span>
    x <span style="color: #339933;">=</span> x<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span><span style="color:#800080;">1.5f</span> <span style="color: #339933;">-</span> xhalf<span style="color: #339933;">*</span>x<span style="color: #339933;">*</span>x<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">return</span> x<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">float InvSqrt (float x) {
    float xhalf = 0.5f*x;
    int i = *(int*)&amp;x;
    i = 0x5f3759df - (i&gt;&gt;1);
    x = *(float*)&amp;i;
    x = x*(1.5f - xhalf*x*x);
    return x;
    }</p></div>
    ;i:2;s:3172:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/**
    * UnionInvSqrt.c
    * Author: Pedro Garcia
    *
    * http://www.sawp.com.br
    * Licensed by Creative Commons: http://creativecommons.org/licenses/by-nc-nd/2.5/en/
    **/</span>
    <span style="color: #993333;">union</span> casting <span style="color: #009900;">&#123;</span>
    <span style="color: #993333;">int</span> i<span style="color: #339933;">;</span>
    <span style="color: #993333;">float</span> f<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #993333;">float</span> UnionInvSqrt <span style="color: #009900;">&#40;</span><span style="color: #993333;">float</span> x<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #993333;">union</span> casting cast<span style="color: #339933;">;</span>
    <span style="color: #993333;">float</span> xhalf <span style="color: #339933;">=</span> <span style="color:#800080;">0.5f</span><span style="color: #339933;">*</span>x<span style="color: #339933;">;</span>
    cast.<span style="color: #202020;">f</span> <span style="color: #339933;">=</span> x<span style="color: #339933;">;</span>
    cast.<span style="color: #202020;">i</span> <span style="color: #339933;">=</span> <span style="color: #208080;">0x5f3759df</span> <span style="color: #339933;">-</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>cast.<span style="color: #202020;">i</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">&gt;&gt;</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>        <span style="color: #666666; font-style: italic;">//   x = *(float*)&amp;i; and i = 0x5f3759df - (i&gt;&gt;1);</span>
    <span style="color: #b1b100;">return</span> cast.<span style="color: #202020;">f</span><span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span><span style="color:#800080;">1.5f</span> <span style="color: #339933;">-</span> xhalf<span style="color: #339933;">*</span>cast.<span style="color: #202020;">f</span><span style="color: #339933;">*</span>cast.<span style="color: #202020;">f</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//   x = x*(1.5f - xhalf*x*x);</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * UnionInvSqrt.c
    * Author: Pedro Garcia
    *
    * http://www.sawp.com.br
    * Licensed by Creative Commons: http://creativecommons.org/licenses/by-nc-nd/2.5/en/
    **/
    union casting {
    int i;
    float f;
    };
    
    float UnionInvSqrt (float x) {
    union casting cast;
    float xhalf = 0.5f*x;
    cast.f = x;
    cast.i = 0x5f3759df - ((cast.i)&gt;&gt;1);        //   x = *(float*)&amp;i; and i = 0x5f3759df - (i&gt;&gt;1);
    return cast.f*(1.5f - xhalf*cast.f*cast.f); //   x = x*(1.5f - xhalf*x*x);
    }</p></div>
    ;i:3;s:2997:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #008000; font-style: italic; font-weight: bold;">/**
    * Java InvSqrt
    * Author: Pedro Garcia
    * sawp@sawp.com.br
    * http://www.sawp.com.br
    * Licensed by Creative Commons: http://creativecommons.org/licenses/by-nc-nd/2.5/en/
    **/</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">strictfp</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">float</span> InvSqrt<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">float</span> x<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    <span style="color: #000066; font-weight: bold;">float</span> xhalf <span style="color: #339933;">=</span> 0.5f <span style="color: #339933;">*</span> x<span style="color: #339933;">;</span>
    <span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #003399;">Float</span>.<span style="color: #006633;">floatToRawIntBits</span><span style="color: #009900;">&#40;</span>x<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// convert integer to keep the representation IEEE 754</span>
    &nbsp;
    i <span style="color: #339933;">=</span> 0x5f3759df <span style="color: #339933;">-</span> <span style="color: #009900;">&#40;</span>i <span style="color: #339933;">&gt;&gt;</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    x <span style="color: #339933;">=</span> <span style="color: #003399;">Float</span>.<span style="color: #006633;">intBitsToFloat</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    x <span style="color: #339933;">=</span> x <span style="color: #339933;">*</span> <span style="color: #009900;">&#40;</span>1.5f <span style="color: #339933;">-</span> xhalf <span style="color: #339933;">*</span> x <span style="color: #339933;">*</span> x<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">return</span> x<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Java InvSqrt
    * Author: Pedro Garcia
    * sawp@sawp.com.br
    * http://www.sawp.com.br
    * Licensed by Creative Commons: http://creativecommons.org/licenses/by-nc-nd/2.5/en/
    **/
    
    strictfp static float InvSqrt(float x){
    float xhalf = 0.5f * x;
    int i = Float.floatToRawIntBits(x); // convert integer to keep the representation IEEE 754
    
    i = 0x5f3759df - (i &gt;&gt; 1);
    x = Float.intBitsToFloat(i);
    x = x * (1.5f - xhalf * x * x);
    
    return x;
    }</p></div>
    ;i:4;s:2688:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #993333;">float</span> InvSqrt<span style="color: #009900;">&#40;</span><span style="color: #993333;">float</span> x<span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
    <span style="color: #993333;">float</span> xhalf <span style="color: #339933;">=</span> <span style="color:#800080;">0.5f</span> <span style="color: #339933;">*</span> x<span style="color: #339933;">;</span>
    <span style="color: #993333;">int</span> i <span style="color: #339933;">=</span> BitConverter.<span style="color: #202020;">ToInt32</span><span style="color: #009900;">&#40;</span>BitConverter.<span style="color: #202020;">GetBytes</span><span style="color: #009900;">&#40;</span>x<span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    i <span style="color: #339933;">=</span> <span style="color: #208080;">0x5f3759df</span> <span style="color: #339933;">-</span> <span style="color: #009900;">&#40;</span>i <span style="color: #339933;">&gt;&gt;</span> <span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    x <span style="color: #339933;">=</span> BitConverter.<span style="color: #202020;">ToSingle</span><span style="color: #009900;">&#40;</span>BitConverter.<span style="color: #202020;">GetBytes</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    x <span style="color: #339933;">=</span> x <span style="color: #339933;">*</span> <span style="color: #009900;">&#40;</span><span style="color:#800080;">1.5f</span> <span style="color: #339933;">-</span> xhalf <span style="color: #339933;">*</span> x <span style="color: #339933;">*</span> x<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">return</span> x<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">float InvSqrt(float x)
    {
    float xhalf = 0.5f * x;
    int i = BitConverter.ToInt32(BitConverter.GetBytes(x), 0);
    i = 0x5f3759df - (i &gt;&gt; 1);
    x = BitConverter.ToSingle(BitConverter.GetBytes(i), 0);
    x = x * (1.5f - xhalf * x * x);
    return x;
    }</p></div>
    ;i:5;s:5742:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="fortran" style="font-family:monospace;"><span style="color: #000066;">real</span> <span style="color: #b1b100;">function</span> InvSqrt<span style="color: #009900;">&#40;</span>x<span style="color: #009900;">&#41;</span>
    <span style="color: #000066;">implicit</span> <span style="color: #000066;">none</span>
    &nbsp;
    <span style="color: #000066;">type</span> casting
    <span style="color: #000066;">real</span> <span style="color: #339933;">::</span> <span style="color: #202020;">x</span>
    <span style="color: #b1b100;">end</span> <span style="color: #000066;">type</span> casting
    &nbsp;
    <span style="color: #000066;">real</span>, <span style="color: #000066;">intent</span><span style="color: #009900;">&#40;</span><span style="color: #000066;">in</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">::</span> <span style="color: #202020;">x</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">! castinger</span>
    <span style="color: #000066;">type</span><span style="color: #009900;">&#40;</span>casting<span style="color: #009900;">&#41;</span>, <span style="color: #000066;">target</span> <span style="color: #339933;">::</span> <span style="color: #202020;">pointerTo</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">! Encode data as an array of integers</span>
    <span style="color: #000066;">integer</span>, <span style="color: #000066;">dimension</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">:</span><span style="color: #009900;">&#41;</span>, <span style="color: #000066;">allocatable</span> <span style="color: #339933;">::</span> <span style="color: #202020;">enc</span>
    <span style="color: #000066;">integer</span> <span style="color: #339933;">::</span> <span style="color: #202020;">length</span>
    <span style="color: #000066;">real</span> <span style="color: #339933;">::</span> <span style="color: #202020;">xhalf</span>
    &nbsp;
    xhalf <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0.5</span> <span style="color: #339933;">*</span> x
    &nbsp;
    <span style="color: #666666; font-style: italic;">! transfer to heap (&quot;promiscuous&quot; operation)</span>
    pointerTo<span style="color: #339933;">%</span>x <span style="color: #339933;">=</span> x
    &nbsp;
    <span style="color: #666666; font-style: italic;">! encode a memory section from a type to other</span>
    length <span style="color: #339933;">=</span> <span style="color: #993333;">size</span><span style="color: #009900;">&#40;</span><span style="color: #993333;">transfer</span><span style="color: #009900;">&#40;</span>pointerTo, enc<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #b1b100;">allocate</span><span style="color: #009900;">&#40;</span>enc<span style="color: #009900;">&#40;</span>length<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #666666; font-style: italic;">! encoded to integer, now, operate</span>
    enc <span style="color: #339933;">=</span> <span style="color: #993333;">transfer</span><span style="color: #009900;">&#40;</span>pointerTo, enc<span style="color: #009900;">&#41;</span>
    &nbsp;
    enc<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1597463007</span> <span style="color: #339933;">-</span> rshift<span style="color: #009900;">&#40;</span>enc<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span>,<span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">! decode</span>
    pointerTo <span style="color: #339933;">=</span> <span style="color: #993333;">transfer</span><span style="color: #009900;">&#40;</span>enc, pointerTo<span style="color: #009900;">&#41;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">! dealloc</span>
    <span style="color: #b1b100;">deallocate</span><span style="color: #009900;">&#40;</span>enc<span style="color: #009900;">&#41;</span>
    &nbsp;
    InvSqrt <span style="color: #339933;">=</span> pointerTo<span style="color: #339933;">%</span>x<span style="color: #339933;">*</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1.5</span> <span style="color: #339933;">-</span> xhalf<span style="color: #339933;">*</span>pointerTo<span style="color: #339933;">%</span>x<span style="color: #339933;">*</span>pointerTo<span style="color: #339933;">%</span>x<span style="color: #009900;">&#41;</span>
    <span style="color: #b1b100;">end</span> <span style="color: #b1b100;">function</span> InvSqrt</pre></td></tr></table><p class="theCode" style="display:none;">real function InvSqrt(x)
    implicit none
    
    type casting
    real :: x
    end type casting
    
    real, intent(in) :: x
    
    ! castinger
    type(casting), target :: pointerTo
    
    ! Encode data as an array of integers
    integer, dimension(:), allocatable :: enc
    integer :: length
    real :: xhalf
    
    xhalf = 0.5 * x
    
    ! transfer to heap (&quot;promiscuous&quot; operation)
    pointerTo%x = x
    
    ! encode a memory section from a type to other
    length = size(transfer(pointerTo, enc))
    allocate(enc(length))
    ! encoded to integer, now, operate
    enc = transfer(pointerTo, enc)
    
    enc(1) = 1597463007 - rshift(enc(1),1)
    
    ! decode
    pointerTo = transfer(enc, pointerTo)
    
    ! dealloc
    deallocate(enc)
    
    InvSqrt = pointerTo%x*(1.5 - xhalf*pointerTo%x*pointerTo%x)
    end function InvSqrt</p></div>
    ";}
categories:
  - Miscellaneous
---
A month ago &#8211; April 2009 – I was talking with a friend about computational methods, efficiency of algorithms, and as common in these areas, implementations of Newton-Raphson method. He commented on the Fast InvSqrt function, used on Quake III’s code, which used to be faster than using the inverse of sqrt (the native library). At the same day, I did a research in google. Several interesting links &#8211; ([1] gamedev, [2] LOMONTE CHRIS, [3] betterexplained.com) &#8211; which taught me about the function: 

<pre lang="c">float InvSqrt (float x) {
	float xhalf = 0.5f*x;
	int i = *(int*)&x;
	i = 0x5f3759df - (i>>1);
	x = *(float*)&i;
	x = x*(1.5f - xhalf*x*x);
	return x;
}</pre>

Then I compiled the function in some small programs to test the efficiency between invSqrt and the native implementation (float) (1.0/sqrt (x)). 

The result was a little disappointing. The native implementation was faster than using the InvSqrt, possibly because architectures and compilers should have improved much in floating point arithmetics since 1999, when Quake III was released. And then I modify the implementation of the function using C union 

<pre lang="c">/**
* UnionInvSqrt.c
* Author: Pedro Garcia
*
* http://www.sawp.com.br
* Licensed by Creative Commons: http://creativecommons.org/licenses/by-nc-nd/2.5/en/
**/
union casting {
	int i;
	float f;
};

float UnionInvSqrt (float x) {
	union casting cast;
	float xhalf = 0.5f*x;
	cast.f = x;
	cast.i = 0x5f3759df - ((cast.i)>>1);        //   x = *(float*)&i; and i = 0x5f3759df - (i>>1);
	return cast.f*(1.5f - xhalf*cast.f*cast.f); //   x = x*(1.5f - xhalf*x*x);
}</pre>

Certainly my function didn’t improve the efficiency in relation to the native implementation. However, using the same numerical value of invsqrt, we can obtain a small improvement in performance using it.

The way used to compare the performance of each function was very simple: in a pre-defined time for execution, which function would generate more terms? In 5 minutes, how many times the function (1/sqrt, UnionSqrt or InvSqrt) would run the code and return?
  
By running in a pre-determined time, the average speed of the generation of terms can be found as:

<p style="text-align: center;">
  <v>=(number of elements generated)/(pre-defined time)
</p>

where

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-307" title="fig12_fig0" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig0.gif" alt="fig12_fig0" width="278" height="28" />
</p>

Obviously, the faster implementation will generate more elements in the same pre-determined time. Therefore, the higher number of elements represents the faster function. Although the operating system processes were the only ones running (no graphical interface nor any other application sharing the processor time), it is natural that the implementation of a program has small variations in execution speed that doesn’t depend of the implementation of the code, but depend of the OS Scheduling. So, to ensure that the oscillation caused by the scheduling would not affect this comparison, I used a variable to store the value of the sum of the elements:

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-308" title="fig12_fig1" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig1.gif" alt="fig12_fig1" width="165" height="27" />
</p>

This series is known as the **Riemann Zeta Function**.

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-309" title="fig12_fig2" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig2.gif" alt="fig12_fig2" width="106" height="37" />
</p>

If S = 1/2, the function that we used for testing

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-310" title="fig12_fig3" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig3.gif" alt="fig12_fig3" width="90" height="40" />
</p>

Thus, the result of the calculations were:

<p style="text-align: center;">
  Using InvSqrt (x):: Terms [1543696484], Serie [380334.639206]
</p>

<p style="text-align: center;">
  Using 1/sqrt (x):: Terms [1623751167], Serie [400518.164524]
</p>

<p style="text-align: center;">
  Using UnionInvSqrt (x):: Terms [1569004170], Serie [386502.806938]
</p>

As I said earlier, the average speed of generation of elements by using the native library was faster. However, if we compare the speed between the InvSqrt and implementation using union, we can see that the implementation using UnionInvSqrt represented an improvement on speed. 

The plot below shows the relation between elements generated per seconds: 

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-311" title="fig12_fig4_elements_generated_in_time_bestintervall" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig4_elements_generated_in_time_bestintervall.gif" alt="fig12_fig4_elements_generated_in_time_bestintervall" width="772" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig4_elements_generated_in_time_bestintervall.gif 772w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig4_elements_generated_in_time_bestintervall-300x155.gif 300w" sizes="(max-width: 772px) 100vw, 772px" />
</p>

In the graphic above, it can be noted that the words generation speed for each function is almost constant, as the graph is parallel to the axis of abscissae. That is, df(x)/dx = CONSTANT. 

This speed is 5.2 Mterms/s (Megaterms per seconds) using the native (float) 1/sqrt (x); 5.0 Mterms/s using the UnionInvSqrt; and 4.65 Mterms/s using a Fast InvSqrt. 

Since the speeds are almost constant, we can calculate the percentage difference between the speed of implementations InvSqrt and UnionInvSqrt: 

<p style="text-align: center;">
  ((5000000-4650000)*100%)/(5000000+4650000) = 3,626943005%
</p>

I.e. UnionInvSqrt is about 3.63% faster than InvSqrt.

Leaving aside the standards (as InvSqrt also did not follow the standard), the implementation using union represents a small improvement in performance. However, this could be of great impact if the function is intensely used during the program. </p> 

&nbsp;

## Error between UnionInvSqrt vs InvSqrt

An interesting fact to observe about the implementations is how the error between them is behaving. 

Comparing the relative error of the implementations InvSqrt and UnionInvSqrt on standard library (float)1.f/sqrt through a graph, we observe that both are behaving in much the same way.

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-312" title="fig12_fig5_error_invsqrt" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig5_error_invsqrt.gif" alt="fig12_fig5_error_invsqrt" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig5_error_invsqrt.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig5_error_invsqrt-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-313" title="fig12_fig6_error_union" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig6_error_union.gif" alt="fig12_fig6_error_union" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig6_error_union.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig6_error_union-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

Notice that the images overlap, we have the same graph.
  
However, if you draw on the difference between the errors, you may notice a small error that occurs between the implementations:

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-314" title="fig12_fig7_diff_invsqrt_union_normal" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig7_diff_invsqrt_union_normal.gif" alt="fig12_fig7_diff_invsqrt_union_normal" width="788" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig7_diff_invsqrt_union_normal.gif 788w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig7_diff_invsqrt_union_normal-300x152.gif 300w" sizes="(max-width: 788px) 100vw, 788px" />
</p>

and this difference has a highly oscillatory behavior:

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-315" title="fig12_fig8_diff_invsqrt_union_zoomed" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig8_diff_invsqrt_union_zoomed.gif" alt="fig12_fig8_diff_invsqrt_union_zoomed" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig8_diff_invsqrt_union_zoomed.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig8_diff_invsqrt_union_zoomed-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

By closely observing to these 2 graphics, it can be noted that they do not have any correlation with time. That is, the numerical behavior is to be analyzed, which does not depend on the state of the machine. 

This difference is not evident in the graph of the relative errors because the relative error of both implementations are around of 10^-6 and the differences between the UnionInvSqrt and InvSqrt is in the range of 10^-10, much smaller than the error on any of the two implementations. 

In theory, the difference between the images of both implementations should be 0, because it is expected that both functions have the same behavior. However, the fact of using only 1 variable in the case of UnionInvSqrt, generates a slightly different behavior when using the 2 variables (in InvSqrt).</p> 

&nbsp;

## InvSqrt in JAVA

The method is so good that can be used for some other platforms or languages. I wondered how this test would be implemented in JAVA. The implementation of InvSqrt in java is as follows:

<pre lang="java">/**
* Java InvSqrt
* Author: Pedro Garcia
* sawp@sawp.com.br
* http://www.sawp.com.br
* Licensed by Creative Commons: http://creativecommons.org/licenses/by-nc-nd/2.5/en/
**/

strictfp static float InvSqrt(float x){
	float xhalf = 0.5f * x;
	int i = Float.floatToRawIntBits(x); // convert integer to keep the representation IEEE 754

	i = 0x5f3759df - (i >> 1);
	x = Float.intBitsToFloat(i);
	x = x * (1.5f - xhalf * x * x);

	return x;
}
</pre></p> 

I applied the same tests as with C, testing error and the difference in efficiency between the InvSqrt and using the native library (float) 1.f/Math.sqrt (x).
  
In the graph, we can observe that there is no advantage in a matter of efficiency to use the InvSqrt: 

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-316" title="fig12_fig9_termosporsegundoemjava_1h1" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig9_termosporsegundoemjava_1h1.gif" alt="fig12_fig9_termosporsegundoemjava_1h1" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig9_termosporsegundoemjava_1h1.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig9_termosporsegundoemjava_1h1-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-317" title="fig12_fig10_termosporsegundoemjava_1h3" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig10_termosporsegundoemjava_1h3.gif" alt="fig12_fig10_termosporsegundoemjava_1h3" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig10_termosporsegundoemjava_1h3.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig10_termosporsegundoemjava_1h3-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

Both implementations have shown the same behavior in the generation of elements per second. 

An interesting fact could be observed using both functions: the number of terms generated by time has a sinusoidal behavior. That is, the speed varies with time, unlike the implementation in C. 

Looking at the curves of the two functions, it can be seen that the approximation of InvSqrt is very close to 1.f/Math.sqrt (x): 

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-318" title="fig12_fig11_invsqrt_math_sobrepostos" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig11_invsqrt_math_sobrepostos.gif" alt="fig12_fig11_invsqrt_math_sobrepostos" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig11_invsqrt_math_sobrepostos.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig11_invsqrt_math_sobrepostos-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

The error of InvSqrt on using standard library is behaving the same way the original implementation in C: 

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-319" title="fig12_fig12_erro2" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig12_erro2.gif" alt="fig12_fig12_erro2" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig12_erro2.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig12_erro2-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

<p style="text-align: center;">
  <img class="aligncenter size-full wp-image-320" title="fig12_fig13_erro4" src="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig13_erro4.gif" alt="fig12_fig13_erro4" width="400" height="400" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig13_erro4.gif 400w, http://www.sawp.com.br/blog/wp-content/uploads/2009/05/fig12_fig13_erro4-300x300.gif 300w" sizes="(max-width: 400px) 100vw, 400px" />
</p>

&nbsp;

## InvSqrt in C#

Also found an implementation of InvSqrt in C # using the class <a href="http://msdn.microsoft.com/en-us/library/system.bitconverter.aspx" target="_blank">BitConverter</a> at stackoverflow.com:

<pre lang="C">float InvSqrt(float x)
{
    float xhalf = 0.5f * x;
    int i = BitConverter.ToInt32(BitConverter.GetBytes(x), 0);
    i = 0x5f3759df - (i >> 1);
    x = BitConverter.ToSingle(BitConverter.GetBytes(i), 0);
    x = x * (1.5f - xhalf * x * x);
    return x;
}
</pre>

I don&#8217;t tested the efficiency of the function or characteristics using .NET . To learn more see the link: <a target="_blank" href="http://stackoverflow.com/questions/268853/is-it-possible-to-write-quakes-fast-invsqrt-function-in-c">http://stackoverflow.com/questions/268853/is-it-possible-to-write-quakes-fast-invsqrt-function-in-c</a> 

That&#8217;s it! Unfortunately I do not have an old computer to test the implementation using union or InvSqrt in Java. However, if you want to see the results of my tests, the sources or test on other architectures and older machines, you can download the files at: 

<p style="text-align: center;">
  <a href="http://www.sawp.com.br/sources/InvSqrtC/" target="_blank">http://www.sawp.com.br/sources/InvSqrtC/</a>
</p>

<p style="text-align: center;">
  <a href="http://www.sawp.com.br/sources/BitsInJava/" target="_blank"> http://www.sawp.com.br/sources/BitsInJava/</a>
</p>

To learn more about Invsqrt, the Wikipedia has an excellent set of information about it: <a href="http://en.wikipedia.org/wiki/Fast_inverse_square_root" target="_blank">http://en.wikipedia.org/wiki/Fast_inverse_square_root</a> </p> 

&nbsp;

## InvSqrt in Fortran 90

<pre lang="fortran">real function InvSqrt(x)
	implicit none

	type casting
		real :: x		
	end type casting

	real, intent(in) :: x

	! castinger
	type(casting), target :: pointerTo

	! Encode data as an array of integers
	integer, dimension(:), allocatable :: enc
	integer :: length
	real :: xhalf

	xhalf = 0.5 * x

	! transfer to heap ("promiscuous" operation)
	pointerTo%x = x

	! encode a memory section from a type to other
	length = size(transfer(pointerTo, enc))
	allocate(enc(length))		
	! encoded to integer, now, operate
	enc = transfer(pointerTo, enc)

	enc(1) = 1597463007 - rshift(enc(1),1)

	! decode
	pointerTo = transfer(enc, pointerTo)
	
	! dealloc
	deallocate(enc)

	InvSqrt = pointerTo%x*(1.5 - xhalf*pointerTo%x*pointerTo%x)
end function InvSqrt</pre>

&nbsp;

## References

[1] www.gamedev.net/community/forums/topic.asp?topic id=139956

[2] Chris Lomont, www.math.purdue.edu/~clomont, “FAST INVERT SQUARE ROOT&#8221;, http://www.lomont.org/Math/Papers/2003/InvSqrt.pdf.

[3] http://betterexplained.com/articles/understanding-quakes-fast-inverse-square-root/
