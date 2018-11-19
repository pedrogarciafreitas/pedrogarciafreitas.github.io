---
id: 892
title: Build Firefox crashes on nsHtml5ElementName.cpp
date: 2011-01-04T09:57:21+00:00
author: CKPYT
excerpt: 'Fixing FreeBSD ports www/libxul: nsHtml5ElementName.cpp nsHtml5StateSnapshot.cpp and how to get through the compile error'
layout: post
guid: http://www.sawp.com.br/blog/?p=892
permalink: p=892
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2180:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="text" style="font-family:monospace;">c++ -o nsHtml5ElementName.o -c -I../../dist/system_wrappers -include ../../cnfig/gcc_hidden.h -DMOZILLA_INTERNAL_API -D_IMPL_NS_COM -DEXPORT_XPT_API -DEXPORT_XPTC_API -D_IMPL_NS_COM_OBSOLETE -D_IMPL_NS_GFX -D_IMPL_NS_WIDGET -DIMPL_XREAPI -DIMPL_NS_NET -DIMPL_THEBES  -DOSTYPE=\&quot;FreeBSD8\&quot; -DOSARCH=FreeBSD  -I. -I. -I../../dist/include -I../../dist/include/nsprpub  -I/usr/local/include/nspr -I/usr/local/tmp/usr/ports/www/firefox/work/mozilla-1.9.2/dist/include/nss   -I/usr/include   -I./../../content/base/src  -I/usr/local/include   -fPIC  -I/usr/local/include  -I/usr/local/include -fno-rtti -fno-exceptions -Wall -Wpointer-arith -Woverloaded-virtual -Wsynth -Wno-ctor-dtor-privacy -Wno-non-virtual-dtor -Wcast-align -Wno-invalid-offsetof -Wno-long-long -O2 -pipe -O2 -fno-strict-aliasing -O2 -fno-strict-aliasing -fshort-wchar -pipe  -DNDEBUG -DTRIMMED -O2  -I/usr/local/include  -I/usr/local/include -DMOZILLA_CLIENT -include ../../mozilla-config.h nsHtml5ElementName.cpp</pre></td></tr></table><p class="theCode" style="display:none;">c++ -o nsHtml5ElementName.o -c -I../../dist/system_wrappers -include ../../cnfig/gcc_hidden.h -DMOZILLA_INTERNAL_API -D_IMPL_NS_COM -DEXPORT_XPT_API -DEXPORT_XPTC_API -D_IMPL_NS_COM_OBSOLETE -D_IMPL_NS_GFX -D_IMPL_NS_WIDGET -DIMPL_XREAPI -DIMPL_NS_NET -DIMPL_THEBES  -DOSTYPE=\&quot;FreeBSD8\&quot; -DOSARCH=FreeBSD  -I. -I. -I../../dist/include -I../../dist/include/nsprpub  -I/usr/local/include/nspr -I/usr/local/tmp/usr/ports/www/firefox/work/mozilla-1.9.2/dist/include/nss   -I/usr/include   -I./../../content/base/src  -I/usr/local/include   -fPIC  -I/usr/local/include  -I/usr/local/include -fno-rtti -fno-exceptions -Wall -Wpointer-arith -Woverloaded-virtual -Wsynth -Wno-ctor-dtor-privacy -Wno-non-virtual-dtor -Wcast-align -Wno-invalid-offsetof -Wno-long-long -O2 -pipe -O2 -fno-strict-aliasing -O2 -fno-strict-aliasing -fshort-wchar -pipe  -DNDEBUG -DTRIMMED -O2  -I/usr/local/include  -I/usr/local/include -DMOZILLA_CLIENT -include ../../mozilla-config.h nsHtml5ElementName.cpp</p></div>
    ";}
categories:
  - FreeBSD
---
Firefox become a compile error on FreeBSD 8.0:

<pre lang="text">c++ -o nsHtml5ElementName.o -c -I../../dist/system_wrappers -include ../../cnfig/gcc_hidden.h -DMOZILLA_INTERNAL_API -D_IMPL_NS_COM -DEXPORT_XPT_API -DEXPORT_XPTC_API -D_IMPL_NS_COM_OBSOLETE -D_IMPL_NS_GFX -D_IMPL_NS_WIDGET -DIMPL_XREAPI -DIMPL_NS_NET -DIMPL_THEBES  -DOSTYPE=\"FreeBSD8\" -DOSARCH=FreeBSD  -I. -I. -I../../dist/include -I../../dist/include/nsprpub  -I/usr/local/include/nspr -I/usr/local/tmp/usr/ports/www/firefox/work/mozilla-1.9.2/dist/include/nss   -I/usr/include   -I./../../content/base/src  -I/usr/local/include   -fPIC  -I/usr/local/include  -I/usr/local/include -fno-rtti -fno-exceptions -Wall -Wpointer-arith -Woverloaded-virtual -Wsynth -Wno-ctor-dtor-privacy -Wno-non-virtual-dtor -Wcast-align -Wno-invalid-offsetof -Wno-long-long -O2 -pipe -O2 -fno-strict-aliasing -O2 -fno-strict-aliasing -fshort-wchar -pipe  -DNDEBUG -DTRIMMED -O2  -I/usr/local/include  -I/usr/local/include -DMOZILLA_CLIENT -include ../../mozilla-config.h nsHtml5ElementName.cpp</pre>

To avoid this error, we must rebuild libxul and Firefox as follows:

<center>
  <br /> <code>cd /usr/ports/www/libxul && make CONFIGURE_ARGS=--enable-optimize=-O3 clean all && make install</code><br /> <code>cd /usr/ports/www/firefox && make CONFIGURE_ARGS=--enable-optimize=-O3 clean all && make install</code><br />
</center>
