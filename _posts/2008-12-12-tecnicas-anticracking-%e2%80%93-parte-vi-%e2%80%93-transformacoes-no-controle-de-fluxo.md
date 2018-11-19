---
id: 219
title: Técnicas AntiCracking – Parte VI – Transformações no Controle de Fluxo
date: 2008-12-12T11:51:21+00:00
author: SAWP
excerpt: |
  Control Flow Transformation (CFT) consiste em alterar a estrutura de um programa para tornar seu código difícil para a leitura humana sem prejudicar a sua funcionalidade original. Como veremos aqui, está intimamente relaciona com a ofuscação de código.
  
  As técnicas que se aplicam à categoria das CFTs são: Inlining, Intervalar Código, Estruturas Opacas, GoTo Hell’s Code e Exceção Proposital.
layout: post
guid: http://www.sawp.com.br/blog/?p=219
permalink: /p=219
wp-syntax-cache-content:
  - |
    a:13:{i:1;s:899:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">inline</span> <span style="color: #0000ff;">bool</span> exemplo<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;inline here&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">inline bool exemplo(){
    puts(&quot;inline here&quot;);
    
    return true;
    }</p></div>
    ;i:2;s:1073:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">function<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    segmentoDeFuncao1<span style="color: #008080;">;</span>  <span style="color: #666666;">// sequencia de logica 1</span>
    segmentoDeFuncao2<span style="color: #008080;">;</span>  <span style="color: #666666;">// sequencia de logica 2</span>
    continuaAFuncao_function<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    segmentoDeFuncao4<span style="color: #008080;">;</span> <span style="color: #666666;">// sequencia de logica 3</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">function(){
    segmentoDeFuncao1;  // sequencia de logica 1
    segmentoDeFuncao2;  // sequencia de logica 2
    continuaAFuncao_function();
    segmentoDeFuncao4; // sequencia de logica 3
    }</p></div>
    ;i:3;s:3066:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">inline</span> function1<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    function1_segmentoDeFuncao1<span style="color: #008080;">;</span>	<span style="color: #666666;">// comeco da sequencia 1</span>
    function1_ segmentoDeFuncao2<span style="color: #008080;">;</span>    <span style="color: #666666;">// comeco da sequencia 2</span>
    function1_ segmentoDeFuncao4<span style="color: #008080;">;</span>    <span style="color: #666666;">// segmento da sequencia 3</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #0000ff;">inline</span> function2<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    function2_segmentoDeFuncao4<span style="color: #008080;">;</span>	<span style="color: #666666;">// continuacao da sequencia 3</span>
    function2_ segmentoDeFuncao2<span style="color: #008080;">;</span>    <span style="color: #666666;">// continuacao da sequencia 2</span>
    function2_ segmentoDeFuncao1<span style="color: #008080;">;</span>    <span style="color: #666666;">// segmento da sequencia 1</span>
    continuaAFuncao_function<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>     <span style="color: #666666;">// não deveria nem continuar, se n existe function() ;)</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">inline</span> function3<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    function3_segmentoDeFuncao4<span style="color: #008080;">;</span>	<span style="color: #666666;">// continuacao da sequencia 3</span>
    function3_ segmentoDeFuncao2<span style="color: #008080;">;</span>    <span style="color: #666666;">// continuacao da sequencia 2</span>
    function3_ segmentoDeFuncao1<span style="color: #008080;">;</span>    <span style="color: #666666;">// continuacao da sequencia 1	</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">inline function1(){
    function1_segmentoDeFuncao1;	// comeco da sequencia 1
    function1_ segmentoDeFuncao2;    // comeco da sequencia 2
    function1_ segmentoDeFuncao4;    // segmento da sequencia 3
    }
    inline function2(){
    function2_segmentoDeFuncao4;	// continuacao da sequencia 3
    function2_ segmentoDeFuncao2;    // continuacao da sequencia 2
    function2_ segmentoDeFuncao1;    // segmento da sequencia 1
    continuaAFuncao_function();     // não deveria nem continuar, se n existe function() ;)
    }
    
    inline function3(){
    function3_segmentoDeFuncao4;	// continuacao da sequencia 3
    function3_ segmentoDeFuncao2;    // continuacao da sequencia 2
    function3_ segmentoDeFuncao1;    // continuacao da sequencia 1
    }</p></div>
    ;i:4;s:1854:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	...
    <span style="color: #007788;">segmentoDeCodigoOriginal1</span><span style="color: #008080;">;</span>
    segmentoDeCodigoOriginal2<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">// estrutura opaca</span>
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span><span style="color: #000040;">!</span><span style="color: #008000;">&#40;</span>x <span style="color: #000080;">==</span> x<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    segmentoDeCodigoInutil0<span style="color: #008080;">;</span>
    segmentoDeCodigoQueNaoSeraExecutado<span style="color: #008080;">;</span>
    ...
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    ...
    <span style="color: #007788;">segmentoDeCodigoOriginal_n</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">while</span><span style="color: #008000;">&#40;</span>x <span style="color: #000080;">==</span> x<span style="color: #000040;">+</span><span style="color: #0000dd;">1</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    codigoDosBobos_Here<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    ...</pre></td></tr></table><p class="theCode" style="display:none;">	...
    segmentoDeCodigoOriginal1;
    segmentoDeCodigoOriginal2;
    
    // estrutura opaca
    if(!(x == x)){
    segmentoDeCodigoInutil0;
    segmentoDeCodigoQueNaoSeraExecutado;
    ...
    }
    
    ...
    segmentoDeCodigoOriginal_n;
    
    while(x == x+1){
    codigoDosBobos_Here();
    }
    
    ...</p></div>
    ;i:5;s:2236:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	codigoRelevanteParaFuncionamentoDoPrograma<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">// tratamento de excecao</span>
    <span style="color: #0000ff;">try</span><span style="color: #008000;">&#123;</span>
    codigoRelevante1<span style="color: #008080;">;</span>		<span style="color: #666666;">// antes da excecao o codigo pode ou n ser relevante para o programa</span>
    codigoRelevante2<span style="color: #008080;">;</span>
    ...
    <span style="color: #007788;">x</span> <span style="color: #000080;">=</span> x<span style="color: #000040;">/</span><span style="color: #008000;">&#40;</span>x<span style="color: #000040;">-</span>x<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>			<span style="color: #666666;">// a partir deste ponto, desvia o fluxo de execucao </span>
    codigoIrrelevante_NExecutado<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span>DivideByZeroException <span style="color: #000040;">&amp;</span>e<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    e.<span style="color: #007788;">printstacktrace</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>			<span style="color: #666666;">// qualquer coisa para fingir que e uma excecao valida </span>
    continuacaoDoProgramaAqui<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	codigoRelevanteParaFuncionamentoDoPrograma;
    
    // tratamento de excecao
    try{
    codigoRelevante1;		// antes da excecao o codigo pode ou n ser relevante para o programa
    codigoRelevante2;
    ...
    x = x/(x-x);			// a partir deste ponto, desvia o fluxo de execucao
    codigoIrrelevante_NExecutado;
    } catch(DivideByZeroException &amp;e){
    e.printstacktrace();			// qualquer coisa para fingir que e uma excecao valida
    continuacaoDoProgramaAqui;
    }</p></div>
    ;i:6;s:2510:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">void</span> throwExcptn<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    &nbsp;
    <span style="color: #666666;">// lanca a excecao</span>
    <span style="color: #0000ff;">try</span><span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">//codigo que pode gerar alguma excecao</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span>ExceptionA <span style="color: #000040;">&amp;</span>ea<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// se a excecao gerada foi do tipo A</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span>ExceptionB <span style="color: #000040;">&amp;</span>eb<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// se a excecao gerada foi do tipo B</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span>ExceptionC <span style="color: #000040;">&amp;</span>ec<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// se a excecao gerada foi do tipo C</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span>runtime_error <span style="color: #000040;">&amp;</span>error<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// se a excecao gerada foi do tipo runtime_error</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">void throwExcptn(){
    
    // lanca a excecao
    try{
    //codigo que pode gerar alguma excecao
    } catch(ExceptionA &amp;ea) {
    // se a excecao gerada foi do tipo A
    } catch(ExceptionB &amp;eb) {
    // se a excecao gerada foi do tipo B
    } catch(ExceptionC &amp;ec) {
    // se a excecao gerada foi do tipo C
    } catch(runtime_error &amp;error) {
    // se a excecao gerada foi do tipo runtime_error
    }
    }</p></div>
    ;i:7;s:3030:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	...
    &nbsp;
    <span style="color: #0000ff;">try</span> <span style="color: #008000;">&#123;</span>
    codigoRelevante1<span style="color: #008080;">;</span>
    codigoRelevante2<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">double</span> <span style="color: #000040;">*</span>ptr <span style="color: #000080;">=</span> <span style="color: #0000dd;">new</span> <span style="color: #0000ff;">double</span><span style="color: #008000;">&#91;</span> <span style="color: #0000dd;">5</span> <span style="color: #000040;">*</span> getFreeMem<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span> <span style="color: #666666;">// erro, tenta alocar 5 vezes a memoria livre</span>
    &nbsp;
    codigoirrelevante1<span style="color: #008080;">;</span>
    codigoirrelevante2<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span>bad_alloc <span style="color: #000040;">&amp;</span>memoryAllocarionException<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span> <span style="color: #666666;">// trata bad_alloc</span>
    codigoRelevante3<span style="color: #008080;">;</span>
    codigoRelevante4<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">double</span> x <span style="color: #000080;">=</span> x<span style="color: #000040;">/</span><span style="color: #008000;">&#40;</span>ln<span style="color: #008000;">&#40;</span>x<span style="color: #000040;">/</span>x<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>		<span style="color: #666666;">// erro, pois trata divisao por zero</span>
    &nbsp;
    codigoirrelevante3<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span>runtime_error <span style="color: #000040;">&amp;</span>runtimeException<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    codigoRelevante5<span style="color: #008080;">;</span>
    ...
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    ...</pre></td></tr></table><p class="theCode" style="display:none;">	...
    
    try {
    codigoRelevante1;
    codigoRelevante2;
    
    double *ptr = new double[ 5 * getFreeMem() ]; // erro, tenta alocar 5 vezes a memoria livre
    
    codigoirrelevante1;
    codigoirrelevante2;
    } catch(bad_alloc &amp;memoryAllocarionException) { // trata bad_alloc
    codigoRelevante3;
    codigoRelevante4;
    
    double x = x/(ln(x/x));		// erro, pois trata divisao por zero
    
    codigoirrelevante3;
    } catch(runtime_error &amp;runtimeException) {
    codigoRelevante5;
    ...
    }
    
    ...</p></div>
    ;i:8;s:3995:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	...
    &nbsp;
    <span style="color: #0000ff;">try</span><span style="color: #008000;">&#123;</span>
    codigoRelevante1<span style="color: #008080;">;</span>
    codigoRelevante2<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">throw</span> bad_cast<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>	<span style="color: #666666;">// forca a geracao de uma excecao para desviar o fluxo</span>
    &nbsp;
    codigoirrelevante1<span style="color: #008080;">;</span>
    codigoirrelevante2<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span> bad_cast <span style="color: #000040;">&amp;</span> <span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    continuaExecucao<span style="color: #008080;">;</span>
    &nbsp;
    ...
    &nbsp;
    <span style="color: #0000ff;">throw</span> length_error<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span> 	<span style="color: #666666;">// gera excecao</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span> length_error <span style="color: #000040;">&amp;</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    continuaExecucaoDeNovo<span style="color: #008080;">;</span>
    &nbsp;
    ...
    &nbsp;
    <span style="color: #0000ff;">throw</span> runtime_error<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>	<span style="color: #666666;">// gera excecao </span>
    ...
    &nbsp;
    <span style="color: #007788;">codigoIrrelevante_Linguica</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span> runtime_error <span style="color: #000040;">&amp;</span> <span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">throw</span> exception<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span><span style="color: #008000;">&#40;</span> exception <span style="color: #000040;">&amp;</span> <span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    codigoRelevante<span style="color: #008080;">;</span> 		<span style="color: #666666;">// codigo, codigo e mais codigo...</span>
    <span style="color: #0000ff;">throw</span> bad_cast<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>		<span style="color: #666666;">// retorna a um bloco de excessao, se precisar</span>
    trataExcecao<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    ...</pre></td></tr></table><p class="theCode" style="display:none;">	...
    
    try{
    codigoRelevante1;
    codigoRelevante2;
    
    throw bad_cast();	// forca a geracao de uma excecao para desviar o fluxo
    
    codigoirrelevante1;
    codigoirrelevante2;
    } catch( bad_cast &amp; ){
    continuaExecucao;
    
    ...
    
    throw length_error(); 	// gera excecao
    } catch( length_error &amp; ) {
    continuaExecucaoDeNovo;
    
    ...
    
    throw runtime_error();	// gera excecao
    ...
    
    codigoIrrelevante_Linguica;
    } catch( runtime_error &amp; ){
    throw exception();
    } catch( exception &amp; ){
    codigoRelevante; 		// codigo, codigo e mais codigo...
    throw bad_cast();		// retorna a um bloco de excessao, se precisar
    trataExcecao;
    }
    ...</p></div>
    ;i:9;s:2946:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">void</span> function<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    codigoRelevanteParaFuncionamentoDoPrograma<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">// estrutura opaca</span>
    <span style="color: #0000ff;">while</span><span style="color: #008000;">&#40;</span>x<span style="color: #000040;">-</span><span style="color: #0000dd;">1</span> <span style="color: #000080;">==</span> x<span style="color: #000040;">+</span><span style="color: #0000dd;">2</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    codigoIrrelevante1<span style="color: #008080;">;</span>
    codigoirrelevante2<span style="color: #008080;">;</span>
    &nbsp;
    codigoEscondido<span style="color: #008080;">:</span>	<span style="color: #666666;">// isso é um rotulo</span>
    codigoRelevanteEscondidoNaEstruturaOpaca<span style="color: #008080;">;</span> <span style="color: #666666;">// nao acessível</span>
    outroCódigoRelevanteNaEstruturaOpaca<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    codigoRelevanteParaFuncionamentoDoPrograma2<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">bool</span> precisaDoCodigoEscondido<span style="color: #000080;">=</span><span style="color: #0000ff;">false</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">while</span><span style="color: #008000;">&#40;</span><span style="color: #000040;">!</span>precisaDoCodigoEscondido<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    ... <span style="color: #666666;">// aguarda precisar do codigo inserido na Estrutura Opaca</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">goto</span> codigoEscondido<span style="color: #008080;">;</span> <span style="color: #666666;">// vai para o codigo que nunca seria acessível gracas a estrutura opaca</span>
    &nbsp;
    ...
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">void function(){
    codigoRelevanteParaFuncionamentoDoPrograma;
    
    // estrutura opaca
    while(x-1 == x+2){
    codigoIrrelevante1;
    codigoirrelevante2;
    
    codigoEscondido:	// isso é um rotulo
    codigoRelevanteEscondidoNaEstruturaOpaca; // nao acessível
    outroCódigoRelevanteNaEstruturaOpaca;
    }
    
    codigoRelevanteParaFuncionamentoDoPrograma2;
    
    bool precisaDoCodigoEscondido=false;
    
    while(!precisaDoCodigoEscondido){
    ... // aguarda precisar do codigo inserido na Estrutura Opaca
    }
    
    goto codigoEscondido; // vai para o codigo que nunca seria acessível gracas a estrutura opaca
    
    ...
    }</p></div>
    ;i:10;s:808:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	<span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">1</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;</span> <span style="color: #0000dd;">1000</span> <span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// your code here</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	for(i=1; i &lt; 1000 ; i++){
    // your code here
    }</p></div>
    ;i:11;s:892:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	<span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">5</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;</span> <span style="color: #0000dd;">5000</span><span style="color: #008080;">;</span> i<span style="color: #000040;">+</span><span style="color: #000080;">=</span><span style="color: #0000dd;">5</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// the same code here</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	for(i=5; i &lt; 5000; i+=5) {
    // the same code here
    }</p></div>
    ;i:12;s:4314:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #339900;">#define LINES 10</span>
    <span style="color: #339900;">#define COLMNS 5</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> original<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">int</span> originalA<span style="color: #008000;">&#91;</span>LINES<span style="color: #008000;">&#93;</span><span style="color: #008000;">&#91;</span>COLMNS<span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">// preenche a tabela</span>
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;</span> LINES <span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> j<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span> j <span style="color: #000080;">&lt;</span> COLMNS<span style="color: #008080;">;</span> j<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    originalA<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #008000;">&#91;</span>j<span style="color: #008000;">&#93;</span> <span style="color: #000080;">=</span> j<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #666666;">//exibe</span>
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;</span> LINES <span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> j<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span> j <span style="color: #000080;">&lt;</span> COLMNS<span style="color: #008080;">;</span> j<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;%i<span style="color: #000099; font-weight: bold;">\t</span>&quot;</span>,originalA<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #008000;">&#91;</span>j<span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">#define LINES 10
    #define COLMNS 5
    
    void original(){
    int originalA[LINES][COLMNS];
    
    // preenche a tabela
    for(int i=0; i &lt; LINES ; i++){
    for(int j=0; j &lt; COLMNS; j++){
    originalA[i][j] = j;
    }
    }
    
    //exibe
    for(int i=0; i &lt; LINES ; i++){
    for(int j=0; j &lt; COLMNS; j++){
    printf(&quot;%i\t&quot;,originalA[i][j]);
    }
    printf(&quot;\n&quot;);
    }
    }</p></div>
    ;i:13;s:4147:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #339900;">#define LINES 10</span>
    <span style="color: #339900;">#define COLMNS 5</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> modified<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">int</span> originalA<span style="color: #008000;">&#91;</span>LINES<span style="color: #000040;">*</span>COLMNS<span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">int</span> i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span>, j<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">//gera</span>
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;</span> LINES<span style="color: #000040;">*</span>COLMNS <span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span>i <span style="color: #000040;">%</span> COLMNS <span style="color: #000080;">==</span> <span style="color: #0000dd;">0</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    j<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    originalA<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span> <span style="color: #000080;">=</span> j<span style="color: #000040;">++</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #666666;">//exibe</span>
    <span style="color: #0000ff;">for</span><span style="color: #008000;">&#40;</span>i<span style="color: #000080;">=</span><span style="color: #0000dd;">0</span><span style="color: #008080;">;</span> i <span style="color: #000080;">&lt;</span> LINES<span style="color: #000040;">*</span>COLMNS <span style="color: #008080;">;</span> i<span style="color: #000040;">++</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span>i <span style="color: #000040;">%</span> COLMNS <span style="color: #000080;">==</span> <span style="color: #0000dd;">0</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;%i<span style="color: #000099; font-weight: bold;">\t</span>&quot;</span>,originalA<span style="color: #008000;">&#91;</span>i<span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">#define LINES 10
    #define COLMNS 5
    
    void modified(){
    int originalA[LINES*COLMNS];
    int i=0, j=0;
    
    //gera
    for(i=0; i &lt; LINES*COLMNS ; i++){
    if(i % COLMNS == 0){
    j=0;
    }
    originalA[i] = j++;
    }
    
    //exibe
    for(i=0; i &lt; LINES*COLMNS ; i++){
    if(i % COLMNS == 0){
    printf(&quot;\n&quot;);
    }
    printf(&quot;%i\t&quot;,originalA[i]);
    }
    }</p></div>
    ";}
