---
id: 1689
title: Kurose’s book exercises (labs) — HTTP Proxy Cache
date: 2012-07-27T16:31:04+00:00
author: SAWP
excerpt: A caching proxy server accelerates service requests by retrieving content saved from a previous request made by the same client or even other clients. Caching proxies keep local copies of frequently requested resources, allowing large organizations to significantly reduce their upstream bandwidth usage and costs, while significantly increasing performance. In this post we shows a Proxy Cache implemented in Scala language.
layout: post
guid: http://www.sawp.com.br/blog/?p=1689
permalink: /p=1689
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:11020:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> HttpResponse<span style="color: #F78811;">&#40;</span>fromServer<span style="color: #000080;">:</span> DataInputStream<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> version <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> status <span style="color: #000080;">=</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> statusLine <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> headers <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> body <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Array<span style="color: #F78811;">&#91;</span>Byte<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>Configs.<span style="color: #000000;">MAX_OBJECT_SIZE</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> length <span style="color: #000080;">=</span> -<span style="color: #F78811;">1</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> line <span style="color: #000080;">=</span> fromServer.<span style="color: #000000;">readLine</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> gotStatusLine <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>line.<span style="color: #000000;">length</span> <span style="color: #000080;">!=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span><span style="color: #000080;">!</span>gotStatusLine<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    statusLine <span style="color: #000080;">=</span> line
    gotStatusLine <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #F78811;">&#123;</span>
    headers +<span style="color: #000080;">=</span> line + Configs.<span style="color: #000000;">CRLF</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>line.<span style="color: #000000;">startsWith</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Content-Length:&quot;</span><span style="color: #F78811;">&#41;</span> ||
    line.<span style="color: #000000;">startsWith</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Content-length:&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> tmp <span style="color: #000080;">=</span> line.<span style="color: #000000;">split</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot; &quot;</span><span style="color: #F78811;">&#41;</span>
    length <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    <span style="color: #F78811;">&#125;</span>
    line <span style="color: #000080;">=</span> fromServer.<span style="color: #000000;">readLine</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error reading headers from server: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> bytesRead <span style="color: #000080;">=</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> buf <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Array<span style="color: #F78811;">&#91;</span>Byte<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>Configs.<span style="color: #000000;">BUF_SIZE</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> loop <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>length <span style="color: #000080;">==</span> -<span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    loop <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    breakable <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>bytesRead <span style="color: #000080;">&lt;</span> length || loop<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> res <span style="color: #000080;">=</span> fromServer.<span style="color: #000000;">read</span><span style="color: #F78811;">&#40;</span>buf, <span style="color: #F78811;">0</span>, Configs.<span style="color: #000000;">BUF_SIZE</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>res <span style="color: #000080;">==</span> <span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    break
    <span style="color: #0000ff; font-weight: bold;">var</span> i <span style="color: #000080;">=</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">&lt;</span> res <span style="color: #000080;">&amp;&amp;</span> <span style="color: #F78811;">&#40;</span>i + bytesRead<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&lt;</span> Configs.<span style="color: #000000;">MAX_OBJECT_SIZE</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    body<span style="color: #F78811;">&#40;</span>bytesRead + i<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> buf<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span>
    i +<span style="color: #000080;">=</span> <span style="color: #F78811;">1</span>
    <span style="color: #F78811;">&#125;</span>
    bytesRead +<span style="color: #000080;">=</span> res
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error reading headers from body: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> toString <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> res <span style="color: #000080;">=</span> statusLine + Configs.<span style="color: #000000;">CRLF</span> + headers + Configs.<span style="color: #000000;">CRLF</span>
    res
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class HttpResponse(fromServer: DataInputStream) {
    var version = &quot;&quot;
    var status = 0
    var statusLine = &quot;&quot;
    var headers = &quot;&quot;
    var body = new Array[Byte](Configs.MAX_OBJECT_SIZE)
    var length = -1
    try {
    var line = fromServer.readLine
    var gotStatusLine = false
    while (line.length != 0) {
    if (!gotStatusLine) {
    statusLine = line
    gotStatusLine = true
    } else {
    headers += line + Configs.CRLF
    }
    if (line.startsWith(&quot;Content-Length:&quot;) ||
    line.startsWith(&quot;Content-length:&quot;)) {
    val tmp = line.split(&quot; &quot;)
    length = tmp(1).toInt
    }
    line = fromServer.readLine
    }
    } catch {
    case e: IOException =&gt;
    println(&quot;Error reading headers from server: &quot; + e)
    }
    try {
    var bytesRead = 0
    var buf = new Array[Byte](Configs.BUF_SIZE)
    var loop = false
    if (length == -1)
    loop = true
    breakable {
    while (bytesRead &lt; length || loop) {
    val res = fromServer.read(buf, 0, Configs.BUF_SIZE)
    if (res == 1)
    break
    var i = 0
    while (i &lt; res &amp;&amp; (i + bytesRead) &lt; Configs.MAX_OBJECT_SIZE) {
    body(bytesRead + i) = buf(i)
    i += 1
    }
    bytesRead += res
    }
    }
    } catch {
    case e: IOException =&gt;
    println(&quot;Error reading headers from body: &quot; + e)
    }
    
    override def toString = {
    val res = statusLine + Configs.CRLF + headers + Configs.CRLF
    res
    }
    }</p></div>
    ;i:2;s:10773:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> HttpRequest<span style="color: #F78811;">&#40;</span>from<span style="color: #000080;">:</span> BufferedReader<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">var</span> method <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">var</span> URI <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">var</span> version <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">var</span> headers <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">var</span> <span style="color: #000080;">_</span>host <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">var</span> <span style="color: #000080;">_</span>port <span style="color: #000080;">=</span> Configs.<span style="color: #000000;">HTTP_PORT</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> firstLine <span style="color: #000080;">=</span> from.<span style="color: #000000;">readLine</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> tmp <span style="color: #000080;">=</span> firstLine.<span style="color: #000000;">split</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot; &quot;</span><span style="color: #F78811;">&#41;</span>
    method <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    URI <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    version <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error reading request line: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;URI:&quot;</span> + URI<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span><span style="color: #000080;">!</span><span style="color: #F78811;">&#40;</span>method equals <span style="color: #6666FF;">&quot;GET&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error: Method not GET&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> line <span style="color: #000080;">=</span> from.<span style="color: #000000;">readLine</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>line.<span style="color: #000000;">length</span> <span style="color: #000080;">!=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    headers +<span style="color: #000080;">=</span> line + Configs.<span style="color: #000000;">CRLF</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>line startsWith <span style="color: #6666FF;">&quot;Host:&quot;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> tmp <span style="color: #000080;">=</span> line.<span style="color: #000000;">split</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot; &quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">indexOf</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">':'</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&gt;</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> tmp2 <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">split</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;:&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #000080;">_</span>host <span style="color: #000080;">=</span> tmp2<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #000080;">_</span>port <span style="color: #000080;">=</span> tmp2<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">else</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #000080;">_</span>host <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #000080;">_</span>port <span style="color: #000080;">=</span> Configs.<span style="color: #000000;">HTTP_PORT</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error reading from socket: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> host <span style="color: #000080;">=</span> <span style="color: #000080;">_</span>host
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> port <span style="color: #000080;">=</span> <span style="color: #000080;">_</span>port
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> toString <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> req <span style="color: #000080;">=</span> method + <span style="color: #6666FF;">&quot; &quot;</span> + URI + <span style="color: #6666FF;">&quot; &quot;</span> + version + Configs.<span style="color: #000000;">CRLF</span>
    req +<span style="color: #000080;">=</span> headers
    req +<span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;Connection: close&quot;</span> + Configs.<span style="color: #000000;">CRLF</span> + Configs.<span style="color: #000000;">CRLF</span>
    req
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class HttpRequest(from: BufferedReader) {
    private var method = &quot;&quot;
    private var URI = &quot;&quot;
    private var version = &quot;&quot;
    private var headers = &quot;&quot;
    private var _host = &quot;&quot;
    private var _port = Configs.HTTP_PORT
    try {
    val firstLine = from.readLine
    val tmp = firstLine.split(&quot; &quot;)
    method = tmp(0)
    URI = tmp(1)
    version = tmp(2)
    } catch {
    case e: IOException =&gt;
    println(&quot;Error reading request line: &quot; + e)
    }
    println(&quot;URI:&quot; + URI)
    if (!(method equals &quot;GET&quot;))
    println(&quot;Error: Method not GET&quot;)
    try {
    var line = from.readLine
    while (line.length != 0) {
    headers += line + Configs.CRLF
    if (line startsWith &quot;Host:&quot;) {
    val tmp = line.split(&quot; &quot;)
    if (tmp(1).indexOf(':') &gt; 0) {
    val tmp2 = tmp(1).split(&quot;:&quot;)
    _host = tmp2(0)
    _port = tmp2(1).toInt
    } else {
    _host = tmp(1)
    _port = Configs.HTTP_PORT
    }
    }
    }
    } catch {
    case e: IOException =&gt;
    println(&quot;Error reading from socket: &quot; + e)
    }
    
    def host = _host
    
    def port = _port
    
    override def toString = {
    var req = method + &quot; &quot; + URI + &quot; &quot; + version + Configs.CRLF
    req += headers
    req += &quot;Connection: close&quot; + Configs.CRLF + Configs.CRLF
    req
    }
    }</p></div>
    ;i:3;s:10599:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> ProxyCache<span style="color: #F78811;">&#40;</span>port<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> socket<span style="color: #000080;">:</span> ServerSocket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">null</span>.<span style="color: #000000;">asInstanceOf</span><span style="color: #F78811;">&#91;</span>ServerSocket<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    socket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> ServerSocket<span style="color: #F78811;">&#40;</span>port<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Socket creation error: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    exit<span style="color: #F78811;">&#40;</span>-<span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> handle<span style="color: #F78811;">&#40;</span>client<span style="color: #000080;">:</span> Socket<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> server<span style="color: #000080;">:</span> Socket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">null</span>.<span style="color: #000000;">asInstanceOf</span><span style="color: #F78811;">&#91;</span>Socket<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> request<span style="color: #000080;">:</span> HttpRequest <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">null</span>.<span style="color: #000000;">asInstanceOf</span><span style="color: #F78811;">&#91;</span>HttpRequest<span style="color: #F78811;">&#93;</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> fromClient <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> BufferedReader<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">new</span> InputStreamReader<span style="color: #F78811;">&#40;</span>client.<span style="color: #000000;">getInputStream</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Reading request...&quot;</span><span style="color: #F78811;">&#41;</span>
    request <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> HttpRequest<span style="color: #F78811;">&#40;</span>fromClient<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Got request...&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error reading request from client: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">return</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    server <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Socket<span style="color: #F78811;">&#40;</span>request.<span style="color: #000000;">host</span>, request.<span style="color: #000000;">port</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> toServer <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DataOutputStream<span style="color: #F78811;">&#40;</span>server.<span style="color: #000000;">getOutputStream</span><span style="color: #F78811;">&#41;</span>
    toServer.<span style="color: #000000;">writeBytes</span><span style="color: #F78811;">&#40;</span>request.<span style="color: #000000;">toString</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> UnknownHostException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Unknown host: &quot;</span> + request.<span style="color: #000000;">host</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>e<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">return</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error writing request to server: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">return</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> fromServer <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DataInputStream<span style="color: #F78811;">&#40;</span>server.<span style="color: #000000;">getInputStream</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> response <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> HttpResponse<span style="color: #F78811;">&#40;</span>fromServer<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> toClient <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DataOutputStream<span style="color: #F78811;">&#40;</span>client.<span style="color: #000000;">getOutputStream</span><span style="color: #F78811;">&#41;</span>
    toClient.<span style="color: #000000;">writeBytes</span><span style="color: #F78811;">&#40;</span>response.<span style="color: #000000;">toString</span><span style="color: #F78811;">&#41;</span>
    toClient.<span style="color: #000000;">write</span><span style="color: #F78811;">&#40;</span>response.<span style="color: #000000;">body</span><span style="color: #F78811;">&#41;</span>
    client.<span style="color: #000000;">close</span>
    server.<span style="color: #000000;">close</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error writing response to client: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class ProxyCache(port: Int) {
    var socket: ServerSocket = null.asInstanceOf[ServerSocket]
    try {
    socket = new ServerSocket(port)
    } catch {
    case e: IOException =&gt;
    println(&quot;Socket creation error: &quot; + e)
    exit(-1)
    }
    
    def handle(client: Socket) {
    var server: Socket = null.asInstanceOf[Socket]
    var request: HttpRequest = null.asInstanceOf[HttpRequest]
    try {
    val fromClient =
    new BufferedReader(new InputStreamReader(client.getInputStream))
    println(&quot;Reading request...&quot;)
    request = new HttpRequest(fromClient)
    println(&quot;Got request...&quot;)
    } catch {
    case e: IOException =&gt;
    println(&quot;Error reading request from client: &quot; + e)
    return
    }
    
    try {
    server = new Socket(request.host, request.port)
    val toServer = new DataOutputStream(server.getOutputStream)
    toServer.writeBytes(request.toString)
    } catch {
    case e: UnknownHostException =&gt;
    println(&quot;Unknown host: &quot; + request.host)
    println(e)
    return
    case e: IOException =&gt;
    println(&quot;Error writing request to server: &quot; + e)
    return
    }
    
    try {
    val fromServer = new DataInputStream(server.getInputStream)
    val response = new HttpResponse(fromServer)
    val toClient = new DataOutputStream(client.getOutputStream)
    toClient.writeBytes(response.toString)
    toClient.write(response.body)
    client.close
    server.close
    } catch {
    case e: IOException =&gt;
    println(&quot;Error writing response to client: &quot; + e)
    }
    }
    }</p></div>
    ;i:4;s:1378:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> Configs <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> CRLF <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> HTTP<span style="color: #000080;">_</span>PORT <span style="color: #000080;">=</span> <span style="color: #F78811;">8080</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> BUF<span style="color: #000080;">_</span>SIZE <span style="color: #000080;">=</span> <span style="color: #F78811;">8192</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> MAX<span style="color: #000080;">_</span>OBJECT<span style="color: #000080;">_</span>SIZE <span style="color: #000080;">=</span> <span style="color: #F78811;">100000</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object Configs {
    val CRLF = &quot;\r\n&quot;
    val HTTP_PORT = 8080
    val BUF_SIZE = 8192
    val MAX_OBJECT_SIZE = 100000
    }</p></div>
    ;i:5;s:3485:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> Main <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> main<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> myPort <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> proxyCache <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> ProxyCache<span style="color: #F78811;">&#40;</span>myPort<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Cache started... Port: &quot;</span> + myPort<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">true</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> client <span style="color: #000080;">=</span> proxyCache.<span style="color: #000000;">socket</span>.<span style="color: #000000;">accept</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Got connection &quot;</span> + client<span style="color: #F78811;">&#41;</span>
    proxyCache.<span style="color: #000000;">handle</span><span style="color: #F78811;">&#40;</span>client<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error reading request from client: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object Main {
    def main(args: Array[String]) {
    val myPort = args(0).toInt
    val proxyCache = new ProxyCache(myPort)
    println(&quot;Cache started... Port: &quot; + myPort)
    while (true) {
    try {
    val client = proxyCache.socket.accept
    println(&quot;Got connection &quot; + client)
    proxyCache.handle(client)
    } catch {
    case e: IOException =&gt;
    println(&quot;Error reading request from client: &quot; + e)
    }
    }
    }
    }</p></div>
    ";}
