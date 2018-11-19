---
id: 1937
title: Convert an Image and an Audio File to a Movie in Linux, BSD or other UNIX-like
date: 2013-03-10T16:50:17+00:00
author: CKPYT
excerpt: |
  This post is about Mp3ToTube. A script for converting an image and audio to a video. Using only bash commands, this script allows you to generate a single music or an entire album in a format acceptable by Youtube.
layout: post
guid: http://www.sawp.com.br/blog/?p=1937
permalink: p=1937
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:1276:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>local<span style="color: #000000; font-weight: bold;">/</span>bin
    <span style="color: #c20cb9; font-weight: bold;">wget</span> http:<span style="color: #000000; font-weight: bold;">//</span>www.sawp.com.br<span style="color: #000000; font-weight: bold;">/</span>projects<span style="color: #000000; font-weight: bold;">/</span>mp3totube<span style="color: #000000; font-weight: bold;">/</span>files<span style="color: #000000; font-weight: bold;">/</span>mp3totube
    <span style="color: #c20cb9; font-weight: bold;">chmod</span> a+x <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>local<span style="color: #000000; font-weight: bold;">/</span>bin<span style="color: #000000; font-weight: bold;">/</span>mp3totube</pre></td></tr></table><p class="theCode" style="display:none;">cd /usr/local/bin
    wget http://www.sawp.com.br/projects/mp3totube/files/mp3totube
    chmod a+x /usr/local/bin/mp3totube</p></div>
    ;i:2;s:290:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"> mp3totube cover.jpg song_to_video.wav .mp4</pre></td></tr></table><p class="theCode" style="display:none;"> mp3totube cover.jpg song_to_video.wav .mp4</p></div>
    ;i:3;s:373:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666;">$ </span>mp3totube album_cover.png <span style="color: #000000; font-weight: bold;">*</span>.mp3 .avi</pre></td></tr></table><p class="theCode" style="display:none;">$ mp3totube album_cover.png *.mp3 .avi</p></div>
    ";}
categories:
  - Miscellaneous
---
I developed a small script to create video from images with audio for Youtube. Since the script was developed using only bash commands, it can be easily installed and used on any UNIX environment.

## Download and Install

To install <a href="http://www.sawp.com.br/projects/mp3totube/" target="_blank">Mp3Totube</a>, copy the script file <a href="http://www.sawp.com.br/projects/mp3totube/files/mp3totube" target="_blank">mp3totube</a> into a directory. For example:

<pre lang="bash">cd /usr/local/bin
wget http://www.sawp.com.br/projects/mp3totube/files/mp3totube
chmod a+x /usr/local/bin/mp3totube
  </pre></p> 

## Usage

Run the script using as input the chosen image, the audio file and the output video type (by extension). 

For example, to convert a single wav audio file to a mp4 video: 

<pre lang="bash">mp3totube cover.jpg song_to_video.wav .mp4</pre>

The output will be the video &#8220;song\_to\_video.mp4&#8221;. The image &#8220;conver.jpg&#8221; will be in all frames. 

To convert each .mp3 file in a directory to the correspondent .avi video: 

<pre lang="bash">$ mp3totube album_cover.png *.mp3 .avi</pre>

In this case, if the directory contains the &#8220;music1.mp3&#8221;, &#8220;song2.mp3&#8221; and &#8220;track.mp3&#8221;, the output will be &#8220;music1.avi&#8221;, &#8220;song2.avi&#8221; and &#8220;track.avi&#8221;. The image &#8220;album_cover.png&#8221; will be in all frames of these three videos. 

See more at project&#8217;s page: <a href="http://www.sawp.com.br/projects/mp3totube/" target="_blank">http://www.sawp.com.br/projects/mp3totube/</a>