categories:
  - Programming Internals
tags:
  - Programming Internals
---
Control Flow Transformation (CFT) consiste em alterar a estrutura de um programa para tornar seu código difícil para a leitura humana sem prejudicar a sua funcionalidade original. Como veremos aqui, está intimamente relaciona com a ofuscação de código.

As técnicas que se aplicam à categoria das CFTs são: Inlining, Intervalar Código, Estruturas Opacas, GoTo Hell&#8217;s Code e Exceção Proposital. 

&nbsp;

## Inlining 

O qualificador inline é uma instrução inserida no código – antes do tipo de retorno de uma função – que solicita ao compilador a replicação de cópias da função ao invés de referenciá-la. 

É utilizado principalmente para evitar chamadas excessivas de função, melhorando a performance em tempo de execução. 

Para pagar o preço dessa vantagem, as múltiplas cópias deste códigos levam à um crescimento no tamanho do programa com instruções repetidas. 

No contexto das técnicas anticracking, funções inline são poderosas por eliminarem as abstrações modulares, utilizadas em linguagens orientadas à objetos, estruturadas, funcionais etc. 

Um assembly gerado com muitas instruções inline prejudicam os crackers porque eles lerão um código sem uma centralização, com difícil identificação dos módulos lógicos e de baixa legibilidade. 

