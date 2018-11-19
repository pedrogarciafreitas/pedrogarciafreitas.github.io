---
id: 795
title: Implementação de um Algoritmo de Unificação em OCaml
date: 2010-10-25T14:02:14+00:00
author: SAWP
excerpt: A unificação é uma operação lógica que produz uma substituição de um termo em outro, identificando os termos ou fazendo a igualdade de condições utilizando alguma teoria equacional (no caso da unificação semântica). Neste post apresentamos e descrevemos uma implementação em OCaml do algoritmo de unificação de Robson.
layout: post
guid: http://www.sawp.com.br/blog/?p=795
permalink: /p=795
wp-syntax-cache-content:
  - |
    a:8:{i:1;s:1446:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">type</span> id    <span style="color: #a52a2a;">=</span> <span style="color: #06c; font-weight: bold;">string</span><span style="color: #a52a2a;">;;</span>
    <span style="color: #06c; font-weight: bold;">type</span> term<span style="color: #a52a2a;">'</span> <span style="color: #a52a2a;">=</span> Var<span style="color: #a52a2a;">'</span> <span style="color: #06c; font-weight: bold;">of</span> id <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">'</span> <span style="color: #06c; font-weight: bold;">of</span> term<span style="color: #a52a2a;">'</span> <span style="color: #a52a2a;">*</span> term<span style="color: #a52a2a;">';;</span>
    <span style="color: #06c; font-weight: bold;">type</span> term  <span style="color: #a52a2a;">=</span> Var <span style="color: #06c; font-weight: bold;">of</span> id <span style="color: #a52a2a;">|</span> Term <span style="color: #06c; font-weight: bold;">of</span> id <span style="color: #a52a2a;">*</span> term <span style="color: #06c; font-weight: bold;">list</span><span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">type id    = string;;
    type term' = Var' of id | Term' of term' * term';;
    type term  = Var of id | Term of id * term list;;</p></div>
    ;i:2;s:740:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">exception</span> UnificationError <span style="color: #06c; font-weight: bold;">of</span> <span style="color: #06c; font-weight: bold;">string</span><span style="color: #a52a2a;">;;</span>
    <span style="color: #06c; font-weight: bold;">exception</span> MatchError <span style="color: #06c; font-weight: bold;">of</span> <span style="color: #06c; font-weight: bold;">string</span><span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">exception UnificationError of string;;
    exception MatchError of string;;</p></div>
    ;i:3;s:2785:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> conv v <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> v <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> Var x               <span style="color: #a52a2a;">-&gt;</span> Var<span style="color: #a52a2a;">'</span> x
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">&#40;</span>x, <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#93;</span><span style="color: #a52a2a;">&#41;</span>         <span style="color: #a52a2a;">-&gt;</span> Var<span style="color: #a52a2a;">'</span> x
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">&#40;</span>a, <span style="color: #a52a2a;">&#91;</span>Var b<span style="color: #a52a2a;">&#93;</span><span style="color: #a52a2a;">&#41;</span>    <span style="color: #a52a2a;">-&gt;</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, Var<span style="color: #a52a2a;">'</span> b<span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">&#40;</span>a, <span style="color: #a52a2a;">&#91;</span>Var h<span style="color: #a52a2a;">;</span> t<span style="color: #a52a2a;">&#93;</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> h, conv t<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> _                   <span style="color: #a52a2a;">-&gt;</span> <span style="color: #06c; font-weight: bold;">raise</span> <span style="color: #a52a2a;">&#40;</span>MatchError <span style="color: #3cb371;">&quot;bad format expression&quot;</span><span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">let rec conv v =
    match v with
    | Var x               -&gt; Var' x
    | Term(x, [])         -&gt; Var' x
    | Term(a, [Var b])    -&gt; Term'(Var' a, Var' b)
    | Term(a, [Var h; t]) -&gt; Term'(Var' a, Term'(Var' h, conv t))
    | _                   -&gt; raise (MatchError &quot;bad format expression&quot;);;</p></div>
    ;i:4;s:1500:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> occurrences a v <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> v <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> Var<span style="color: #a52a2a;">'</span> b <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> b <span style="color: #a52a2a;">=</span> Var<span style="color: #a52a2a;">'</span> a<span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>f, subexpr<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#40;</span>occurrences a f<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">||</span> <span style="color: #a52a2a;">&#40;</span>occurrences a subexpr<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">let rec occurrences a v =
    match v with
    | Var' b -&gt; (Var' b = Var' a)
    | Term'(f, subexpr) -&gt; (occurrences a f) || (occurrences a subexpr);;</p></div>
    ;i:5;s:1769:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> substitute tm1 tm2 <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> tm2 <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">as</span> alpha <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#40;</span><span style="color: #06c; font-weight: bold;">try</span> <span style="color: #06c; font-weight: bold;">List</span><span style="color: #a52a2a;">.</span>assoc a tm1 <span style="color: #06c; font-weight: bold;">with</span> Not_found <span style="color: #a52a2a;">-&gt;</span> alpha<span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>t1, t2<span style="color: #a52a2a;">&#41;</span>     <span style="color: #a52a2a;">-&gt;</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>substitute tm1 t1, substitute tm1 t2<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">let rec substitute tm1 tm2 =
    match tm2 with
    | (Var' a) as alpha -&gt; (try List.assoc a tm1 with Not_found -&gt; alpha)
    | Term'(t1, t2)     -&gt; Term'(substitute tm1 t1, substitute tm1 t2);;</p></div>
    ;i:6;s:4646:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> coupling expr <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> expr <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>exp1, exp2<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">when</span> exp1 <span style="color: #a52a2a;">=</span> exp2 <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#93;</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span>
    <span style="color: #06c; font-weight: bold;">if</span> occurrences a <span style="color: #06c; font-weight: bold;">exp</span> <span style="color: #06c; font-weight: bold;">then</span>
    <span style="color: #06c; font-weight: bold;">raise</span> <span style="color: #a52a2a;">&#40;</span>UnificationError <span style="color: #3cb371;">&quot;not unifiable: circularity&quot;</span><span style="color: #a52a2a;">&#41;</span>
    <span style="color: #06c; font-weight: bold;">else</span>
    <span style="color: #a52a2a;">&#91;</span>a, <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#93;</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span><span style="color: #06c; font-weight: bold;">exp</span>, Var<span style="color: #a52a2a;">'</span> a<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span> coupling <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>s1 ,s2<span style="color: #a52a2a;">&#41;</span>, Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>t1 ,t2<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span>
    <span style="color: #06c; font-weight: bold;">let</span> s <span style="color: #a52a2a;">=</span> coupling <span style="color: #a52a2a;">&#40;</span>s1 ,t1<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">let</span> m1 <span style="color: #a52a2a;">=</span> coupling <span style="color: #a52a2a;">&#40;</span>substitute s s2 , substitute s t2<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">let</span> tail_subs <span style="color: #a52a2a;">&#40;</span>a, <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">=</span> <span style="color: #a52a2a;">&#40;</span>a, substitute m1 <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">List</span><span style="color: #a52a2a;">.</span>append <span style="color: #a52a2a;">&#40;</span><span style="color: #06c; font-weight: bold;">List</span><span style="color: #a52a2a;">.</span>map tail_subs s<span style="color: #a52a2a;">&#41;</span> m1<span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">let rec coupling expr =
    match expr with
    | (exp1, exp2) when exp1 = exp2 -&gt; []
    | (Var' a, exp) -&gt;
    if occurrences a exp then
    raise (UnificationError &quot;not unifiable: circularity&quot;)
    else
    [a, exp]
    | (exp, Var' a) -&gt; coupling (Var' a, exp)
    | (Term'(s1 ,s2), Term'(t1 ,t2)) -&gt;
    let s = coupling (s1 ,t1) in
    let m1 = coupling (substitute s s2 , substitute s t2) in
    let tail_subs (a, exp) = (a, substitute m1 exp) in
    List.append (List.map tail_subs s) m1;;</p></div>
    ;i:7;s:2126:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #06c; font-weight: bold;">let</span> unif e1 e2 <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">let</span> exp1 <span style="color: #a52a2a;">=</span> conv e1 <span style="color: #06c; font-weight: bold;">and</span>
    exp2 <span style="color: #a52a2a;">=</span> conv e2 <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">let</span> l <span style="color: #a52a2a;">=</span> coupling <span style="color: #a52a2a;">&#40;</span>exp1, exp2<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">match</span> l <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#40;</span>c, Var<span style="color: #a52a2a;">'</span> y<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#93;</span> <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#40;</span>c, Var<span style="color: #a52a2a;">'</span> y<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#93;</span>
    <span style="color: #a52a2a;">|</span> _ <span style="color: #a52a2a;">-&gt;</span> <span style="color: #06c; font-weight: bold;">raise</span> <span style="color: #a52a2a;">&#40;</span>UnificationError <span style="color: #3cb371;">&quot;not unifiable: head symbol conflict&quot;</span><span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">let unif e1 e2 =
    let exp1 = conv e1 and
    exp2 = conv e2 in
    let l = coupling (exp1, exp2) in
    match l with
    | [(c, Var' y)] -&gt; [(c, Var' y)]
    | _ -&gt; raise (UnificationError &quot;not unifiable: head symbol conflict&quot;);;</p></div>
    ;i:8;s:15409:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="ocaml" style="font-family:monospace;"><span style="color: #5d478b; font-style: italic;">(*
    * Another unification algorithm.
    *
    * Author: Pedro Garcia Freitas [sawp@sawp.com.br]
    *         http://www.sawp.com.br
    *
    *)</span>
    &nbsp;
    <span style="color: #5d478b; font-style: italic;">(*
    * Exception
    *)</span>
    <span style="color: #06c; font-weight: bold;">exception</span> UnificationError <span style="color: #06c; font-weight: bold;">of</span> <span style="color: #06c; font-weight: bold;">string</span><span style="color: #a52a2a;">;;</span>
    <span style="color: #06c; font-weight: bold;">exception</span> ListError <span style="color: #06c; font-weight: bold;">of</span> <span style="color: #06c; font-weight: bold;">string</span><span style="color: #a52a2a;">;;</span>
    <span style="color: #06c; font-weight: bold;">exception</span> MatchError <span style="color: #06c; font-weight: bold;">of</span> <span style="color: #06c; font-weight: bold;">string</span><span style="color: #a52a2a;">;;</span>
    &nbsp;
    <span style="color: #5d478b; font-style: italic;">(*
    * Abstract types
    *)</span>
    <span style="color: #06c; font-weight: bold;">type</span> id <span style="color: #a52a2a;">=</span> <span style="color: #06c; font-weight: bold;">string</span><span style="color: #a52a2a;">;;</span>
    <span style="color: #06c; font-weight: bold;">type</span> term<span style="color: #a52a2a;">'</span> <span style="color: #a52a2a;">=</span> Var<span style="color: #a52a2a;">'</span> <span style="color: #06c; font-weight: bold;">of</span> id <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">'</span> <span style="color: #06c; font-weight: bold;">of</span> term<span style="color: #a52a2a;">'</span> <span style="color: #a52a2a;">*</span> term<span style="color: #a52a2a;">';;</span>
    <span style="color: #06c; font-weight: bold;">type</span> term <span style="color: #a52a2a;">=</span> Var <span style="color: #06c; font-weight: bold;">of</span> id <span style="color: #a52a2a;">|</span> Term <span style="color: #06c; font-weight: bold;">of</span> id <span style="color: #a52a2a;">*</span> term <span style="color: #06c; font-weight: bold;">list</span><span style="color: #a52a2a;">;;</span>
    &nbsp;
    <span style="color: #5d478b; font-style: italic;">(*
    * Perform Substitution
    *)</span>
    &nbsp;
    <span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> substitute tm1 tm2 <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> tm2 <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">as</span> alpha <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#40;</span><span style="color: #06c; font-weight: bold;">try</span> <span style="color: #06c; font-weight: bold;">List</span><span style="color: #a52a2a;">.</span>assoc a tm1 <span style="color: #06c; font-weight: bold;">with</span> Not_found <span style="color: #a52a2a;">-&gt;</span> alpha<span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>t1 ,t2<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>substitute tm1 t1, substitute tm1 t2<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span>
    &nbsp;
    <span style="color: #5d478b; font-style: italic;">(*
    * Check Occurrences of a variable in a expression
    *)</span>
    <span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> occurrences a v <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> v <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> Var<span style="color: #a52a2a;">'</span> b <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> b <span style="color: #a52a2a;">=</span> Var<span style="color: #a52a2a;">'</span> a<span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>f, subexpr<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#40;</span>occurrences a f<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">||</span> <span style="color: #a52a2a;">&#40;</span>occurrences a subexpr<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span>
    &nbsp;
    <span style="color: #5d478b; font-style: italic;">(*
    * Convert the term to term'
    *)</span>
    <span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> conv v <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> v <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> Var x               <span style="color: #a52a2a;">-&gt;</span> Var<span style="color: #a52a2a;">'</span> x
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">&#40;</span>x, <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#93;</span><span style="color: #a52a2a;">&#41;</span>         <span style="color: #a52a2a;">-&gt;</span> Var<span style="color: #a52a2a;">'</span> x
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">&#40;</span>a,<span style="color: #a52a2a;">&#91;</span>Var b<span style="color: #a52a2a;">&#93;</span><span style="color: #a52a2a;">&#41;</span>     <span style="color: #a52a2a;">-&gt;</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, Var<span style="color: #a52a2a;">'</span> b<span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> Term<span style="color: #a52a2a;">&#40;</span>a, <span style="color: #a52a2a;">&#91;</span>Var h<span style="color: #a52a2a;">;</span> t<span style="color: #a52a2a;">&#93;</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span> Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> h, conv t<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> _                   <span style="color: #a52a2a;">-&gt;</span> <span style="color: #06c; font-weight: bold;">raise</span> <span style="color: #a52a2a;">&#40;</span>MatchError <span style="color: #3cb371;">&quot;bad format expression&quot;</span><span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span>
    &nbsp;
    <span style="color: #5d478b; font-style: italic;">(*
    * Verify coupling variables and sub-expression from one to another
    *)</span>
    <span style="color: #06c; font-weight: bold;">let</span> <span style="color: #06c; font-weight: bold;">rec</span> coupling expr <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">match</span> expr <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>exp1, exp2<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">when</span> exp1 <span style="color: #a52a2a;">=</span> exp2 <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#93;</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span>
    <span style="color: #06c; font-weight: bold;">if</span> occurrences a <span style="color: #06c; font-weight: bold;">exp</span> <span style="color: #06c; font-weight: bold;">then</span>
    <span style="color: #06c; font-weight: bold;">raise</span> <span style="color: #a52a2a;">&#40;</span>UnificationError <span style="color: #3cb371;">&quot;not unifiable: circularity&quot;</span><span style="color: #a52a2a;">&#41;</span>
    <span style="color: #06c; font-weight: bold;">else</span>
    <span style="color: #a52a2a;">&#91;</span>a, <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#93;</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span><span style="color: #06c; font-weight: bold;">exp</span>, Var<span style="color: #a52a2a;">'</span> a<span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span> coupling <span style="color: #a52a2a;">&#40;</span>Var<span style="color: #a52a2a;">'</span> a, <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#40;</span>Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>s1 ,s2<span style="color: #a52a2a;">&#41;</span>, Term<span style="color: #a52a2a;">'</span><span style="color: #a52a2a;">&#40;</span>t1 ,t2<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">-&gt;</span>
    <span style="color: #06c; font-weight: bold;">let</span> s <span style="color: #a52a2a;">=</span> coupling<span style="color: #a52a2a;">&#40;</span>s1 ,t1<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">let</span> m1 <span style="color: #a52a2a;">=</span> coupling<span style="color: #a52a2a;">&#40;</span>substitute s s2 , substitute s t2<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">let</span> tail_subs <span style="color: #a52a2a;">&#40;</span>a,<span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #a52a2a;">=</span> <span style="color: #a52a2a;">&#40;</span>a,substitute m1 <span style="color: #06c; font-weight: bold;">exp</span><span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">List</span><span style="color: #a52a2a;">.</span>append <span style="color: #a52a2a;">&#40;</span><span style="color: #06c; font-weight: bold;">List</span><span style="color: #a52a2a;">.</span>map tail_subs s<span style="color: #a52a2a;">&#41;</span> m1<span style="color: #a52a2a;">;;</span>
    &nbsp;
    <span style="color: #5d478b; font-style: italic;">(*
    * Unify using coupling
    *)</span>
    <span style="color: #06c; font-weight: bold;">let</span> unif e1 e2 <span style="color: #a52a2a;">=</span>
    <span style="color: #06c; font-weight: bold;">let</span> exp1 <span style="color: #a52a2a;">=</span> conv e1 <span style="color: #06c; font-weight: bold;">and</span>
    exp2 <span style="color: #a52a2a;">=</span> conv e2 <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">let</span> l <span style="color: #a52a2a;">=</span> coupling <span style="color: #a52a2a;">&#40;</span>exp1, exp2<span style="color: #a52a2a;">&#41;</span> <span style="color: #06c; font-weight: bold;">in</span>
    <span style="color: #06c; font-weight: bold;">match</span> l <span style="color: #06c; font-weight: bold;">with</span>
    <span style="color: #a52a2a;">|</span> <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#40;</span>c, Var<span style="color: #a52a2a;">'</span> y<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#93;</span> <span style="color: #a52a2a;">-&gt;</span> <span style="color: #a52a2a;">&#91;</span><span style="color: #a52a2a;">&#40;</span>c, Var<span style="color: #a52a2a;">'</span> y<span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">&#93;</span>
    <span style="color: #a52a2a;">|</span> _ <span style="color: #a52a2a;">-&gt;</span> <span style="color: #06c; font-weight: bold;">raise</span> <span style="color: #a52a2a;">&#40;</span>UnificationError <span style="color: #3cb371;">&quot;not unifiable: head symbol conflict&quot;</span><span style="color: #a52a2a;">&#41;</span><span style="color: #a52a2a;">;;</span></pre></td></tr></table><p class="theCode" style="display:none;">(*
    * Another unification algorithm.
    *
    * Author: Pedro Garcia Freitas [sawp@sawp.com.br]
    *         http://www.sawp.com.br
    *
    *)
    
    (*
    * Exception
    *)
    exception UnificationError of string;;
    exception ListError of string;;
    exception MatchError of string;;
    
    (*
    * Abstract types
    *)
    type id = string;;
    type term' = Var' of id | Term' of term' * term';;
    type term = Var of id | Term of id * term list;;
    
    (*
    * Perform Substitution
    *)
    
    let rec substitute tm1 tm2 =
    match tm2 with
    | (Var' a) as alpha -&gt; (try List.assoc a tm1 with Not_found -&gt; alpha)
    | Term'(t1 ,t2) -&gt; Term'(substitute tm1 t1, substitute tm1 t2);;
    
    (*
    * Check Occurrences of a variable in a expression
    *)
    let rec occurrences a v =
    match v with
    | Var' b -&gt; (Var' b = Var' a)
    | Term'(f, subexpr) -&gt; (occurrences a f) || (occurrences a subexpr);;
    
    (*
    * Convert the term to term'
    *)
    let rec conv v =
    match v with
    | Var x               -&gt; Var' x
    | Term(x, [])         -&gt; Var' x
    | Term(a,[Var b])     -&gt; Term'(Var' a, Var' b)
    | Term(a, [Var h; t]) -&gt; Term'(Var' a, Term'(Var' h, conv t))
    | _                   -&gt; raise (MatchError &quot;bad format expression&quot;);;
    
    (*
    * Verify coupling variables and sub-expression from one to another
    *)
    let rec coupling expr =
    match expr with
    | (exp1, exp2) when exp1 = exp2 -&gt; []
    | (Var' a, exp) -&gt;
    if occurrences a exp then
    raise (UnificationError &quot;not unifiable: circularity&quot;)
    else
    [a, exp]
    | (exp, Var' a) -&gt; coupling (Var' a, exp)
    | (Term'(s1 ,s2), Term'(t1 ,t2)) -&gt;
    let s = coupling(s1 ,t1) in
    let m1 = coupling(substitute s s2 , substitute s t2) in
    let tail_subs (a,exp) = (a,substitute m1 exp) in
    List.append (List.map tail_subs s) m1;;
    
    (*
    * Unify using coupling
    *)
    let unif e1 e2 =
    let exp1 = conv e1 and
    exp2 = conv e2 in
    let l = coupling (exp1, exp2) in
    match l with
    | [(c, Var' y)] -&gt; [(c, Var' y)]
    | _ -&gt; raise (UnificationError &quot;not unifiable: head symbol conflict&quot;);;</p></div>
    ";}
categories:
  - Miscellaneous
---
## Introdução 

Unificação é um processo utilizado em lógica que consiste em atribuir valores para variáveis de diferentes expressões para testar se uma expressão pode ser substituída em outra. Isto é, se existe uma substituição $$\sigma $$ atuando em um conjunto finito de termos $$S $$ tal que $$ S \overrightarrow{\sigma} U $$ , onde $$U $$ é um conjunto unitário. 

Em uma expressão unificável $P$ existe duas expressões $$Y $$ e $$f(X) $$, tal que exista $$P(f(X)) $$ e $$P(Y) $$ que possuam equivalência. Por exemplo, para unificarmos as expressões $$f(g(X),Y) $$ e $$f(g(a),X) $$, precisamos de $$X = a $$ e $$Y = a $$ . Desta maneira, ambos termos são $$f(g(a),a) $$ , sendo esta última expressão a forma mais reduzida, uma vez que impossível de se unificar $$g(a) $$ e $$a $$. 

Para verificar se uma expressão é unificável, nosso programa verifica a relação de tipos entre sub-expressões, obedecendo as seguintes definições:

  1. Termos são expressões construídas a partir de constantes, variáveis e símbolos funcionais de aridade finita:
          
    <center>
      <tt>$$t ::= c~|~x~|~f(t_1, t_2, \ldots,t_n) $$</tt>
    </center>

  2. Uma substituição $$\sigma $$ é um conjunto $${v\_1/t\_1, v\_2/t\_2, \ldots, v\_n/t\_n} $$ , onde cada variável $$v\_i $$ é distinta das outras e cada $$t\_i $$ é um termo distinto de $$v\_i $$ . Chamamos de ligação da substituição $$v\_i/t_i $$. 
  3. Para dois conjuntos distintos de substituições
          
    <center>
      $$\theta = \{u_1/s_1, \ldots, u_m/s_m\} $$
    </center>
    
    
  
    e
          
    <center>
      $$\sigma = \{v_1/t_1, \ldots, v_n/t_n\} $$
    </center>
    
    
  
    uma composição $$\theta\sigma $$ é a substituição obtida do conjunto $$\{u\_1/s\_1\sigma, \ldots, u\_m/s\_m\sigma, v\_1/t\_1, \ldots, v\_n/t\_n\} $$ eliminando qualquer ligação $$u\_i/s\_i\sigma $$ , para qual $$u\_i = s\_i\sigma $$ e qualquer ligação $$v\_j/t\_j $$ para qual $$v\_j \in \{u\_1, \ldots, u_m\} $$ . 
  4. Seja $$S $$ um conjunto finito de termos. Uma substituição $$\theta $$ é denominada um unificador de $$S $$ se $$S\theta $$ for um **conjunto unitário**. 
  5. Um unificador $$\theta $$ para um conjunto finito $$S $$ de termos é denominado um **unificador mais geral** de $$S $$ se $$\forall $$ unificador de $$\sigma $$ de $$S $$ $$\exists $$ uma substituição $$\gamma $$ tal que $$\sigma = \theta\gamma $$ . 
  6. Seja $$S $$ um conjunto finito de termos. O conjunto de conflitos de $$S $$ consiste dos sub-termos mais a esquerda dos termos de $$S $$ que se diferenciam. 

&nbsp;

## Algoritmo 

A existência das definições anteriores são verificadas pelo seguinte algoritmo:

**Inicio**

> > $$k := 0 $$
    
> > $$\sigma_k = \varepsilon $$
    
> > **Enquanto** $$S ~ \sigma_k ~ nao ~ unitario $$ **repita:**
> > 
> > > Seja $$D $$ o conjunto de conflitos de $$S \sigma_k $$
      
> > > **Se** $$\exists ~ v,t \in D $$ com $$v $$ variavel, $$t $$ termos sem ocorrencias de $$v $$ **Entao**
> > > 
> > > > $$\sigma\_{k+1} := \sigma\_k{v/t} $$ 
> > > 
> > > **Senão**
> > > 
> > > > reporte que $$S $$ não unificável e saia 
> > 
> > $$k := k + 1 $$ 
> 
> retorna $$\sigma_k $$, o unificador de $$S $$ 

**Fim**

&nbsp;

## Implementação 

### Os tipos 

Para representarmos uma expressão qualquer, precisamos definir um tipo abstrato. No nosso programa, definimos três tipos: 

<div>
  <pre lang="ocaml">type id    = string;;
type term' = Var' of id | Term' of term' * term';;
type term  = Var of id | Term of id * term list;;    </pre>
</div>

onde
    


  * $$id$$ é o tipo fundamental da menor sub-expressão possível. Este tipo pode ser visto como valores de variáveis. 
  * $$term&#8217;$$ é o tipo que representa uma expressão. No caso, este expressão pode ser uma variável</p> 
      * $$Var&#8217;$$ é associado com valores do tipo &#8220;id&#8221;, ou então uma sub-expressão composta por dois sub-termos deste tipo. 
  * $$term$$ é um tipo que foi definido apenas para receber uma entrada de expressões contendo a interface proposta para este trabalho. 

Podemos notar que o tipo $$term&#8217; $$ é definido recursivamente e gerará uma _árvore binária_ com nós não-marcados. Isso serve para o programa armazenar nas folhas os termos mais simples, que serão as variáveis. Desta maneira, podemos comparar em cada sub-árvore as regras necessárias para haver unificação. 

&nbsp;

### As exceções 

Nosso programa prevê dois possíveis erros durante a execução:

  * _Erro na unificação_: Quando avalia uma sub-expressão e ela não obedece aos requisitos para unificação. 
  * _Erro de conformidade_: Quando uma expressão de entrada é mal-formada. Ou seja, ela não corresponde à uma expressão avaliável. 

Tais exceções são definidas em Ocaml como: 

<div>
  <pre lang="ocaml">exception UnificationError of string;;
exception MatchError of string;;</pre>
</div></p> 

&nbsp;

### Conversão de tipos

Para este trabalho, foi proposto que a entrada de uma expressão deveria ser composta de um termo composto por uma _string_ e uma lista formada por uma variável e um sub-termo com a mesma definição. Por exemplo:
    


<center>
  <br /> $$Term(&#8220;f&#8221;, [Var &#8220;x&#8221;; Term(&#8220;g&#8221;, [Var &#8220;y&#8221;])])$$<br />
</center>

Embora esta notação seja simples, ela não pode ser utilizada diretamente em nossa implementação, uma vez que a abordagem escolhida para avaliação consiste em comparar sub-expressões de tipo iguais. Sendo assim, a expressão válida para as funções do nosso programa precisariam ser escritas da forma
    


<center>
  <br /> $$Term'(Var&#8217; &#8220;f&#8221;, Term'(Var&#8217; &#8220;x&#8221;, Term'(Var&#8217; &#8220;g&#8221;, Term'(Var&#8217; &#8220;y&#8221;))))$$<br />
</center>


    
que é menos conveniente para leitura do ser humano. 

Sendo assim, segue abaixo a função que faz a conversão da primeira forma para a segunda: 

<div>
  <pre lang="ocaml">let rec conv v =
  match v with
    | Var x               -> Var' x
    | Term(x, [])         -> Var' x
    | Term(a, [Var b])    -> Term'(Var' a, Var' b)
    | Term(a, [Var h; t]) -> Term'(Var' a, Term'(Var' h, conv t))
    | _                   -> raise (MatchError "bad format expression");;</pre>
</div>

Nesta função podemos notar que o tipo básico de ambos os casos (variáveis) possuem equivalência em qualquer uma das formas. 

Além disso, as constantes &#8212; denotadas por $$Term(x, [])$$ &#8212; são tratadas como variáveis pelas funções relacionadas à unificação. 

Os demais termos são definidos e convertidos recursivamente ou geram um erro se forem expressões mal-formadas. 

&nbsp;

### Busca de ocorrências 

Antes de reavaliar uma unificação de sub-termos, nosso programa verifica se ocorre situações de conflitos entre elas. O primeiro destes conflitos ocorre quando termos uma expressão $$X $$ e outra expressão $$f(X) $$ . A substituição $$X=f(X) $$ não é unificável por gerar um conflito conhecido como dependência cíclica ou circularidade. 

Assim, para uma variável $$a $$ e uma expressão qualquer $$v $$ , o programa busca se esta variável ocorre em alguma sub-expressão de $$v $$ através da seguinte função: 

<div>
  <pre lang="ocaml">let rec occurrences a v =
  match v with
    | Var' b -> (Var' b = Var' a)
    | Term'(f, subexpr) -> (occurrences a f) || (occurrences a subexpr);;</pre>
</div>

A expressão $$v $$ é sempre formada por uma variável ou por composições de &#8212; $$f $$ e $$subexpr $$ . Assim, a chamada recursiva presente na última linha garante que todos sub-termos da expressão original serão verificados. Ainda nessa linha, observamos que a operação lógica _ou_ retornará _verdadeiro_ se houver ao menos uma ocorrência da variável testada. Assim, a função retorna _verdadeiro_ sempre que houver uma condição de dependência circular nas expressões unificadas. 

&nbsp;

### Substituição 

A função de substituição procura a ocorrência de um termo na expressão e troca este termo por outro. Como o unificador só existe se houver uma substituição que transforme o conjunto de termos, esta função é fundamental para o funcionamento do programa. 

A substituição é implementada de forma a procurar a ocorrência da variável $$a $$ em uma sub-expressão $$tm1 $$ . Para isso, utilizamos a função $$List.assoc $$, que retorna o valor associado à chave $$a $$ em uma lista associativa. Caso não haja ocorrência desta variável na expressão, ela é retornada pela função. Tal função é apresentada abaixo:

<div>
  <pre lang="ocaml">let rec substitute tm1 tm2 =
  match tm2 with
    | (Var' a) as alpha -> (try List.assoc a tm1 with Not_found -> alpha)
    | Term'(t1, t2)     -> Term'(substitute tm1 t1, substitute tm1 t2);;</pre>
</div>

O comportamento explicado anteriormente é repetido recursivamente, substituindo-se os termos mais simples nas expressões compostas, como observamos pela última linha. 

&nbsp;

### Acoplamento

A primeira parte do algoritmo de unificação é implementada na função chamada $$coupling $$. Este função recebe uma dupla de expressões e faz os seguintes testes:

  1. Verifica se duas expressões são idênticas. Caso sejam, retorna uma lista vazia, uma vez que não há unificação de uma expressão por ela mesmo. 
  2. Verifica ocorrências de uma variável $$a $$ em uma expressão $$exp $$ . Se este caso aparece, então ocorre _circularidade_ e não ocorre unificação (primeiro $$UnificationError$$). 
  3. Se os casos acima não ocorrerem, então ambas expressões são formadas por termos compostos por mais de uma simples variável. Para esta situação, a função $$coupling $$ tenta substituir a primeira na segunda e fazer as verificações anteriores recursivamente. 

Segue a implementação dos passos descritos:

<div>
  <pre lang="ocaml">let rec coupling expr =
  match expr with
    | (exp1, exp2) when exp1 = exp2 -> []
    | (Var' a, exp) -> 
        if occurrences a exp then
          raise (UnificationError "not unifiable: circularity")
        else
          [a, exp]
    | (exp, Var' a) -> coupling (Var' a, exp)
    | (Term'(s1 ,s2), Term'(t1 ,t2)) ->
        let s = coupling (s1 ,t1) in
        let m1 = coupling (substitute s s2 , substitute s t2) in
        let tail_subs (a, exp) = (a, substitute m1 exp) in
          List.append (List.map tail_subs s) m1;;</pre>
</div>

&nbsp;

### Unificação 

A função $$unif$$ consiste apenas em:

  1. receber duas expressões distintas $$e1 $$ e $$e2 $$ , 
  2. convertê-las para o formato utilizado pelas outras funções, 
  3. verificar o resultado do acoplamento entre elas, 
  4. e decidir se há uma substituição possível de uma expressão em outra. Caso isso não ocorra, então a unificação não é possível (segundo $$UnificationError$$). 

Esta função é implementada como

<div>
  <pre lang="ocaml">let unif e1 e2 =
  let exp1 = conv e1 and
      exp2 = conv e2 in
  let l = coupling (exp1, exp2) in
    match l with
      | [(c, Var' y)] -> [(c, Var' y)] 
      | _ -> raise (UnificationError "not unifiable: head symbol conflict");;</pre>
</div>

&nbsp;

## Resultados 

A implementação foi testada para os três casos: duas expressões válidas e unificáveis, para o caso trivial de circularidade e para duas expressões não unificáveis. 

Para funções unificáveis:

> `# unif (Term("f",[Var "x"; Term("g",[Var "y"])]))<br />
       (Term("f",[Var "x"; Term("g",[Var "x"])]));;<br />
- : (id * term') list = [("y", Var' "x")]<br />
` 

Para funções não-unificáveis:

> `# unif (Term("f",[Var "x"; Term("g",[Var "y"])]))<br />
       (Term("f",[Var "x"; Term("f",[Var "x"])]));;</p>
<p>Exception: UnificationError "not unifiable: head symbol conflict".` 

Para condições de circularidade:

> `# unif (Var "x") (Term("f", [Var "x"]));;</p>
<p>Exception: UnificationError "not unifiable: circularity".`

&nbsp;

## Conclusão 

Esta implementação utiliza uma abordagem elegante e eficiente, consistindo em um conjunto pequeno de funções para abranger todos os casos possíveis do algoritmo de Robson. 

Como trabalho futuro, podemos modificá-la para utilizar apenas uma estrutura de dados na representação dos termos. Se fizermos isto sem aumentar o tamanho das funções, podemos ter um código ainda mais conciso e eficiente. 

&nbsp;

## Código Completo

<div>
  <pre lang="ocaml">(*
 * Another unification algorithm.
 *
 * Author: Pedro Garcia Freitas [sawp@sawp.com.br]
 *         http://www.sawp.com.br
 *
 *)

(*
 * Exception
 *)
exception UnificationError of string;;
exception ListError of string;;
exception MatchError of string;;

(*
 * Abstract types
 *)
type id = string;;
type term' = Var' of id | Term' of term' * term';;
type term = Var of id | Term of id * term list;;

(*
 * Perform Substitution
 *)

let rec substitute tm1 tm2 =
  match tm2 with
    | (Var' a) as alpha -> (try List.assoc a tm1 with Not_found -> alpha)
    | Term'(t1 ,t2) -> Term'(substitute tm1 t1, substitute tm1 t2);;

(*
 * Check Occurrences of a variable in a expression
 *)
let rec occurrences a v =
  match v with
    | Var' b -> (Var' b = Var' a)
    | Term'(f, subexpr) -> (occurrences a f) || (occurrences a subexpr);;

(*
 * Convert the term to term'
 *)
let rec conv v =
  match v with
    | Var x               -> Var' x
    | Term(x, [])         -> Var' x
    | Term(a,[Var b])     -> Term'(Var' a, Var' b)
    | Term(a, [Var h; t]) -> Term'(Var' a, Term'(Var' h, conv t))
    | _                   -> raise (MatchError "bad format expression");;

(*
 * Verify coupling variables and sub-expression from one to another
 *)
let rec coupling expr =
  match expr with
    | (exp1, exp2) when exp1 = exp2 -> []
    | (Var' a, exp) -> 
        if occurrences a exp then
          raise (UnificationError "not unifiable: circularity")
        else
          [a, exp]
    | (exp, Var' a) -> coupling (Var' a, exp)
    | (Term'(s1 ,s2), Term'(t1 ,t2)) ->
        let s = coupling(s1 ,t1) in
        let m1 = coupling(substitute s s2 , substitute s t2) in
        let tail_subs (a,exp) = (a,substitute m1 exp) in
          List.append (List.map tail_subs s) m1;;

(*
 * Unify using coupling
 *)
let unif e1 e2 =
  let exp1 = conv e1 and
      exp2 = conv e2 in
  let l = coupling (exp1, exp2) in
    match l with
      | [(c, Var' y)] -> [(c, Var' y)] 
      | _ -> raise (UnificationError "not unifiable: head symbol conflict");;</pre>
</div>

Disponível em <a target="_blank" href="http://sawp.com.br/code/general/unif.ml">http://sawp.com.br/code/general/unif.ml</a> 

<fieldset>
  <legend> 
  
  <h2>
    Referências
  </h2></legend> 
  
  <ul>
    <li>
      <a name="bibitemkikey"><b>[kikey]</b> Jason Hickey. &#8220;Introduction to Objective Caml&#8221;. 2008. </a>
    </li>
    <li>
      <a name="bibitemHarrison"> <b>[Harrison]</b> John Harrison. &#8220;Introduction to Functional Programming&#8221;. 1998. </a>
    </li>
    <li>
      <a href="http://en.wikipedia.org/wiki/Unification_(computing)" target="_blank">http://en.wikipedia.org/wiki/Unification_(computing)</a>
    </li>
  </ul>
</fieldset>