categories:
  - Scala Notes
---
These codes are implementations of the exercise described here: <a href="http://www.cs.uic.edu/~troy/spring05/cs450/mp1.html" target="_blank">http://www.cs.uic.edu/~troy/spring05/cs450/mp1.html</a>

## HttpResponse



<pre lang="scala">class HttpResponse(fromServer: DataInputStream) {
  var version = ""
  var status = 0
  var statusLine = ""
  var headers = ""
  var body = new Array[Byte](Configs.MAX_OBJECT_SIZE)
  var length = -1
  try {
    var line = fromServer.readLine
    var gotStatusLine = false
    while (line.length != 0) {
      if (!gotStatusLine) {
        statusLine = line
        gotStatusLine = true
      } else {
        headers += line + Configs.CRLF
      }
      if (line.startsWith("Content-Length:") ||
        line.startsWith("Content-length:")) {
        val tmp = line.split(" ")
        length = tmp(1).toInt
      }
      line = fromServer.readLine
    }
  } catch {
    case e: IOException =>
      println("Error reading headers from server: " + e)
  }
  try {
    var bytesRead = 0
    var buf = new Array[Byte](Configs.BUF_SIZE)
    var loop = false
    if (length == -1)
      loop = true
    breakable {
      while (bytesRead &lt; length || loop) {
        val res = fromServer.read(buf, 0, Configs.BUF_SIZE)
        if (res == 1)
          break
        var i = 0
        while (i &lt; res &#038;&#038; (i + bytesRead) &lt; Configs.MAX_OBJECT_SIZE) {
          body(bytesRead + i) = buf(i)
          i += 1
        }
        bytesRead += res
      }
    }
  } catch {
    case e: IOException =>
      println("Error reading headers from body: " + e)
  }

  override def toString = {
    val res = statusLine + Configs.CRLF + headers + Configs.CRLF
    res
  }
}</pre>

