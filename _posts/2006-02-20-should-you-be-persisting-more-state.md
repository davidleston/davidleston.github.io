---
id: 5
title: Should you be persisting more state?
date: 2006-02-20T00:47:15+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=5
permalink: /2006/02/should-you-be-persisting-more-state/
categories:
  - Programming
---
Lost state is state that has been destroyed, deleted, garbage collected or otherwise removed from storage not because of some domain specified reason.  In the best case because of limited storage capabilities, but because the value of the state is underestimated.

Microsoft Word has autosave.  By default, every ten minutes the document you’re editing is persisted to disk in case of an unexpected termination of the application.  I always change this to one minute, because why would you ever want to wait ten?

And why doesn’t New Egg’s shopping cart remember what I had in it?  I’ve had business people tell me customers get angry when they see items in their cart many months later.  I argue, at least have it be an option to review.  Like an automated (private) wish list.

Suppose you have a web server produce views of product information that is expensive to acquire. Perhaps it’s over a web service or a remote database.  Often, you’ll cache this information in memory, trading aging data for faster request processing.  But what if there’s a power outage, and both the web server and database suddenly shut down.  If your application starts running before the web service or database, then your application is missing an opportunity to process requests. If you had stale data, you could still provide information to anxious customers.  Even if you didn’t want to show old quantity levels or prices, you could still provide a description, and maybe a notice that you’ll be fully operational in a moment.

Consider dumping in-memory state, such as a cache, to disk if the connection to the data source is lost or during low load.