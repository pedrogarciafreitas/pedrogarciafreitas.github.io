---
id: 214
title: Técnicas AntiCracking – Parte V – Burlando Disassemblers
date: 2008-12-12T11:40:08+00:00
author: SAWP
excerpt: Uma técnica sofisticada de enganar disassemblers consiste em usar um trecho do programa para alterar os bits das outras partes do programa, que desejamos proteger. A estratégia usada é deslocar os bits de um trecho do programa para que este pedaço pareça possuir outras instruções. Desta forma, o decompilador irá interpretar essas instruções e fornecer informações erradas ao atacante.
layout: post
guid: http://www.sawp.com.br/blog/?p=214
permalink: p=214
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1113:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	__asm<span style="color: #008000;">&#40;</span>“	Algum código para disfarçar<span style="color: #008080;">;</span>”
    “jmp Desvio<span style="color: #008080;">;</span>”
    “_emit <span style="color: #208080;">0x0f</span>”
    “Desvio<span style="color: #008080;">:</span> ”
    “mov <span style="color: #000040;">%</span>eax, <span style="color: #008000;">&#91;</span>AlgumaVariavelQualquer<span style="color: #008000;">&#93;</span> <span style="color: #008080;">;</span>”
    “push <span style="color: #000040;">%</span>eax <span style="color: #008080;">;</span>”
    “call FuncaoQualquer”
    <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">	__asm(“	Algum código para disfarçar;”
    “jmp Desvio;”
    “_emit 0x0f”
    “Desvio: ”
    “mov %eax, [AlgumaVariavelQualquer] ;”
    “push %eax ;”
    “call FuncaoQualquer”
    );</p></div>
    ;i:2;s:2415:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;">	<span style="color: #339900;">#define paste(a,b) a##b</span>
    &nbsp;
    <span style="color: #0000ff;">inline</span> ofuscar<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    __asm<span style="color: #008000;">&#40;</span>
    “mov <span style="color: #000040;">%</span>eax, __LINE__ <span style="color: #000040;">*</span> <span style="color: #208080;">0x66699902</span><span style="color: #008080;">;</span>”
    “cmp <span style="color: #000040;">%</span>eax, __LINE__ <span style="color: #000040;">*</span> <span style="color: #208080;">0x9cb16d48</span><span style="color: #008080;">;</span>”
    “je paste<span style="color: #008000;">&#40;</span>Junk, __LINE__<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>”
    “mov <span style="color: #000040;">%</span>eax, paste<span style="color: #008000;">&#40;</span>After, __LINE__<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>”
    “jmp <span style="color: #000040;">%</span>eax<span style="color: #008080;">;</span>”
    “paste<span style="color: #008000;">&#40;</span>Junk, __LINE__<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>”
    “emit<span style="color: #008000;">&#40;</span><span style="color: #208080;">0xd8</span><span style="color: #000040;">+</span>__LINE__ <span style="color: #000040;">%</span> <span style="color: #0000dd;">8</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span> ”
    “paste<span style="color: #008000;">&#40;</span>After, __LINE__<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>”
    <span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	#define paste(a,b) a##b
    
    inline ofuscar(){
    __asm(
    “mov %eax, __LINE__ * 0x66699902;”
    “cmp %eax, __LINE__ * 0x9cb16d48;”
    “je paste(Junk, __LINE__);”
    “mov %eax, paste(After, __LINE__);”
    “jmp %eax;”
    “paste(Junk, __LINE__);”
    “emit(0xd8+__LINE__ % 8); ”
    “paste(After, __LINE__);”
    );
    }</p></div>
    ";}
categories:
  - Programming Internals
tags:
  - anticraking
  - Programming Internals
---
Confusing Disassemblers (CD) são técnicas aplicadas em programas voltados à plataformas que utilizam processadores de instruções com tamanho variável. Nestas plataformas – normalmente CISCs, como a IA32 – é possível criar uma armadilha para os disassamblers de forma que eles não consigam interpretar a instrução como um comando ASM. Ou seja, consiste em dessincronizar a instrução real (formada por zeros-e-uns) com a forma abstrata dela (código legível, asm).

Antes de discutirmos sobre como as técnicas são aplicadas é importante entender que a diferença entre elas se dá devido à forma como cada disassembler analisa o código.

## 1. Conversão Linear (CLin)

