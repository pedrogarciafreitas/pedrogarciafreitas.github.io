---
id: 1681
title: 'Kurose&#8217;s book exercises (labs)  &#8212; UDP Pinger (Server and Client)'
date: 2012-07-27T15:19:06+00:00
author: SAWP
excerpt: "Kurose's computer network book exercise: implement a pseudo-ICMP (Internet Control Message Protocol) ."
layout: post
guid: http://www.sawp.com.br/blog/?p=1681
permalink: p=1681
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:1101:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> PingMessage<span style="color: #F78811;">&#40;</span>addr<span style="color: #000080;">:</span> InetAddress, port<span style="color: #000080;">:</span> Int, message<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> getAddress <span style="color: #000080;">=</span> addr
    <span style="color: #0000ff; font-weight: bold;">def</span> getMessage <span style="color: #000080;">=</span> message
    <span style="color: #0000ff; font-weight: bold;">def</span> getPort <span style="color: #000080;">=</span> port
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class PingMessage(addr: InetAddress, port: Int, message: String) {
    def getAddress = addr
    def getMessage = message
    def getPort = port
    }</p></div>
    ;i:2;s:6339:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> UDPPinger <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">protected</span> <span style="color: #0000ff; font-weight: bold;">val</span> socket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DatagramSocket<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> sendPing<span style="color: #F78811;">&#40;</span>ping<span style="color: #000080;">:</span> PingMessage<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> host <span style="color: #000080;">=</span> ping.<span style="color: #000000;">getAddress</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> port <span style="color: #000080;">=</span> ping.<span style="color: #000000;">getPort</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> message <span style="color: #000080;">=</span> ping.<span style="color: #000000;">getMessage</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> msgBytes <span style="color: #000080;">=</span> message.<span style="color: #000000;">getBytes</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> msglen <span style="color: #000080;">=</span> message.<span style="color: #000000;">length</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> packet <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DatagramPacket<span style="color: #F78811;">&#40;</span>msgBytes, msglen, host, port<span style="color: #F78811;">&#41;</span>
    socket.<span style="color: #000000;">send</span><span style="color: #F78811;">&#40;</span>packet<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Sent message to &quot;</span> + host + <span style="color: #6666FF;">&quot;:&quot;</span> + port<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> IOException <span style="color: #000080;">=&gt;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Error sending packet: &quot;</span> + e<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> receivePing <span style="color: #000080;">=</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> recvBuf <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Array<span style="color: #F78811;">&#91;</span>Byte<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>Configs.<span style="color: #000000;">MAX_PING_LEN</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> recvPacket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DatagramPacket<span style="color: #F78811;">&#40;</span>recvBuf, Configs.<span style="color: #000000;">MAX_PING_LEN</span><span style="color: #F78811;">&#41;</span>
    socket.<span style="color: #000000;">receive</span><span style="color: #F78811;">&#40;</span>recvPacket<span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Received message from &quot;</span> +
    recvPacket.<span style="color: #000000;">getAddress</span> + <span style="color: #6666FF;">&quot;:&quot;</span> + recvPacket.<span style="color: #000000;">getPort</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> recvMsg <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> String<span style="color: #F78811;">&#40;</span>recvPacket.<span style="color: #000000;">getData</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> reply <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> PingMessage<span style="color: #F78811;">&#40;</span>recvPacket.<span style="color: #000000;">getAddress</span>,
    recvPacket.<span style="color: #000000;">getPort</span>, recvMsg<span style="color: #F78811;">&#41;</span>
    reply
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class UDPPinger {
    protected val socket = new DatagramSocket()
    
    def sendPing(ping: PingMessage) {
    val host = ping.getAddress
    val port = ping.getPort
    val message = ping.getMessage
    val msgBytes = message.getBytes
    val msglen = message.length
    try {
    val packet = new DatagramPacket(msgBytes, msglen, host, port)
    socket.send(packet)
    println(&quot;Sent message to &quot; + host + &quot;:&quot; + port)
    } catch {
    case e: IOException =&gt;
    println(&quot;Error sending packet: &quot; + e)
    }
    }
    
    def receivePing = {
    val recvBuf = new Array[Byte](Configs.MAX_PING_LEN)
    val recvPacket = new DatagramPacket(recvBuf, Configs.MAX_PING_LEN)
    socket.receive(recvPacket)
    println(&quot;Received message from &quot; +
    recvPacket.getAddress + &quot;:&quot; + recvPacket.getPort)
    val recvMsg = new String(recvPacket.getData)
    val reply = new PingMessage(recvPacket.getAddress,
    recvPacket.getPort, recvMsg)
    reply
    }
    }</p></div>
    ;i:3;s:11718:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">class</span> UDPClient<span style="color: #F78811;">&#40;</span>remoteHost<span style="color: #000080;">:</span> String, remotePort<span style="color: #000080;">:</span> Int, numberOfPings<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">extends</span> UDPPinger <span style="color: #0000ff; font-weight: bold;">with</span> Runnable <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">var</span> numReplies <span style="color: #000080;">=</span> <span style="color: #F78811;">0</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> replies <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Array<span style="color: #F78811;">&#91;</span>Boolean<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>numberOfPings<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> rtt <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Array<span style="color: #F78811;">&#91;</span>Long<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>numberOfPings<span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> <span style="color: #0000ff; font-weight: bold;">this</span><span style="color: #F78811;">&#40;</span>remoteHost<span style="color: #000080;">:</span> String, remotePort<span style="color: #000080;">:</span> Int<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">this</span><span style="color: #F78811;">&#40;</span>remoteHost, remotePort, Configs.<span style="color: #000000;">NUM_PINGS</span><span style="color: #F78811;">&#41;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">def</span> run <span style="color: #F78811;">&#123;</span>
    sendAllPings
    sendReplyTimeout
    printStatistics
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendAllPings <span style="color: #F78811;">&#123;</span>
    socket.<span style="color: #000000;">setSoTimeout</span><span style="color: #F78811;">&#40;</span>Configs.<span style="color: #000000;">TIMEOUT</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">&lt;</span> - <span style="color: #F78811;">0</span> until numberOfPings<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> message <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;PING &quot;</span> + i + <span style="color: #6666FF;">&quot; &quot;</span> + <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">new</span> Date<span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">getTime</span> + <span style="color: #6666FF;">&quot; &quot;</span>
    replies<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">false</span>
    rtt<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> Configs.<span style="color: #000000;">RTT</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> hostName <span style="color: #000080;">=</span> InetAddress.<span style="color: #000000;">getByName</span><span style="color: #F78811;">&#40;</span>remoteHost<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> ping <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> PingMessage<span style="color: #F78811;">&#40;</span>hostName, remotePort, message<span style="color: #F78811;">&#41;</span>
    sendPing<span style="color: #F78811;">&#40;</span>ping<span style="color: #F78811;">&#41;</span>
    handleReply<span style="color: #F78811;">&#40;</span>receivePing.<span style="color: #000000;">getMessage</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> sendReplyTimeout <span style="color: #F78811;">&#123;</span>
    socket.<span style="color: #000000;">setSoTimeout</span><span style="color: #F78811;">&#40;</span>Configs.<span style="color: #000000;">REPLY_TIMEOUT</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span>numReplies <span style="color: #000080;">&lt;</span> numberOfPings<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">try</span> <span style="color: #F78811;">&#123;</span>
    handleReply<span style="color: #F78811;">&#40;</span>receivePing.<span style="color: #000000;">getMessage</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span> <span style="color: #0000ff; font-weight: bold;">catch</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">case</span> e<span style="color: #000080;">:</span> SocketTimeoutException <span style="color: #000080;">=&gt;</span>
    numReplies <span style="color: #000080;">=</span> numberOfPings
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> printStatistics <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">for</span> <span style="color: #F78811;">&#40;</span>i <span style="color: #000080;">&lt;</span> - <span style="color: #F78811;">0</span> until numberOfPings<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> s <span style="color: #000080;">=</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>rtt<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">&gt;</span> <span style="color: #F78811;">0</span><span style="color: #F78811;">&#41;</span>
    rtt<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toString</span>
    <span style="color: #0000ff; font-weight: bold;">else</span>
    <span style="color: #6666FF;">&quot;1&quot;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;PING &quot;</span> + i + <span style="color: #6666FF;">&quot;: &quot;</span> + replies<span style="color: #F78811;">&#40;</span>i<span style="color: #F78811;">&#41;</span> + <span style="color: #6666FF;">&quot; RTT: &quot;</span> + s + <span style="color: #6666FF;">&quot; ms&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    &nbsp;
    <span style="color: #0000ff; font-weight: bold;">private</span> <span style="color: #0000ff; font-weight: bold;">def</span> handleReply<span style="color: #F78811;">&#40;</span>reply<span style="color: #000080;">:</span> String<span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> tmp <span style="color: #000080;">=</span> reply.<span style="color: #000000;">split</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot; &quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> pingNumber <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">1</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toInt</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> then <span style="color: #000080;">=</span> tmp<span style="color: #F78811;">&#40;</span><span style="color: #F78811;">2</span><span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">toLong</span>
    replies<span style="color: #F78811;">&#40;</span>pingNumber<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">true</span>
    rtt<span style="color: #F78811;">&#40;</span>pingNumber<span style="color: #F78811;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">new</span> Date<span style="color: #F78811;">&#41;</span>.<span style="color: #000000;">getTime</span> - then
    numReplies +<span style="color: #000080;">=</span> <span style="color: #F78811;">1</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class UDPClient(remoteHost: String, remotePort: Int, numberOfPings: Int)
    extends UDPPinger with Runnable {
    var numReplies = 0
    val replies = new Array[Boolean](numberOfPings)
    val rtt = new Array[Long](numberOfPings)
    
    def this(remoteHost: String, remotePort: Int) =
    this(remoteHost, remotePort, Configs.NUM_PINGS)
    
    def run {
    sendAllPings
    sendReplyTimeout
    printStatistics
    }
    
    private def sendAllPings {
    socket.setSoTimeout(Configs.TIMEOUT)
    for (i &lt; - 0 until numberOfPings) {
    val message = &quot;PING &quot; + i + &quot; &quot; + (new Date).getTime + &quot; &quot;
    replies(i) = false
    rtt(i) = Configs.RTT
    val hostName = InetAddress.getByName(remoteHost)
    val ping = new PingMessage(hostName, remotePort, message)
    sendPing(ping)
    handleReply(receivePing.getMessage)
    }
    }
    
    private def sendReplyTimeout {
    socket.setSoTimeout(Configs.REPLY_TIMEOUT)
    while (numReplies &lt; numberOfPings) {
    try {
    handleReply(receivePing.getMessage)
    } catch {
    case e: SocketTimeoutException =&gt;
    numReplies = numberOfPings
    }
    }
    }
    
    private def printStatistics {
    for (i &lt; - 0 until numberOfPings) {
    val s =
    if (rtt(i) &gt; 0)
    rtt(i).toString
    else
    &quot;1&quot;
    println(&quot;PING &quot; + i + &quot;: &quot; + replies(i) + &quot; RTT: &quot; + s + &quot; ms&quot;)
    }
    }
    
    private def handleReply(reply: String) {
    val tmp = reply.split(&quot; &quot;)
    val pingNumber = tmp(1).toInt
    val then = tmp(2).toLong
    replies(pingNumber) = true
    rtt(pingNumber) = (new Date).getTime - then
    numReplies += 1
    }
    }</p></div>
    ;i:4;s:1937:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> PingerClient <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> main<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> host <span style="color: #000080;">=</span> <span style="color: #6666FF;">&quot;127.0.0.1&quot;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> port <span style="color: #000080;">=</span> <span style="color: #F78811;">9876</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Contacting host &quot;</span> + host + <span style="color: #6666FF;">&quot; at port &quot;</span> + port<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> client <span style="color: #000080;">=</span>  <span style="color: #0000ff; font-weight: bold;">new</span> UDPClient<span style="color: #F78811;">&#40;</span>host, port, <span style="color: #F78811;">20</span><span style="color: #F78811;">&#41;</span>
    client.<span style="color: #000000;">run</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object PingerClient {
    def main(args: Array[String]) {
    val host = &quot;127.0.0.1&quot;
    val port = 9876
    println(&quot;Contacting host &quot; + host + &quot; at port &quot; + port)
    val client =  new UDPClient(host, port, 20)
    client.run
    }
    }</p></div>
    ;i:5;s:5104:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> PingerServer <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> main<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> serverPort <span style="color: #000080;">=</span> <span style="color: #F78811;">9876</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> serverSocket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DatagramSocket<span style="color: #F78811;">&#40;</span>serverPort<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> receiveData <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> Array<span style="color: #F78811;">&#91;</span>Byte<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#40;</span>Configs.<span style="color: #000000;">MAX_PING_LEN</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">while</span> <span style="color: #F78811;">&#40;</span><span style="color: #0000ff; font-weight: bold;">true</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> receivePacket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DatagramPacket<span style="color: #F78811;">&#40;</span>receiveData, receiveData.<span style="color: #000000;">length</span><span style="color: #F78811;">&#41;</span>
    serverSocket.<span style="color: #000000;">receive</span><span style="color: #F78811;">&#40;</span>receivePacket<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> sentence <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> String<span style="color: #F78811;">&#40;</span>receivePacket.<span style="color: #000000;">getData</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">if</span> <span style="color: #F78811;">&#40;</span>sentence <span style="color: #000080;">!=</span> <span style="color: #0000ff; font-weight: bold;">null</span> <span style="color: #000080;">&amp;&amp;</span> <span style="color: #000080;">!</span>sentence.<span style="color: #000000;">equals</span><span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;&quot;</span><span style="color: #F78811;">&#41;</span><span style="color: #F78811;">&#41;</span>
    println<span style="color: #F78811;">&#40;</span>sentence<span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> ip <span style="color: #000080;">=</span> receivePacket.<span style="color: #000000;">getAddress</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> port <span style="color: #000080;">=</span> receivePacket.<span style="color: #000000;">getPort</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> data <span style="color: #000080;">=</span> sentence.<span style="color: #000000;">getBytes</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> sendPacket <span style="color: #000080;">=</span> <span style="color: #0000ff; font-weight: bold;">new</span> DatagramPacket<span style="color: #F78811;">&#40;</span>data, data.<span style="color: #000000;">length</span>, ip, port<span style="color: #F78811;">&#41;</span>
    serverSocket.<span style="color: #000000;">send</span><span style="color: #F78811;">&#40;</span>sendPacket<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object PingerServer {
    def main(args: Array[String]) {
    val serverPort = 9876
    val serverSocket = new DatagramSocket(serverPort)
    val receiveData = new Array[Byte](Configs.MAX_PING_LEN)
    while (true) {
    val receivePacket = new DatagramPacket(receiveData, receiveData.length)
    serverSocket.receive(receivePacket)
    val sentence = new String(receivePacket.getData)
    if (sentence != null &amp;&amp; !sentence.equals(&quot;&quot;))
    println(sentence)
    val ip = receivePacket.getAddress
    val port = receivePacket.getPort
    val data = sentence.getBytes
    val sendPacket = new DatagramPacket(data, data.length, ip, port)
    serverSocket.send(sendPacket)
    }
    }
    }</p></div>
    ;i:6;s:1415:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> Configs <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> MAX<span style="color: #000080;">_</span>PING<span style="color: #000080;">_</span>LEN <span style="color: #000080;">=</span> <span style="color: #F78811;">1024</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> NUM<span style="color: #000080;">_</span>PINGS <span style="color: #000080;">=</span> <span style="color: #F78811;">10</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> TIMEOUT <span style="color: #000080;">=</span> <span style="color: #F78811;">1000</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> REPLY<span style="color: #000080;">_</span>TIMEOUT <span style="color: #000080;">=</span> <span style="color: #F78811;">5000</span>
    <span style="color: #0000ff; font-weight: bold;">val</span> RTT <span style="color: #000080;">=</span> <span style="color: #F78811;">1000000</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object Configs {
    val MAX_PING_LEN = 1024
    val NUM_PINGS = 10
    val TIMEOUT = 1000
    val REPLY_TIMEOUT = 5000
    val RTT = 1000000
    }</p></div>
    ;i:7;s:2419:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="scala" style="font-family:monospace;"><span style="color: #0000ff; font-weight: bold;">object</span> PingerTestSimulation <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">def</span> main<span style="color: #F78811;">&#40;</span>args<span style="color: #000080;">:</span> Array<span style="color: #F78811;">&#91;</span>String<span style="color: #F78811;">&#93;</span><span style="color: #F78811;">&#41;</span> <span style="color: #F78811;">&#123;</span>
    println<span style="color: #F78811;">&#40;</span><span style="color: #6666FF;">&quot;Start ping simulation...&quot;</span><span style="color: #F78811;">&#41;</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> Thread <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> run <span style="color: #F78811;">&#123;</span>
    PingerServer.<span style="color: #000000;">main</span><span style="color: #F78811;">&#40;</span>args<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>.<span style="color: #000000;">start</span>
    <span style="color: #0000ff; font-weight: bold;">new</span> Thread <span style="color: #F78811;">&#123;</span>
    <span style="color: #0000ff; font-weight: bold;">override</span> <span style="color: #0000ff; font-weight: bold;">def</span> run <span style="color: #F78811;">&#123;</span>
    PingerClient.<span style="color: #000000;">main</span><span style="color: #F78811;">&#40;</span>args<span style="color: #F78811;">&#41;</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span>.<span style="color: #000000;">start</span>
    <span style="color: #F78811;">&#125;</span>
    <span style="color: #F78811;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">object PingerTestSimulation {
    def main(args: Array[String]) {
    println(&quot;Start ping simulation...&quot;)
    new Thread {
    override def run {
    PingerServer.main(args)
    }
    }.start
    new Thread {
    override def run {
    PingerClient.main(args)
    }
    }.start
    }
    }</p></div>
    ";}
