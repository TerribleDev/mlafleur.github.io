---
title: ImageLists
excerpt: ""
tags: null
---
=Arial size=2>In keeping with my tradition of <a title=http://weblogs.asp.net/mlafleur/posts/4911.aspx href="/mlafleur/posts/4911.aspx">simplifying</a> <a title=http://weblogs.asp.net/mlafleur/posts/8663.aspx href="/mlafleur/posts/8663.aspx">my point</a>, I've trimmed down my 30 page manifesto on ImageLists to the following:

<div align=left>=Arial color=#800000 size=2><strong>Sealed ImageLists suck and I'm getting ulcers from working with them. </strong></div>
<div align=left> </div>
<div align=left>=Arial size=2>Ok, so maybe I should explain a bit more here. I have a rather large application with a rather large number of windows. Each of these windows has a toolbar and menu of some kind. And more importantly, they all use the same collection of images (of the 100 images in my collection, 60% are used in 90% of the windows). </font><font face=Arial size=2>And thanks to someone on the .NET team, I'm forced to either maintain a separate ImageList for each of my windows or loose all design-time functionality of the ImageList. </div>
=Arial size=2>I'm not looking for the world, just a shared ImageList. If I could just build my own UserControl that inherits from ImageList, I could then add my images to the UserControl and in turn use that control on my forms. Then I need only maintain a single ImageList that every form could have immediate access too. It would be ImageList Nirvana. But no, I'm get to remain stuck in ImageList Hell because someone at Microsoft deemed me to dangerous and sealed the damn class. Thanks...
