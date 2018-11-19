---
id: 1700
title: Kurose’s book exercises (labs) — HTTP Web Server
date: 2012-07-27T23:47:12+00:00
author: SAWP
excerpt: Simple HTTP Server.
layout: post
guid: http://www.sawp.com.br/blog/?p=1700
permalink: p=1700
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:4581:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> WebServer <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> main<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Server listening...&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> port <span style="color: #000080;">=</span> getPort<span style="color: #F78811;">&#40;</span>args<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> socket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> ServerSocket<span style="color: #F78811;">&#40;</span>port<span style="color: #F78811;">&#41;</span>
    process<span style="color: #F78811;">&#40;</span>port, socket<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> process<span style="color: #F78811;">&#40;</span>port<span style="color: #000080;">:</span> Int, socket<span style="color: #000080;">:</span> ServerSocket<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">true</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> connection <span style="color: #000080;">=</span> socket.<span style="color: #000000;">accept</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> request <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> HttpRequest<span style="color: #F78811;">&#40;</span>connection<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">new</span> Thread<span style="color: #F78811;">&#40;</span>request<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">start</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> getPort<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>args.<span style="color: #000000;">length</span> <span style="color: #000080;">&gt;</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    <span style="color: #0000ff; font-weight: bold;">else</span>
    Configs.<span style="color: #000000;">HTTP_PORT</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object WebServer {
    def main(args: Array[String]) {
    println(&quot;Server listening...&quot;)
    val port = getPort(args)
    val socket = new ServerSocket(port)
    process(port, socket)
    }
    
    private def process(port: Int, socket: ServerSocket) {
    while (true) {
    val connection = socket.accept
    val request = new HttpRequest(connection)
    (new Thread(request)).start
    }
    }
    
    private def getPort(args: Array[String]) = {
    if (args.length &gt; 0)
    args(0).toInt
    else
    Configs.HTTP_PORT
    }
    }</p></div>
    ;i:2;s:2720:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> Configs <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> CRLF <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> HTTP<span style="color: #000080;">_</span>PORT <span style="color: #000080;">=</span> <span style="color: #F78811;">8080</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> BUF<span style="color: #000080;">_</span>SIZE <span style="color: #000080;">=</span> <span style="color: #F78811;">8192</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> MAX<span style="color: #000080;">_</span>OBJECT<span style="color: #000080;">_</span>SIZE <span style="color: #000080;">=</span> <span style="color: #F78811;">100000</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> HTTP<span style="color: #000080;">_</span>404 <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span><span style="color: #6666FF;">&quot;
    &lt;html&gt;
    &lt;head&gt;&lt;title&gt;Object not found&lt;/title&gt;&lt;/head&gt;
    &lt;body&gt;&lt;h1&gt;Object not found!&lt;/h1&gt;
    &lt;h2&gt;Error 404&lt;/h2&gt;
    &lt;address&gt;
    &lt;a href=&quot;</span>http<span style="color: #000080;">:</span><span style="color: #008000; font-style: italic;">//www.sawp.com.br&quot;&gt;www.sawp.com.br&lt;/a&gt;&lt;br /&gt;</span>
    <span style="color: #000080;">&lt;</span>/address<span style="color: #000080;">&gt;</span>
    <span style="color: #000080;">&lt;</span>/body<span style="color: #000080;">&gt;</span>
    <span style="color: #000080;">&lt;</span>/html<span style="color: #000080;">&gt;</span><span style="color: #6666FF;">&quot;&quot;</span><span style="color: #6666FF;">&quot;
    }</span></pre></td></tr></table><p class="theCode" style="display:none;">object Configs {
    val CRLF = &quot;\r\n&quot;
    val HTTP_PORT = 8080
    val BUF_SIZE = 8192
    val MAX_OBJECT_SIZE = 100000
    val HTTP_404 = &quot;&quot;&quot;
    &lt;html&gt;
    &lt;head&gt;&lt;title&gt;Object not found&lt;/title&gt;&lt;/head&gt;
    &lt;body&gt;&lt;h1&gt;Object not found!&lt;/h1&gt;
    &lt;h2&gt;Error 404&lt;/h2&gt;
    &lt;address&gt;
    &lt;a href=&quot;http://www.sawp.com.br&quot;&gt;www.sawp.com.br&lt;/a&gt;&lt;br /&gt;
    &lt;/address&gt;
    &lt;/body&gt;
    &lt;/html&gt;&quot;&quot;&quot;
    }</p></div>
    ;i:3;s:17107:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> HttpRequest<span style="color: #F78811;">&#40;</span>s<span style="color: #000080;">:</span> Socket<span style="color: #F78811;">&#41;</span> <span style="color: #0000ff; font-weight: bold;">extends</span> Runnable <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">val</span> is <span style="color: #000080;">=</span> s.<span style="color: #000000;">getInputStream</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">val</span> os <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DataOutputStream<span style="color: #F78811;">&#40;</span>s.<span style="color: #000000;">getOutputStream</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">val</span> br <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> BufferedReader<span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">new</span> InputStreamReader<span style="color: #F78811;">&#40;</span>is<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">val</span> requestLineHTTPRequest <span style="color: #000080;">=</span> br.<span style="color: #000000;">readLine</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> run <span style="color: #F78811;">&#123;</span>
    showServerMessage<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> fileName <span style="color: #000080;">=</span> extractFilenameFromRequestLine<span style="color: #F78811;">&#40;</span>requestLineHTTPRequest<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> fis <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> FileInputStream<span style="color: #F78811;">&#40;</span>fileName<span style="color: #F78811;">&#41;</span>
    processRequestedFile<span style="color: #F78811;">&#40;</span>fis, fileName<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> FileNotFoundException <span style="color: #000080;">=&gt;</span>
    processFileNotFound<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> Exception <span style="color: #000080;">=&gt;</span> println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error -&gt; HttpRequest: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    closeStreamsAndSockets<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;-.-&quot;</span> <span style="color: #000080;">*</span> <span style="color: #F78811;">20</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">this</span>.<span style="color: #000000;">finalize</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> processRequestedFile<span style="color: #F78811;">&#40;</span>fis<span style="color: #000080;">:</span> FileInputStream, fn<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Request file: &quot;</span> + fn<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> statusLine <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;HTTP/1.0 200 OK&quot;</span> + Configs.<span style="color: #000000;">CRLF</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> contentTypeLine <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;Content-Type: &quot;</span> + contentType<span style="color: #F78811;">&#40;</span>fn<span style="color: #F78811;">&#41;</span> + Configs.<span style="color: #000000;">CRLF</span>
    sendContents<span style="color: #F78811;">&#40;</span>statusLine<span style="color: #000080;">:</span> String, contentTypeLine<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span>
    sendBytes<span style="color: #F78811;">&#40;</span>fis, os<span style="color: #F78811;">&#41;</span>
    fis.<span style="color: #000000;">close</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> processFileNotFound<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;File not found request&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> statusLine <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;HTTP/1.0 404 Not Found&quot;</span> + Configs.<span style="color: #000000;">CRLF</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> contentTypeLine <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;Content-Type: text/html&quot;</span> + Configs.<span style="color: #000000;">CRLF</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> entityBody <span style="color: #000080;">=</span> Configs.<span style="color: #000000;">HTTP_404</span>
    sendContents<span style="color: #F78811;">&#40;</span>statusLine, contentTypeLine<span style="color: #F78811;">&#41;</span>
    sendEntityBody<span style="color: #F78811;">&#40;</span>entityBody<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendContents<span style="color: #F78811;">&#40;</span>statusLine<span style="color: #000080;">:</span> String, contentTypeLine<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    os.<span style="color: #000000;">writeBytes</span><span style="color: #F78811;">&#40;</span>statusLine<span style="color: #F78811;">&#41;</span>
    os.<span style="color: #000000;">writeBytes</span><span style="color: #F78811;">&#40;</span>contentTypeLine<span style="color: #F78811;">&#41;</span>
    os.<span style="color: #000000;">writeBytes</span><span style="color: #F78811;">&#40;</span>Configs.<span style="color: #000000;">CRLF</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendEntityBody<span style="color: #F78811;">&#40;</span>entityBody<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    os.<span style="color: #000000;">writeBytes</span><span style="color: #F78811;">&#40;</span>entityBody<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> closeStreamsAndSockets<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    os.<span style="color: #000000;">close</span>
    br.<span style="color: #000000;">close</span>
    s.<span style="color: #000000;">close</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> showServerMessage<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Request received:&quot;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>requestLineHTTPRequest<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> headerLine <span style="color: #000080;">=</span> br.<span style="color: #000000;">readLine</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>headerLine.<span style="color: #000000;">length</span> <span style="color: #000080;">!=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span>headerLine<span style="color: #F78811;">&#41;</span>
    headerLine <span style="color: #000080;">=</span> br.<span style="color: #000000;">readLine</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> extractFilenameFromRequestLine<span style="color: #F78811;">&#40;</span>request<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> tokens <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> StringTokenizer<span style="color: #F78811;">&#40;</span>request<span style="color: #F78811;">&#41;</span>
    tokens.<span style="color: #000000;">nextToken</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> fileName <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;.&quot;</span> + tokens.<span style="color: #000000;">nextToken</span>
    fileName
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendBytes<span style="color: #F78811;">&#40;</span>fis<span style="color: #000080;">:</span> FileInputStream, os<span style="color: #000080;">:</span> OutputStream<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> buffer <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Array<span style="color: #F78811;">&#91;</span>Byte<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1024</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> bytes <span style="color: #000080;">=</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">do</span> <span style="color: #F78811;">&#123;</span>
    os.<span style="color: #000000;">write</span><span style="color: #F78811;">&#40;</span>buffer, <span style="color: #F78811;">0</span>, bytes<span style="color: #F78811;">&#41;</span>
    bytes <span style="color: #000080;">=</span> fis.<span style="color: #000000;">read</span><span style="color: #F78811;">&#40;</span>buffer<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>bytes <span style="color: #000080;">&gt;=</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> contentType<span style="color: #F78811;">&#40;</span>fileName<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span><span style="color: #000080;">:</span> String <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>fileName.<span style="color: #000000;">endsWith</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;.htm&quot;</span><span style="color: #F78811;">&#41;</span> || fileName.<span style="color: #000000;">endsWith</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;.html&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #6666FF;">&quot;text/html&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">else</span>
    <span style="color: #6666FF;">&quot;application/octet-stream&quot;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class HttpRequest(s: Socket) extends Runnable {
    private val is = s.getInputStream
    private val os = new DataOutputStream(s.getOutputStream)
    private val br = new BufferedReader(new InputStreamReader(is))
    private val requestLineHTTPRequest = br.readLine
    
    override def run {
    showServerMessage()
    val fileName = extractFilenameFromRequestLine(requestLineHTTPRequest)
    try {
    val fis = new FileInputStream(fileName)
    processRequestedFile(fis, fileName)
    } catch {
    case e: FileNotFoundException =&gt;
    processFileNotFound()
    case e: Exception =&gt; println(&quot;Error -&gt; HttpRequest: &quot; + e)
    }
    closeStreamsAndSockets()
    println(&quot;-.-&quot; * 20)
    this.finalize
    }
    
    private def processRequestedFile(fis: FileInputStream, fn: String) {
    println(&quot;Request file: &quot; + fn)
    val statusLine = &quot;HTTP/1.0 200 OK&quot; + Configs.CRLF
    val contentTypeLine = &quot;Content-Type: &quot; + contentType(fn) + Configs.CRLF
    sendContents(statusLine: String, contentTypeLine: String)
    sendBytes(fis, os)
    fis.close
    }
    
    private def processFileNotFound() {
    println(&quot;File not found request&quot;)
    val statusLine = &quot;HTTP/1.0 404 Not Found&quot; + Configs.CRLF
    val contentTypeLine = &quot;Content-Type: text/html&quot; + Configs.CRLF
    val entityBody = Configs.HTTP_404
    sendContents(statusLine, contentTypeLine)
    sendEntityBody(entityBody)
    }
    
    private def sendContents(statusLine: String, contentTypeLine: String) {
    os.writeBytes(statusLine)
    os.writeBytes(contentTypeLine)
    os.writeBytes(Configs.CRLF)
    }
    
    private def sendEntityBody(entityBody: String) {
    os.writeBytes(entityBody)
    }
    
    private def closeStreamsAndSockets() {
    os.close
    br.close
    s.close
    }
    
    private def showServerMessage() {
    println(&quot;Request received:&quot;)
    println(requestLineHTTPRequest)
    var headerLine = br.readLine
    while (headerLine.length != 0) {
    println(headerLine)
    headerLine = br.readLine
    }
    }
    
    private def extractFilenameFromRequestLine(request: String) = {
    val tokens = new StringTokenizer(request)
    tokens.nextToken
    val fileName = &quot;.&quot; + tokens.nextToken
    fileName
    }
    
    private def sendBytes(fis: FileInputStream, os: OutputStream) {
    val buffer = new Array[Byte](1024)
    var bytes = 0
    do {
    os.write(buffer, 0, bytes)
    bytes = fis.read(buffer)
    } while (bytes &gt;= 0)
    }
    
    private def contentType(fileName: String): String =
    if (fileName.endsWith(&quot;.htm&quot;) || fileName.endsWith(&quot;.html&quot;))
    &quot;text/html&quot;
    else
    &quot;application/octet-stream&quot;
    }</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">object WebServer {
  def main(args: Array[String]) {
    println("Server listening...")
    val port = getPort(args)
    val socket = new ServerSocket(port)
    process(port, socket)
  }

  private def process(port: Int, socket: ServerSocket) {
    while (true) {
      val connection = socket.accept
      val request = new HttpRequest(connection)
      (new Thread(request)).start
    }
  }

  private def getPort(args: Array[String]) = {
    if (args.length > 0)
      args(0).toInt
    else
      Configs.HTTP_PORT
  }
}</pre>

