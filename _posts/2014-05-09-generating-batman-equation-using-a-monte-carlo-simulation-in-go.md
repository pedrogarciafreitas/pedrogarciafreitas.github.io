---
id: 2076
title: Generating the Batman Equation using a Monte Carlo Simulation
date: 2014-05-09T00:38:03+00:00
author: SAWP
excerpt: The batman curve is a piecewise curve in the shape of the logo of the Batman superhero originally posted on reddit.com on Jul. 28, 2011. In this post, I present a little code, written in Go, to generate this funny plot.
layout: post
guid: http://www.sawp.com.br/blog/?p=2076
permalink: p=2076
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:18180:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="go" style="font-family:monospace;"><span style="color: #b1b100; font-weight: bold;">package</span> main
    &nbsp;
    <span style="color: #b1b100; font-weight: bold;">import</span> <span style="color: #339933;">(</span>
    <span style="color: #cc66cc;">&quot;code.google.com/p/plotinum/plot&quot;</span>
    <span style="color: #cc66cc;">&quot;code.google.com/p/plotinum/plotter&quot;</span>
    <span style="color: #cc66cc;">&quot;math&quot;</span>
    <span style="color: #cc66cc;">&quot;math/rand&quot;</span>
    <span style="color: #cc66cc;">&quot;time&quot;</span>
    <span style="color: #339933;">)</span>
    &nbsp;
    <span style="color: #993333;">func</span> main<span style="color: #339933;">()</span> <span style="color: #339933;">{</span>
    rand<span style="color: #339933;">.</span>Seed<span style="color: #339933;">(</span>time<span style="color: #339933;">.</span>Now<span style="color: #339933;">()</span><span style="color: #339933;">.</span>Unix<span style="color: #339933;">())</span>
    p<span style="color: #339933;">,</span> err <span style="color: #339933;">:=</span> plot<span style="color: #339933;">.</span>New<span style="color: #339933;">()</span>
    s<span style="color: #339933;">,</span> err <span style="color: #339933;">:=</span> plotter<span style="color: #339933;">.</span>NewScatter<span style="color: #339933;">(</span>batman<span style="color: #339933;">(</span><span style="color: #cc66cc;">90000</span><span style="color: #339933;">))</span>
    s<span style="color: #339933;">.</span>Shape <span style="color: #339933;">=</span> plot<span style="color: #339933;">.</span>CircleGlyph<span style="color: #339933;">{}</span>
    p<span style="color: #339933;">.</span>Add<span style="color: #339933;">(</span>s<span style="color: #339933;">)</span>
    err <span style="color: #339933;">=</span> p<span style="color: #339933;">.</span>Save<span style="color: #339933;">(</span><span style="color: #cc66cc;">8</span><span style="color: #339933;">,</span> <span style="color: #cc66cc;">4</span><span style="color: #339933;">,</span> <span style="color: #cc66cc;">&quot;points.png&quot;</span><span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">if</span> err <span style="color: #339933;">!=</span> <span style="color: #000000; font-weight: bold;">nil</span> <span style="color: #339933;">{</span>
    <span style="color: #000066;">panic</span><span style="color: #339933;">(</span>err<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span>
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> batman<span style="color: #339933;">(</span>n <span style="color: #993333;">int</span><span style="color: #339933;">)</span> plotter<span style="color: #339933;">.</span>XYs <span style="color: #339933;">{</span>
    pts <span style="color: #339933;">:=</span> <span style="color: #000066;">make</span><span style="color: #339933;">(</span>plotter<span style="color: #339933;">.</span>XYs<span style="color: #339933;">,</span> n<span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">for</span> <span style="">i</span> <span style="color: #339933;">:=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> <span style="">i</span> &lt; n<span style="color: #339933;">;</span> <span style="">i</span><span style="color: #339933;">++</span> <span style="color: #339933;">{</span>
    pts<span style="color: #339933;">[</span><span style="">i</span><span style="color: #339933;">]</span><span style="color: #339933;">.</span>X <span style="color: #339933;">=</span> rand<span style="color: #339933;">.</span>Float64<span style="color: #339933;">()</span><span style="color: #339933;">*</span><span style="color: #cc66cc;">14</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">7</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span>
    <span style="color: #b1b100; font-weight: bold;">if</span> <span style="">i</span> &lt; n<span style="color: #339933;">/</span><span style="color: #cc66cc;">2</span> <span style="color: #339933;">{</span>
    pts<span style="color: #339933;">[</span><span style="">i</span><span style="color: #339933;">]</span><span style="color: #339933;">.</span>Y <span style="color: #339933;">=</span> up<span style="color: #339933;">(</span>pts<span style="color: #339933;">[</span><span style="">i</span><span style="color: #339933;">]</span><span style="color: #339933;">.</span>X<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span> <span style="color: #b1b100; font-weight: bold;">else</span> <span style="color: #339933;">{</span>
    pts<span style="color: #339933;">[</span><span style="">i</span><span style="color: #339933;">]</span><span style="color: #339933;">.</span>Y <span style="color: #339933;">=</span> down<span style="color: #339933;">(</span>pts<span style="color: #339933;">[</span><span style="">i</span><span style="color: #339933;">]</span><span style="color: #339933;">.</span>X<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span>
    <span style="color: #339933;">}</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> pts
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> down<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">if</span> math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> &gt; <span style="color: #cc66cc;">4</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> <span style="color: #339933;">-</span>wings<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span> <span style="color: #b1b100; font-weight: bold;">else</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> tail<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span>
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> up<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">switch</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">case</span> math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> &gt; <span style="color: #cc66cc;">3</span><span style="color: #339933;">:</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> wings<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">case</span> math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> &gt; <span style="color: #cc66cc;">1</span><span style="color: #339933;">:</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> arms<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">case</span> math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> &gt; <span style="color: #cc66cc;">0</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">75</span> &amp;&amp; math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> &lt; <span style="color: #cc66cc;">1</span><span style="color: #339933;">:</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> neck<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">case</span> math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> &gt; <span style="color: #cc66cc;">0</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">5</span> &amp;&amp; math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> &lt; <span style="color: #cc66cc;">0</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">75</span><span style="color: #339933;">:</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> ears<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">default</span><span style="color: #339933;">:</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> head<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span>
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> head<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">25</span>
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> ears<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> <span style="color: #cc66cc;">3</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">*</span>math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> <span style="color: #339933;">+</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">75</span>
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> neck<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> <span style="color: #cc66cc;">9</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">8</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">*</span>math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> arms<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    m <span style="color: #339933;">:=</span> <span style="color: #cc66cc;">4</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span> <span style="color: #339933;">-</span> math<span style="color: #339933;">.</span>Pow<span style="color: #339933;">(</span>math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span><span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">,</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">71</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">5</span><span style="color: #339933;">*</span>math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span> <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">5</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">35</span><span style="color: #339933;">*</span>math<span style="color: #339933;">.</span>Sqrt<span style="color: #339933;">(</span>m<span style="color: #339933;">)</span>
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> tail<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    y1 <span style="color: #339933;">:=</span> math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x <span style="color: #339933;">/</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">)</span>
    y2 <span style="color: #339933;">:=</span> x<span style="color: #339933;">*</span>x<span style="color: #339933;">*</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">.</span>09 <span style="color: #339933;">+</span> <span style="color: #cc66cc;">3</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span>
    y3 <span style="color: #339933;">:=</span> math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>math<span style="color: #339933;">.</span>Abs<span style="color: #339933;">(</span>x<span style="color: #339933;">)</span><span style="color: #339933;">-</span><span style="color: #cc66cc;">2</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">)</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span>
    y4 <span style="color: #339933;">:=</span> math<span style="color: #339933;">.</span>Sqrt<span style="color: #339933;">(</span><span style="color: #cc66cc;">1</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span> <span style="color: #339933;">-</span> y3<span style="color: #339933;">*</span>y3<span style="color: #339933;">)</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> y1 <span style="color: #339933;">-</span> y2 <span style="color: #339933;">+</span> y4
    <span style="color: #339933;">}</span>
    &nbsp;
    <span style="color: #993333;">func</span> wings<span style="color: #339933;">(</span>x <span style="color: #993333;">float64</span><span style="color: #339933;">)</span> <span style="color: #993333;">float64</span> <span style="color: #339933;">{</span>
    <span style="color: #b1b100; font-weight: bold;">return</span> <span style="color: #cc66cc;">3</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span> <span style="color: #339933;">*</span> math<span style="color: #339933;">.</span>Sin<span style="color: #339933;">(</span>math<span style="color: #339933;">.</span>Acos<span style="color: #339933;">(</span>x<span style="color: #339933;">/</span><span style="color: #cc66cc;">7</span><span style="color: #339933;">.</span><span style="color: #cc66cc;">0</span><span style="color: #339933;">))</span>
    <span style="color: #339933;">}</span></pre></td></tr></table><p class="theCode" style="display:none;">package main
    
    import (
    &quot;code.google.com/p/plotinum/plot&quot;
    &quot;code.google.com/p/plotinum/plotter&quot;
    &quot;math&quot;
    &quot;math/rand&quot;
    &quot;time&quot;
    )
    
    func main() {
    rand.Seed(time.Now().Unix())
    p, err := plot.New()
    s, err := plotter.NewScatter(batman(90000))
    s.Shape = plot.CircleGlyph{}
    p.Add(s)
    err = p.Save(8, 4, &quot;points.png&quot;)
    if err != nil {
    panic(err)
    }
    }
    
    func batman(n int) plotter.XYs {
    pts := make(plotter.XYs, n)
    for i := 0; i &lt; n; i++ {
    pts[i].X = rand.Float64()*14.0 - 7.0
    if i &lt; n/2 {
    pts[i].Y = up(pts[i].X)
    } else {
    pts[i].Y = down(pts[i].X)
    }
    }
    return pts
    }
    
    func down(x float64) float64 {
    if math.Abs(x) &gt; 4 {
    return -wings(x)
    } else {
    return tail(x)
    }
    }
    
    func up(x float64) float64 {
    switch {
    case math.Abs(x) &gt; 3:
    return wings(x)
    case math.Abs(x) &gt; 1:
    return arms(x)
    case math.Abs(x) &gt; 0.75 &amp;&amp; math.Abs(x) &lt; 1:
    return neck(x)
    case math.Abs(x) &gt; 0.5 &amp;&amp; math.Abs(x) &lt; 0.75:
    return ears(x)
    default:
    return head(x)
    }
    }
    
    func head(x float64) float64 {
    return 2.25
    }
    
    func ears(x float64) float64 {
    return 3.0*math.Abs(x) + 0.75
    }
    
    func neck(x float64) float64 {
    return 9.0 - 8.0*math.Abs(x)
    }
    
    func arms(x float64) float64 {
    m := 4.0 - math.Pow(math.Abs(x)-1.0, 2)
    return 2.71 - 0.5*math.Abs(x) + 1.5 - 1.35*math.Sqrt(m)
    }
    
    func tail(x float64) float64 {
    y1 := math.Abs(x / 2.0)
    y2 := x*x*0.09 + 3.0
    y3 := math.Abs(math.Abs(x)-2.0) - 1.0
    y4 := math.Sqrt(1.0 - y3*y3)
    return y1 - y2 + y4
    }
    
    func wings(x float64) float64 {
    return 3.0 * math.Sin(math.Acos(x/7.0))
    }</p></div>
    ";}
categories:
  - Programming Internals
---
The BatMan equation has been making the rounds on the internet recently. The Go code below uses the Plotium library to plot the results.

<pre lang="go">package main

import (
	"code.google.com/p/plotinum/plot"
	"code.google.com/p/plotinum/plotter"
	"math"
	"math/rand"
	"time"
)

func main() {
	rand.Seed(time.Now().Unix())
	p, err := plot.New()
	s, err := plotter.NewScatter(batman(90000))
	s.Shape = plot.CircleGlyph{}
	p.Add(s)
	err = p.Save(8, 4, "points.png")
	if err != nil {
		panic(err)
	}
}

func batman(n int) plotter.XYs {
	pts := make(plotter.XYs, n)
	for i := 0; i &lt; n; i++ {
		pts[i].X = rand.Float64()*14.0 - 7.0
		if i &lt; n/2 {
			pts[i].Y = up(pts[i].X)
		} else {
			pts[i].Y = down(pts[i].X)
		}
	}
	return pts
}

func down(x float64) float64 {
	if math.Abs(x) > 4 {
		return -wings(x)
	} else {
		return tail(x)
	}
}

func up(x float64) float64 {
	switch {
	case math.Abs(x) > 3:
		return wings(x)
	case math.Abs(x) > 1:
		return arms(x)
	case math.Abs(x) > 0.75 && math.Abs(x) &lt; 1:
		return neck(x)
	case math.Abs(x) > 0.5 && math.Abs(x) &lt; 0.75:
		return ears(x)
	default:
		return head(x)
	}
}

func head(x float64) float64 {
	return 2.25
}

func ears(x float64) float64 {
	return 3.0*math.Abs(x) + 0.75
}

func neck(x float64) float64 {
	return 9.0 - 8.0*math.Abs(x)
}

func arms(x float64) float64 {
	m := 4.0 - math.Pow(math.Abs(x)-1.0, 2)
	return 2.71 - 0.5*math.Abs(x) + 1.5 - 1.35*math.Sqrt(m)
}

func tail(x float64) float64 {
	y1 := math.Abs(x / 2.0)
	y2 := x*x*0.09 + 3.0
	y3 := math.Abs(math.Abs(x)-2.0) - 1.0
	y4 := math.Sqrt(1.0 - y3*y3)
	return y1 - y2 + y4
}

func wings(x float64) float64 {
	return 3.0 * math.Sin(math.Acos(x/7.0))
}
</pre>

The result:

<img src="http://www.sawp.com.br/blog/wp-content/uploads/2014/05/points.png" alt="Batman Equation" height="384" width="768" />
