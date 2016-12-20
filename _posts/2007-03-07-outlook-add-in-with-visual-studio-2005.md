---
Title: >
  Outlook 2003 Add-in with Visual Studio
  2005?
Published: 2007-03-07 22:42:03
Excerpt: ""
views:
  - 'a:1:{i:0;s:4:"3294";}'
dsq_thread_id:
  - 'a:1:{i:0;s:10:"3538635213";}'
author:
  - Marc LaFleur
post_date:
  - 2007-03-07 22:42:03
post_excerpt:
  - ""
permalink:
  - /outlook-add-in-with-visual-studio-2005/
---
<p>Thinking of building an add-in for Outlook 2003 with Visual Studio 2005? Don't do it. Really, don't do it. What? Ok, if you must...</p>  <p>I've just spend the last three days building an add-in and installing on on a single PC. This totaled about 3 hours of development time and the rest was getting the darn thing to load! Honestly, it was the single most frustrating thing I've ever encountered in years. </p>  <p>The problem was that the setup program that Visual Studio 2005 automatically generates when you create an add-in project doesn't include everything you need. </p>  <p>Here is how I fixed the problem:</p>  <p>Before you can load your add-in you need to make sure the following is installed:</p>  <ul>   <li>Visual Studio 2005 Tools for Office Second Edition Runtime (found at <a title="http://shrinkster.com/mnh" href="http://shrinkster.com/mnh" target="_blank">http://shrinkster.com/mnh</a>) </li>    <li>Office 2003 Update: Redistributable Primary Interop Assemblies (found at <a title="http://shrinkster.com/mni" href="http://shrinkster.com/mni" target="_blank">http://shrinkster.com/mni</a>)</li> </ul>  <p>After that you'll need to &quot;fully trust&quot; your assemblies. This can only be done with signed assemblies. I remember being a pain with VS 2003 but turns out is a breeze with VS 2005. Just open up the Properties for the project and select the Signing tab. From there is was fairly self explanatory. </p>  <p>Now comes the part that gave me problems. After you have everything installed (including your nice newly signed assemblies) you need to give permission to those assemblies. This is done using a tool called CASPOL.EXE. Here is the command line for registering your file:</p>  <blockquote>   <p>caspol -u -ag All_Code -url &quot;&lt;full path to your file&gt;&quot; FullTrust -n &quot;&lt;assembly name&gt;&quot;</p> </blockquote>  <p>If you have more than one file (or the above didn't work) you can also do this for a directory. </p>  <blockquote>   <p>caspol -u -ag All_Code -url &quot;&lt;directory path&gt;*&quot; FullTrust</p> </blockquote>  <p>I hope this helps save someone from the pain I experienced over the last few days. Hopefully this will get easier with the next release of Visual Studio...</p>  <p><em>Updated to reference Outlook 2003. I wasn't clear about that in the original post. </em></p>