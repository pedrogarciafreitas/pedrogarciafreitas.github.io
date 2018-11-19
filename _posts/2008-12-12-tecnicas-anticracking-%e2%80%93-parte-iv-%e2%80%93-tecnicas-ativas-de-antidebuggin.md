---
id: 207
title: Técnicas AntiCracking – Parte IV – Técnicas Ativas de Antidebug
date: 2008-12-12T11:33:34+00:00
author: SAWP
excerpt: |
  No post “A Fórmula do Crack” discutimos alguma coisa sobre debuggers. Como é o processo de debuggin em user-mode e kernel-mode, como cada um deles trabalha quando um usuário anexa um processo à eles, quando fixa um breakpoints em uma instrução etc.
  O que não foi discutido é a forma como o debugger atua: quando o usuário escolhe pontos de parada para conferir o andamento da execução do programa é comum o debugger substituir a(s) instrução(ões) por uma instrução própria, que só ele entenda.
layout: post
guid: http://www.sawp.com.br/blog/?p=207
permalink: p=207
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:2613:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #ff0000; font-style: italic;">/*
    * da mesma forma que fizemos como exemplo no tópico “Detectando Máquinas Virtuais”,
    * antes de termos uma função para inicializar o programa, sempre colocamos a função
    * para teste das condicoes (onde testamos licença, presença de vm, de debugger, etc).
    *
    * no java, seria equivalente ao bloco static{ } da primeira classe a ser carregada.
    */</span>
    <span style="color: #0000ff;">void</span> prestarter<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    __asm<span style="color: #008000;">&#40;</span>
    mov <span style="color: #000040;">%</span>eax, <span style="color: #000040;">%</span>fs<span style="color: #008080;">:</span> <span style="color: #008000;">&#91;</span><span style="color:#800080;">00000018</span><span style="color: #008000;">&#93;</span>
    mov <span style="color: #000040;">%</span>eax, <span style="color: #008000;">&#91;</span><span style="color: #000040;">%</span>eax<span style="color: #000040;">+</span><span style="color: #208080;">0x30</span><span style="color: #008000;">&#93;</span>
    cmp byte ptr <span style="color: #008000;">&#91;</span><span style="color: #000040;">%</span>eax<span style="color: #000040;">+</span><span style="color: #208080;">0x02</span><span style="color: #008000;">&#93;</span>, <span style="color: #0000dd;">0</span>
    je _RunProgram
    <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> RunProgram<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// start you program here</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
    * da mesma forma que fizemos como exemplo no tópico “Detectando Máquinas Virtuais”,
    * antes de termos uma função para inicializar o programa, sempre colocamos a função
    * para teste das condicoes (onde testamos licença, presença de vm, de debugger, etc).
    *
    * no java, seria equivalente ao bloco static{ } da primeira classe a ser carregada.
    */
    void prestarter(){
    __asm(
    mov %eax, %fs: [00000018]
    mov %eax, [%eax+0x30]
    cmp byte ptr [%eax+0x02], 0
    je _RunProgram
    );
    }
    
    void RunProgram(){
    // start you program here
    }</p></div>
    ;i:2;s:3846:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">&nbsp;
    <span style="color: #0000ff;">void</span> prestarter<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">bool</span> trapFlag <span style="color: #000080;">=</span> <span style="color: #0000ff;">true</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">try</span> <span style="color: #008000;">&#123;</span>
    __asm__<span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;pushfd; &quot;</span>
    <span style="color: #FF0000;">&quot;or dword ptr[%esp], 0x100; &quot;</span>
    <span style="color: #FF0000;">&quot;popfd;&quot;</span>
    <span style="color: #FF0000;">&quot;nop;&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span> <span style="color: #0000ff;">catch</span> <span style="color: #008000;">&#40;</span>Exception e<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    trapFlag <span style="color: #000080;">=</span> <span style="color: #0000ff;">false</span><span style="color: #008080;">;</span>	<span style="color: #666666;">// uma exceção foi gerada, então não existe debugger</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span>trapFlag<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">printf</span><span style="color: #008000;">&#40;</span>“Debugger esta presente.”<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    die<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>			<span style="color: #666666;">// programa morre aqui, não executa se tiver debugger</span>
    <span style="color: #008000;">&#125;</span><span style="color: #0000ff;">else</span><span style="color: #008000;">&#123;</span>
    RunProgram<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>	<span style="color: #666666;">// as opções, funcionalidades, etc, são abertas aqui</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> RunProgram<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// start you program here</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">void</span> main<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    prestarter<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">
    void prestarter(){
    bool trapFlag = true;
    
    try {
    __asm__(&quot;pushfd; &quot;
    &quot;or dword ptr[%esp], 0x100; &quot;
    &quot;popfd;&quot;
    &quot;nop;&quot;);
    } catch (Exception e) {
    trapFlag = false;	// uma exceção foi gerada, então não existe debugger
    }
    
    if(trapFlag){
    printf(“Debugger esta presente.”);
    die();			// programa morre aqui, não executa se tiver debugger
    }else{
    RunProgram();	// as opções, funcionalidades, etc, são abertas aqui
    }
    }
    
    void RunProgram(){
    // start you program here
    }
    
    void main(){
    prestarter();
    }</p></div>
    ";}
