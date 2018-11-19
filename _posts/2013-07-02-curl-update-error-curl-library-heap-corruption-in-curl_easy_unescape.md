---
id: 2057
title: 'cURL update error: cURL library &#8212; heap corruption in curl_easy_unescape.'
date: 2013-07-02T09:33:38+00:00
author: SAWP
excerpt: How to force the build/upgrade cURL on FreeBSD.
layout: post
guid: http://www.sawp.com.br/blog/?p=2057
permalink: /p=2057
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:1439:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">===<span style="color: #000000; font-weight: bold;">&gt;</span>  curl-7.24.0_3 has known vulnerabilities:
    Affected package: curl-7.24.0_3
    Type of problem: cURL library <span style="color: #660033;">--</span> heap corruption <span style="color: #000000; font-weight: bold;">in</span> curl_easy_unescape.
    Reference: http:<span style="color: #000000; font-weight: bold;">//</span>portaudit.FreeBSD.org<span style="color: #000000; font-weight: bold;">/</span>01cf67b3-dc3b-11e2-a6cd-c48508086173.html
    =<span style="color: #000000; font-weight: bold;">&gt;</span> Please update your ports <span style="color: #c20cb9; font-weight: bold;">tree</span> and try again.
    <span style="color: #000000; font-weight: bold;">***</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span>check-vulnerable<span style="color: #7a0874; font-weight: bold;">&#93;</span> Error code <span style="color: #000000;">1</span></pre></td></tr></table><p class="theCode" style="display:none;">===&gt;  curl-7.24.0_3 has known vulnerabilities:
    Affected package: curl-7.24.0_3
    Type of problem: cURL library -- heap corruption in curl_easy_unescape.
    Reference: http://portaudit.FreeBSD.org/01cf67b3-dc3b-11e2-a6cd-c48508086173.html
    =&gt; Please update your ports tree and try again.
    *** [check-vulnerable] Error code 1</p></div>
    ;i:2;s:701:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">make</span> <span style="color: #660033;">-C</span> <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>ports<span style="color: #000000; font-weight: bold;">/</span>ftp<span style="color: #000000; font-weight: bold;">/</span>curl <span style="color: #007800;">DISABLE_VULNERABILITIES</span>=<span style="color: #000000;">1</span></pre></td></tr></table><p class="theCode" style="display:none;">make -C /usr/ports/ftp/curl DISABLE_VULNERABILITIES=1</p></div>
    ;i:3;s:454:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">portmaster <span style="color: #660033;">-m</span> <span style="color: #ff0000;">&quot;DISABLE_VULNERABILITIES=1&quot;</span> ftp<span style="color: #000000; font-weight: bold;">/</span>curl</pre></td></tr></table><p class="theCode" style="display:none;">portmaster -m &quot;DISABLE_VULNERABILITIES=1&quot; ftp/curl</p></div>
    ";}
categories:
  - FreeBSD
---
If you want to update the cURL and is experiencing the following error:

<pre lang="bash">===>  curl-7.24.0_3 has known vulnerabilities:
Affected package: curl-7.24.0_3
Type of problem: cURL library -- heap corruption in curl_easy_unescape.
Reference: http://portaudit.FreeBSD.org/01cf67b3-dc3b-11e2-a6cd-c48508086173.html
=> Please update your ports tree and try again.
*** [check-vulnerable] Error code 1
</pre>

Try:

<pre lang="bash">make -C /usr/ports/ftp/curl DISABLE_VULNERABILITIES=1
</pre>

or if you are using <tt>portmaster</tt>:

<pre lang="bash">portmaster -m "DISABLE_VULNERABILITIES=1" ftp/curl
</pre>