categories:
  - Scala Notes
---
The exercise description is:

> In this lab, you will study a simple Internet ping server written in the Java language, and implement a corresponding client. The functionality provided by these programs are similar to the standard ping programs available in modern operating systems, except that they use UDP rather than Internet Control Message Protocol (ICMP) to communicate with each other. (Java does not provide a straightforward means to interact with ICMP.) 
> 
> The ping protocol allows a client machine to send a packet of data to a remote machine, and have the remote machine return the data back to the client unchanged (an action referred to as echoing). Among other uses, the ping protocol allows hosts to determine round-trip times to other machines. 

## ICMP Message



Pinger Message Class:

<pre lang="scala">class PingMessage(addr: InetAddress, port: Int, message: String) {
  def getAddress = addr
  def getMessage = message
  def getPort = port
}</pre>

## UDP Pinger Protocol



<pre lang="scala">class UDPPinger {
  protected val socket = new DatagramSocket()

  def sendPing(ping: PingMessage) {
    val host = ping.getAddress
    val port = ping.getPort
    val message = ping.getMessage
    val msgBytes = message.getBytes
    val msglen = message.length
    try {
      val packet = new DatagramPacket(msgBytes, msglen, host, port)
      socket.send(packet)
      println("Sent message to " + host + ":" + port)
    } catch {
      case e: IOException =>
        println("Error sending packet: " + e)
    }
  }

  def receivePing = {
    val recvBuf = new Array[Byte](Configs.MAX_PING_LEN)
    val recvPacket = new DatagramPacket(recvBuf, Configs.MAX_PING_LEN)
    socket.receive(recvPacket)
    println("Received message from " +
      recvPacket.getAddress + ":" + recvPacket.getPort)
    val recvMsg = new String(recvPacket.getData)
    val reply = new PingMessage(recvPacket.getAddress,
      recvPacket.getPort, recvMsg)
    reply
  }
}</pre>

