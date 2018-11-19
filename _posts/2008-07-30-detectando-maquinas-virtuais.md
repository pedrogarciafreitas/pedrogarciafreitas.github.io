---
id: 101
title: Detectando Máquinas Virtuais
date: 2008-07-30T16:20:14+00:00
author: SAWP
excerpt: 'As vezes precisamos que nosso programa se comporte de forma diferente quando rodar em uma máquina virtual. Principalmente quando queremos dificultar o processo de engenharia reversa do nosso programa, antecipando o ambiente em que o cracker trabalhará, ou ainda, queremos restringir algumas funcionalidades que teriam a segurança reduzida, se rodasse numa MV.	'
layout: post
guid: http://www.sawp.com.br/blog/?p=101
permalink: p=101
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:2333:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #ff0000; font-style: italic;">/*
    * main.cpp
    *
    *  Created on: 23/07/2008
    *  Author: SAWP
    *
    *
    *  If on a VM, the programa dont execute. The program starter is called if
    *        running on hardware.
    *
    * www.sawp.com.br
    */</span>
    <span style="color: #339900;">#include</span>
    <span style="color: #0000ff;">using</span> <span style="color: #0000ff;">namespace</span> std<span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cout</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cin</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #339900;">#include &quot;SystemMon.h&quot;</span>
    &nbsp;
    <span style="color: #0000ff;">int</span> main<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    SystemMon <span style="color: #000040;">*</span>ptrSysMon <span style="color: #000080;">=</span> <span style="color: #0000ff;">NULL</span><span style="color: #008080;">;</span>
    ptrSysMon <span style="color: #000080;">=</span> <span style="color: #0000dd;">new</span> SystemMon<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000dd;">exit</span><span style="color: #008000;">&#40;</span><span style="color: #0000dd;">0</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
    * main.cpp
    *
    *  Created on: 23/07/2008
    *  Author: SAWP
    *
    *
    *  If on a VM, the programa dont execute. The program starter is called if
    *        running on hardware.
    *
    * www.sawp.com.br
    */
    #include
    using namespace std;
    using std::cout;
    using std::cin;
    
    #include &quot;SystemMon.h&quot;
    
    int main(void){
    SystemMon *ptrSysMon = NULL;
    ptrSysMon = new SystemMon();
    
    exit(0);
    }</p></div>
    ;i:2;s:9021:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #ff0000; font-style: italic;">/*
    * SystemMon.cpp
    *
    *  Created on: 23/07/2008
    *  Author: SAWP
    */</span>
    &nbsp;
    <span style="color: #339900;">#include &quot;SystemMon.h&quot;</span>
    <span style="color: #339900;">#include </span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/** ### Public ### **/</span>
    &nbsp;
    SystemMon<span style="color: #008080;">::</span><span style="color: #007788;">SystemMon</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    programStarter<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    SystemMon<span style="color: #008080;">::</span>~SystemMon<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// TODO Auto-generated destructor stub</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/** ### Private ### **/</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/**
    * Detect if is on virtual machine.
    *
    * Based on: http://invisiblethings.org/tools/redpill.c
    *
    * modified from joanna at invisiblethings.org
    * should compile and run on any Intel based OS
    *
    * http://invisiblethings.org
    */</span>
    <span style="color: #0000ff;">const</span> <span style="color: #0000ff;">bool</span> SystemMon<span style="color: #008080;">::</span><span style="color: #007788;">isVirtualMachine</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
    &nbsp;
    <span style="color: #0000ff;">unsigned</span> <span style="color: #0000ff;">char</span> m<span style="color: #008000;">&#91;</span> <span style="color: #0000dd;">6</span> <span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span>
    <span style="color: #666666;">//unsigned char rpill[] = &quot;\x0f\x01\x0d\x00\x00\x00\x00\xc3&quot;; </span>
    <span style="color: #0000ff;">unsigned</span> <span style="color: #0000ff;">char</span> rpill<span style="color: #008000;">&#91;</span><span style="color: #008000;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #FF0000;">&quot;<span style="color: #660099; font-weight: bold;">\x0F</span><span style="color: #660099; font-weight: bold;">\x01</span><span style="color: #660099; font-weight: bold;">\x0D</span><span style="color: #660099; font-weight: bold;">\x00</span><span style="color: #660099; font-weight: bold;">\x00</span><span style="color: #660099; font-weight: bold;">\x00</span><span style="color: #660099; font-weight: bold;">\x00</span><span style="color: #660099; font-weight: bold;">\xc3</span>&quot;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #000040;">*</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">unsigned</span><span style="color: #000040;">*</span><span style="color: #008000;">&#41;</span> <span style="color: #000040;">&amp;</span>rpill<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">3</span><span style="color: #008000;">&#93;</span><span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #0000ff;">unsigned</span><span style="color: #008000;">&#41;</span> m<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#40;</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span> <span style="color: #000040;">&amp;</span>rpill<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span>m<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">5</span><span style="color: #008000;">&#93;</span> <span style="color: #000080;">&gt;</span> <span style="color: #208080;">0xd0</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff;">return</span> <span style="color: #0000ff;">false</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/**
    * The program functionality
    */</span>
    <span style="color: #0000ff;">void</span> SystemMon<span style="color: #008080;">::</span><span style="color: #007788;">program</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;Hello World, Im not in VM. Im the host!&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #ff0000; font-style: italic;">/**
    * start the program if running without VM
    */</span>
    <span style="color: #0000ff;">void</span> SystemMon<span style="color: #008080;">::</span><span style="color: #007788;">programStarter</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    <span style="color: #666666;">// your start-check code here...</span>
    &nbsp;
    <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span><span style="color: #000040;">!</span>this<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span>isVirtualMachine<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#123;</span>
    this<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span>program<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span> <span style="color: #666666;">//start the program if isnt in VM</span>
    <span style="color: #008000;">&#125;</span><span style="color: #0000ff;">else</span><span style="color: #008000;">&#123;</span>
    <span style="color: #0000dd;">puts</span><span style="color: #008000;">&#40;</span><span style="color: #FF0000;">&quot;Execute at host machine.&quot;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #0000dd;">exit</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">EXIT_SUCCESS</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span> <span style="color: #666666;">// Don't allow execute.</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
    * SystemMon.cpp
    *
    *  Created on: 23/07/2008
    *  Author: SAWP
    */
    
    #include &quot;SystemMon.h&quot;
    #include
    
    /** ### Public ### **/
    
    SystemMon::SystemMon() {
    programStarter();
    }
    
    SystemMon::~SystemMon() {
    // TODO Auto-generated destructor stub
    }
    
    /** ### Private ### **/
    
    /**
    * Detect if is on virtual machine.
    *
    * Based on: http://invisiblethings.org/tools/redpill.c
    *
    * modified from joanna at invisiblethings.org
    * should compile and run on any Intel based OS
    *
    * http://invisiblethings.org
    */
    const bool SystemMon::isVirtualMachine() {
    
    unsigned char m[ 6 ];
    //unsigned char rpill[] = &quot;\x0f\x01\x0d\x00\x00\x00\x00\xc3&quot;;
    unsigned char rpill[] = &quot;\x0F\x01\x0D\x00\x00\x00\x00\xc3&quot;;
    
    *((unsigned*) &amp;rpill[3]) = (unsigned) m;
    ((void(*)()) &amp;rpill)();
    
    if(m[5] &gt; 0xd0){
    return true;
    }
    
    return false;
    }
    
    /**
    * The program functionality
    */
    void SystemMon::program(){
    puts(&quot;Hello World, Im not in VM. Im the host!&quot;);
    }
    
    /**
    * start the program if running without VM
    */
    void SystemMon::programStarter(){
    // your start-check code here...
    
    if(!this-&gt;isVirtualMachine()){
    this-&gt;program(); //start the program if isnt in VM
    }else{
    puts(&quot;Execute at host machine.&quot;);
    exit(EXIT_SUCCESS); // Don't allow execute.
    }
    }</p></div>
    ";}
