---
title: Updated Wish-List
excerpt: ""
tags: null
---
Now that we are half-way through 2004, I thought I would take a look back at my <a href="http://weblogs.asp.net/mlafleur/archive/2004/01/04/47472.aspx">New Year Wish-List </a>and see how far we have come. 

<p dir=ltr><font face=Symbol size=3><span><span>
<hr id=null/>
&#183;="Times New Roman" size=1>         </font></span></span>To have the C# team come to the realization that Edit &amp; Continue is in fact <i>not</i> the devils playground. Maybe they don&#8217;t make typos but <i>I</i> sure do (some 10 in the post alone I bet). Having to restart the entire application to fix a single letter is a massive productivity killer. Edit &amp; Continue, it is your friend.</p>
This one may require sending foul smelling fish products to the C# team's office. 



=Symbol size=3><span>&#183;<span>         </span></span>For someone to finally unseal the ImageList component. Or at least implement the ImageList as an interface so we can develop our own. For those of us who build commercial apps with hundreds of windows this is a huge issue. Someone decides that the &#8220;New&#8221; icon should be changed and we spend the next week changing it in 99 places (yes, 99. Because we <i>always</i> forget to change one someplace).  Hell, think of the memory savings that could be had by only having a single global ImageList rather than 100 separate ones with 99% of the same images in them.

Hmm.... I may have to stock quite a bit a foul smelling fish products.



=Symbol size=3><span>&#183;<span>         </span></span>A <i>real</i> source code control system API. See that one that you have now? Give it too Frodo and send him to Mt. Doom right away. It is evil and needs to be destroyed. Source Code Control is the most overlooked aspect of software development and the poor API support provided by Visual Studio is doing nothing to help correct it. 

While it is unclear what effect the new SCC system from Microsoft will have on the exposed API, I suspect it will improve things quite a bit. So it looks like this one will actually happen.



=Symbol size=3><span>&#183;<span>         </span></span>Yukon by Q2

Yukon by Q2 2008? OK, that is unfair. SQL Express at least shows that progress is being made. Maybe by early Q4 then?



=Symbol size=3><span>&#183;<span>         </span></span>Someone to confirm that there will in fact be an MSDE version of Yukon. I always assumed so but someone pointed out that this has never been explicitly stated.

<strong>100% answered by SQL Express. Congrats to the Express guys by the way. I really like what I've seen so far.</strong>



=Symbol size=3><span>&#183;<span>         </span></span>A [Replaced] attribute that goes one step beyond [Obsolete] in that it causes Visual Studio to automatically replace the old reference with the new reference. The best example is with property values persisted in the InitializeComponent method. When you <br />&#8221;Obsolete&#8221; a property Visual Studio doesn&#8217;t remove the old reference so you get a slew of compiler warnings that you must then delve into generated code to fix. This is even worse if you actually remove the property all together. It would be nice if the system could handle this automatically and use [Replaced(NewFunctionName)] to point to the new property. 

No idea. Someone hinted to me back in February that an answer to this problem was coming with VS 2005, but I've not seen it. 

<p>
<hr id=null/>
So we have a 1:6 ratio. Considering I've yet to loose a pound, stop smoking completely, or pick up jogging I would have to say that my wish-list is doing much better than my resolutions. </p>