<pre lang="cpp">inline bool exemplo(){
	puts("inline here");

	return true;
}
</pre>

Por exemplo, imagine que desejamos proteger nosso programa com uma função que, de tempos em tempos, procura no registro do sistema o serial válido. Se nenhum serial for encontrado, trava o programa. 

Podemos associar as chamadas desta função com algumas ações produzidas pelo usuário. Quando ele abrir o programa, pedir para atualizá-lo ou quando mudar alguma opção, chamaremos a função de checagem dos registros. 

Um cracker experiente notaria que tais ações são os gatilhos para a chamada da verificação nos registros. Assim, reverteria nosso código, encontraria a função e alteraria nossa identificação de validade. 

Contudo, se transformássemos esta função com o qualificador inline, mesclaríamos a verificação dos registros com os códigos das ações, descentralizando a informação e confundindo o cracker. 

&nbsp;

## Intervalar Código

Uma técnica pertencente à categoria das CFTs que consiste em dividir um bloco em funções, intervalando suas implementações em funções diferentes. É muito interessante de ser aplicada quando associada à um paradigma orientado à objetos. 

Por exemplo, uma função ou método que altera os dados de uma variável pode ser dividida em várias outras, dificultando a leitura. 

<pre lang="cpp">function(){
	segmentoDeFuncao1;  // sequencia de logica 1
	segmentoDeFuncao2;  // sequencia de logica 2
	continuaAFuncao_function();
	segmentoDeFuncao4; // sequencia de logica 3
}
</pre>