categories:
  - Virtualization
tags:
  - Virtualization
---
## 1. Introdução

As vezes precisamos que nosso programa se comporte de forma diferente quando estiver executando em uma máquina virtual. Conseguir a restrição de funcionalidades em ambiente virtualizado é, além de mais uma técnica anticracking – utilizada para evitar análise online de código –, um importante recurso para garantir compatibilidade, segurança, estabilidade e proteção de recursos.

Um desenvolvedor que necessita proteger seu código, precisa dificultar o processo de engenharia reversa do seu programa, antecipando as condições do ambiente em que o cracker trabalhará. Ou seja, deve de restringir algumas funcionalidades que torna o código permissível ao cracking.

Para o cracking, conhecer as técnicas de detecção de máquinas virtuais é fundamental para criação de software que utilizem VM Escape. Encontrar brechas em MV permite que acessemos como superusuários uma máquina virtual e, em alguns casos, até a máquina hospedeira.

## 2. A Pílula Vermelha

O programa que abaixo é uma simples aplicação da detecção de VM: impedir ações para dificultar o processo da análise online do código.

Com base no código de Joanna Rutkowska, &#8220;Red Pill&#8221; (em uma referencia ao filme Matrix), nosso programa restringe a execução de algumas de suas partes, permitindo que rode somente em ambientes não-virtuais.