## HttpRequest



<pre lang="scala">class HttpRequest(from: BufferedReader) {
  private var method = ""
  private var URI = ""
  private var version = ""
  private var headers = ""
  private var _host = ""
  private var _port = Configs.HTTP_PORT
  try {
    val firstLine = from.readLine
    val tmp = firstLine.split(" ")
    method = tmp(0)
    URI = tmp(1)
    version = tmp(2)
  } catch {
    case e: IOException =>
      println("Error reading request line: " + e)
  }
  println("URI:" + URI)
  if (!(method equals "GET"))
    println("Error: Method not GET")
  try {
    var line = from.readLine
    while (line.length != 0) {
      headers += line + Configs.CRLF
      if (line startsWith "Host:") {
        val tmp = line.split(" ")
        if (tmp(1).indexOf(':') > 0) {
          val tmp2 = tmp(1).split(":")
          _host = tmp2(0)
          _port = tmp2(1).toInt
        } else {
          _host = tmp(1)
          _port = Configs.HTTP_PORT
        }
      }
    }
  } catch {
    case e: IOException =>
      println("Error reading from socket: " + e)
  }

  def host = _host

  def port = _port

  override def toString = {
    var req = method + " " + URI + " " + version + Configs.CRLF
    req += headers
    req += "Connection: close" + Configs.CRLF + Configs.CRLF
    req
  }
}</pre>

