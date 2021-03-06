---
title: Web Search with Lucene.NET
excerpt: ""
tags:
  - Lucene
  - Search
  - WebDev
---
I've been working with <a href="http://www.dotlucene.net/" target="_blank">Lucene.NET</a> and a project called <a href="http://www.seekafile.org/" target="_blank">Seekafile</a> based on it for the last few days. 
  Seekafile runs as a windows service that builds a Lucene index in the background. You can then use it to build Windows and Web clients that search that index. 
  Using a few lines of code I was able to quickly build an index of our intranet (including text, html, Word documents, etc) and a simple web site to search it. 
  This all started after I tried to use the Microsoft Index Service. I was able to get it up and running quick enough but the search capabilities were pretty limiting. What I wanted was "Google" style searching and the Index Service doesn't seem capable of doing it (at least not without more of a development effort invested into it).
  There were a few issues with Seekafile, namely that the management UI is somewhat limited (adding index directories is tedious for example) and you cannot exclude directories or filter what is added to the index. But other than that it does exactly what I needed - add a simple searchable index to our intranet. 
  Overall I though it worked really well and it has running without incident for 24 hours. 