Pode ser reescrito como:

<pre lang="cpp">inline function1(){
	function1_segmentoDeFuncao1;	// comeco da sequencia 1
	function1_ segmentoDeFuncao2;    // comeco da sequencia 2
	function1_ segmentoDeFuncao4;    // segmento da sequencia 3
}
inline function2(){
	function2_segmentoDeFuncao4;	// continuacao da sequencia 3
	function2_ segmentoDeFuncao2;    // continuacao da sequencia 2
	function2_ segmentoDeFuncao1;    // segmento da sequencia 1
	continuaAFuncao_function();     // não deveria nem continuar, se n existe function() ;)
}

inline function3(){
	function3_segmentoDeFuncao4;	// continuacao da sequencia 3
	function3_ segmentoDeFuncao2;    // continuacao da sequencia 2
	function3_ segmentoDeFuncao1;    // continuacao da sequencia 1	
}
</pre></p> 

Veja que este processo intervalado é associado com a capacidade de gerar repetição de código por meio de instruções inline. O uso do comando inline também é importante para evitar o overhead de chamadas de funções em alguns casos. 

&nbsp;

## Estrutura Opaca

Também conhecida como “Predicados opacos”, é uma técnica que consiste em criar uma condição lógica cujo resultado é constante através de falsos predicados. 