A idéia é simples: o programa possui uma função inicializadora, que poderia ser protegida ou não por um keycheker. Esta função (programStarter) verifica se o programa está dentro de uma máquina virtual. Se estiver, ele emite uma mensagem dizendo que não continuará sua execução e termina.

Novamente, este exemplo é um resumo simplificado de como alguns sistemas (como o Windows Vista) fazem para bloquear seus recursos quando executado em máquinas virtuais. Segue abaixo o código.

<pre lang="cpp">/*
 * main.cpp
 *
 *  Created on: 23/07/2008
 *  Author: SAWP
 *
 *
 *  If on a VM, the programa dont execute. The program starter is called if 
 *        running on hardware.
 *
 * www.sawp.com.br
 */
#include
using namespace std;
using std::cout;
using std::cin;

#include "SystemMon.h"

int main(void){
	SystemMon *ptrSysMon = NULL;
	ptrSysMon = new SystemMon();

	exit(0);
}</pre>



<pre lang="c++">/*
 * SystemMon.h
 *
 *  Created on: 23/07/2008
 *  Author: SAWP
 */

#ifndef SYSTEMMON_H_
#define SYSTEMMON_H_

class SystemMon {
public:
	SystemMon();
	virtual ~SystemMon();
protected:
	const bool isVirtualMachine(void) ;
	void programStarter(void);
	void program(void);
};

#endif /* SYSTEMMON_H_ */</pre>



<pre lang="cpp">/*
 * SystemMon.cpp
 *
 *  Created on: 23/07/2008
 *  Author: SAWP
 */

#include "SystemMon.h"
#include 

/** ### Public ### **/

SystemMon::SystemMon() {
	programStarter();
}

SystemMon::~SystemMon() {
	// TODO Auto-generated destructor stub
}

/** ### Private ### **/

/**
 * Detect if is on virtual machine.
 *
 * Based on: http://invisiblethings.org/tools/redpill.c
 *
 * modified from joanna at invisiblethings.org
 * should compile and run on any Intel based OS
 *
 * http://invisiblethings.org
 */
const bool SystemMon::isVirtualMachine() {

	unsigned char m[ 6 ];
	//unsigned char rpill[] = "\x0f\x01\x0d\x00\x00\x00\x00\xc3"; 
	unsigned char rpill[] = "\x0F\x01\x0D\x00\x00\x00\x00\xc3";

	*((unsigned*) &rpill[3]) = (unsigned) m;
	((void(*)()) &rpill)();

	if(m[5] > 0xd0){
		return true;
	}

	return false;
}

/**
 * The program functionality
 */
void SystemMon::program(){
	puts("Hello World, Im not in VM. Im the host!");
}

/**
 * start the program if running without VM
 */
void SystemMon::programStarter(){
	// your start-check code here...

	if(!this->isVirtualMachine()){
		this->program(); //start the program if isnt in VM
	}else{
		puts("Execute at host machine.");
		exit(EXIT_SUCCESS); // Don't allow execute.
	}
}</pre>

Conforme o autor do código, Rutkowska, tomando o pílula vermelha, é mais ou menos como o código da função `isVirtualMachine()`, que retornará true se estiver executada em uma máquina virtual.