## UDP Pinger Client



The multithreaded client class:

<pre lang="scala">class UDPClient(remoteHost: String, remotePort: Int, numberOfPings: Int)
    extends UDPPinger with Runnable {
  var numReplies = 0
  val replies = new Array[Boolean](numberOfPings)
  val rtt = new Array[Long](numberOfPings)

  def this(remoteHost: String, remotePort: Int) =
    this(remoteHost, remotePort, Configs.NUM_PINGS)

  def run {
    sendAllPings
    sendReplyTimeout
    printStatistics
  }

  private def sendAllPings {
    socket.setSoTimeout(Configs.TIMEOUT)
    for (i &lt; - 0 until numberOfPings) {
      val message = "PING " + i + " " + (new Date).getTime + " "
      replies(i) = false
      rtt(i) = Configs.RTT
      val hostName = InetAddress.getByName(remoteHost)
      val ping = new PingMessage(hostName, remotePort, message)
      sendPing(ping)
      handleReply(receivePing.getMessage)
    }
  }

  private def sendReplyTimeout {
    socket.setSoTimeout(Configs.REPLY_TIMEOUT)
    while (numReplies &lt; numberOfPings) {
      try {
        handleReply(receivePing.getMessage)
      } catch {
        case e: SocketTimeoutException =>
          numReplies = numberOfPings
      }
    }
  }

  private def printStatistics {
    for (i &lt; - 0 until numberOfPings) {
      val s =
        if (rtt(i) > 0)
          rtt(i).toString
        else
          "1"
      println("PING " + i + ": " + replies(i) + " RTT: " + s + " ms")
    }
  }

  private def handleReply(reply: String) {
    val tmp = reply.split(" ")
    val pingNumber = tmp(1).toInt
    val then = tmp(2).toLong
    replies(pingNumber) = true
    rtt(pingNumber) = (new Date).getTime - then
    numReplies += 1
  }
}</pre>

