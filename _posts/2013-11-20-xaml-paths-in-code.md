---
layout: post
title: XAML Paths, in Code
categories: [code]
tags: [XAML]
description: Generate path data for XAML Path objects in the code
---

So I'm working on a Windows Store app, I want to create a Path object, but do it in code instead of in XAML because I'll be adding more than one and a few other reasons. I figured this should be easy.

<code>new Path { Data = ... }</code> and Data property is a&nbsp;Geometry class - not a string like in XAML. Doh.Well, maybe not the end of the world. Let's look at Geometry, but after a moment isn't non-trivial to turn what I have into a small block of code. So then we&nbsp;<a href="http://stackoverflow.com/questions/2029680/wpf-c-sharp-path-how-to-get-from-a-string-with-path-data-to-geometry-in-code-n" target="_blank">ask Stackoverflow</a>. There's a great answer, use <a href="http://msdn.microsoft.com/en-us/library/system.windows.media.geometry.parse(v=vs.110).aspx" target="_blank"><code>Geometry.Parse</code></a>, which hides out in <code>System.Windows.Media</code>. No problem. Turns out you can't access that namespace in store apps. 

Yeah. Not helpful. But you can bind to the property once the object is created. This I was able to do.

<script src="https://gist.github.com/TravisTheTechie/7573666.js"></script>

So, <code>Geometry.Parse</code> is obviously used in Windows Store apps, but it's not accessible. I'm not sure exactly why, but now I have a way to get around it. Maybe it will help you too. 