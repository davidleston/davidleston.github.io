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
```csharp
override render(HtmlWriter) {
  HtmlWriter.Flush()
  DoSomeExpensiveOperation()
  // or join with a thread that's loading state
  base.Render(HtmlWriter)
}
```

This way, you can send the headers and navigation to the client so they'll see something while you're waiting for something to finish. Perhaps the client won't even finish downloading the headers when the render completes, you've gotten the first byte out faster.