---
id: 821
title: FreeBSD G95 linker error
date: 2010-11-01T16:38:25+00:00
author: SAWP
layout: post
guid: http://www.sawp.com.br/blog/?p=821
permalink: /p=821
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:23097:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #00ff00; font-style: italic;">/**
    * huffman.scala - Computes huffman compression algorithm.
    *
    *
    * Autor: Pedro Garcia Freitas [sawp@sawp.com.br]
    * License: Creative Commons
    *      &lt;http: //creativecommons.org/licenses/by-nc-nd/2.5/en/&gt;
    *
    * Apr 2011
    */</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">type</span> Node <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span>Double, Any<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> huffman<span style="color: #F78811;">&#40;</span>list<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>Double, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>String, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> appendCode<span style="color: #F78811;">&#40;</span>m<span style="color: #000080;">:</span> String, x<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span>  <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>i,j<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span> - x<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> <span style="color: #F78811;">&#40;</span>i, m + j<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> sortByFrequency<span style="color: #F78811;">&#40;</span>x<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> sorter<span style="color: #F78811;">&#40;</span>e1<span style="color: #000080;">:</span> Node, e2<span style="color: #000080;">:</span> Node<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>e1.<span style="color: #000080;">_</span>1 <span style="color: #000080;">&lt;</span> e2.<span style="color: #000080;">_</span>1<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">true</span> <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    x.<span style="color: #000000;">sortWith</span><span style="color: #F78811;">&#40;</span>sorter<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> group<span style="color: #F78811;">&#40;</span>l<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> ll <span style="color: #000080;">=</span> sortByFrequency<span style="color: #F78811;">&#40;</span>l<span style="color: #F78811;">&#41;</span>
    ll <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> Tuple2<span style="color: #F78811;">&#40;</span>f1<span style="color: #000080;">:</span> Double, f2<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span>
    Tuple2<span style="color: #F78811;">&#40;</span>g1<span style="color: #000080;">:</span> Double, g2<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span>
    group<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>f1 + g1, appendCode<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;0&quot;</span>, f2<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">:::</span> appendCode<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;1&quot;</span>, g2<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> t<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> ll
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> combining<span style="color: #F78811;">&#40;</span>e<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Node<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> e <span style="color: #0000ff; font-weight: bold;">match</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> c <span style="color: #000080;">::</span> t <span style="color: #000080;">=&gt;</span> c.<span style="color: #000080;">_</span>2
    <span style="color: #0000ff; font-weight: bold;">case</span> <span style="color: #000080;">_</span> <span style="color: #000080;">=&gt;</span> error<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Not defined&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> k <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>i,j<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span> - list<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> <span style="color: #F78811;">&#40;</span>i, List<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>j, <span style="color: #6666FF;">&quot;&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> combined <span style="color: #000080;">=</span> group<span style="color: #F78811;">&#40;</span>k<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> result <span style="color: #000080;">=</span> combining<span style="color: #F78811;">&#40;</span>combined<span style="color: #F78811;">&#41;</span>
    result.<span style="color: #000000;">asInstanceOf</span><span style="color: #F78811;">&#91;</span>List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>String, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#93;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> calculateAverageLength<span style="color: #F78811;">&#40;</span>probs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>Double, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span>,
    codes<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>String, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> Double <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> getProbabilities<span style="color: #F78811;">&#40;</span>probs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>Double, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>prob, letter<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span>- probs<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> prob
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> getCodeLength<span style="color: #F78811;">&#40;</span>cods<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>String, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>letter, code<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span>- cods<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> code.<span style="color: #000000;">length</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> calculateAverage<span style="color: #F78811;">&#40;</span>codeLengths<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Int<span style="color: #F78811;">&#93;</span>, probs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Double<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> zipedCodesLengths <span style="color: #000080;">=</span> codeLengths.<span style="color: #000000;">zip</span><span style="color: #F78811;">&#40;</span>probs<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> len <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">for</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>codelen, prob<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span>- zipedCodesLengths<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> codelen <span style="color: #000080;">*</span> prob
    <span style="color: #0000ff; font-weight: bold;">val</span> average <span style="color: #000080;">=</span> len.<span style="color: #000000;">sum</span>
    average
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> probabilities <span style="color: #000080;">=</span> getProbabilities<span style="color: #F78811;">&#40;</span>probs<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> codeLengths <span style="color: #000080;">=</span> getCodeLength<span style="color: #F78811;">&#40;</span>codes<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> average <span style="color: #000080;">=</span> calculateAverage<span style="color: #F78811;">&#40;</span>codeLengths, probabilities<span style="color: #F78811;">&#41;</span>
    average
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> calculateEntropy<span style="color: #F78811;">&#40;</span>probs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>Double, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> getProbabilities<span style="color: #F78811;">&#40;</span>probs<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span><span style="color: #F78811;">&#40;</span>Double, String<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#40;</span>prob, letter<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span>- probs<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> prob
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> getLocalEntropy<span style="color: #F78811;">&#40;</span>probabilities<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Double<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>prob <span style="color: #000080;">&lt;</span>- probabilities<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">yield</span> prob <span style="color: #000080;">*</span> <span style="color: #F78811;">&#40;</span>math.<span style="color: #000000;">log</span><span style="color: #F78811;">&#40;</span>prob<span style="color: #F78811;">&#41;</span> / math.<span style="color: #000000;">log</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2.0</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> getEntropy<span style="color: #F78811;">&#40;</span>localEntropy<span style="color: #000080;">:</span> List<span style="color: #F78811;">&#91;</span>Double<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    -localEntropy.<span style="color: #000000;">sum</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> probabilities <span style="color: #000080;">=</span> getProbabilities<span style="color: #F78811;">&#40;</span>probs<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> localEntropy <span style="color: #000080;">=</span> getLocalEntropy<span style="color: #F78811;">&#40;</span>probabilities<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> entropy <span style="color: #000080;">=</span> getEntropy<span style="color: #F78811;">&#40;</span>localEntropy<span style="color: #F78811;">&#41;</span>
    entropy
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #00ff00; font-style: italic;">/* Tests */</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> probs <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.4</span>, <span style="color: #6666FF;">&quot;A&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.2</span>, <span style="color: #6666FF;">&quot;B&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.1</span>, <span style="color: #6666FF;">&quot;C&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.05</span>, <span style="color: #6666FF;">&quot;D&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span>
    <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.1</span>, <span style="color: #6666FF;">&quot;E&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.075</span>, <span style="color: #6666FF;">&quot;F&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> <span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0.075</span>, <span style="color: #6666FF;">&quot;G&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">::</span> Nil
    <span style="color: #0000ff; font-weight: bold;">val</span> codes <span style="color: #000080;">=</span> huffman<span style="color: #F78811;">&#40;</span>probs<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> averagelen <span style="color: #000080;">=</span> calculateAverageLength<span style="color: #F78811;">&#40;</span>probs, codes<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> entropy <span style="color: #000080;">=</span> calculateEntropy<span style="color: #F78811;">&#40;</span>probs<span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Frequency and Symbols: &quot;</span> + probs<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Huffman code: &quot;</span> + codes<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Average length: &quot;</span> + averagelen<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Entropy: &quot;</span> + entropy<span style="color: #F78811;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * huffman.scala - Computes huffman compression algorithm.
    *
    *
    * Autor: Pedro Garcia Freitas [sawp@sawp.com.br]
    * License: Creative Commons
    *      &lt;http: //creativecommons.org/licenses/by-nc-nd/2.5/en/&gt;
    *
    * Apr 2011
    */
    
    type Node = (Double, Any)
    
    def huffman(list: List[(Double, String)]): List[(String, String)] = {
    def appendCode(m: String, x: List[Node]): List[Node]  =
    for ((i,j) &lt; - x) yield (i, m + j)
    
    def sortByFrequency(x: List[Node]) = {
    def sorter(e1: Node, e2: Node) =
    if (e1._1 &lt; e2._1) true else false
    x.sortWith(sorter)
    }
    
    def group(l: List[Node]): List[Node] = {
    val ll = sortByFrequency(l)
    ll match {
    case Tuple2(f1: Double, f2: List[Node]) ::
    Tuple2(g1: Double, g2: List[Node]) :: t =&gt;
    group((f1 + g1, appendCode(&quot;0&quot;, f2) ::: appendCode(&quot;1&quot;, g2)) :: t)
    case _ =&gt; ll
    }
    }
    
    def combining(e: List[Node]) = e match {
    case c :: t =&gt; c._2
    case _ =&gt; error(&quot;Not defined&quot;)
    }
    
    val k = for ((i,j) &lt; - list) yield (i, List((j, &quot;&quot;)))
    val combined = group(k)
    val result = combining(combined)
    result.asInstanceOf[List[(String, String)]]
    }
    
    def calculateAverageLength(probs: List[(Double, String)],
    codes: List[(String, String)]): Double = {
    def getProbabilities(probs: List[(Double, String)]) =
    for ((prob, letter) &lt;- probs) yield prob
    
    def getCodeLength(cods: List[(String, String)]) =
    for ((letter, code) &lt;- cods) yield code.length
    
    def calculateAverage(codeLengths: List[Int], probs: List[Double]) = {
    val zipedCodesLengths = codeLengths.zip(probs)
    val len = for((codelen, prob) &lt;- zipedCodesLengths) yield codelen * prob
    val average = len.sum
    average
    }
    
    val probabilities = getProbabilities(probs)
    val codeLengths = getCodeLength(codes)
    val average = calculateAverage(codeLengths, probabilities)
    average
    }
    
    def calculateEntropy(probs: List[(Double, String)]) = {
    def getProbabilities(probs: List[(Double, String)]) =
    for ((prob, letter) &lt;- probs) yield prob
    
    def getLocalEntropy(probabilities: List[Double]) =
    for (prob &lt;- probabilities) yield prob * (math.log(prob) / math.log(2.0))
    
    def getEntropy(localEntropy: List[Double]) =
    -localEntropy.sum
    
    val probabilities = getProbabilities(probs)
    val localEntropy = getLocalEntropy(probabilities)
    val entropy = getEntropy(localEntropy)
    entropy
    }
    
    
    /* Tests */
    val probs = (0.4, &quot;A&quot;) :: (0.2, &quot;B&quot;) :: (0.1, &quot;C&quot;) :: (0.05, &quot;D&quot;) ::
    (0.1, &quot;E&quot;) :: (0.075, &quot;F&quot;) :: (0.075, &quot;G&quot;) :: Nil
    val codes = huffman(probs)
    val averagelen = calculateAverageLength(probs, codes)
    val entropy = calculateEntropy(probs)
    
    println(&quot;\n&quot;)
    println(&quot;Frequency and Symbols: &quot; + probs)
    println(&quot;Huffman code: &quot; + codes)
    println(&quot;Average length: &quot; + averagelen)
    println(&quot;Entropy: &quot; + entropy)</p></div>
    ";}
categories:
  - FreeBSD
---
If **G95** gives this error:
  


<center>
  <code>ld: cannot find -lf95</code>
</center>


  
tries:
  


<center>
  <code>echo "export LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/bin" >> ~/.bashrc</code>
</center>


  
if you use BASH or
  


<center>
  <code>echo "setenv LIBRARY_PATH /usr/local/lib" >> ~/.cshrc</code>
</center>


  
if you use CSH.

Restart terminal and try again! ;)