Sejam as condições if(x != x) e while(1==2) . Veja que estas condições nunca serão satisfeitas e podem ser utilizadas para inserir trechos de código dentro de um programa que não terão nenhuma funcionalidade. 

Isso pode servir como um fator de distração para confundir um cracker ou uma ferramenta de decompilação, como o IDA PRO (que utiliza desvios condicionais para gerar seus diagramas), que irá interpretar o código dentro destes blocos como sendo um trecho válido do programa. 

O objetivo destas estruturas “opacas” é criar blocos que irão dificultar a distinção o código original – responsável pelo funcionamento do programa – do código-armadilha. Um fato interessante desta técnica é que ela consegue enganar bem decompiladores e até alguns deobfuscadores, além de também confundir até os mais experientes crackers.

<pre lang="cpp">...
	segmentoDeCodigoOriginal1;
	segmentoDeCodigoOriginal2;
	
	// estrutura opaca
	if(!(x == x)){
		segmentoDeCodigoInutil0;
		segmentoDeCodigoQueNaoSeraExecutado;
		...
	}

	...
	segmentoDeCodigoOriginal_n;

	while(x == x+1){
		codigoDosBobos_Here();
	}

	...
</pre></p> 

&nbsp;

## Exceção Proposital

Proposital Exception (PE) é uma forma de CFT que consiste em gerar exceções para desviar o fluxo de execução. É muito semelhante à abordagem da Estrutura Opaca, mas ao invés de utilizar condicionais, utiliza os recursos de tratamento de exceção da linguagem. 

