---
id: 7
title: Faster first byte.
date: 2006-02-20T00:57:18+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=7
permalink: /2006/02/faster-first-byte/
categories:
  - Programming
---
override render(HtmlWriter)
  
HtmlWriter.Flush
  
DoSomeExpensiveOperation
  
// or join with a thread that&#8217;s loading state
  
base.Render(HtmlWriter)

This way, you can send the headers and navigation to the client so they&#8217;ll see something while you&#8217;re waiting for something to finish. Perhaps the client won&#8217;t even finish downloading the headers when the render completes, you&#8217;ve gotten the first byte out faster.