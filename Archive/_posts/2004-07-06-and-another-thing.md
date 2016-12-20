---
ID: 499
post_title: 'And Another Thing&#8230;'
author: Marc LaFleur
post_date: 2004-07-06 15:36:00
post_excerpt: ""
layout: post
permalink: >
  http://massivescale.com/and-another-thing/
published: true
views:
  - "158"
---
<P>While I'm updating <A href="http://weblogs.asp.net/mlafleur/archive/2004/07/06/174199.aspx">wish-lists</A>&nbsp;I'd like to add something to this list: more control over web reference proxy generation. I understand that this may in fact be solved by VS 2005's new web services tools, but on the off chance that it isn't I'd like to get this out there.</P>
<P>Our latest application uses web services for the entire data layer. This means that 90% of the business logic and all of the database communication is handled by a web service (really it is handled by a number of web services due to the size of the application). </P>
<P>One of the issues we've run into is in managing this. We want to maintain a single assembly that houses all of the web references and associated helper classes. With a large number of class libraries and executables this saves us a ton of time and&nbsp;it system actually works pretty well. We have AppSoap.dll that holds the web references and a few other classes and this is in turn referenced by a dozen or so other assemblies. </P>
<P>But there is one issue, the proxy generate builds the reference.cs and gives a number of items an &#8220;Internal&#8221; protection level. This means that while we can reference &lt;namespace&gt;.&lt;typed dataset&gt;.&lt;typed datatable&gt; we cannot access the column names in that dataset. </P>
<P>The sort of it: either keep it all public so I can reference my web services anywhere I need to or give me control over it. Right now I have to search and replace &#8220;Internal&#8221; with &#8220;Public&#8221; every time I update the web service. Yuk...</P>