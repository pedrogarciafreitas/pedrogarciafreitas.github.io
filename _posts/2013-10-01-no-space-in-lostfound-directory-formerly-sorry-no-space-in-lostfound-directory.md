---
id: 2064
title: No space in lost+found directory (SORRY. NO SPACE IN lost+found DIRECTORY)
date: 2013-10-01T14:15:16+00:00
author: SAWP
excerpt: Fix the fsck error on FreeBSD.
layout: post
guid: http://www.sawp.com.br/blog/?p=2064
permalink: /p=2064
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:829:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># mount -f /dev/ad0s1a /tmp_mnt</span>
    <span style="color: #666666; font-style: italic;"># rm -rfv /tmp_mnt/lost+found/</span>
    <span style="color: #666666; font-style: italic;"># mkdir /tmp_mnt/lost+found</span>
    <span style="color: #666666; font-style: italic;"># umount /tmp_mnt</span>
    <span style="color: #666666; font-style: italic;"># fsck -y /dev/ad0s1a</span>
    <span style="color: #666666; font-style: italic;"># reboot</span></pre></td></tr></table><p class="theCode" style="display:none;"># mount -f /dev/ad0s1a /tmp_mnt
    # rm -rfv /tmp_mnt/lost+found/
    # mkdir /tmp_mnt/lost+found
    # umount /tmp_mnt
    # fsck -y /dev/ad0s1a
    # reboot</p></div>
    ";}
categories:
  - FreeBSD
---
Type as root:

<pre lang="bash"># mount -f /dev/ad0s1a /tmp_mnt
# rm -rfv /tmp_mnt/lost+found/
# mkdir /tmp_mnt/lost+found
# umount /tmp_mnt
# fsck -y /dev/ad0s1a
# reboot</pre>