Uma exceção é um problema ocorrido em tempo de execução, não previsto pelo compilador. “Exceção” sugere que o problema ocorre raramente, ou seja, não é a regra. Linguagens que permitem o tratamento de exceções possibilita aos programadores escrever programas robustos e tolerantes à falhas, capazes de tratar erros de forma elegante. 

A princípio, a previsão de erros poderia ser feita pelo programador. Ele deveria colocar estruturas condicionais de controle para prever o erro. Embora esse tipo de abordagem funcionasse, mesclar a lógica e tratamento de erros poderia trazer uma série de desvantagens. 

A primeira delas seria a dificuldade de manutenção. A leitura, modificação, depuração e divisão de tarefas ficariam certamente prejudicadas. 

A segunda desvantagem é que a mistura de lógica de programa e de tratamento de erro pode degradar o desempenho do programa, pois o força a realizar testes freqüentes para determinar se a tarefa foi executada corretamente. 

Assim, como espera-se que um erro seja um caso excepcional, uma excessiva seqüência de testes criaria uma perda de performance desnecessária. Por isso o tratamento de exceções permite que o programador remova as instruções de condição do programa e substitui por um único código de tratamento de erro, aprimorando a sua clareza, desempenho, modificabilidade e leitura. 

O uso de exceções produzidas propositalmente é interessante pois gera um código de baixo nível extremamente difícil de se entender e com eficiência superior à estruturas opacas simples. 

No código abaixo veremos como gerar uma exceção propositalmente dividindo um valor por zero e inserindo um código que queremos ofuscar no tratamento de erros. 

<pre lang="cpp">codigoRelevanteParaFuncionamentoDoPrograma;

	// tratamento de excecao
	try{ 
		codigoRelevante1;		// antes da excecao o codigo pode ou n ser relevante para o programa
		codigoRelevante2;
		...
		x = x/(x-x);			// a partir deste ponto, desvia o fluxo de execucao 
		codigoIrrelevante_NExecutado;
	} catch(DivideByZeroException &e){
		e.printstacktrace();			// qualquer coisa para fingir que e uma excecao valida 
		continuacaoDoProgramaAqui;
	}
</pre>

O tratamento de exceções é projetado para erros síncronos, tais como subscritos de arrays fora do intervalo (ArrayOutOfBounds), overflow e underflow aritmético (quando um número é maior ou menor do que a arquitetura do processador suporta), divisão por zero, alocação de memória inválida, tratamento de arquivos, erros de casting, de tipos etc. 

Quando tratamos erros podemos também cascatear em diferentes sub-blocos o tratamento de exceção. Podemos criar diferentes handlers de exceção para tratar diferentes tipos de exceções geradas. Ou seja, criamos vários blocos catch para processar exatamente o tipo de exceção que ocorreu. 

Normalmente um handler catch informa ao usuário sobre o erro, registra em um log o erro, termina o programa ou tenta outra estratégia de correção do erro. 

Veja no código abaixo um bloco que trata de diferentes erros.

<pre lang="cpp">void throwExcptn(){
	
	// lanca a excecao
	try{
		//codigo que pode gerar alguma excecao
	} catch(ExceptionA &ea) {
		// se a excecao gerada foi do tipo A
	} catch(ExceptionB &eb) {
		// se a excecao gerada foi do tipo B
	} catch(ExceptionC &ec) {
		// se a excecao gerada foi do tipo C
	} catch(runtime_error &error) {
		// se a excecao gerada foi do tipo runtime_error
	}
}
</pre></p> 

Aproveitando desta capacidade de cascateamento de handlers catchs, podemos transformar o controle do fluxo do nosso programa para confundir os crackers. Um esquema de como isso pode ser feito segue abaixo:

