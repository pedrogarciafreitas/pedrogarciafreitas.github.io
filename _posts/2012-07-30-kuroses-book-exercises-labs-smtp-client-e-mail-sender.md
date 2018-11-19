---
id: 1707
title: Kurose’s book exercises (labs) — SMTP Client (E-mail Sender)
date: 2012-07-30T16:15:24+00:00
author: SAWP
excerpt: "Kurose's Mail Client Lab."
layout: post
guid: http://www.sawp.com.br/blog/?p=1707
permalink: p=1707
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:4498:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> EmailSender <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> checkInputParams<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>args.<span style="color: #000000;">length</span> <span style="color: #000080;">&lt;</span> <span style="color: #F78811;">5</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Wrong number of arguments!&quot;</span><span style="color: #F78811;">&#41;</span>
    exit
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> main<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    checkInputParams<span style="color: #F78811;">&#40;</span>args<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">val</span> server <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> port <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> from <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> to <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">3</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> subject <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">4</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> msg <span style="color: #000080;">=</span> args<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">5</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;SMTP SERVER: &quot;</span> + server + <span style="color: #6666FF;">&quot; PORT: &quot;</span> + port<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> es <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> EmailSender<span style="color: #F78811;">&#40;</span>server, port, from, to, subject, msg<span style="color: #F78811;">&#41;</span>
    es.<span style="color: #000000;">process</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object EmailSender {
    private def checkInputParams(args: Array[String]) {
    if (args.length &lt; 5) {
    println(&quot;Wrong number of arguments!&quot;)
    exit
    }
    }
    
    def main(args: Array[String]) {
    checkInputParams(args)
    
    val server = args(0)
    val port = args(1).toInt
    val from = args(2)
    val to = args(3)
    val subject = args(4)
    val msg = args(5)
    
    println(&quot;SMTP SERVER: &quot; + server + &quot; PORT: &quot; + port)
    val es = new EmailSender(server, port, from, to, subject, msg)
    es.process
    }
    }</p></div>
    ;i:2;s:21136:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> EmailSender<span style="color: #F78811;">&#40;</span>server<span style="color: #000080;">:</span> String, port<span style="color: #000080;">:</span> Int, from<span style="color: #000080;">:</span> String,
    to<span style="color: #000080;">:</span> String, subject<span style="color: #000080;">:</span> String, message<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">val</span> socket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Socket<span style="color: #F78811;">&#40;</span>server, port<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">val</span> os <span style="color: #000080;">=</span> socket.<span style="color: #000000;">getOutputStream</span>
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">val</span> br <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> is <span style="color: #000080;">=</span> socket.<span style="color: #000000;">getInputStream</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> isr <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> InputStreamReader<span style="color: #F78811;">&#40;</span>is<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> br <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> BufferedReader<span style="color: #F78811;">&#40;</span>isr<span style="color: #F78811;">&#41;</span>
    br
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> process <span style="color: #F78811;">&#123;</span>
    readWelcomeMessage
    sendHelo
    sendEmailFrom<span style="color: #F78811;">&#40;</span>from<span style="color: #F78811;">&#41;</span>
    sendRcptTo<span style="color: #F78811;">&#40;</span>to<span style="color: #F78811;">&#41;</span>
    sendDATA
    sendDATE
    sendFrom<span style="color: #F78811;">&#40;</span>from<span style="color: #F78811;">&#41;</span>
    sendTo<span style="color: #F78811;">&#40;</span>to<span style="color: #F78811;">&#41;</span>
    sendSubject<span style="color: #F78811;">&#40;</span>subject<span style="color: #F78811;">&#41;</span>
    sendMensage<span style="color: #F78811;">&#40;</span>message<span style="color: #F78811;">&#41;</span>
    sendEndOfMessage
    sendQuit
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> readWelcomeMessage <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> response <span style="color: #000080;">=</span> br.<span style="color: #000000;">readLine</span>
    println<span style="color: #F78811;">&#40;</span>response<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span><span style="color: #000080;">!</span>response.<span style="color: #000000;">startsWith</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;220&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;220 reply not received from server.&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendHelo <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> command <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;helo <span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;&gt;&gt;&quot;</span> + command<span style="color: #F78811;">&#41;</span>
    os.<span style="color: #000000;">write</span><span style="color: #F78811;">&#40;</span>command.<span style="color: #000000;">getBytes</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;US-ASCII&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> response <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;&quot;</span>
    breakable <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>br.<span style="color: #000000;">ready</span><span style="color: #F78811;">&#41;</span>
    response <span style="color: #000080;">=</span> response + br.<span style="color: #000000;">readLine</span><span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span> + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    <span style="color: #F78811;">&#125;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;&lt; &lt;&quot;</span> + response<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendWithoutResponse<span style="color: #F78811;">&#40;</span>str<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;&gt;&gt;&quot;</span> + str<span style="color: #F78811;">&#41;</span>
    os.<span style="color: #000000;">write</span><span style="color: #F78811;">&#40;</span>str.<span style="color: #000000;">getBytes</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;US-ASCII&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendWithResponse<span style="color: #F78811;">&#40;</span>command<span style="color: #000080;">:</span> String, code<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;&gt;&gt;&quot;</span> + command<span style="color: #F78811;">&#41;</span>
    os.<span style="color: #000000;">write</span><span style="color: #F78811;">&#40;</span>command.<span style="color: #000000;">getBytes</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;US-ASCII&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> response <span style="color: #000080;">=</span> br.<span style="color: #000000;">readLine</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;&lt; &lt;&quot;</span> + response<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span><span style="color: #000080;">!</span>response.<span style="color: #000000;">startsWith</span><span style="color: #F78811;">&#40;</span>code<span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">throw</span> <span style="color: #0000ff; font-weight: bold;">new</span> Exception<span style="color: #F78811;">&#40;</span>code + <span style="color: #6666FF;">&quot; reply not received from server.&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendEmailFrom<span style="color: #F78811;">&#40;</span>m<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> command <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;MAIL FROM:&quot;</span> + m + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithResponse<span style="color: #F78811;">&#40;</span>command, <span style="color: #6666FF;">&quot;250&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendRcptTo<span style="color: #F78811;">&#40;</span>rcpt<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> command <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;RCPT TO:&lt;&quot;</span> + rcpt + <span style="color: #6666FF;">&quot;&gt;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithResponse<span style="color: #F78811;">&#40;</span>command, <span style="color: #6666FF;">&quot;250&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendDATA <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> command <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;DATA<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithResponse<span style="color: #F78811;">&#40;</span>command, <span style="color: #6666FF;">&quot;354&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendEndOfMessage <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> command <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;.<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithResponse<span style="color: #F78811;">&#40;</span>command, <span style="color: #6666FF;">&quot;250&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendQuit <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> command <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;QUIT<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithResponse<span style="color: #F78811;">&#40;</span>command, <span style="color: #6666FF;">&quot;221&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendDATE <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> full <span style="color: #000080;">=</span> DateFormat.<span style="color: #000000;">FULL</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> locale <span style="color: #000080;">=</span> Locale.<span style="color: #000000;">US</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> dateFormat <span style="color: #000080;">=</span> DateFormat.<span style="color: #000000;">getDateTimeInstance</span><span style="color: #F78811;">&#40;</span>full, full, locale<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> dDate <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Date
    <span style="color: #0000ff; font-weight: bold;">val</span> date <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;DATE: &quot;</span> + dateFormat.<span style="color: #000000;">format</span><span style="color: #F78811;">&#40;</span>dDate<span style="color: #F78811;">&#41;</span> + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithoutResponse<span style="color: #F78811;">&#40;</span>date<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendFrom<span style="color: #F78811;">&#40;</span>mail<span style="color: #000080;">_</span>from<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> str <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;From:&quot;</span> + mail<span style="color: #000080;">_</span>from + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithoutResponse<span style="color: #F78811;">&#40;</span>str<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendTo<span style="color: #F78811;">&#40;</span>rcpt<span style="color: #000080;">_</span>to<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> str <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;To:&quot;</span> + rcpt<span style="color: #000080;">_</span>to + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithoutResponse<span style="color: #F78811;">&#40;</span>str<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendSubject<span style="color: #F78811;">&#40;</span>subject<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> str <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;SUBJECT:&quot;</span> + subject + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithoutResponse<span style="color: #F78811;">&#40;</span>str<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendMensage<span style="color: #F78811;">&#40;</span>message<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> str <span style="color: #000080;">=</span> message + <span style="color: #6666FF;">&quot;<span style="color: #6666ff; font-weight: bold;">\r</span><span style="color: #6666ff; font-weight: bold;">\n</span>&quot;</span>
    sendWithoutResponse<span style="color: #F78811;">&#40;</span>str<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class EmailSender(server: String, port: Int, from: String,
    to: String, subject: String, message: String) {
    private val socket = new Socket(server, port)
    private val os = socket.getOutputStream
    private val br = {
    val is = socket.getInputStream
    val isr = new InputStreamReader(is)
    val br = new BufferedReader(isr)
    br
    }
    
    def process {
    readWelcomeMessage
    sendHelo
    sendEmailFrom(from)
    sendRcptTo(to)
    sendDATA
    sendDATE
    sendFrom(from)
    sendTo(to)
    sendSubject(subject)
    sendMensage(message)
    sendEndOfMessage
    sendQuit
    }
    
    private def readWelcomeMessage {
    val response = br.readLine
    println(response)
    if (!response.startsWith(&quot;220&quot;))
    throw new Exception(&quot;220 reply not received from server.&quot;)
    }
    
    private def sendHelo {
    val command = &quot;helo \r\n&quot;
    println(&quot;&gt;&gt;&quot; + command)
    os.write(command.getBytes(&quot;US-ASCII&quot;))
    var response = &quot;&quot;
    breakable {
    while (br.ready)
    response = response + br.readLine() + &quot;\n&quot;
    }
    println(&quot;&lt; &lt;&quot; + response)
    }
    
    private def sendWithoutResponse(str: String) {
    println(&quot;&gt;&gt;&quot; + str)
    os.write(str.getBytes(&quot;US-ASCII&quot;))
    }
    
    private def sendWithResponse(command: String, code: String) {
    println(&quot;&gt;&gt;&quot; + command)
    os.write(command.getBytes(&quot;US-ASCII&quot;))
    val response = br.readLine
    println(&quot;&lt; &lt;&quot; + response)
    if (!response.startsWith(code))
    throw new Exception(code + &quot; reply not received from server.&quot;)
    }
    
    private def sendEmailFrom(m: String) {
    val command = &quot;MAIL FROM:&quot; + m + &quot;\r\n&quot;
    sendWithResponse(command, &quot;250&quot;)
    }
    
    private def sendRcptTo(rcpt: String) {
    val command = &quot;RCPT TO:&lt;&quot; + rcpt + &quot;&gt;\r\n&quot;
    sendWithResponse(command, &quot;250&quot;)
    }
    
    private def sendDATA {
    val command = &quot;DATA\r\n&quot;
    sendWithResponse(command, &quot;354&quot;)
    }
    
    private def sendEndOfMessage {
    val command = &quot;.\r\n&quot;
    sendWithResponse(command, &quot;250&quot;)
    }
    
    private def sendQuit {
    val command = &quot;QUIT\r\n&quot;
    sendWithResponse(command, &quot;221&quot;)
    }
    
    private def sendDATE {
    val full = DateFormat.FULL
    val locale = Locale.US
    val dateFormat = DateFormat.getDateTimeInstance(full, full, locale)
    val dDate = new Date
    val date = &quot;DATE: &quot; + dateFormat.format(dDate) + &quot;\r\n&quot;
    sendWithoutResponse(date)
    }
    
    private def sendFrom(mail_from: String) {
    val str = &quot;From:&quot; + mail_from + &quot;\r\n&quot;
    sendWithoutResponse(str)
    }
    
    private def sendTo(rcpt_to: String) {
    val str = &quot;To:&quot; + rcpt_to + &quot;\r\n&quot;
    sendWithoutResponse(str)
    }
    
    private def sendSubject(subject: String) {
    val str = &quot;SUBJECT:&quot; + subject + &quot;\r\n&quot;
    sendWithoutResponse(str)
    }
    
    private def sendMensage(message: String) {
    val str = message + &quot;\r\n&quot;
    sendWithoutResponse(str)
    }
    }</p></div>
    ";}
