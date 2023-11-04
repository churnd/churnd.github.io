+++
title = "Syntax Highlighting With Less"
Categories = []
+++
I love the syntax highlighting that VI/VIM provides.  I refuse to use any text editor without it.  It just makes it much easier on my eyes to navigate the code.  It&#8217;s a very useful feature, and I have no idea why common [pagers][1] such as <span class="Apple-style-span" style="font-style:italic;">more</span> or <span class="Apple-style-span" style="font-style:italic;">less</span> don&#8217;t offer this. <div>
</div>

<div>
  Hope is not lost though!  You can use one of VIM&#8217;s macros to act similar to <span class="Apple-style-span" style="font-style:italic;">less</span> but with highlighting!  This is done by setting an alias in your .bash_profile or .bashrc file, which is in your home directory.  Here&#8217;s how:
</div>

<div>
  <ol>
    <li>
      Open up a terminal and type <span class="Apple-style-span" style="font-style:italic;">cd</span>.  This will take you to your home directory in case you aren&#8217;t already.
    </li>
    <li>
      You need to edit your .bashrc or .bash_profile include this alias:  <span class="Apple-style-span" style="font-weight:bold;">alias vless=&#8217;vim -u /usr/share/vim/vim71/macros/less.vim&#8217;</span>.  You will most likely have to modify that path depending on your system, but it should always start with <span class="Apple-style-span" style="font-weight:bold;">/usr/share/vim</span>.
    </li>
    <li>
      Save and close, then type &#8220;. .bashrc&#8221; or &#8220;. .bash_profile&#8221; to re-read the file and have the alias take effect.
    </li>
  </ol>
  
  <div>
    You&#8217;re done!  Now instead of using <span class="Apple-style-span" style="font-style:italic;">less</span> to read a file, you can use <span class="Apple-style-span" style="font-style:italic;">vless</span>.  The great thing about aliases is they can be whatever you want.  You can even set it to override <span class="Apple-style-span" style="font-style:italic;">less</span> itself if you want.
  </div>
  
  <div>
  </div>
  
  <div>
    I&#8217;m not sure if basic functionality is any different between <span class="Apple-style-span" style="font-style:italic;">less</span> and <span class="Apple-style-span" style="font-style:italic;">vless</span>.  Both use <span class="Apple-style-span" style="font-weight:bold;">/</span> to search and <span class="Apple-style-span" style="font-weight:bold;">q</span> to quit, and navigate the file the same.  If there are any differences, they certainly don&#8217;t bother me.  :)
  </div>
</div>

 [1]: http://en.wikipedia.org/wiki/Terminal_pager
