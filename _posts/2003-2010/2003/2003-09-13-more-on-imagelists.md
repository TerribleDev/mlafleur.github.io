---
title: More On ImageLists
excerpt: ""
tags: null
---
=Verdana size=2>The other day I blogged about </font><a href="http://weblogs.asp.net/mlafleur/posts/27017.aspx">my frustrations with the ImageList </a><font face=Verdana size=2>control. My knee-jerk reaction was to call for un-sealing the ImageList and many people were quick to point out why it was sealed in the first place (some not so politely I might add). After some more thought on the topic, I think I may have found a way to leave the ImageList sealed, but still allow me to solve my problem.

=Verdana size=2>The ImageList holds a collection of Images and these images are typically stored in an ImageStream object. One of the things you can do with an ImageStream from an ImageList is pass it to another ImageList control. So when I talk about creating a "Global ImageList", what I'm really asking for is a "Global ImageStream".

=Verdana size=2>The problem now is that the ImageStream property isn't available at design time. If the .NET team were make it available, I could point it to my global ImageStream and have it available at both run and design time, solving my problem completely.

=Verdana size=2>Comments? 

=Verdana size=2> 

 