categories:
  - Scala Notes
---
<pre lang="scala">object EmailSender {
  private def checkInputParams(args: Array[String]) {
    if (args.length &lt; 5) {
      println("Wrong number of arguments!")
      exit
    }
  }

  def main(args: Array[String]) {
    checkInputParams(args)

    val server = args(0)
    val port = args(1).toInt
    val from = args(2)
    val to = args(3)
    val subject = args(4)
    val msg = args(5)

    println("SMTP SERVER: " + server + " PORT: " + port)
    val es = new EmailSender(server, port, from, to, subject, msg)
    es.process
  }
}</pre>

<pre lang="scala">class EmailSender(server: String, port: Int, from: String,
                  to: String, subject: String, message: String) {
  private val socket = new Socket(server, port)
  private val os = socket.getOutputStream
  private val br = {
    val is = socket.getInputStream
    val isr = new InputStreamReader(is)
    val br = new BufferedReader(isr)
    br
  }

  def process {
    readWelcomeMessage
    sendHelo
    sendEmailFrom(from)
    sendRcptTo(to)
    sendDATA
    sendDATE
    sendFrom(from)
    sendTo(to)
    sendSubject(subject)
    sendMensage(message)
    sendEndOfMessage
    sendQuit
  }

  private def readWelcomeMessage {
    val response = br.readLine
    println(response)
    if (!response.startsWith("220"))
      throw new Exception("220 reply not received from server.")
  }

  private def sendHelo {
    val command = "helo \r\n"
    println(">>" + command)
    os.write(command.getBytes("US-ASCII"))
    var response = ""
    breakable {
      while (br.ready)
        response = response + br.readLine() + "\n"
    }
    println("&lt; &lt;" + response)
  }

  private def sendWithoutResponse(str: String) {
    println(">>" + str)
    os.write(str.getBytes("US-ASCII"))
  }

  private def sendWithResponse(command: String, code: String) {
    println(">>" + command)
    os.write(command.getBytes("US-ASCII"))
    val response = br.readLine
    println("&lt; &lt;" + response)
    if (!response.startsWith(code))
      throw new Exception(code + " reply not received from server.")
  }

  private def sendEmailFrom(m: String) {
    val command = "MAIL FROM:" + m + "\r\n"
    sendWithResponse(command, "250")
  }

  private def sendRcptTo(rcpt: String) {
    val command = "RCPT TO:&lt;" + rcpt + ">\r\n"
    sendWithResponse(command, "250")
  }

  private def sendDATA {
    val command = "DATA\r\n"
    sendWithResponse(command, "354")
  }

  private def sendEndOfMessage {
    val command = ".\r\n"
    sendWithResponse(command, "250")
  }

  private def sendQuit {
    val command = "QUIT\r\n"
    sendWithResponse(command, "221")
  }

  private def sendDATE {
    val full = DateFormat.FULL
    val locale = Locale.US
    val dateFormat = DateFormat.getDateTimeInstance(full, full, locale)
    val dDate = new Date
    val date = "DATE: " + dateFormat.format(dDate) + "\r\n"
    sendWithoutResponse(date)
  }

  private def sendFrom(mail_from: String) {
    val str = "From:" + mail_from + "\r\n"
    sendWithoutResponse(str)
  }

  private def sendTo(rcpt_to: String) {
    val str = "To:" + rcpt_to + "\r\n"
    sendWithoutResponse(str)
  }

  private def sendSubject(subject: String) {
    val str = "SUBJECT:" + subject + "\r\n"
    sendWithoutResponse(str)
  }

  private def sendMensage(message: String) {
    val str = message + "\r\n"
    sendWithoutResponse(str)
  }
}</pre>