## ProxyCache



<pre lang="scala">class ProxyCache(port: Int) {
  var socket: ServerSocket = null.asInstanceOf[ServerSocket]
  try {
    socket = new ServerSocket(port)
  } catch {
    case e: IOException =>
      println("Socket creation error: " + e)
      exit(-1)
  }

  def handle(client: Socket) {
    var server: Socket = null.asInstanceOf[Socket]
    var request: HttpRequest = null.asInstanceOf[HttpRequest]
    try {
      val fromClient =
        new BufferedReader(new InputStreamReader(client.getInputStream))
      println("Reading request...")
      request = new HttpRequest(fromClient)
      println("Got request...")
    } catch {
      case e: IOException =>
        println("Error reading request from client: " + e)
        return
    }

    try {
      server = new Socket(request.host, request.port)
      val toServer = new DataOutputStream(server.getOutputStream)
      toServer.writeBytes(request.toString)
    } catch {
      case e: UnknownHostException =>
        println("Unknown host: " + request.host)
        println(e)
        return
      case e: IOException =>
        println("Error writing request to server: " + e)
        return
    }

    try {
      val fromServer = new DataInputStream(server.getInputStream)
      val response = new HttpResponse(fromServer)
      val toClient = new DataOutputStream(client.getOutputStream)
      toClient.writeBytes(response.toString)
      toClient.write(response.body)
      client.close
      server.close
    } catch {
      case e: IOException =>
        println("Error writing response to client: " + e)
    }
  }
}</pre>

## Configs



<pre lang="scala">object Configs {
  val CRLF = "\r\n"
  val HTTP_PORT = 8080
  val BUF_SIZE = 8192
  val MAX_OBJECT_SIZE = 100000
}</pre>

## The Main



<pre lang="scala">object Main {
  def main(args: Array[String]) {
    val myPort = args(0).toInt
    val proxyCache = new ProxyCache(myPort)
    println("Cache started... Port: " + myPort)
    while (true) {
      try {
        val client = proxyCache.socket.accept
        println("Got connection " + client)
        proxyCache.handle(client)
      } catch {
        case e: IOException =>
          println("Error reading request from client: " + e)
      }
    }
  }
}</pre>

These codes can be found here: <a href="http://www.sawp.com.br/code/kurose/proxycache/ProxyCache.scala" target="_blank">ProxyCache.scala</a>
