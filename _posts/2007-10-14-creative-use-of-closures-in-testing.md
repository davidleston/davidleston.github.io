---
id: 30
title: Creative use of closures in testing.
date: 2007-10-14T12:52:15+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=30
permalink: /2007/10/creative-use-of-closures-in-testing/
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1672:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    </pre></td><td class="code"><pre class="csharp" style="font-family:monospace;"><span style="color: #008000;">&#91;</span>Test<span style="color: #008000;">&#93;</span>
    <span style="color: #0600FF; font-weight: bold;">public</span> <span style="color: #6666cc; font-weight: bold;">void</span> DivideByZeroThrowsException<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span>
    <span style="color: #008000;">&#123;</span>
      Assert<span style="color: #008000;">.</span><span style="color: #0000FF;">Throws</span><span style="color: #008000;">&lt;</span><span style="color: #000000;">System</span><span style="color: #008000;">.</span><span style="color: #0000FF;">DivideByZeroException</span><span style="color: #008000;">&gt;</span><span style="color: #008000;">&#40;</span>
        <span style="color: #6666cc; font-weight: bold;">delegate</span>
        <span style="color: #008000;">&#123;</span>
          DivideNumbers<span style="color: #008000;">&#40;</span><span style="color: #FF0000;">5</span>, <span style="color: #FF0000;">0</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
        <span style="color: #008000;">&#125;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">[Test]
    public void DivideByZeroThrowsException()
    {
      Assert.Throws&lt;System.DivideByZeroException&gt;(
        delegate
        {
          DivideNumbers(5, 0);
        });
    }</p></div>
    ";}
categories:
  - Programming
---
Having moved to Java, I do miss closures. xUnit.net has a creative use of closures in their unit testing framework:

<pre lang="csharp" line="1">[Test]
public void DivideByZeroThrowsException()
{
  Assert.Throws&lt;System.DivideByZeroException>(
    delegate
    {
      DivideNumbers(5, 0);
    });
}</pre>

This code snippet was taken from [xUnit.net&#8217;s documentation](http://www.codeplex.com/xunit/Wiki/View.aspx?title=HowToUse&referringTitle=Home).

Previously, each test method could have an expected exception. Now, one can have multiple calls which are expected to throw an exception in a single test method. Good thinking!