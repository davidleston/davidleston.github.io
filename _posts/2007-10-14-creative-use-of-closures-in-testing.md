---
id: 30
title: Creative use of closures in testing.
date: 2007-10-14T12:52:15+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=30
permalink: /2007/10/creative-use-of-closures-in-testing/
categories:
  - Programming
---
Having moved to Java, I do miss closures. xUnit.net has a creative use of closures in their unit testing framework:

```csharp
[Test]
public void DivideByZeroThrowsException() {
  Assert.Throws<System.DivideByZeroException>(
    delegate {
      DivideNumbers(5, 0);
    });
}
```

This code snippet was taken from [xUnit.net's documentation](http://www.codeplex.com/xunit/Wiki/View.aspx?title=HowToUse&referringTitle=Home).

Previously, each test method could have an expected exception. Now, one can have multiple calls which are expected to throw an exception in a single test method. Good thinking!