<pre lang="cpp">...

	try {
		codigoRelevante1;
		codigoRelevante2;

		double *ptr = new double[ 5 * getFreeMem() ]; // erro, tenta alocar 5 vezes a memoria livre

		codigoirrelevante1;
		codigoirrelevante2;
	} catch(bad_alloc &memoryAllocarionException) { // trata bad_alloc
		codigoRelevante3;
		codigoRelevante4;

		double x = x/(ln(x/x));		// erro, pois trata divisao por zero

		codigoirrelevante3;
	} catch(runtime_error &runtimeException) { 
		codigoRelevante5;
		...
	}

	...
</pre></p> 

Uma outra forma de aproveitar os vários handlers catch é relançar uma exceção. Normalmente relançamento de exceções implicam em uma perda de performance, mas são frequentemente utilizadas por blocos que processam apenas parcialmente um erro. 

Independendo de um handler poder ou não processar uma exceção, poderá relançá-la para o próximo handler. A instrução que permite isso é a throw . 

Uma estratégia que é feita quando deseja-se modificar o fluxo de execução é gerar diferentes exceções que são nativas da linguagem. No exemplo abaixo, forçamos o programa a tratar diferentes exceções e misturamos códigos válidos e de despistamento. 

<pre lang="cpp">...

	try{
		codigoRelevante1;
		codigoRelevante2;
		
		throw bad_cast();	// forca a geracao de uma excecao para desviar o fluxo
		
		codigoirrelevante1;
		codigoirrelevante2;
	} catch( bad_cast & ){
		continuaExecucao;

		...

		throw length_error(); 	// gera excecao
	} catch( length_error & ) {
		continuaExecucaoDeNovo;

		...

		throw runtime_error();	// gera excecao 
		...

		codigoIrrelevante_Linguica;
	} catch( runtime_error & ){
		throw exception();
	} catch( exception & ){
		codigoRelevante; 		// codigo, codigo e mais codigo...
		throw bad_cast();		// retorna a um bloco de excessao, se precisar
		trataExcecao;
	}
	...
</pre></p> 

&nbsp;

## Goto Hell&#8217;s Code

É uma variante da “Estrutura Opaca”. Porém, utiliza uma instrução de desvio (normalmente inserida em uma linguagem de alto nível pelo comando obsoleto goto) para forçar o acesso à segmentos de códigos nunca seriam acessíveis pela estrutura opaca. 

A instrução goto permite ao programador especificar uma transferência de controle para vários possíveis destinos do programa – criando o chamado “código macarrônico”. 

O goto, então, é o responsável pela quebra da programação estruturada, pois permite criar desvios incondicionais. Desta forma, o resultado do comando goto é uma mudança no fluxo de controle do programa sem obedecer necessariamente à orientação estruturada da linguagem. 

Para utilizar a instrução goto basta inserir o rótulo do ponto de desvio após esta instrução. Um rótulo é um identificador seguido por dois pontos e deve aparecer na mesma função em que a instrução goto que ele referencia. 

Vale lembrar que a utilização desta instrução é muito pouco recomendada, pois o uso indiscriminado de instruções de desvio incondicional gera muitas dificuldades no desenvolvimento de um software. Com a invenção da programação estruturada os programadores praticamente aboliram o goto. Hoje, alguns programadores ainda utilizam esta instrução como saída rápida para uma estrutura muito aninhada, que perde muita eficiência nos testes das condicionais. 

Para exemplificar o uso da instrução goto e como ela é utilizada para dificultar a reversão, segue o código abaixo:

<pre lang="cpp">void function(){
	codigoRelevanteParaFuncionamentoDoPrograma;

	// estrutura opaca
	while(x-1 == x+2){
		codigoIrrelevante1;
		codigoirrelevante2;
		
		codigoEscondido:	// isso é um rotulo
			codigoRelevanteEscondidoNaEstruturaOpaca; // nao acessível
			outroCódigoRelevanteNaEstruturaOpaca;
	}

	codigoRelevanteParaFuncionamentoDoPrograma2;

	bool precisaDoCodigoEscondido=false;

	while(!precisaDoCodigoEscondido){
		... // aguarda precisar do codigo inserido na Estrutura Opaca
	}

	goto codigoEscondido; // vai para o codigo que nunca seria acessível gracas a estrutura opaca

	...
}
</pre></p> 

Como podemos ver no código acima, Goto Hells Code (GHC) é utilizado em conjunto com a Estrutura Opaca, sendo na verdade uma variação desta. 

A aplicação desta técnica é muito útil principalmente contra o IDA PRO pois ela força o decompilador desencadear uma série de diagramas de fluxos errados, levando o cracker à entender o funcionamento das estruturas do programa de uma forma completamente equivocada. 

Como o goto não depende de condição nenhuma para desviar o programa, pode também ser associada com outras técnicas de Transformação no Controle do Fluxo, como a Exceção Proposital. 

O interessante da abordagem de GHC é que ela é extremamente eficiente para confundir os crackers e não exige perda de performance do programa, já que a instrução goto é usada em aplicativos orientados ao desempenho. 