categories:
  - Programming Internals
tags:
  - anticraking
  - Programming Internals
---
As técnicas mencionadas abaixo são utilizadas para dificultar a análise dinâmica do código, aquela quando usamos um debugger. 

No post “A Fórmula do Crack” discutimos alguma coisa sobre debuggers. Como é o processo de debuggin em user-mode e kernel-mode, como cada um deles trabalha quando um usuário anexa um processo à eles, quando fixa um breakpoints em uma instrução etc. 

O que não foi discutido é a forma como o debugger atua: quando o usuário escolhe pontos de parada para conferir o andamento da execução do programa é comum o debugger substituir a(s) instrução(ões) por uma instrução própria, que só ele entenda. Esta instrução é conhecida como “interrupção de breakpoint” (breakpoint interrupt) e não é executada pelo programa, mas notifica ao debugger que uma interrupção foi encontrada naquele ponto. Quando a execução chega nesta instrução, o debugger congela a execução do programa e podemos inspecionar seu estado. 

Sabendo que estas instruções geram comportamentos específicos &#8211; como levantamento de exceções &#8211; utilizamo-as como chaves para detecção dos debuggers.

## 1. hadUserModeDebugger__</p> 

hadUserModeDebbuger, também conhecido como UserDebuggerInformation ou isDebuggerPresentAPI é uma API (Aplication Program Interface) usada na detecção de debuggers que trabalham em user-mode, tais como o OllyDbg. 

Quando implementada em um aplicativo acessa o “Process Environment Block” (PEB) para determinar se um debugger foi encontrado. A implementação do código é a seguinte:

<pre lang="cpp">/*
* da mesma forma que fizemos como exemplo no tópico “Detectando Máquinas Virtuais”, 
* antes de termos uma função para inicializar o programa, sempre colocamos a função
* para teste das condicoes (onde testamos licença, presença de vm, de debugger, etc).
*
* no java, seria equivalente ao bloco static{ } da primeira classe a ser carregada.
*/
void prestarter(){
	__asm(
		mov %eax, %fs: [00000018]
		mov %eax, [%eax+0x30]
		cmp byte ptr [%eax+0x02], 0
		je _RunProgram
	);
}

void RunProgram(){
	// start you program here
}
</pre></p> 

&nbsp;

## 2. The Trick

Esta técnica consiste em utilizar uma “flag” (Trap Flag) para detectar se uma exceção específica é gerada ou não. É uma abordagem semelhante à alguns algoritmos de detecção de máquinas virtuais, como já comentei antes (“The Jerry Code”, http://www.trapkit.de/research/vmm/jerry/index.html , que utiliza instruções que não são da arquitetura física para gera exceções específicas para detecção). 

Um valor booleano é criado para determinar se o sistema caiu na armadilha ou não. A armadilha é a seguinte: se a exceção não é gerada, então é porque um debugger retirou a exceção para que o programa possa ser analisado. Ou seja, a única possibilidade da “flag” não mudar de estado é que “algo” impeça a exceção. E este “algo” é o próprio debugger. 

A vantagem desta abordagem é que ela pode detectar de forma simples qualquer debugger que esteja monitorando o programa que desejamos proteger, seja em modo usuário ou kernel. 

Também é uma forma relativamente segura, pois não depende de uma API externa do sistema operacional e mantém todo o controle dentro da própria aplicação. 

Uma implementação da Armadilha é a seguinte:

<pre lang="cpp">void prestarter(){
	bool trapFlag = true;	

	try { 
		__asm__("pushfd; " 
				"or dword ptr[%esp], 0x100; " 
				"popfd;" 
				"nop;"); 
	} catch (Exception e) { 
		trapFlag = false;	// uma exceção foi gerada, então não existe debugger
	}

	if(trapFlag){
		printf(“Debugger esta presente.”);
		die();			// programa morre aqui, não executa se tiver debugger
	}else{
		RunProgram();	// as opções, funcionalidades, etc, são abertas aqui
	}
}

void RunProgram(){
	// start you program here
}

void main(){
	prestarter();
}
</pre></p> 

&nbsp;

## Conclusão

Estas implementações tendem a ser bem eficientes, mas deve-se ficar claro que é restrita à família NT. Embora as AADTs sejam as que oferecem menos perda de performance (quase nula, como observa-se nos códigos acima), são as que oferecem mais riscos, pois qualquer incompatibilidade com o ambiente de execução acarreta em um erro fatal, impedindo execução do programa. 

Outra desvantagem das AADTs é que elas são dependentes de arquitetura. O que torna o sistema não-portável.</p> 

&nbsp;
