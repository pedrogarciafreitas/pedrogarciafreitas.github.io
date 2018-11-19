---
id: 1773
title: 'libxul does not update its dependents ports &#8212; Script &#8220;configure&#8221; failed unexpectedly.'
date: 2012-09-22T10:46:08+00:00
author: SAWP
excerpt: Problem when recompile libxul and its dependences.
layout: post
guid: http://www.sawp.com.br/blog/?p=1773
permalink: /p=1773
categories:
  - FreeBSD
---
If you have this problem when compiling some port that depends of libxul:

<div>
  <blockquote>
    <p>
      <tt>checking which gecko to use... libxul<br /> checking manual gecko home set... checking for compiler -fshort-wchar option... yes<br /> checking whether to enable C++ RTTI... no<br /> checking whether we have a gtk 2 gecko build... configure: error: This program needs a gtk 2 gecko build<br /> ===> Script "configure" failed unexpectedly.<br /> Please run the gnomelogalyzer, available from<br /> "http://www.freebsd.org/gnome/gnomelogalyzer.sh", which will diagnose the<br /> problem and suggest a solution. If - and only if - the gnomelogalyzer cannot<br /> solve the problem, report the build failure to the FreeBSD GNOME team at<br /> gnome@FreeBSD.org, and attach (a)<br /> "/usr/ports/x11/yelp/work/yelp-2.30.2/config.log", (b) the output of the<br /> failed make command, and (c) the gnomelogalyzer output. Also, it might be a<br /> good idea to provide an overview of all packages installed on your system<br /> (i.e. an `ls /var/db/pkg`). Put your attachment up on any website,<br /> copy-and-paste into http://freebsd-gnome.pastebin.com, or use send-pr(1) with<br /> the attachment. Try to avoid sending any attachments to the mailing list<br /> (gnome@FreeBSD.org), because attachments sent to FreeBSD mailing lists are<br /> usually discarded by the mailing list software.<br /> *** Error code 1<br /> </tt><tt><br /> Stop in /usr/ports/x11/yelp.<br /> </tt><tt><br /> ===>>> make failed for x11/yelp<br /> ===>>> Aborting update<br /> </tt><tt><br /> ===>>> Update for x11/yelp failed<br /> ===>>> Aborting update<br /> </tt><tt><br /> Terminated</tt>
    </p>
  </blockquote>
</div>

try:

<div>
  <center>
    <code># portmaster -o www/libxul19 www/libxul</code>
  </center>
</div>
