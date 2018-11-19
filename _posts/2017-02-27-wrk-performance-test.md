---
id: 2110
title: wrk performance test
date: 2017-02-27T15:35:34+00:00
author: SAWP
excerpt: Straightfoward server benchmark test
layout: post
guid: http://www.sawp.com.br/blog/?p=2110
permalink: /p=2110
categories:
  - Quick Tips For Networking
---
## Basic Usage 

> wrk -t12 -c400 -d30s http://localhost:8080/

## Pipeline 

First, create the pipeline.lua script

<pre>init = function(args$$
   request_uri = args[1]
   depth = tonumber(args[2]$$ or 1

   local r = {}
   for i=1,depth do
     r[i] = wrk.format(nil, request_uri$$
   end
   req = table.concat(r$$
end

request = function($$
   return req
end
</pre>

and run

> wrk -t4 -c128 -d30s http://localhost:8080 -s pipeline.lua &#8211;latency &#8212; / 16
