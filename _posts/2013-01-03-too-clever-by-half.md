---
Title: Too Clever By Half
Published: 2013-01-03 16:33:34
Excerpt: "So I'm a bit of a stickler for fool-proof configuration, sometimes to my own detriment. I'm also clever...too clever by half. "
views:
  - 'a:1:{i:0;s:3:"296";}'
dsq_thread_id:
  - 'a:1:{i:0;s:10:"3612666840";}'
author:
  - Marc LaFleur
post_date:
  - 2013-01-03 16:33:34
post_excerpt:
  - "So I'm a bit of a stickler for fool-proof configuration, sometimes to my own detriment. I'm also clever...too clever by half. "
permalink:
  - /too-clever-by-half/
---
So I'm a bit of a stickler for fool-proof configuration, sometimes to my own detriment.  In response to my earlier <a title="Bing Maps SDK" href="http://massivescale.azurewebsites.net/bing-maps-sdk/" target="_blank">Bing Maps SDK</a> issue with x64 I thought I would be really clever and just remove x64 as a target platform from the solution configuration. I thought it was clever. Heck, It <em>was</em> clever....too clever it seems.

It turns out that removing a Solution Platform from your solution will result in a rather unceremonious Visual Studio crash when you attempt to Create App Package for the store. The package utility seems to assume you have the default platforms configured; likely a safe assumption unless you have me for an end-user.

Luckily adding it back was quick and painless and the crash went away.

&nbsp;