The Client:



<pre lang="scala">object PingerClient {
  def main(args: Array[String]) {
    val host = "127.0.0.1"
    val port = 9876
    println("Contacting host " + host + " at port " + port)
    val client =  new UDPClient(host, port, 20)
    client.run
  }
}</pre>

## UDP Pinger Server



<pre lang="scala">object PingerServer {
  def main(args: Array[String]) {
    val serverPort = 9876
    val serverSocket = new DatagramSocket(serverPort)
    val receiveData = new Array[Byte](Configs.MAX_PING_LEN)
    while (true) {
      val receivePacket = new DatagramPacket(receiveData, receiveData.length)
      serverSocket.receive(receivePacket)
      val sentence = new String(receivePacket.getData)
      if (sentence != null && !sentence.equals(""))
        println(sentence)
      val ip = receivePacket.getAddress
      val port = receivePacket.getPort
      val data = sentence.getBytes
      val sendPacket = new DatagramPacket(data, data.length, ip, port)
      serverSocket.send(sendPacket)
    }
  }
}</pre>

## Secondary and auxiliary modules



<pre lang="scala">object Configs {
  val MAX_PING_LEN = 1024
  val NUM_PINGS = 10
  val TIMEOUT = 1000
  val REPLY_TIMEOUT = 5000
  val RTT = 1000000
}</pre>

## Simulations



Assuming you&#8217;re running the client and server on the same machine (127.0.0.1), you can run the code:

<pre lang="scala">object PingerTestSimulation {
  def main(args: Array[String]) {
    println("Start ping simulation...")
    new Thread {
      override def run {
        PingerServer.main(args)
      }
    }.start
    new Thread { 
      override def run {
        PingerClient.main(args)
      }
    }.start
  }
}</pre>

These codes can be found here: <a href="http://www.sawp.com.br/code/kurose/pinger/UDPPinger.scala" target="_blank">UDPPinger.scala</a>, <a href="http://www.sawp.com.br/code/kurose/pinger/PingerServer.scala" target="_blank">PingerServer.scala</a>, <a href="http://www.sawp.com.br/code/kurose/pinger/PingerClient.scala" target="_blank">PingerClient.scala</a> e <a href="http://www.sawp.com.br/code/kurose/pinger/PingerTestSimulation.scala" target="_blank">PingerTestSimulation.scala</a>
