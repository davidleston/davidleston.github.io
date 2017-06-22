---
id: 10
title: Screen scraping poker web sites
date: 2006-06-09T22:13:49+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=10
permalink: /2006/06/screen-scraping-poker-web-sites/
categories:
  - Programming
---
[Screen scraping](http://en.wikipedia.org/wiki/Screen_scraping) is very brittle. It will require continual maintenance and will never be complete. A good screen scraper is like writing a parser. Extracting semantic meaning from text with a poor signal to noise ratio is non-trivial.

Ideally, you would access the data via an API or a feed.  [Google](http://code.google.com/more/#products-apis-android "Google APIs"), [Amazon](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2Fgp%2Fbrowse.html%3Fnode%3D3435361&tag=davidleston-20&linkCode=ur2&camp=1789&creative=9325 "Amazon Web Services"), [Flickr](http://www.flickr.com/services/api/ "Flickr APIs") and many other sites provide free programmatic access to data. Sites like [Ebates](http://www.ebates.com/cash-back/rss-feeds.htm "Ebates feeds") offer feeds of data for free. If your data is not available for free, you may be able to purchase access to an API or feed.

Screen scraping can be used well for other purposes, e.g. testing the UI layer of a web application. In this application of screen scraping, the same organization generates and tests the UI.

What you really want is to be inside these poker web sites. You want to be able to be a sort of plug-in for your customers. I suggest taking a look at [the Book Burro extension for Firefox](http://bookburro.org/), then visit [Amazon](http://www.amazon.com/gp/product/1593271204?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=1593271204 "Webbots, Spiders, and Screen Scrapers: A Guide to Developing Internet Agents with PHP/CURL by Michael Schrenk"). Book Burro adds an interface widget on top of the Amazon page with prices from other bookstores on the web. This is a cross-platform solution.

I've read that the poker sites are not much bothered by poker bots. As long as people gamble, they're happy. Maybe you could find a poker site that would let you plug in your software&#8230; or make your own site for all the users of your software to play on and they think they're playing other people. A game server, now that's a completely different kind of software.