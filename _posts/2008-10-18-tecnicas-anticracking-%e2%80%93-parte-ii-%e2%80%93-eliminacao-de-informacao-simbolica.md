---
id: 148
title: Técnicas AntiCracking – Parte II – Eliminação de Informação Simbólica
date: 2008-10-18T15:08:06+00:00
author: SAWP
excerpt: Os compiladores costumam gerar informações simbólicas – para representar as lincagens – quando convertem as relações de importação e exportação de tabelas e extensões. Um programa com grande uso de DLLs, onde cada uma exporta uma grande quantidade de funções, necessitará de uma lista relacionando onde estão as funções exportadas, normalmente indicando o que elas fazem, o que é de grande serventia para os crackers. Neste artigo, apresento algumas das informações que podem ser usadas como pontos de referência para engenharia reversa.
layout: post
guid: http://www.sawp.com.br/blog/?p=148
permalink: /p=148
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:6371:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #339900;">#include &lt; stdio .h &gt;</span>
    &nbsp;
    <span style="color: #339900;">#define NMAX 1000</span>
    <span style="color: #339900;">#define APR0 &quot;O CRIVO DE ERASTOTENES\n&quot;</span>
    <span style="color: #339900;">#define APR1 &quot;Codigo com informacao simbolica explicita\n&quot;</span>
    <span style="color: #339900;">#define APR2 &quot;www.sawp.com.br \n\n&quot;</span>
    &nbsp;
    <span style="color: #0000ff;">int</span> pilhaCrivo<span style="color: #008000;">&#91;</span>NMAX<span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span>
    &nbsp;
    &nbsp;
    <span style="color: #0000ff;">void</span> apresentacao<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span>APR0<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span>APR1<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span>APR2<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> fazListaDeNumeros<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">int</span> i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">for</span> <span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">2</span><span style="color: #008080;">;</span> i<span style="color: #000080;">&lt;</span> <span style="color: #000080;">=</span>NMAX<span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    pilhaCrivo<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #000080;">=</span>i<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> mostra<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">int</span> i,j<span style="color: #008080;">;</span>
    <span style="color: #0000ff;">for</span> <span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">2</span><span style="color: #008080;">;</span> i<span style="color: #000080;">&lt;=</span>NMAX<span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">if</span> <span style="color: #008000;">&#40;</span>pilhaCrivo<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #000080;">==</span>i<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;%d <span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>, i<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">for</span> <span style="color: #008000;">&#40;</span>j<span style="color: #000080;">=</span>i<span style="color: #000040;">+</span>i<span style="color: #008080;">;</span> j<span style="color: #000080;">&lt;=</span>NMAX<span style="color: #008080;">;</span> j<span style="color: #000040;">+</span><span style="color: #000080;">=</span>i<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    pilhaCrivo<span style="color: #008000;">&#91;</span>j<span style="color: #008000;">&#93;</span><span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">int</span> main<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    apresentacao<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    fazListaDeNumeros<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    mostra<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">return</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">#include &lt; stdio .h &gt;
    
    #define NMAX 1000
    #define APR0 &quot;O CRIVO DE ERASTOTENES\n&quot;
    #define APR1 &quot;Codigo com informacao simbolica explicita\n&quot;
    #define APR2 &quot;www.sawp.com.br \n\n&quot;
    
    int pilhaCrivo[NMAX];
    
    
    void apresentacao(){
    printf(APR0);
    printf(APR1);
    printf(APR2);
    }
    
    void fazListaDeNumeros(){
    int i=0;
    for (i=2; i&lt; =NMAX; i++) {
    pilhaCrivo[i]=i;
    }
    }
    
    void mostra(void){
    int i,j;
    for (i=2; i&lt;=NMAX; i++) {
    if (pilhaCrivo[i]==i) {
    printf(&quot;%d \n&quot;, i);
    for (j=i+i; j&lt;=NMAX; j+=i) {
    pilhaCrivo[j]=0;
    }
    }
    }
    }
    
    int main() {
    apresentacao();
    fazListaDeNumeros();
    mostra();
    
    return 1;
    }</p></div>
    ;i:2;s:11708:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #339900;">#include &lt; 8203099666.h &gt;</span>
    <span style="color: #339900;">#include &lt; 1010011010.h &gt;</span>
    <span style="color: #339900;">#include &lt; 75981212.h &gt;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #007788;">string</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cout</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #339900;">#define N32MMX2 1000</span>
    <span style="color: #339900;">#define APR1 &quot;Htinlt%htr%nsktwrfhft%xnrgtqnhf%j}uqnhnyf3&quot; </span>
    <span style="color: #339900;">#define APR2 &quot;|||3xf|u3htr3gw&quot; </span>
    <span style="color: #339900;">#define APR0 </span>
    T<span style="color: #000040;">%</span>HWN<span style="color: #008000;">&#91;</span>T<span style="color: #000040;">%</span>IJ<span style="color: #000040;">%</span>JWFXYTYJSJX
    &nbsp;
    &nbsp;
    <span style="color: #0000ff;">int</span> PH040x12<span style="color: #008000;">&#91;</span>N32MMX2<span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span>
    &nbsp;
    &nbsp;
    <span style="color: #0000ff;">void</span> rot13_d3c0d3<span style="color: #008000;">&#40;</span>string <span style="color: #000040;">&amp;</span> INx990012<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> kkk<span style="color: #000080;">=</span><span style="color: #0000dd;">5</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">int</span> a5c11c0d3<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>i<span style="color: #000080;">&lt;</span> inx990012 .<span style="color: #007788;">length</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    a5c11c0d3 <span style="color: #000080;">=</span> <span style="color: #0000ff;">static_cast</span><span style="color: #000080;">&lt;</span> <span style="color: #0000ff;">int</span> <span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span>INx990012<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span><span style="color: #000040;">-</span> kkk<span style="color: #008080;">;</span>
    INx990012<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span> <span style="color: #000080;">=</span>  <span style="color: #0000ff;">static_cast</span><span style="color: #000080;">&lt;</span> <span style="color: #0000ff;">char</span> <span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span>a5c11c0d3<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> st4rt3R_09833<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    string h0xx3232122<span style="color: #008000;">&#91;</span><span style="color: #008000;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#123;</span>APR0, APR1, APR2<span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    &nbsp;
    rot13_d3c0d3<span style="color: #008000;">&#40;</span>h0xx3232122<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">0</span><span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    rot13_d3c0d3<span style="color: #008000;">&#40;</span>h0xx3232122<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">1</span><span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    rot13_d3c0d3<span style="color: #008000;">&#40;</span>h0xx3232122<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">2</span><span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000dd;">cout</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> h0xx3232122<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">0</span><span style="color: #008000;">&#93;</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> <span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> h0xx3232122<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">1</span><span style="color: #008000;">&#93;</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> <span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> h0xx3232122<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">2</span><span style="color: #008000;">&#93;</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> <span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    &nbsp;
    <span style="color: #0000ff;">void</span> HP00x98765432<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">int</span> i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">for</span> <span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">2</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;=</span> N32MMX2<span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    PH040x12<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #000080;">=</span>i<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> IB00x98701234<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">int</span> i,j<span style="color: #008080;">;</span>
    <span style="color: #0000ff;">for</span> <span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">2</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;=</span> N32MMX2<span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">if</span> <span style="color: #008000;">&#40;</span>PH040x12<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #000080;">==</span>i<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;%d <span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>, i<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">for</span> <span style="color: #008000;">&#40;</span>j<span style="color: #000080;">=</span>i<span style="color: #000040;">+</span>i<span style="color: #008080;">;</span> j <span style="color: #000080;">&lt;=</span> N32MMX2<span style="color: #008080;">;</span> j<span style="color: #000040;">+</span><span style="color: #000080;">=</span>i<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    PH040x12<span style="color: #008000;">&#91;</span>j<span style="color: #008000;">&#93;</span><span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">int</span> main<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    st4rt3R_09833<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    HP00x98765432<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    IB00x98701234<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">return</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">#include &lt; 8203099666.h &gt;
    #include &lt; 1010011010.h &gt;
    #include &lt; 75981212.h &gt;
    using std::string;
    using std::cout;
    
    #define N32MMX2 1000
    #define APR1 &quot;Htinlt%htr%nsktwrfhft%xnrgtqnhf%j}uqnhnyf3&quot;
    #define APR2 &quot;|||3xf|u3htr3gw&quot;
    #define APR0
    T%HWN[T%IJ%JWFXYTYJSJX
    
    
    int PH040x12[N32MMX2];
    
    
    void rot13_d3c0d3(string &amp; INx990012){
    const int kkk=5;
    int a5c11c0d3;
    
    for(int i=0;i&lt; inx990012 .length();i++) {
    a5c11c0d3 = static_cast&lt; int &gt;(INx990012[i])- kkk;
    INx990012[i] =  static_cast&lt; char &gt;(a5c11c0d3);
    }
    }
    
    void st4rt3R_09833(){
    string h0xx3232122[] = {APR0, APR1, APR2};
    
    rot13_d3c0d3(h0xx3232122[0]);
    rot13_d3c0d3(h0xx3232122[1]);
    rot13_d3c0d3(h0xx3232122[2]);
    
    cout &lt; &lt; h0xx3232122[0] &lt; &lt; &quot;\n&quot; &lt; &lt; h0xx3232122[1] &lt; &lt; &quot;\n&quot; &lt; &lt; h0xx3232122[2] &lt; &lt; &quot;\n\n&quot;;
    }
    
    
    void HP00x98765432(){
    int i=0;
    for (i=2; i &lt;= N32MMX2; i++) {
    PH040x12[i]=i;
    }
    }
    
    void IB00x98701234(void){
    int i,j;
    for (i=2; i &lt;= N32MMX2; i++) {
    if (PH040x12[i]==i) {
    printf(&quot;%d \n&quot;, i);
    for (j=i+i; j &lt;= N32MMX2; j+=i) {
    PH040x12[j]=0;
    }
    }
    }
    }
    
    int main() {
    st4rt3R_09833();
    HP00x98765432();
    IB00x98701234();
    
    return 1;
    }</p></div>
    ;i:3;s:24165:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="asm" style="font-family:monospace;">	<span style="color: #339933;">.</span>file	<span style="color: #7f007f;">&quot;main.c&quot;</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span> <span style="color: #0000ff; font-weight: bold;">.rdata</span><span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;dr&quot;</span>
    LC0<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;O CRIVO DE ERASTOTENES\12\0&quot;</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">4</span>
    LC1<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;Codigo com informacao simbolica explicita\12\0&quot;</span>
    LC2<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;www.sawp.com.br \12\12\0&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span>globl _apresentacao
    <span style="color: #339933;">.</span>def	_apresentacao<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    _apresentacao<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC0<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	_printf
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC1<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	_printf
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC2<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	_printf
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span>globl _fazListaDeNumeros
    <span style="color: #339933;">.</span>def	_fazListaDeNumeros<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    _fazListaDeNumeros<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L3<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1000</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jg</span>	L2
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> _pilhaCrivo<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    incl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L3
    L2<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span> <span style="color: #0000ff; font-weight: bold;">.rdata</span><span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;dr&quot;</span>
    LC3<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;%d \12\0&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span>globl _mostra
    <span style="color: #339933;">.</span>def	_mostra<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    _mostra<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">24</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L7<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1000</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jg</span>	L6
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	_pilhaCrivo<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">jne</span>	L9
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC3<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	_printf
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L11<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1000</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jg</span>	L9
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> _pilhaCrivo<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L11
    L9<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    incl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L7
    L6<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span>def	___main<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>globl _main
    <span style="color: #339933;">.</span>def	_main<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    _main<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    andl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">15</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">15</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    shrl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    sall	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__alloca
    <span style="color: #00007f; font-weight: bold;">call</span>	___main
    <span style="color: #00007f; font-weight: bold;">call</span>	_apresentacao
    <span style="color: #00007f; font-weight: bold;">call</span>	_fazListaDeNumeros
    <span style="color: #00007f; font-weight: bold;">call</span>	_mostra
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span>comm	_pilhaCrivo<span style="color: #339933;">,</span> <span style="color: #ff0000;">4000</span>	 # <span style="color: #ff0000;">4000</span>
    <span style="color: #339933;">.</span>def	_printf<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span></pre></td></tr></table><p class="theCode" style="display:none;">	.file	&quot;main.c&quot;
    .section .rdata,&quot;dr&quot;
    LC0:
    .ascii &quot;O CRIVO DE ERASTOTENES\12\0&quot;
    .align 4
    LC1:
    .ascii &quot;Codigo com informacao simbolica explicita\12\0&quot;
    LC2:
    .ascii &quot;www.sawp.com.br \12\12\0&quot;
    .text
    .globl _apresentacao
    .def	_apresentacao;	.scl	2;	.type	32;	.endef
    _apresentacao:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$8, %esp
    movl	$LC0, (%esp)
    call	_printf
    movl	$LC1, (%esp)
    call	_printf
    movl	$LC2, (%esp)
    call	_printf
    leave
    ret
    .globl _fazListaDeNumeros
    .def	_fazListaDeNumeros;	.scl	2;	.type	32;	.endef
    _fazListaDeNumeros:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$4, %esp
    movl	$0, -4(%ebp)
    movl	$2, -4(%ebp)
    L3:
    cmpl	$1000, -4(%ebp)
    jg	L2
    movl	-4(%ebp), %edx
    movl	-4(%ebp), %eax
    movl	%eax, _pilhaCrivo(,%edx,4)
    leal	-4(%ebp), %eax
    incl	(%eax)
    jmp	L3
    L2:
    leave
    ret
    .section .rdata,&quot;dr&quot;
    LC3:
    .ascii &quot;%d \12\0&quot;
    .text
    .globl _mostra
    .def	_mostra;	.scl	2;	.type	32;	.endef
    _mostra:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$24, %esp
    movl	$2, -4(%ebp)
    L7:
    cmpl	$1000, -4(%ebp)
    jg	L6
    movl	-4(%ebp), %eax
    movl	_pilhaCrivo(,%eax,4), %eax
    cmpl	-4(%ebp), %eax
    jne	L9
    movl	-4(%ebp), %eax
    movl	%eax, 4(%esp)
    movl	$LC3, (%esp)
    call	_printf
    movl	-4(%ebp), %eax
    addl	-4(%ebp), %eax
    movl	%eax, -8(%ebp)
    L11:
    cmpl	$1000, -8(%ebp)
    jg	L9
    movl	-8(%ebp), %eax
    movl	$0, _pilhaCrivo(,%eax,4)
    movl	-4(%ebp), %edx
    leal	-8(%ebp), %eax
    addl	%edx, (%eax)
    jmp	L11
    L9:
    leal	-4(%ebp), %eax
    incl	(%eax)
    jmp	L7
    L6:
    leave
    ret
    .def	___main;	.scl	2;	.type	32;	.endef
    .globl _main
    .def	_main;	.scl	2;	.type	32;	.endef
    _main:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$8, %esp
    andl	$-16, %esp
    movl	$0, %eax
    addl	$15, %eax
    addl	$15, %eax
    shrl	$4, %eax
    sall	$4, %eax
    movl	%eax, -4(%ebp)
    movl	-4(%ebp), %eax
    call	__alloca
    call	___main
    call	_apresentacao
    call	_fazListaDeNumeros
    call	_mostra
    movl	$1, %eax
    leave
    ret
    .comm	_pilhaCrivo, 4000	 # 4000
    .def	_printf;	.scl	2;	.type	32;	.endef</p></div>
    ;i:4;s:157022:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="asm" style="font-family:monospace;">	<span style="color: #339933;">.</span>file	<span style="color: #7f007f;">&quot;main.cpp&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>def	__ZSt17__verify_groupingPKcjRKSs<span style="color: #666666; font-style: italic;">;	.scl	3;	.type	32;	.endef</span>
    __ZSt17__verify_groupingPKcjRKSs<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">40</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNKSs4sizeEv
    decl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    decl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZSt3minIjERKT_S2_S2_
    movl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movb	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">24</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L2<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">24</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">jae</span>	L5
    cmpb	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L5
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNKSsixEj
    movsbl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #339933;">-</span><span style="color: #ff0000;">24</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movsbl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    <span style="color: #00007f; font-weight: bold;">sete</span>	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">al</span>
    movb	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">al</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    decl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">24</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    incl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L2
    L5<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L6
    cmpb	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L6
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNKSsixEj
    movsbl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movsbl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    <span style="color: #00007f; font-weight: bold;">sete</span>	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">al</span>
    movb	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">al</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    decl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L5
    L6<span style="color: #339933;">:</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #ff0000;">16</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNKSsixEj
    movsbl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movsbl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    <span style="color: #00007f; font-weight: bold;">jg</span>	L8
    movzbl	<span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    andl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movb	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">al</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">25</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L9
    L8<span style="color: #339933;">:</span>
    movb	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">25</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L9<span style="color: #339933;">:</span>
    movzbl	<span style="color: #339933;">-</span><span style="color: #ff0000;">25</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movb	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">al</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movzbl	<span style="color: #339933;">-</span><span style="color: #ff0000;">17</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span>lcomm __ZSt8__ioinit<span style="color: #339933;">,</span><span style="color: #ff0000;">16</span>
    <span style="color: #339933;">.</span>globl _PH040x12
    <span style="color: #0000ff; font-weight: bold;">.bss</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">32</span>
    _PH040x12<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>space <span style="color: #ff0000;">4000</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>globl __Z12rot13_d3c0d3RSs
    <span style="color: #339933;">.</span>def	__Z12rot13_d3c0d3RSs<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    __Z12rot13_d3c0d3RSs<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">24</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">5</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L11<span style="color: #339933;">:</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNKSs6lengthEv
    cmpl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jae</span>	L10
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsixEj
    movsbl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">5</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsixEj
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movb	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">al</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    incl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L11
    L10<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span>def	__Unwind_SjLj_Resume<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	___gxx_personality_sj0<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__Unwind_SjLj_Register<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__Unwind_SjLj_Unregister<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span> <span style="color: #0000ff; font-weight: bold;">.rdata</span><span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;dr&quot;</span>
    LC0<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;T%HWN[T%IJ%JWFXYTYJSJX\0&quot;</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">4</span>
    LC1<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;Htinlt%htr%nsktwrfhft%xnrgtqnhf%j}uqnhnyf3\0&quot;</span>
    LC2<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;|||3xf|u3htr3gw\0&quot;</span>
    LC3<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;\12\0&quot;</span>
    LC4<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;\12\12\0&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>globl __Z13st4rt3R_09833v
    <span style="color: #339933;">.</span>def	__Z13st4rt3R_09833v<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    __Z13st4rt3R_09833v<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edi</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esi</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebx</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">172</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>___gxx_personality_sj0<span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">84</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LLSDA1426<span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">80</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">76</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">24</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>L47<span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">108</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Unwind_SjLj_Register
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">112</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">112</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">116</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">120</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcEC1Ev
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC0<span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">116</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsC1EPKcRKSaIcE
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L16
    L15<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">124</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcED1Ev
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">124</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L17<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L27
    L16<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcED1Ev
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">116</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    decl	<span style="color: #339933;">-</span><span style="color: #ff0000;">120</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcEC1Ev
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC1<span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">116</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">3</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsC1EPKcRKSaIcE
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L20
    L19<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">132</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcED1Ev
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">132</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L21<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L27
    L20<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcED1Ev
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">116</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    decl	<span style="color: #339933;">-</span><span style="color: #ff0000;">120</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcEC1Ev
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC2<span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">116</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsC1EPKcRKSaIcE
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L24
    L23<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">136</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcED1Ev
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">136</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L25<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L27
    L24<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">56</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSaIcED1Ev
    decl	<span style="color: #339933;">-</span><span style="color: #ff0000;">120</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L28
    L27<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">140</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">112</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L30
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    subl	<span style="color: #339933;">-</span><span style="color: #ff0000;">120</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">144</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">144</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    sall	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">112</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    addl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">144</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L31<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">144</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">112</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L30
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">144</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">144</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsD1Ev
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L31
    L30<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">140</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L33<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #339933;">-</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Unwind_SjLj_Resume
    L28<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z12rot13_d3c0d3RSs
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z12rot13_d3c0d3RSs
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z12rot13_d3c0d3RSs
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>__ZSt4cout<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC3<span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC3<span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC4<span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L36
    L47<span style="color: #339933;">:</span>
    leal	<span style="color: #ff0000;">24</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">156</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">100</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">156</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L23
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">156</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L19
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">3</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">156</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L15
    L35<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">148</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    testl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L38
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">12</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L39<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L38
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsD1Ev
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L39
    L38<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">148</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L41<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">128</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #339933;">-</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Unwind_SjLj_Resume
    L36<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    testl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L14
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">12</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L45<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">40</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">je</span>	L14
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">152</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #339933;">-</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">104</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSsD1Ev
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L45
    L14<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">108</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Unwind_SjLj_Unregister
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">172</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    popl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebx</span>
    popl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esi</span>
    popl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edi</span>
    popl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span>	<span style="color: #339933;">.</span>gcc_except_table<span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;dr&quot;</span>
    LLSDA1426<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">byte</span>	<span style="color: #ff0000;">0xff</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">byte</span>	<span style="color: #ff0000;">0xff</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">byte</span>	<span style="color: #ff0000;">0x1</span>
    <span style="color: #339933;">.</span>uleb128 LLSDACSE1426<span style="color: #339933;">-</span>LLSDACSB1426
    LLSDACSB1426<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x0</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x0</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x1</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x0</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x2</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x0</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x3</span>
    <span style="color: #339933;">.</span>uleb128 <span style="color: #ff0000;">0x0</span>
    LLSDACSE1426<span style="color: #339933;">:</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>globl __Z13HP00x98765432v
    <span style="color: #339933;">.</span>def	__Z13HP00x98765432v<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    __Z13HP00x98765432v<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L49<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1000</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jg</span>	L48
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> _PH040x12<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    incl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L49
    L48<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span> <span style="color: #0000ff; font-weight: bold;">.rdata</span><span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;dr&quot;</span>
    LC5<span style="color: #339933;">:</span>
    <span style="color: #339933;">.</span>ascii <span style="color: #7f007f;">&quot;%d \12\0&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>globl __Z13IB00x98701234v
    <span style="color: #339933;">.</span>def	__Z13IB00x98701234v<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    __Z13IB00x98701234v<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">24</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">2</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L53<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1000</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jg</span>	L52
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	_PH040x12<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">jne</span>	L55
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>LC5<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	_printf
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L57<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1000</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jg</span>	L55
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> _PH040x12<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">,%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L57
    L55<span style="color: #339933;">:</span>
    leal	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    incl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L53
    L52<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span>def	___main<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>globl _main
    <span style="color: #339933;">.</span>def	_main<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    _main<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    andl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #339933;">-</span><span style="color: #ff0000;">16</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">15</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    addl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">15</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    shrl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    sall	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__alloca
    <span style="color: #00007f; font-weight: bold;">call</span>	___main
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z13st4rt3R_09833v
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z13HP00x98765432v
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z13IB00x98701234v
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span>	<span style="color: #0000ff; font-weight: bold;">.text</span><span style="color: #0000ff; font-weight: bold;">$</span>_ZSt3minIjERKT_S2_S2_<span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;x&quot;</span>
    <span style="color: #339933;">.</span>linkonce discard
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>globl __ZSt3minIjERKT_S2_S2_
    <span style="color: #339933;">.</span>def	__ZSt3minIjERKT_S2_S2_<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    __ZSt3minIjERKT_S2_S2_<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">4</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span>
    movl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    cmpl	<span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">edx</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">jae</span>	L62
    movl	<span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jmp</span>	L61
    L62<span style="color: #339933;">:</span>
    movl	<span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span><span style="color: #339933;">,</span> <span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    L61<span style="color: #339933;">:</span>
    movl	<span style="color: #339933;">-</span><span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">eax</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>def	__Z41__static_initialization_and_destruction_0ii<span style="color: #666666; font-style: italic;">;	.scl	3;	.type	32;	.endef</span>
    __Z41__static_initialization_and_destruction_0ii<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">65535</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jne</span>	L64
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jne</span>	L64
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>__ZSt8__ioinit<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSt8ios_base4InitC1Ev
    L64<span style="color: #339933;">:</span>
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">65535</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">12</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jne</span>	L63
    cmpl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">8</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">jne</span>	L63
    movl	<span style="color: #0000ff; font-weight: bold;">$</span>__ZSt8__ioinit<span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__ZNSt8ios_base4InitD1Ev
    L63<span style="color: #339933;">:</span>
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>def	__GLOBAL__I_PH040x12<span style="color: #666666; font-style: italic;">;	.scl	3;	.type	32;	.endef</span>
    __GLOBAL__I_PH040x12<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">65535</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">1</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z41__static_initialization_and_destruction_0ii
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span>	<span style="color: #339933;">.</span>ctors<span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;w&quot;</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">4</span>
    <span style="color: #339933;">.</span>long	__GLOBAL__I_PH040x12
    <span style="color: #0000ff; font-weight: bold;">.text</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">2</span>
    <span style="color: #339933;">.</span>def	__GLOBAL__D_PH040x12<span style="color: #666666; font-style: italic;">;	.scl	3;	.type	32;	.endef</span>
    __GLOBAL__D_PH040x12<span style="color: #339933;">:</span>
    pushl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    movl	<span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">ebp</span>
    subl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">8</span><span style="color: #339933;">,</span> <span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">65535</span><span style="color: #339933;">,</span> <span style="color: #ff0000;">4</span><span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    movl	<span style="color: #0000ff; font-weight: bold;">$</span><span style="color: #ff0000;">0</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">&#40;</span><span style="color: #339933;">%</span><span style="color: #46aa03; font-weight: bold;">esp</span><span style="color: #009900; font-weight: bold;">&#41;</span>
    <span style="color: #00007f; font-weight: bold;">call</span>	__Z41__static_initialization_and_destruction_0ii
    <span style="color: #00007f; font-weight: bold;">leave</span>
    <span style="color: #00007f; font-weight: bold;">ret</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">section</span>	<span style="color: #339933;">.</span>dtors<span style="color: #339933;">,</span><span style="color: #7f007f;">&quot;w&quot;</span>
    <span style="color: #339933;">.</span><span style="color: #0000ff; font-weight: bold;">align</span> <span style="color: #ff0000;">4</span>
    <span style="color: #339933;">.</span>long	__GLOBAL__D_PH040x12
    <span style="color: #339933;">.</span>def	__ZNSt8ios_base4InitD1Ev<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	_printf<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNSsD1Ev<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNSsC1EPKcRKSaIcE<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNSaIcED1Ev<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNSaIcEC1Ev<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNSsixEj<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNKSs6lengthEv<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNSt8ios_base4InitC1Ev<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNKSsixEj<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span>
    <span style="color: #339933;">.</span>def	__ZNKSs4sizeEv<span style="color: #666666; font-style: italic;">;	.scl	2;	.type	32;	.endef</span></pre></td></tr></table><p class="theCode" style="display:none;">	.file	&quot;main.cpp&quot;
    .text
    .align 2
    .def	__ZSt17__verify_groupingPKcjRKSs;	.scl	3;	.type	32;	.endef
    __ZSt17__verify_groupingPKcjRKSs:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$40, %esp
    movl	16(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNKSs4sizeEv
    decl	%eax
    movl	%eax, -4(%ebp)
    movl	12(%ebp), %eax
    decl	%eax
    movl	%eax, -12(%ebp)
    leal	-12(%ebp), %eax
    movl	%eax, 4(%esp)
    leal	-4(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZSt3minIjERKT_S2_S2_
    movl	(%eax), %eax
    movl	%eax, -8(%ebp)
    movl	-4(%ebp), %eax
    movl	%eax, -16(%ebp)
    movb	$1, -17(%ebp)
    movl	$0, -24(%ebp)
    L2:
    movl	-24(%ebp), %eax
    cmpl	-8(%ebp), %eax
    jae	L5
    cmpb	$0, -17(%ebp)
    je	L5
    movl	-16(%ebp), %eax
    movl	%eax, 4(%esp)
    movl	16(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNKSsixEj
    movsbl	(%eax),%edx
    movl	8(%ebp), %eax
    addl	-24(%ebp), %eax
    movsbl	(%eax),%eax
    cmpl	%eax, %edx
    sete	%al
    movb	%al, -17(%ebp)
    leal	-16(%ebp), %eax
    decl	(%eax)
    leal	-24(%ebp), %eax
    incl	(%eax)
    jmp	L2
    L5:
    cmpl	$0, -16(%ebp)
    je	L6
    cmpb	$0, -17(%ebp)
    je	L6
    movl	-16(%ebp), %eax
    movl	%eax, 4(%esp)
    movl	16(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNKSsixEj
    movsbl	(%eax),%edx
    movl	8(%ebp), %eax
    addl	-8(%ebp), %eax
    movsbl	(%eax),%eax
    cmpl	%eax, %edx
    sete	%al
    movb	%al, -17(%ebp)
    leal	-16(%ebp), %eax
    decl	(%eax)
    jmp	L5
    L6:
    movl	$0, 4(%esp)
    movl	16(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNKSsixEj
    movsbl	(%eax),%edx
    movl	8(%ebp), %eax
    addl	-8(%ebp), %eax
    movsbl	(%eax),%eax
    cmpl	%eax, %edx
    jg	L8
    movzbl	-17(%ebp), %eax
    andl	$1, %eax
    movb	%al, -25(%ebp)
    jmp	L9
    L8:
    movb	$0, -25(%ebp)
    L9:
    movzbl	-25(%ebp), %eax
    movb	%al, -17(%ebp)
    movzbl	-17(%ebp), %eax
    leave
    ret
    .lcomm __ZSt8__ioinit,16
    .globl _PH040x12
    .bss
    .align 32
    _PH040x12:
    .space 4000
    .text
    .align 2
    .globl __Z12rot13_d3c0d3RSs
    .def	__Z12rot13_d3c0d3RSs;	.scl	2;	.type	32;	.endef
    __Z12rot13_d3c0d3RSs:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$24, %esp
    movl	$5, -4(%ebp)
    movl	$0, -12(%ebp)
    L11:
    movl	8(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNKSs6lengthEv
    cmpl	%eax, -12(%ebp)
    jae	L10
    movl	-12(%ebp), %eax
    movl	%eax, 4(%esp)
    movl	8(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSsixEj
    movsbl	(%eax),%eax
    subl	$5, %eax
    movl	%eax, -8(%ebp)
    movl	-12(%ebp), %eax
    movl	%eax, 4(%esp)
    movl	8(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSsixEj
    movl	%eax, %edx
    movl	-8(%ebp), %eax
    movb	%al, (%edx)
    leal	-12(%ebp), %eax
    incl	(%eax)
    jmp	L11
    L10:
    leave
    ret
    .def	__Unwind_SjLj_Resume;	.scl	2;	.type	32;	.endef
    .def	___gxx_personality_sj0;	.scl	2;	.type	32;	.endef
    .def	__Unwind_SjLj_Register;	.scl	2;	.type	32;	.endef
    .def	__Unwind_SjLj_Unregister;	.scl	2;	.type	32;	.endef
    .section .rdata,&quot;dr&quot;
    LC0:
    .ascii &quot;T%HWN[T%IJ%JWFXYTYJSJX\0&quot;
    .align 4
    LC1:
    .ascii &quot;Htinlt%htr%nsktwrfhft%xnrgtqnhf%j}uqnhnyf3\0&quot;
    LC2:
    .ascii &quot;|||3xf|u3htr3gw\0&quot;
    LC3:
    .ascii &quot;\12\0&quot;
    LC4:
    .ascii &quot;\12\12\0&quot;
    .text
    .align 2
    .globl __Z13st4rt3R_09833v
    .def	__Z13st4rt3R_09833v;	.scl	2;	.type	32;	.endef
    __Z13st4rt3R_09833v:
    pushl	%ebp
    movl	%esp, %ebp
    pushl	%edi
    pushl	%esi
    pushl	%ebx
    subl	$172, %esp
    movl	$___gxx_personality_sj0, -84(%ebp)
    movl	$LLSDA1426, -80(%ebp)
    leal	-76(%ebp), %eax
    leal	-24(%ebp), %edx
    movl	%edx, (%eax)
    movl	$L47, %edx
    movl	%edx, 4(%eax)
    movl	%esp, 8(%eax)
    leal	-108(%ebp), %eax
    movl	%eax, (%esp)
    call	__Unwind_SjLj_Register
    leal	-40(%ebp), %eax
    movl	%eax, -112(%ebp)
    movl	-112(%ebp), %edx
    movl	%edx, -116(%ebp)
    movl	$2, -120(%ebp)
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcEC1Ev
    leal	-56(%ebp), %eax
    movl	%eax, 8(%esp)
    movl	$LC0, 4(%esp)
    movl	-116(%ebp), %eax
    movl	%eax, (%esp)
    movl	$4, -104(%ebp)
    call	__ZNSsC1EPKcRKSaIcE
    jmp	L16
    L15:
    movl	-128(%ebp), %edx
    movl	%edx, -124(%ebp)
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcED1Ev
    movl	-124(%ebp), %eax
    movl	%eax, -128(%ebp)
    L17:
    jmp	L27
    L16:
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcED1Ev
    addl	$4, -116(%ebp)
    decl	-120(%ebp)
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcEC1Ev
    leal	-56(%ebp), %eax
    movl	%eax, 8(%esp)
    movl	$LC1, 4(%esp)
    movl	-116(%ebp), %edx
    movl	%edx, (%esp)
    movl	$3, -104(%ebp)
    call	__ZNSsC1EPKcRKSaIcE
    jmp	L20
    L19:
    movl	-128(%ebp), %eax
    movl	%eax, -132(%ebp)
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcED1Ev
    movl	-132(%ebp), %edx
    movl	%edx, -128(%ebp)
    L21:
    jmp	L27
    L20:
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcED1Ev
    addl	$4, -116(%ebp)
    decl	-120(%ebp)
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcEC1Ev
    leal	-56(%ebp), %eax
    movl	%eax, 8(%esp)
    movl	$LC2, 4(%esp)
    movl	-116(%ebp), %eax
    movl	%eax, (%esp)
    movl	$2, -104(%ebp)
    call	__ZNSsC1EPKcRKSaIcE
    jmp	L24
    L23:
    movl	-128(%ebp), %edx
    movl	%edx, -136(%ebp)
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcED1Ev
    movl	-136(%ebp), %eax
    movl	%eax, -128(%ebp)
    L25:
    jmp	L27
    L24:
    leal	-56(%ebp), %eax
    movl	%eax, (%esp)
    call	__ZNSaIcED1Ev
    decl	-120(%ebp)
    jmp	L28
    L27:
    movl	-128(%ebp), %edx
    movl	%edx, -140(%ebp)
    cmpl	$0, -112(%ebp)
    je	L30
    movl	$2, %eax
    subl	-120(%ebp), %eax
    movl	%eax, -144(%ebp)
    movl	-144(%ebp), %eax
    sall	$2, %eax
    movl	-112(%ebp), %edx
    addl	%eax, %edx
    movl	%edx, -144(%ebp)
    L31:
    movl	-144(%ebp), %eax
    cmpl	%eax, -112(%ebp)
    je	L30
    subl	$4, -144(%ebp)
    movl	-144(%ebp), %edx
    movl	%edx, (%esp)
    movl	$0, -104(%ebp)
    call	__ZNSsD1Ev
    jmp	L31
    L30:
    movl	-140(%ebp), %eax
    movl	%eax, -128(%ebp)
    L33:
    movl	-128(%ebp), %edx
    movl	%edx, (%esp)
    movl	$-1, -104(%ebp)
    call	__Unwind_SjLj_Resume
    L28:
    leal	-40(%ebp), %eax
    movl	%eax, (%esp)
    movl	$1, -104(%ebp)
    call	__Z12rot13_d3c0d3RSs
    leal	-40(%ebp), %eax
    addl	$4, %eax
    movl	%eax, (%esp)
    call	__Z12rot13_d3c0d3RSs
    leal	-40(%ebp), %eax
    addl	$8, %eax
    movl	%eax, (%esp)
    call	__Z12rot13_d3c0d3RSs
    leal	-40(%ebp), %eax
    movl	%eax, 4(%esp)
    movl	$__ZSt4cout, (%esp)
    call	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
    movl	$LC3, 4(%esp)
    movl	%eax, (%esp)
    call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
    leal	-40(%ebp), %edx
    addl	$4, %edx
    movl	%edx, 4(%esp)
    movl	%eax, (%esp)
    call	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
    movl	$LC3, 4(%esp)
    movl	%eax, (%esp)
    call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
    leal	-40(%ebp), %edx
    addl	$8, %edx
    movl	%edx, 4(%esp)
    movl	%eax, (%esp)
    call	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
    movl	$LC4, 4(%esp)
    movl	%eax, (%esp)
    call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
    jmp	L36
    L47:
    leal	24(%ebp), %ebp
    movl	-104(%ebp), %eax
    movl	%eax, -156(%ebp)
    movl	-100(%ebp), %edx
    movl	%edx, -128(%ebp)
    cmpl	$1, -156(%ebp)
    je	L23
    cmpl	$2, -156(%ebp)
    je	L19
    cmpl	$3, -156(%ebp)
    je	L15
    L35:
    movl	-128(%ebp), %eax
    movl	%eax, -148(%ebp)
    leal	-40(%ebp), %eax
    testl	%eax, %eax
    je	L38
    leal	-40(%ebp), %edx
    movl	%edx, -152(%ebp)
    addl	$12, -152(%ebp)
    L39:
    leal	-40(%ebp), %eax
    cmpl	-152(%ebp), %eax
    je	L38
    subl	$4, -152(%ebp)
    movl	-152(%ebp), %eax
    movl	%eax, (%esp)
    movl	$0, -104(%ebp)
    call	__ZNSsD1Ev
    jmp	L39
    L38:
    movl	-148(%ebp), %edx
    movl	%edx, -128(%ebp)
    L41:
    movl	-128(%ebp), %eax
    movl	%eax, (%esp)
    movl	$-1, -104(%ebp)
    call	__Unwind_SjLj_Resume
    L36:
    leal	-40(%ebp), %eax
    testl	%eax, %eax
    je	L14
    leal	-40(%ebp), %edx
    movl	%edx, -152(%ebp)
    addl	$12, -152(%ebp)
    L45:
    leal	-40(%ebp), %eax
    cmpl	-152(%ebp), %eax
    je	L14
    subl	$4, -152(%ebp)
    movl	-152(%ebp), %eax
    movl	%eax, (%esp)
    movl	$-1, -104(%ebp)
    call	__ZNSsD1Ev
    jmp	L45
    L14:
    leal	-108(%ebp), %eax
    movl	%eax, (%esp)
    call	__Unwind_SjLj_Unregister
    addl	$172, %esp
    popl	%ebx
    popl	%esi
    popl	%edi
    popl	%ebp
    ret
    .section	.gcc_except_table,&quot;dr&quot;
    LLSDA1426:
    .byte	0xff
    .byte	0xff
    .byte	0x1
    .uleb128 LLSDACSE1426-LLSDACSB1426
    LLSDACSB1426:
    .uleb128 0x0
    .uleb128 0x0
    .uleb128 0x1
    .uleb128 0x0
    .uleb128 0x2
    .uleb128 0x0
    .uleb128 0x3
    .uleb128 0x0
    LLSDACSE1426:
    .text
    .align 2
    .globl __Z13HP00x98765432v
    .def	__Z13HP00x98765432v;	.scl	2;	.type	32;	.endef
    __Z13HP00x98765432v:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$4, %esp
    movl	$0, -4(%ebp)
    movl	$2, -4(%ebp)
    L49:
    cmpl	$1000, -4(%ebp)
    jg	L48
    movl	-4(%ebp), %edx
    movl	-4(%ebp), %eax
    movl	%eax, _PH040x12(,%edx,4)
    leal	-4(%ebp), %eax
    incl	(%eax)
    jmp	L49
    L48:
    leave
    ret
    .section .rdata,&quot;dr&quot;
    LC5:
    .ascii &quot;%d \12\0&quot;
    .text
    .align 2
    .globl __Z13IB00x98701234v
    .def	__Z13IB00x98701234v;	.scl	2;	.type	32;	.endef
    __Z13IB00x98701234v:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$24, %esp
    movl	$2, -4(%ebp)
    L53:
    cmpl	$1000, -4(%ebp)
    jg	L52
    movl	-4(%ebp), %eax
    movl	_PH040x12(,%eax,4), %eax
    cmpl	-4(%ebp), %eax
    jne	L55
    movl	-4(%ebp), %eax
    movl	%eax, 4(%esp)
    movl	$LC5, (%esp)
    call	_printf
    movl	-4(%ebp), %eax
    addl	-4(%ebp), %eax
    movl	%eax, -8(%ebp)
    L57:
    cmpl	$1000, -8(%ebp)
    jg	L55
    movl	-8(%ebp), %eax
    movl	$0, _PH040x12(,%eax,4)
    movl	-4(%ebp), %edx
    leal	-8(%ebp), %eax
    addl	%edx, (%eax)
    jmp	L57
    L55:
    leal	-4(%ebp), %eax
    incl	(%eax)
    jmp	L53
    L52:
    leave
    ret
    .def	___main;	.scl	2;	.type	32;	.endef
    .align 2
    .globl _main
    .def	_main;	.scl	2;	.type	32;	.endef
    _main:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$8, %esp
    andl	$-16, %esp
    movl	$0, %eax
    addl	$15, %eax
    addl	$15, %eax
    shrl	$4, %eax
    sall	$4, %eax
    movl	%eax, -4(%ebp)
    movl	-4(%ebp), %eax
    call	__alloca
    call	___main
    call	__Z13st4rt3R_09833v
    call	__Z13HP00x98765432v
    call	__Z13IB00x98701234v
    movl	$1, %eax
    leave
    ret
    .section	.text$_ZSt3minIjERKT_S2_S2_,&quot;x&quot;
    .linkonce discard
    .align 2
    .globl __ZSt3minIjERKT_S2_S2_
    .def	__ZSt3minIjERKT_S2_S2_;	.scl	2;	.type	32;	.endef
    __ZSt3minIjERKT_S2_S2_:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$4, %esp
    movl	12(%ebp), %eax
    movl	8(%ebp), %edx
    movl	(%eax), %eax
    cmpl	(%edx), %eax
    jae	L62
    movl	12(%ebp), %eax
    movl	%eax, -4(%ebp)
    jmp	L61
    L62:
    movl	8(%ebp), %eax
    movl	%eax, -4(%ebp)
    L61:
    movl	-4(%ebp), %eax
    leave
    ret
    .text
    .align 2
    .def	__Z41__static_initialization_and_destruction_0ii;	.scl	3;	.type	32;	.endef
    __Z41__static_initialization_and_destruction_0ii:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$8, %esp
    cmpl	$65535, 12(%ebp)
    jne	L64
    cmpl	$1, 8(%ebp)
    jne	L64
    movl	$__ZSt8__ioinit, (%esp)
    call	__ZNSt8ios_base4InitC1Ev
    L64:
    cmpl	$65535, 12(%ebp)
    jne	L63
    cmpl	$0, 8(%ebp)
    jne	L63
    movl	$__ZSt8__ioinit, (%esp)
    call	__ZNSt8ios_base4InitD1Ev
    L63:
    leave
    ret
    .align 2
    .def	__GLOBAL__I_PH040x12;	.scl	3;	.type	32;	.endef
    __GLOBAL__I_PH040x12:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$8, %esp
    movl	$65535, 4(%esp)
    movl	$1, (%esp)
    call	__Z41__static_initialization_and_destruction_0ii
    leave
    ret
    .section	.ctors,&quot;w&quot;
    .align 4
    .long	__GLOBAL__I_PH040x12
    .text
    .align 2
    .def	__GLOBAL__D_PH040x12;	.scl	3;	.type	32;	.endef
    __GLOBAL__D_PH040x12:
    pushl	%ebp
    movl	%esp, %ebp
    subl	$8, %esp
    movl	$65535, 4(%esp)
    movl	$0, (%esp)
    call	__Z41__static_initialization_and_destruction_0ii
    leave
    ret
    .section	.dtors,&quot;w&quot;
    .align 4
    .long	__GLOBAL__D_PH040x12
    .def	__ZNSt8ios_base4InitD1Ev;	.scl	2;	.type	32;	.endef
    .def	_printf;	.scl	2;	.type	32;	.endef
    .def	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc;	.scl	2;	.type	32;	.endef
    .def	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E;	.scl	2;	.type	32;	.endef
    .def	__ZNSsD1Ev;	.scl	2;	.type	32;	.endef
    .def	__ZNSsC1EPKcRKSaIcE;	.scl	2;	.type	32;	.endef
    .def	__ZNSaIcED1Ev;	.scl	2;	.type	32;	.endef
    .def	__ZNSaIcEC1Ev;	.scl	2;	.type	32;	.endef
    .def	__ZNSsixEj;	.scl	2;	.type	32;	.endef
    .def	__ZNKSs6lengthEv;	.scl	2;	.type	32;	.endef
    .def	__ZNSt8ios_base4InitC1Ev;	.scl	2;	.type	32;	.endef
    .def	__ZNKSsixEj;	.scl	2;	.type	32;	.endef
    .def	__ZNKSs4sizeEv;	.scl	2;	.type	32;	.endef</p></div>
    ;i:5;s:2570:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">void</span> rot13ASC_decode<span style="color: #008000;">&#40;</span>string <span style="color: #000040;">&amp;</span> input<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">int</span> key<span style="color: #000080;">=</span><span style="color: #0000dd;">13</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">int</span> asciicode<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>i <span style="color: #000080;">&lt;</span> input .<span style="color: #007788;">length</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    asciicode <span style="color: #000080;">=</span> <span style="color: #0000ff;">static_cast</span><span style="color: #000080;">&lt;</span> <span style="color: #0000ff;">int</span> <span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span>input<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span><span style="color: #000040;">-</span> key<span style="color: #008080;">;</span>
    input<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span> <span style="color: #000080;">=</span>  <span style="color: #0000ff;">static_cast</span><span style="color: #000080;">&lt;</span> <span style="color: #0000ff;">char</span> <span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span>asciicode<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">void rot13ASC_decode(string &amp; input){
    const int key=13;
    int asciicode;
    
    for(int i=0;i &lt; input .length();i++) {
    asciicode = static_cast&lt; int &gt;(input[i])- key;
    input[i] =  static_cast&lt; char &gt;(asciicode);
    }
    }</p></div>
    ";}
categories:
  - Programming Internals
---
Se um desenvolvedor deseja se inteirar de como age um cracker deve testar se seu programa gera informações simbólicas antes de lançá-lo no mercado. Ainda que não seja possível remover toda essa informação da estrutura de um programa, modificar alguns pontos críticos pode ser crucial para o sucesso ou não da proteção.

A eliminação total não ocorre porque programamos em linguagens de alto nível, como C e C++, que são convertidas em instruções processáveis através de um compilador. É o compilador que acaba gerando dados que servem como &#8220;pontos de referências&#8221; para quem investiga um código disassemblado.

Os compiladores costumam gerar informações simbólicas – para representar as lincagens – quando convertem as relações de importação e exportação de tabelas e extensões. Um programa com grande uso de DLLs, onde cada uma exporta uma grande quantidade de funções, necessitará de uma lista relacionando onde estão as funções exportadas, normalmente indicando o que elas fazem, o que é de grande serventia para os crackers.

Para confundir as referências que possam ser lógicas para o cracker, vale a pena exportar as funções com números ao invés de nomes. Essa pequena medida é eficiente no atraso do trabalho de um cracker, especialmente se usadas linguagens de orientadas a objetos, como C++ e Turbo Pascal.

Pessoalmente, nas poucas vezes que me deparei com códigos numéricos referenciando subrotinas acabei desistindo do trabalho devido à exaustiva e tediosa tarefa de só me ter números com pouco sentido.

A questão da informação simbólica é diferente com as linguagens que geram um assembly em bytecode. Estas linguagens muitas vezes usam códigos nominais internos para a referenciação dos endereços. Então, todos nomes internos são preservados quando o programa é compilado. Por esta estrutura nominal, os bytecodes são mais facilmente decompilados que os códigos binários.

As strings não podem ser simplesmente eliminadas, mas elas podem ser recolocadas com outras strings de forma que as referências cruzadas não fiquem prejudicadas. 

Veja o código que mantém as informações simbólicas:

<pre lang="cpp">#include &lt; stdio .h >

#define NMAX 1000
#define APR0 "O CRIVO DE ERASTOTENES\n"
#define APR1 "Codigo com informacao simbolica explicita\n"
#define APR2 "www.sawp.com.br \n\n"

int pilhaCrivo[NMAX];


void apresentacao(){
	printf(APR0);
	printf(APR1);
	printf(APR2);
}

void fazListaDeNumeros(){
	int i=0;
	for (i=2; i&lt; =NMAX; i++) {
	        pilhaCrivo[i]=i;
	}
}

void mostra(void){
	int i,j;
	for (i=2; i&lt;=NMAX; i++) {
	        if (pilhaCrivo[i]==i) {
	            printf("%d \n", i);
	            for (j=i+i; j&lt;=NMAX; j+=i) {
	                pilhaCrivo[j]=0;
	            }
	        }
	    }
}

int main() {
	apresentacao();
	fazListaDeNumeros();
	mostra();

	return 1;
}
</pre>

Agora veja o código abaixo, onde as informações simbólicas foram removidas: 

<div>
  <pre lang="cpp">
#include &lt; 8203099666.h >
#include &lt; 1010011010.h >
#include &lt; 75981212.h >
using std::string;
using std::cout;

#define N32MMX2 1000
#define APR1 "Htinlt%htr%nsktwrfhft%xnrgtqnhf%j}uqnhnyf3" 
#define APR2 "|||3xf|u3htr3gw" 
#define APR0 
T%HWN[T%IJ%JWFXYTYJSJX


int PH040x12[N32MMX2];


void rot13_d3c0d3(string & INx990012){
	const int kkk=5;
	int a5c11c0d3;

	for(int i=0;i&lt; inx990012 .length();i++) {
		a5c11c0d3 = static_cast&lt; int >(INx990012[i])- kkk;
		INx990012[i] =  static_cast&lt; char >(a5c11c0d3);
	}
}

void st4rt3R_09833(){
	string h0xx3232122[] = {APR0, APR1, APR2};

	rot13_d3c0d3(h0xx3232122[0]);
	rot13_d3c0d3(h0xx3232122[1]);
	rot13_d3c0d3(h0xx3232122[2]);

	cout &lt; &lt; h0xx3232122[0] &lt; &lt; "\n" &lt; &lt; h0xx3232122[1] &lt; &lt; "\n" &lt; &lt; h0xx3232122[2] &lt; &lt; "\n\n";
}


void HP00x98765432(){
	int i=0;
	for (i=2; i &lt;= N32MMX2; i++) {
	        PH040x12[i]=i;
	}
}

void IB00x98701234(void){
	int i,j;
	for (i=2; i &lt;= N32MMX2; i++) {
	        if (PH040x12[i]==i) {
	            printf("%d \n", i);
	            for (j=i+i; j &lt;= N32MMX2; j+=i) {
	                PH040x12[j]=0;
	            }
	        }
	    }
}

int main() {
	st4rt3R_09833();
	HP00x98765432();
	IB00x98701234();

	return 1;
}
</pre>
</div>

Da mesma forma, comparemos o código em assembly: 

<pre lang="asm">.file	"main.c"
	.section .rdata,"dr"
LC0:
	.ascii "O CRIVO DE ERASTOTENES\12\0"
	.align 4
LC1:
	.ascii "Codigo com informacao simbolica explicita\12\0"
LC2:
	.ascii "www.sawp.com.br \12\12\0"
	.text
.globl _apresentacao
	.def	_apresentacao;	.scl	2;	.type	32;	.endef
_apresentacao:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	movl	$LC0, (%esp)
	call	_printf
	movl	$LC1, (%esp)
	call	_printf
	movl	$LC2, (%esp)
	call	_printf
	leave
	ret
.globl _fazListaDeNumeros
	.def	_fazListaDeNumeros;	.scl	2;	.type	32;	.endef
_fazListaDeNumeros:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$4, %esp
	movl	$0, -4(%ebp)
	movl	$2, -4(%ebp)
L3:
	cmpl	$1000, -4(%ebp)
	jg	L2
	movl	-4(%ebp), %edx
	movl	-4(%ebp), %eax
	movl	%eax, _pilhaCrivo(,%edx,4)
	leal	-4(%ebp), %eax
	incl	(%eax)
	jmp	L3
L2:
	leave
	ret
	.section .rdata,"dr"
LC3:
	.ascii "%d \12\0"
	.text
.globl _mostra
	.def	_mostra;	.scl	2;	.type	32;	.endef
_mostra:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$24, %esp
	movl	$2, -4(%ebp)
L7:
	cmpl	$1000, -4(%ebp)
	jg	L6
	movl	-4(%ebp), %eax
	movl	_pilhaCrivo(,%eax,4), %eax
	cmpl	-4(%ebp), %eax
	jne	L9
	movl	-4(%ebp), %eax
	movl	%eax, 4(%esp)
	movl	$LC3, (%esp)
	call	_printf
	movl	-4(%ebp), %eax
	addl	-4(%ebp), %eax
	movl	%eax, -8(%ebp)
L11:
	cmpl	$1000, -8(%ebp)
	jg	L9
	movl	-8(%ebp), %eax
	movl	$0, _pilhaCrivo(,%eax,4)
	movl	-4(%ebp), %edx
	leal	-8(%ebp), %eax
	addl	%edx, (%eax)
	jmp	L11
L9:
	leal	-4(%ebp), %eax
	incl	(%eax)
	jmp	L7
L6:
	leave
	ret
	.def	___main;	.scl	2;	.type	32;	.endef
.globl _main
	.def	_main;	.scl	2;	.type	32;	.endef
_main:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	andl	$-16, %esp
	movl	$0, %eax
	addl	$15, %eax
	addl	$15, %eax
	shrl	$4, %eax
	sall	$4, %eax
	movl	%eax, -4(%ebp)
	movl	-4(%ebp), %eax
	call	__alloca
	call	___main
	call	_apresentacao
	call	_fazListaDeNumeros
	call	_mostra
	movl	$1, %eax
	leave
	ret
	.comm	_pilhaCrivo, 4000	 # 4000
	.def	_printf;	.scl	2;	.type	32;	.endef
</pre>

Agora o mesmo código sem informações simbólicas explícitas:

<pre lang="asm">.file	"main.cpp"
	.text
	.align 2
	.def	__ZSt17__verify_groupingPKcjRKSs;	.scl	3;	.type	32;	.endef
__ZSt17__verify_groupingPKcjRKSs:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$40, %esp
	movl	16(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNKSs4sizeEv
	decl	%eax
	movl	%eax, -4(%ebp)
	movl	12(%ebp), %eax
	decl	%eax
	movl	%eax, -12(%ebp)
	leal	-12(%ebp), %eax
	movl	%eax, 4(%esp)
	leal	-4(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZSt3minIjERKT_S2_S2_
	movl	(%eax), %eax
	movl	%eax, -8(%ebp)
	movl	-4(%ebp), %eax
	movl	%eax, -16(%ebp)
	movb	$1, -17(%ebp)
	movl	$0, -24(%ebp)
L2:
	movl	-24(%ebp), %eax
	cmpl	-8(%ebp), %eax
	jae	L5
	cmpb	$0, -17(%ebp)
	je	L5
	movl	-16(%ebp), %eax
	movl	%eax, 4(%esp)
	movl	16(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNKSsixEj
	movsbl	(%eax),%edx
	movl	8(%ebp), %eax
	addl	-24(%ebp), %eax
	movsbl	(%eax),%eax
	cmpl	%eax, %edx
	sete	%al
	movb	%al, -17(%ebp)
	leal	-16(%ebp), %eax
	decl	(%eax)
	leal	-24(%ebp), %eax
	incl	(%eax)
	jmp	L2
L5:
	cmpl	$0, -16(%ebp)
	je	L6
	cmpb	$0, -17(%ebp)
	je	L6
	movl	-16(%ebp), %eax
	movl	%eax, 4(%esp)
	movl	16(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNKSsixEj
	movsbl	(%eax),%edx
	movl	8(%ebp), %eax
	addl	-8(%ebp), %eax
	movsbl	(%eax),%eax
	cmpl	%eax, %edx
	sete	%al
	movb	%al, -17(%ebp)
	leal	-16(%ebp), %eax
	decl	(%eax)
	jmp	L5
L6:
	movl	$0, 4(%esp)
	movl	16(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNKSsixEj
	movsbl	(%eax),%edx
	movl	8(%ebp), %eax
	addl	-8(%ebp), %eax
	movsbl	(%eax),%eax
	cmpl	%eax, %edx
	jg	L8
	movzbl	-17(%ebp), %eax
	andl	$1, %eax
	movb	%al, -25(%ebp)
	jmp	L9
L8:
	movb	$0, -25(%ebp)
L9:
	movzbl	-25(%ebp), %eax
	movb	%al, -17(%ebp)
	movzbl	-17(%ebp), %eax
	leave
	ret
.lcomm __ZSt8__ioinit,16
.globl _PH040x12
	.bss
	.align 32
_PH040x12:
	.space 4000
	.text
	.align 2
.globl __Z12rot13_d3c0d3RSs
	.def	__Z12rot13_d3c0d3RSs;	.scl	2;	.type	32;	.endef
__Z12rot13_d3c0d3RSs:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$24, %esp
	movl	$5, -4(%ebp)
	movl	$0, -12(%ebp)
L11:
	movl	8(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNKSs6lengthEv
	cmpl	%eax, -12(%ebp)
	jae	L10
	movl	-12(%ebp), %eax
	movl	%eax, 4(%esp)
	movl	8(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSsixEj
	movsbl	(%eax),%eax
	subl	$5, %eax
	movl	%eax, -8(%ebp)
	movl	-12(%ebp), %eax
	movl	%eax, 4(%esp)
	movl	8(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSsixEj
	movl	%eax, %edx
	movl	-8(%ebp), %eax
	movb	%al, (%edx)
	leal	-12(%ebp), %eax
	incl	(%eax)
	jmp	L11
L10:
	leave
	ret
	.def	__Unwind_SjLj_Resume;	.scl	2;	.type	32;	.endef
	.def	___gxx_personality_sj0;	.scl	2;	.type	32;	.endef
	.def	__Unwind_SjLj_Register;	.scl	2;	.type	32;	.endef
	.def	__Unwind_SjLj_Unregister;	.scl	2;	.type	32;	.endef
	.section .rdata,"dr"
LC0:
	.ascii "T%HWN[T%IJ%JWFXYTYJSJX\0"
	.align 4
LC1:
	.ascii "Htinlt%htr%nsktwrfhft%xnrgtqnhf%j}uqnhnyf3\0"
LC2:
	.ascii "|||3xf|u3htr3gw\0"
LC3:
	.ascii "\12\0"
LC4:
	.ascii "\12\12\0"
	.text
	.align 2
.globl __Z13st4rt3R_09833v
	.def	__Z13st4rt3R_09833v;	.scl	2;	.type	32;	.endef
__Z13st4rt3R_09833v:
	pushl	%ebp
	movl	%esp, %ebp
	pushl	%edi
	pushl	%esi
	pushl	%ebx
	subl	$172, %esp
	movl	$___gxx_personality_sj0, -84(%ebp)
	movl	$LLSDA1426, -80(%ebp)
	leal	-76(%ebp), %eax
	leal	-24(%ebp), %edx
	movl	%edx, (%eax)
	movl	$L47, %edx
	movl	%edx, 4(%eax)
	movl	%esp, 8(%eax)
	leal	-108(%ebp), %eax
	movl	%eax, (%esp)
	call	__Unwind_SjLj_Register
	leal	-40(%ebp), %eax
	movl	%eax, -112(%ebp)
	movl	-112(%ebp), %edx
	movl	%edx, -116(%ebp)
	movl	$2, -120(%ebp)
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcEC1Ev
	leal	-56(%ebp), %eax
	movl	%eax, 8(%esp)
	movl	$LC0, 4(%esp)
	movl	-116(%ebp), %eax
	movl	%eax, (%esp)
	movl	$4, -104(%ebp)
	call	__ZNSsC1EPKcRKSaIcE
	jmp	L16
L15:
	movl	-128(%ebp), %edx
	movl	%edx, -124(%ebp)
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcED1Ev
	movl	-124(%ebp), %eax
	movl	%eax, -128(%ebp)
L17:
	jmp	L27
L16:
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcED1Ev
	addl	$4, -116(%ebp)
	decl	-120(%ebp)
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcEC1Ev
	leal	-56(%ebp), %eax
	movl	%eax, 8(%esp)
	movl	$LC1, 4(%esp)
	movl	-116(%ebp), %edx
	movl	%edx, (%esp)
	movl	$3, -104(%ebp)
	call	__ZNSsC1EPKcRKSaIcE
	jmp	L20
L19:
	movl	-128(%ebp), %eax
	movl	%eax, -132(%ebp)
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcED1Ev
	movl	-132(%ebp), %edx
	movl	%edx, -128(%ebp)
L21:
	jmp	L27
L20:
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcED1Ev
	addl	$4, -116(%ebp)
	decl	-120(%ebp)
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcEC1Ev
	leal	-56(%ebp), %eax
	movl	%eax, 8(%esp)
	movl	$LC2, 4(%esp)
	movl	-116(%ebp), %eax
	movl	%eax, (%esp)
	movl	$2, -104(%ebp)
	call	__ZNSsC1EPKcRKSaIcE
	jmp	L24
L23:
	movl	-128(%ebp), %edx
	movl	%edx, -136(%ebp)
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcED1Ev
	movl	-136(%ebp), %eax
	movl	%eax, -128(%ebp)
L25:
	jmp	L27
L24:
	leal	-56(%ebp), %eax
	movl	%eax, (%esp)
	call	__ZNSaIcED1Ev
	decl	-120(%ebp)
	jmp	L28
L27:
	movl	-128(%ebp), %edx
	movl	%edx, -140(%ebp)
	cmpl	$0, -112(%ebp)
	je	L30
	movl	$2, %eax
	subl	-120(%ebp), %eax
	movl	%eax, -144(%ebp)
	movl	-144(%ebp), %eax
	sall	$2, %eax
	movl	-112(%ebp), %edx
	addl	%eax, %edx
	movl	%edx, -144(%ebp)
L31:
	movl	-144(%ebp), %eax
	cmpl	%eax, -112(%ebp)
	je	L30
	subl	$4, -144(%ebp)
	movl	-144(%ebp), %edx
	movl	%edx, (%esp)
	movl	$0, -104(%ebp)
	call	__ZNSsD1Ev
	jmp	L31
L30:
	movl	-140(%ebp), %eax
	movl	%eax, -128(%ebp)
L33:
	movl	-128(%ebp), %edx
	movl	%edx, (%esp)
	movl	$-1, -104(%ebp)
	call	__Unwind_SjLj_Resume
L28:
	leal	-40(%ebp), %eax
	movl	%eax, (%esp)
	movl	$1, -104(%ebp)
	call	__Z12rot13_d3c0d3RSs
	leal	-40(%ebp), %eax
	addl	$4, %eax
	movl	%eax, (%esp)
	call	__Z12rot13_d3c0d3RSs
	leal	-40(%ebp), %eax
	addl	$8, %eax
	movl	%eax, (%esp)
	call	__Z12rot13_d3c0d3RSs
	leal	-40(%ebp), %eax
	movl	%eax, 4(%esp)
	movl	$__ZSt4cout, (%esp)
	call	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
	movl	$LC3, 4(%esp)
	movl	%eax, (%esp)
	call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
	leal	-40(%ebp), %edx
	addl	$4, %edx
	movl	%edx, 4(%esp)
	movl	%eax, (%esp)
	call	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
	movl	$LC3, 4(%esp)
	movl	%eax, (%esp)
	call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
	leal	-40(%ebp), %edx
	addl	$8, %edx
	movl	%edx, 4(%esp)
	movl	%eax, (%esp)
	call	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E
	movl	$LC4, 4(%esp)
	movl	%eax, (%esp)
	call	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
	jmp	L36
L47:
	leal	24(%ebp), %ebp
	movl	-104(%ebp), %eax
	movl	%eax, -156(%ebp)
	movl	-100(%ebp), %edx
	movl	%edx, -128(%ebp)
	cmpl	$1, -156(%ebp)
	je	L23
	cmpl	$2, -156(%ebp)
	je	L19
	cmpl	$3, -156(%ebp)
	je	L15
L35:
	movl	-128(%ebp), %eax
	movl	%eax, -148(%ebp)
	leal	-40(%ebp), %eax
	testl	%eax, %eax
	je	L38
	leal	-40(%ebp), %edx
	movl	%edx, -152(%ebp)
	addl	$12, -152(%ebp)
L39:
	leal	-40(%ebp), %eax
	cmpl	-152(%ebp), %eax
	je	L38
	subl	$4, -152(%ebp)
	movl	-152(%ebp), %eax
	movl	%eax, (%esp)
	movl	$0, -104(%ebp)
	call	__ZNSsD1Ev
	jmp	L39
L38:
	movl	-148(%ebp), %edx
	movl	%edx, -128(%ebp)
L41:
	movl	-128(%ebp), %eax
	movl	%eax, (%esp)
	movl	$-1, -104(%ebp)
	call	__Unwind_SjLj_Resume
L36:
	leal	-40(%ebp), %eax
	testl	%eax, %eax
	je	L14
	leal	-40(%ebp), %edx
	movl	%edx, -152(%ebp)
	addl	$12, -152(%ebp)
L45:
	leal	-40(%ebp), %eax
	cmpl	-152(%ebp), %eax
	je	L14
	subl	$4, -152(%ebp)
	movl	-152(%ebp), %eax
	movl	%eax, (%esp)
	movl	$-1, -104(%ebp)
	call	__ZNSsD1Ev
	jmp	L45
L14:
	leal	-108(%ebp), %eax
	movl	%eax, (%esp)
	call	__Unwind_SjLj_Unregister
	addl	$172, %esp
	popl	%ebx
	popl	%esi
	popl	%edi
	popl	%ebp
	ret
	.section	.gcc_except_table,"dr"
LLSDA1426:
	.byte	0xff
	.byte	0xff
	.byte	0x1
	.uleb128 LLSDACSE1426-LLSDACSB1426
LLSDACSB1426:
	.uleb128 0x0
	.uleb128 0x0
	.uleb128 0x1
	.uleb128 0x0
	.uleb128 0x2
	.uleb128 0x0
	.uleb128 0x3
	.uleb128 0x0
LLSDACSE1426:
	.text
	.align 2
.globl __Z13HP00x98765432v
	.def	__Z13HP00x98765432v;	.scl	2;	.type	32;	.endef
__Z13HP00x98765432v:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$4, %esp
	movl	$0, -4(%ebp)
	movl	$2, -4(%ebp)
L49:
	cmpl	$1000, -4(%ebp)
	jg	L48
	movl	-4(%ebp), %edx
	movl	-4(%ebp), %eax
	movl	%eax, _PH040x12(,%edx,4)
	leal	-4(%ebp), %eax
	incl	(%eax)
	jmp	L49
L48:
	leave
	ret
	.section .rdata,"dr"
LC5:
	.ascii "%d \12\0"
	.text
	.align 2
.globl __Z13IB00x98701234v
	.def	__Z13IB00x98701234v;	.scl	2;	.type	32;	.endef
__Z13IB00x98701234v:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$24, %esp
	movl	$2, -4(%ebp)
L53:
	cmpl	$1000, -4(%ebp)
	jg	L52
	movl	-4(%ebp), %eax
	movl	_PH040x12(,%eax,4), %eax
	cmpl	-4(%ebp), %eax
	jne	L55
	movl	-4(%ebp), %eax
	movl	%eax, 4(%esp)
	movl	$LC5, (%esp)
	call	_printf
	movl	-4(%ebp), %eax
	addl	-4(%ebp), %eax
	movl	%eax, -8(%ebp)
L57:
	cmpl	$1000, -8(%ebp)
	jg	L55
	movl	-8(%ebp), %eax
	movl	$0, _PH040x12(,%eax,4)
	movl	-4(%ebp), %edx
	leal	-8(%ebp), %eax
	addl	%edx, (%eax)
	jmp	L57
L55:
	leal	-4(%ebp), %eax
	incl	(%eax)
	jmp	L53
L52:
	leave
	ret
	.def	___main;	.scl	2;	.type	32;	.endef
	.align 2
.globl _main
	.def	_main;	.scl	2;	.type	32;	.endef
_main:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	andl	$-16, %esp
	movl	$0, %eax
	addl	$15, %eax
	addl	$15, %eax
	shrl	$4, %eax
	sall	$4, %eax
	movl	%eax, -4(%ebp)
	movl	-4(%ebp), %eax
	call	__alloca
	call	___main
	call	__Z13st4rt3R_09833v
	call	__Z13HP00x98765432v
	call	__Z13IB00x98701234v
	movl	$1, %eax
	leave
	ret
	.section	.text$_ZSt3minIjERKT_S2_S2_,"x"
	.linkonce discard
	.align 2
.globl __ZSt3minIjERKT_S2_S2_
	.def	__ZSt3minIjERKT_S2_S2_;	.scl	2;	.type	32;	.endef
__ZSt3minIjERKT_S2_S2_:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$4, %esp
	movl	12(%ebp), %eax
	movl	8(%ebp), %edx
	movl	(%eax), %eax
	cmpl	(%edx), %eax
	jae	L62
	movl	12(%ebp), %eax
	movl	%eax, -4(%ebp)
	jmp	L61
L62:
	movl	8(%ebp), %eax
	movl	%eax, -4(%ebp)
L61:
	movl	-4(%ebp), %eax
	leave
	ret
	.text
	.align 2
	.def	__Z41__static_initialization_and_destruction_0ii;	.scl	3;	.type	32;	.endef
__Z41__static_initialization_and_destruction_0ii:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	cmpl	$65535, 12(%ebp)
	jne	L64
	cmpl	$1, 8(%ebp)
	jne	L64
	movl	$__ZSt8__ioinit, (%esp)
	call	__ZNSt8ios_base4InitC1Ev
L64:
	cmpl	$65535, 12(%ebp)
	jne	L63
	cmpl	$0, 8(%ebp)
	jne	L63
	movl	$__ZSt8__ioinit, (%esp)
	call	__ZNSt8ios_base4InitD1Ev
L63:
	leave
	ret
	.align 2
	.def	__GLOBAL__I_PH040x12;	.scl	3;	.type	32;	.endef
__GLOBAL__I_PH040x12:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	movl	$65535, 4(%esp)
	movl	$1, (%esp)
	call	__Z41__static_initialization_and_destruction_0ii
	leave
	ret
	.section	.ctors,"w"
	.align 4
	.long	__GLOBAL__I_PH040x12
	.text
	.align 2
	.def	__GLOBAL__D_PH040x12;	.scl	3;	.type	32;	.endef
__GLOBAL__D_PH040x12:
	pushl	%ebp
	movl	%esp, %ebp
	subl	$8, %esp
	movl	$65535, 4(%esp)
	movl	$0, (%esp)
	call	__Z41__static_initialization_and_destruction_0ii
	leave
	ret
	.section	.dtors,"w"
	.align 4
	.long	__GLOBAL__D_PH040x12
	.def	__ZNSt8ios_base4InitD1Ev;	.scl	2;	.type	32;	.endef
	.def	_printf;	.scl	2;	.type	32;	.endef
	.def	__ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc;	.scl	2;	.type	32;	.endef
	.def	__ZStlsIcSt11char_traitsIcESaIcEERSt13basic_ostreamIT_T0_ES7_RKSbIS4_S5_T1_E;	.scl	2;	.type	32;	.endef
	.def	__ZNSsD1Ev;	.scl	2;	.type	32;	.endef
	.def	__ZNSsC1EPKcRKSaIcE;	.scl	2;	.type	32;	.endef
	.def	__ZNSaIcED1Ev;	.scl	2;	.type	32;	.endef
	.def	__ZNSaIcEC1Ev;	.scl	2;	.type	32;	.endef
	.def	__ZNSsixEj;	.scl	2;	.type	32;	.endef
	.def	__ZNKSs6lengthEv;	.scl	2;	.type	32;	.endef
	.def	__ZNSt8ios_base4InitC1Ev;	.scl	2;	.type	32;	.endef
	.def	__ZNKSsixEj;	.scl	2;	.type	32;	.endef
	.def	__ZNKSs4sizeEv;	.scl	2;	.type	32;	.endef
</pre></p> 

Ambos códigos realizam a mesma tarefa: exibir a mensagem &#8220;O CRIVO DE ERASTOTENES. Codigo com informacao simbolica explicita. www.sawp.com.br” e em seguida-se calcula os números primos existentes de 2 à 1000. 

Contudo, claramente observamos no segundo código que as strings não visíveis. Isso faz com que seja quase impossível para o cracker saber sobre o que se trata aquela informação, pois ele precisaria do código responsável pela decriptação da informação simbólica. No caso, a função responsável por tornar o texto visível para o usuário e invisível para o cracker é a “rot13_d3c0d3”.

Para quem tiver curiosidade, rot13_d3c0d3 substitui um caractere por outro que têm seu asccii-13. Veja:

<pre lang="cpp">void rot13ASC_decode(string & input){
	const int key=13;
	int asciicode;

	for(int i=0;i &lt; input .length();i++) {
		asciicode = static_cast&lt; int >(input[i])- key;
		input[i] =  static_cast&lt; char >(asciicode);
	}
}
</pre></p> 

Normalmente os crackers se deparam com codificações reversíveis, como BASE64, rot13,rot64, algum algoritmo derivado de Cifras de César-Vigenere ou algum algoritmo de transposição. 

Notamos então que colocar as constantes em texto explícito é uma forma extremamente vulnerável por deixar pontos de referências para os crackers se localizarem na nossa aplicação. 

Observamos também que o código assembly com as informações simbólicas removidas é muito mais extenso e possui muito mais instruções que o código original. Isso reforça uma das desvantagens descritas na PARTE 1 sobre anti-cracking: sempre há perda de desempenho ao implementar técnicas anticracking.

Este é um ponto importante e que deve sempre estar na cabeça do desenvolvedor. No nosso pequeno exemplo já tivemos um considerável aumento de instruções. E este crescimento é propagado quão maior for o código da aplicação, representando significativa perda de eficiência. 

Deve-se ficar claro que o código aqui apresentado é apenas para exemplificar. Alguém que necessite proteger sua aplicação, certamente está trabalhando em um projeto grande, com vários arquivos-fontes, muitas classes e funções. Então, obviamente, não há como eliminar as informações simbólicas “na mão”. 

O que as empresas que empregam técnicas anti-cracking fazem é construir parsers especiais e scripts especiais de compilação. Desta forma, o código ao invés de ser enviado direto para o compilador, são transformados por estes scripts em um código de sem informações simbólicas destes e só então são compilados.