<pre lang="scala">object Configs {
  val CRLF = "\r\n"
  val HTTP_PORT = 8080
  val BUF_SIZE = 8192
  val MAX_OBJECT_SIZE = 100000
  val HTTP_404 = """

  
  <h1>
  Object not found!
</h1>
    

<h2>
  Error 404
</h2>
    

<address>
  <a href="http://www.sawp.com.br">www.sawp.com.br</a><br />
      
</address>
  
"""
}</pre>

<pre lang="scala">class HttpRequest(s: Socket) extends Runnable {
  private val is = s.getInputStream
  private val os = new DataOutputStream(s.getOutputStream)
  private val br = new BufferedReader(new InputStreamReader(is))
  private val requestLineHTTPRequest = br.readLine

  override def run {
    showServerMessage()
    val fileName = extractFilenameFromRequestLine(requestLineHTTPRequest)
    try {
      val fis = new FileInputStream(fileName)
      processRequestedFile(fis, fileName)
    } catch {
      case e: FileNotFoundException =>
        processFileNotFound()
      case e: Exception => println("Error -> HttpRequest: " + e)
    }
    closeStreamsAndSockets()
    println("-.-" * 20)
    this.finalize
  }

  private def processRequestedFile(fis: FileInputStream, fn: String) {
    println("Request file: " + fn)
    val statusLine = "HTTP/1.0 200 OK" + Configs.CRLF
    val contentTypeLine = "Content-Type: " + contentType(fn) + Configs.CRLF
    sendContents(statusLine: String, contentTypeLine: String)
    sendBytes(fis, os)
    fis.close
  }

  private def processFileNotFound() {
    println("File not found request")
    val statusLine = "HTTP/1.0 404 Not Found" + Configs.CRLF
    val contentTypeLine = "Content-Type: text/html" + Configs.CRLF
    val entityBody = Configs.HTTP_404
    sendContents(statusLine, contentTypeLine)
    sendEntityBody(entityBody)
  }

  private def sendContents(statusLine: String, contentTypeLine: String) {
    os.writeBytes(statusLine)
    os.writeBytes(contentTypeLine)
    os.writeBytes(Configs.CRLF)
  }

  private def sendEntityBody(entityBody: String) {
    os.writeBytes(entityBody)
  }

  private def closeStreamsAndSockets() {
    os.close
    br.close
    s.close
  }

  private def showServerMessage() {
    println("Request received:")
    println(requestLineHTTPRequest)
    var headerLine = br.readLine
    while (headerLine.length != 0) {
      println(headerLine)
      headerLine = br.readLine
    }
  }

  private def extractFilenameFromRequestLine(request: String) = {
    val tokens = new StringTokenizer(request)
    tokens.nextToken
    val fileName = "." + tokens.nextToken
    fileName
  }

  private def sendBytes(fis: FileInputStream, os: OutputStream) {
    val buffer = new Array[Byte](1024)
    var bytes = 0
    do {
      os.write(buffer, 0, bytes)
      bytes = fis.read(buffer)
    } while (bytes >= 0)
  }

  private def contentType(fileName: String): String =
    if (fileName.endsWith(".htm") || fileName.endsWith(".html"))
      "text/html"
    else
      "application/octet-stream"
}</pre>