A maior desvantagem deste método é que o uso abusivo de gotos pode levar à formação de programas muito difíceis de depurar, modificar e manter.

&nbsp;

## Transformação de Dados

Christian Collberg trata as Transformações de Dados (Data Transformations – DT) em separado, contudo o código de baixo nível que será gerado possui as mesmas características das Transformações de Fluxo. Pois, na verdade, não há bem uma transformada no armazenamento interno dos dados – como ocorre na remoção simbólica ou na encriptação –, e sim uma forma diferente de tratá-los. 

O foco principal das Dts consiste em alterar pequenas partes das estruturas de dados de um programa. Isso é aplicado como uma técnica anticracking porque quando se reconhece uma estrutura de dados, há grande possibilidade de se saber como o programa funciona. Logo, as Transformações de Dados são voltadas à confundir principalmente o leitor humano, diferente de outras técnicas voltadas à enganar outros softwares. 

Uma abordagem usada para transformar os dados está em modificar o funcionamento de algumas variáveis no programa. Normalmente alteramos as variáveis que tem os valores modificados com mais freqüência ou as que guardam dados-chaves para o cracker. 

Isto pode ser efetivo porque força a geração de um assembly com instruções que não são intuitivas para um leitor humano. 

Um bom exemplo de transformação de dados pode ser simplesmente mudar o intervalo incremental em um laço de repetição com contagem. No caso de um contador poderíamos incrementar de 2 em 2, 3 em 3, 5 em 5, ou qualquer valor que correspondesse ao mesmo intervalo total. 

Veja o seguinte código:

<pre lang="cpp">for(i=1; i &lt; 1000 ; i++){
		// your code here
	}
</pre>

poderia ser reescrito com um outro intervalo:

<pre lang="cpp">for(i=5; i &lt; 5000; i+=5) {
		// the same code here
	}
</pre></p> 

Note que a funcionalidade de ambos laços são equivalentes. 

Esta pequena – e trivial – modificação poderia tornar o código de baixo nível pouco intuitivo. Todavia, se dentro do bloco tivermos um código extenso, que dependa do valor do índice, a leitura e entendimento para o programador pode ser difícil ou confuso. 

Por isso esta técnica normalmente é inserida por programas que ofuscam código, é aplicada em tempo de compilação ou o código fonte é modificado por algum programa para obedecer à esta transformação. 

Um cuidado que devemos tomar é com a otimização dos compiladores, que tendem à retirar operações que geram códigos equivalentes. 

&nbsp;

Uma outra transformação de dados muito utilizada consiste em modificar o leiaute de arranjos para que preserve sua funcionalidade original, mas que confunda o cracker sobre seu propósito. 

Há diversas maneiras de se implantar esta transformação. A forma ideal está em como estes dados são utilizados. 

Por exemplo, quando queremos ler dados de arquivos para um arrays e utilizamos estes arrays como consulta e com pouca modificação, podemos unir em um grande array todos os pequenos arrays, guardando as referências dos índices equivalentes à cada array diferente em variáveis diferentes. 

Quando temos o caso oposto, ou seja, quando nosso programa modifica frequentemente dados em uma estrutura de arranjos, podemos quebrar um array em diferentes arrays. Isto promove certa eficiência e pode confundir o cracker sobre o propósito da estrutura. 

Um outro caso ainda pode ser a mudança de dimensões que podemos promover em um array. Por exemplo, sabemos que a memória do computador é seqüencial e contígua. As matrizes com mais de 1 dimensão são abstrações que as linguagens de alto nível permitem. O que podemos fazer é justamente quebrar estas abstrações, dividindo um array de certa dimensão em outro para inserir um fator de confusão para o cracker. 

Um exemplo trivial seria:

<pre lang="cpp">#define LINES 10
#define COLMNS 5

void original(){
	int originalA[LINES][COLMNS];

	// preenche a tabela
	for(int i=0; i &lt; LINES ; i++){
		for(int j=0; j &lt; COLMNS; j++){
			originalA[i][j] = j;
		}
	}

	//exibe
	for(int i=0; i &lt; LINES ; i++){
		for(int j=0; j &lt; COLMNS; j++){
			printf("%i\t",originalA[i][j]);
		}
		printf("\n");
	}
}
</pre>

que poderia ser reescrito como:

<pre lang="cpp">#define LINES 10
#define COLMNS 5

void modified(){
	int originalA[LINES*COLMNS];
	int i=0, j=0;

	//gera
	for(i=0; i &lt; LINES*COLMNS ; i++){
		if(i % COLMNS == 0){
			j=0;
		}
		originalA[i] = j++;
	}

	//exibe
	for(i=0; i &lt; LINES*COLMNS ; i++){
		if(i % COLMNS == 0){
			printf("\n");
		}
		printf("%i\t",originalA[i]);
	}
}
</pre>

&nbsp;</p>
