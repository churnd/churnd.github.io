+++
title = "Time MacHine Sparsebundle Size Update"
+++
A follow-up to this post:  <http://churnd.net/2009/03/09/set-time-machine-image-size/>

Apparently Apple got keen to what people were doing regarding manually limiting the sparsebundle image size.  As of update 10.6.3 or so, they &#8220;fixed&#8221; Time Machine to where it will resize the sparsebundle back to encompass the whole volume.  I cannot think of one good reason why Apple would do this, unless there is some problem caused by it.  I&#8217;ve been using it successfully for 5 different clients for a year.

<!--more-->

Good news is, we can reclaim our resizing superpowers & make them stick.  Doing so also involves delving into the command line, but if you did the previous command successfully, this one won&#8217;t be any more difficult.

Basically you have to run this:  
[sourcecode language="bash"]sudo chmod a-w bundlename.sparsebundle/Info.*[/sourcecode]  
then (the previous command):  
[sourcecode language="bash"]sudo hdiutil resize -size 250g bundlename.sparsebundle[/sourcecode]

This command removes all write privileges to the Info.plist and Info.bckup files inside the sparsebundle being used with Time Machine.  Resizing any sparsebundle requires being able to write to these files, so if they can&#8217;t be written to, it&#8217;ll just complain that the resize can&#8217;t be completed in your system logs (see Console.app).  I have not tested it fully, but I think this command **must be run on the server itself**.

Now you don&#8217;t have to sit by and watch helplessly as Time Machine fills up the volume you&#8217;re backing up to.  This is the kind of control that Apple should have built into Time Machine anyway.

Keep in mind though&#8230; if you ever need to resize your sparsebundle again, for example, you get a bigger HD & start using more space than the sparsebundle can contain, <strike>you&#8217;ll need to un-do the first step above before you can grow it:  
`sudo chmod a+w bundlename.sparsebundle/Info.*`  
then:</strike>  
*Actually, I don&#8217;t think you need to do this chmod because you&#8217;re using sudo&#8230;*

[sourcecode language="bash"]sudo hdiutil resize -size 500g bundlename.sparsebundle[/sourcecode]

Not too complicated, is it? That&#8217;s why I can&#8217;t figure out why Apple wouldn&#8217;t want to give this functionality to users via the Time Machine preference pane.
