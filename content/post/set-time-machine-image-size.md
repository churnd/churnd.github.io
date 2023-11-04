+++
title = "Set Time MacHine Image Size"
Categories = []
+++
With the [new server][1] up and running at home, I&#8217;ve finally got the wife&#8217;s laptop backed up via Time Machine over AFP. The problem is, Time Machine will use the entire drive if you let it. I definitely don&#8217;t want that. I thought about doing quotas, but I use the drive for other stuff too, and quotas would have applied to everything which I didn&#8217;t want.

The answer is simple&#8230; resize the sparsebundle:

`hdiutil resize -size 100g -shrinkonly laptop_00xxxxxxxx.sparsebundle`

Just mount the share designated for Time Machine use, navigate to it via Terminal, and enter the above command, using the appropriate info. You&#8217;ll need to change the end to point to whatever your sparsebundle is named (usually the name of your Mac plus it&#8217;s primary ethernet ID). You can also adjust the size to whatever you see fit. 100g means 100GB.

You need to have ownership of the sparsebundle or use sudo if you don&#8217;t.

You can also increase the size should you need it by replacing **-shrinkonly** with **-growonly**.

Cool. <img src='http://churnd.net/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' />

 [1]: http://churnd.net/2009/03/08/leopard-server/