Conversão linear é uma abordagem utilizada por alguns disassemblers que simplesmente desassembla a instrução seqüencialmente, sem levar em conta como as instruções variam ao longo do fluxo de execução. Ou seja, o disassembler simplesmente faz a conversão em paridade: a seqüência X equivale à instrução Y, e isso a cada instrução, uma após outra, não importando os desvios que ocorrem pelo código.

Desta forma, quando empregada a conversão linear, o disassembler irá converter instrução por instrução, o que significa que uma seqüência dados no meio do código poderia confundir o disassembler fazendo com que ele interpretasse aquilo como comando.

Os disassemblers que conheço, e mencionei no artigo “A Fórmula de um Crack”, que aplicam a técnica de conversão linear são: Numega SoftIce ( veja: <a href="http://www.caloni.com.br/blog/archives/introducao-ao-softice" target="_blank">http://www.caloni.com.br/blog/archives/introducao-ao-softice</a> ), Microsoft WinDbg ( <a href="http://www.microsoft.com/whdc/DevTools/Debugging/default.mspx" target="_self">http://www.microsoft.com/whdc/DevTools/Debugging/default.mspx</a> ) e o Syster (Baseado no SoftIce ( <a href="http://www.sysersoft.com/" target="_blank">http://www.sysersoft.com/</a> ) .

Veja o código:

<pre lang="cpp">__asm(“	Algum código para disfarçar;”
			“jmp Desvio;”
			“_emit 0x0f”
			“Desvio: ”
			“mov %eax, [AlgumaVariavelQualquer] ;”
			“push %eax ;”
			“call FuncaoQualquer”
	);</pre>

Este código irá confundir os desassembladores que utilizam CLin, gerando uma outra seqüência totalmente diferente da original, afetando até mesmo o entendimento do código que o cracker está buscando.

Contudo, se utilizássemos um disassembler como o IDA PRO este código acima não traria muitos efeitos pois desviaria para a próxima instrução junto com “Desvio”, sem misturar dados com instruções.

## 2. Conversão com Ligação Recursiva (CLR)

Enquanto na conversão linear as instruções são transcritas uma-a-uma, sem levar em conta como o programa é executado, na Ligação Recursiva as instruções são analisadas de acordo com suas ligações através do fluxo de execução. Ou seja, quando aparece um comando de desvio para outra instrução, que aponta para certo endereço, o disassembler também converte este endereço, seguindo o fluxo de execução. Assim, Ligação Recursiva acaba sendo mais tolerante às técnicas anti-disassembly.

Os principais disassemblers que implementam a CLR são: o fabuloso OllyDbg e o IDA Pro (a qual cria até fluxogramas para visualizarmos exatamente os desvios no código).

## 3. Burlando

A função ofuscar abaixo insere uma seqüência de instruções em assembly que pode confundir alguns disassemblers.

<pre lang="cpp">#define paste(a,b) a##b

	inline ofuscar(){
		__asm(
			“mov %eax, __LINE__ * 0x66699902;”
			“cmp %eax, __LINE__ * 0x9cb16d48;”
			“je paste(Junk, __LINE__);”
			“mov %eax, paste(After, __LINE__);”
			“jmp %eax;”
			“paste(Junk, __LINE__);”
			“emit(0xd8+__LINE__ % 8); ”
			“paste(After, __LINE__);”
		);
	}</pre>

Note que é possível criar uma dezena de variações destas função. Se distribuirmos esta função (ou suas combinações) através do código alvo podemos tornar o processo de cracking extremamente cansativo.

Contudo, – como sempre digo – anticracking sempre acarreta uma perda de eficiência no programa-alvo. O uso excessivo desta função ofuscar() poderia causar um aumento considerável no conjunto de instruções. Como conseqüência consumiria mais memória e disco.

Outra medida interessante, mas que comprometeria muito a eficiência, é fazer um programa que gere diferentes combinações da função ofuscar() e as espalhe pelo código. Isso porque utilizar a mesma função gera padrões repetitivos no objeto final, o que tornaria sua proteção extremamente vulnerável para ferramentas que buscam trechos repetitivos.

Particularmente não penso que seja a solução mais interessante. A remoção de informação simbólica é uma boa, combinada com ofuscação e Transformações no Controle do Fluxo acabam sempre sendo as abordagens mais eficientes.