_&#8220;Red Pill&#8221;_ é um código chama atenção porque consegue detectar uma MV com um código reduzido. Ela também é _asm-free_, ou seja, independe de compiladores e pode rodar em qualquer sistema operacional, sendo uma solução portável.

Veja o programa sendo executado em uma máquina virtual com MS Windows como _guest_:

<p style="text-align: center;">
  <br /> Download: <a href="http://www.megaupload.com/pt/?d=I7T4TND0" target="_blank">http://www.megaupload.com/pt/?d=I7T4TND0</a>
</p>

Agora, o mesmo programa compilado e executado em um _Host Unix_. 

<p style="text-align: center;">
  <br /> Download: <a href="http://www.megaupload.com/pt/?d=RMVQ14YK" target="_blank">http://www.megaupload.com/pt/?d=RMVQ14YK</a>
</p>

## 3. Funcionamento

Este código utiliza a instrução `SIDT ( _asm sidt idt )` , codificada como `0F010D[endereço]` (“\x0f\x01\x0d”) ou a `SIDTL`, codificada como `0F01F8[endereço]` (ou _asm sidtl 0xfffffff8(%ebp)), que guarda o conteúdo da “interrupt descriptor table register” (`IDTR`) no operador destino.

O mais interessante sobre a instrução `SIDT` é que ela pode ser executada sem controle de privilégio, mas pode retornar o conteúdo do registrador usado internamente pelo sistema operacional (Risc&#8217;s: $k0,$k1, Cisc&#8217;s: sensitive register, exclusivos do SO).

Como este é apenas um registrador de `IDTR`, se estiver em uma MV teria ainda que ter outro(s) registradores do sistema operacional host. Então, a máquina virtual precisará recolocar o `IDTR` do sistema que estiver rodando em um lugar seguro a fim de evitar um conflito com o SO host.

Contudo, a MV não pode saber onde o sistema virtual irá executar a instrução SIDT, desde que ela não gere uma exceção. Assim, nosso processo “captura” o endereço recolocado pela MV na IDTR.

&#8220;Red Pill&#8221; então detecta se o `IDTR` e verifica o local dele, dependendo do que ela retorna sabe-se se o ambiente se o ambiente é virtualizado ou não.

Na VMWARE o endereço recolocado do `IDTR` tem base `0xFFxxxxxx` e no VirtualPC é recolocado numa região `0xe8XXXXXX`. Segundo o autor do código ( <http://invisiblethings.org> ), &#8220;Red Pill&#8221; foi testado utilizando as MV: VmWare Workstation 4 e o Virtual PC 2004, ambos rodando em um host com WinXp.

Veja mais da pesquisa em: <a href="http://www.offensivecomputing.net/files/active/0/vm.pdf" target="_blank">http://www.offensivecomputing.net/files/active/0/vm.pdf</a> .

Eu testei o código utilizando a máquina virtual VirtualBox 1.5.6_OSE, utilizando como host os sistemas: WinXp Sp1, Linux Ubuntu 8.04 e Free BSD. Em todos foi detectado que o programa estava sendo executado diretamente no host.

Nas máquinas virtuais compilei e executei no Ubuntu e no Windows XP. Em ambos sistemas foi detectado que a execução ocorria em ambiente virtualizado. Logo, o código funciona com sucesso nas três máquinas virtuais e em todos os sistemas mencionados.

Nas figuras abaixo podemos ver um Host e uma máquina virtual rodando, ao mesmo tempo, o mesmo programa: 

<p style="text-align: center;">
  <img class="aligncenter size-medium wp-image-231" title="both_destacado" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both_destacado-300x187.png" alt="both_destacado" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both_destacado-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both_destacado-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both_destacado.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
</p>

<p style="text-align: center;">
  <img class="aligncenter size-medium wp-image-230" title="both" src="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both-300x187.png" alt="both" width="300" height="187" srcset="http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both-300x187.png 300w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both-1024x640.png 1024w, http://www.sawp.com.br/blog/wp-content/uploads/2008/07/both.png 1280w" sizes="(max-width: 300px) 100vw, 300px" />
</p>

<p style="text-align: center;">
  <h2>
    4. Algo Mais?
  </h2>
  
  <p>
    Como podemos observar, a técnica utilizada para detecção da Pílula Vermelha consiste em checar indícios da MV por processos e também checando a existência da MV buscando no <code>SIDTR</code> (<em>Store Interrupt Descriptor Table Register</em>).
  </p>
  
  <p>
    Esta técnica é a que permite dificultar mais o trabalho de cracking, desde que os processos fiquem monitorados de forma correta e as chamadas da função ficarem distribuídas pelo programa.
  </p>
  
  <p>
    Como o código é pequeno (quase uma instrução da CPU), aplicando à Pílula Vermelha a técnica de inlining, torna-se um inferno para o cracker entender o local no código onde está a proteção.
  </p>
  
  <p>
    Porém, há outras formas de se detectar a presença de um ambiente virtualizado: Checar hardwares (se há assinatura conhecida, como sendo de uma MV); ou procurar por MV nos registros ou em arquivos específicos. Contudo, estes métodos são mais fáceis de se burlar. Basta que o usuário modifique alguns registros no sistema.
  </p>
  
  <h2>
    5. Outros Códigos
  </h2>
  
  <p>
    Existem ainda outros códigos disponíveis que podem ser interessantes para o programador.
  </p>
  
  <h3>
    5.1 Scoopy-Doo
  </h3>
  
  <p>
    Trata-se de um código escrito por Tobias Klein <a href=" http://www.trapkit.de"> http://www.trapkit.de</a>. Atua testando registros na <code>SIDTR</code> (<em>Store Interrupt Descriptor Table Register</em>), na <code>SGDTR</code> ( <em>Store Global Descriptor Table Register</em>) e na <code>SLDT</code> ( <em>Store Local Descriptor Table</em> ) e é focado para detectar a presença da VMWare.
  </p>
  
  <p>
    É descrito como sendo uma &#8220;suíte&#8221; de instruções. Utiliza instruções que testam os IA32 <code>SIDT, SGDT, e SLDT</code>. É um teste semelhante à Red Pill, mas com menor portabilidade.
  </p>
  
  <p>
    A portabilidade também é prejudicada pelos testes de busca de hardware. O Scoopy-Doo busca pela presença de hardware virtualizado. Como os sistemas operacionais diferentes possuem forma de classificação de hardwares diferentes, deve-se ter versões de código alternativas para comunicação entre programa-SO.
  </p>
  
  <p>
    No Linux o scoopy-Doo busca no diretório /proc pela string &#8220;VmWare&#8221;, associando com os componentes de E/S, portas-padrão utilizadas pelas MV ( /proc/iomem, /proc/ioports, /proc/scsi/scsi ) e ainda tenta encontrar a presença de máquinas virtuais buscando processos específicos – analisando o retorno do comando dmesg.
  </p>
  
  <p>
    No Windows, procura por registros no sistema:
  </p>
  
  <p style="text-align: center;">
    HKEY_LOCAL_MACHINE\HARDWARE\DEVICEMAP\Scsi\Scsi Port
  </p>
  
  <p style="text-align: center;">
    0\Scsi Bus 0\Target Id 0\Logical Unit Id 0\Identifier
  </p>
  
  <p style="text-align: center;">
    HKEY_LOCAL_MACHINE\HARDWARE\DEVICEMAP\Scsi\Scsi Port
  </p>
  
  <p style="text-align: center;">
    1\Scsi Bus 0\Target Id 0\Logical Unit Id 0\Identifier
  </p>
  
  <p style="text-align: center;">
    HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\
  </p>
  
  <p style="text-align: center;">
    {4D36E968-E325-11CE-BFC1-08002BE10318}\0000\DriverDesc
  </p>
  
  <p style="text-align: center;">
    HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Class\
  </p>
  
  <p style="text-align: center;">
    {4D36E968-E325-11CE-BFC1-
  </p>
  
  <p style="text-align: center;">
    08002BE10318}\0000\ProviderName
  </p>
  
  <p>
    Segundo o autor possui maior garantia de se identificar o ambiente. sendo três testes pelo preço de um! Realmente, é muito eficiente, mas contribui como fator limitante à portabilidade do código usuário.
  </p>
  
  <p>
    A página do autor é: <a href="http://www.trapkit.de" target="_blank">http://www.trapkit.de</a> . Pode-se fazer o download dos fontes em: <a href="http://www.trapkit.de/research/vmm/scoopydoo/scoopy_doo.tar.gz">http://www.trapkit.de/research/vmm/scoopydoo/scoopy_doo.tar.gz</a> (Unix-like) ou <a href="http://www.trapkit.de/research/vmm/scoopydoo/scoopy_doo_win.zip">http://www.trapkit.de/research/vmm/scoopydoo/scoopy_doo_win.zip</a> (Windows).
  </p>
  
  <h3>
    5.2 VmDetect[ion]
  </h3>
  
  <p>
    Escrito por lallous (<a href="http://www.codeproject.com/script/Membership/Profiles.aspx?mid=139861" target="_blank">http://www.codeproject.com/script/Membership/Profiles.aspx?mid=139861</a>). Este código utiliza diferentes técnicas para detectar a presença das MV: VirtualPC e VmWare.
  </p>
  
  <p>
    VmDetect consiste em determinar se o código está sendo executado em uma VirtualPC tentando executar uma instrução não-padrão do set de instruções x86 emulados/usados pelo VirtualPC.
  </p>
  
  <p>
    Em uma máquina real o uso de uma instrução não-existente geraria um erro fatal na aplicação. O processador iria parar o programa e notificar o erro para o SO.
  </p>
  
  <p>
    Porém, é possível ao programador prever uma situação de erro através dos controle de exceções. Cria-se uma função que, se o erro ocorrer, retorna true, senão retorna falso.
  </p>
  
  <p>
    Essas funções são conhecidas como “error-handling code” e é este mecanismo que permite detectar a VirtualPC.
  </p>
  
  <p>
    É um código muito efetivo na detecção. Muito recomendado quando se quer restringir funcionalidades para uma MV específica (por exemplo, a Microsoft construindo produtos que só executam na sua VirtualPC). Todavia, possui pouquíssima portabilidade e é muito dependente de arquitetura.
  </p>
  
  <p>
    Os fontes e documentação podem ser encontrados em: <a href="http://www.codeproject.com/KB/system/VmDetect.aspx" target="_blank">http://www.codeproject.com/KB/system/VmDetect.aspx</a> .
  </p>
  
  <h3>
    5.3 The Jerry Code
  </h3>
  
  <p>
    De forma semelhante ao código da VmDetection, Jerry utiliza uma instrução não-padrão da arquitetura para testa a presença da máquina virtual.
  </p>
  
  <p>
    Também de autoria de Tobias Klein ( <a href="http://www.trapkit.de" target="_blank">http://www.trapkit.de</a> ), pode ser encontrado em <a href="http://www.trapkit.de/research/vmm/jerry/index.html" target="_blank">http://www.trapkit.de/research/vmm/jerry/index.html</a> .
  </p>
  
  <h3>
    5.4 ScoopyNg
  </h3>
  
  <p>
    Evolução do Jerry e do Scoopy Doo. Seu código pode ser encontrado em: <a href="http://www.trapkit.de/research/vmm/scoopyng/ScoopyNG.zip" target="_blank">http://www.trapkit.de/research/vmm/scoopyng/ScoopyNG.zip</a>
  </p>
  
  <h2>
    6. Conclusão
  </h2>
  
  <p>
    A detecção de máquinas virtuais é um grande passo para os programadores que querem proteger seu código de um processo de análise online ou restringir recursos por questões de segurança.
  </p>
  
  <p>
    Para um cracker é extremamente necessário saber da existência desses recursos para quando se deparar com código que &#8220;não se comporta como aparentemente deveria&#8221;. Uma das técnicas anti-cracking consiste neste tipo de detecção, antevendo os métodos de reversão.
  </p>
  
  <p>
    A detecção de MV pode ser somente o primeiro passo para se testar acessos à regiões de dados que supostamente deveria estar protegida pelo sistema operacional.
  </p>
  
  <p>
    Com o aumento crescente de recursos de hardware, a virtualização é um ramo da computação que vêm crescendo muito nesta última década. Com a crescente aceitação de sistemas operacionais livres coexistindo com Windows, a virtualização tende a estar cada dia mais presente entre os usuários comuns. Por isso se tornará mais e mais importante o uso de técnicas de detecção e, por conseqüência, anti-detecção de máquinas virtuais.
  </p>
