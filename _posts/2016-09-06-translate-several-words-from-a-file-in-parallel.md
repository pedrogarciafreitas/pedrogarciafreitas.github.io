---
id: 2096
title: Translate several words from a file in parallel
date: 2016-09-06T11:03:11+00:00
author: SAWP
excerpt: Translate several words from a file in parallel using google-translator-cli in BASH.
layout: post
guid: http://www.sawp.com.br/blog/?p=2096
permalink: p=2096
categories:
  - Miscellaneous
---
<pre>#!/bin/sh

function translate_line() {
    l=$(echo $1 | awk '{print tolower($0)}');
    echo -n "${l}:"; 
    echo `trans -no-auto -brief :en $l`;
} 
export -f translate_line
parallel --will-cite -k translate_line ::: `cat Lista-de-Palavras.txt`
</pre>
