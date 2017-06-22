---
id: 37
title: Using instant messaging for distributed application communication
date: 2008-06-29T19:11:51+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=37
permalink: /2008/06/xmpp-jabber-distributed-application-messaging/
categories:
  - Other
---
During the first session of [the Lightweight Languages 3 workshop (includes video of the talks)](http://ll3.ai.mit.edu/ "Hosted by the Dynamic Languages Group at the MIT Artificial Intelligence Lab"), Dana Moore and Bill Wright presented **ACME: Toward a LL Testing Framework for Large Distributed Systems** ([abstract](http://ll3.ai.mit.edu/abstracts.html#acme "ACME - Toward a LL Testing Framework for Large Distributed Systems abstract")), in which they described a distributed application which used [the XMPP (aka Jabber) instant messaging protocol](http://en.wikipedia.org/wiki/Extensible_Messaging_and_Presence_Protocol "article on Wikipedia") to communicate between nodes.

XMPP addresses many complexities of inter-node communication in a distributed application, such as presence, heartbeat, queuing messages for offline nodes (offline messages), group broadcast (chat rooms), and status.

Here some other resources promoting instant messaging as a communication bus for distributed applications:

  * [Mickaël Rémond&#8217;s blog](http://www.process-one.net/en/blogs/user/mremond/) talks about using XMPP (Jabber) inside distributed Erlang applications. [Here are slides from Mickaël Rémond&#8217;s presentation entitled Messaging with Erlang and Jabber](http://www.slideshare.net/Arbow/messaging-with-erlang-and-jabber/).
  * [A proposed standard for game sessions using XMPP (Jabber) by by Michal Vaner](http://www.xmpp.org/extensions/inbox/gamesessions.html)
  * [A proposed universal Go server using XMPP (Jabber) by Mike Albon](http://www.hopeless-newbie.co.uk/UGS/)
  * [Peer-to-Peer: Building Secure, Scalable, and Manageable Networks by Dana Moore and John Hebeler &#8211; book on Amazon](http://www.amazon.com/gp/product/0072192844?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0072192844)
  * [Jabber Developer&#8217;s Handbook by William Wright and Dana Moore &#8211; book on Amazon](http://www.amazon.com/gp/product/0672325365?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0672325365 "Statistically improbable phrases found in this book: dialback key, pipe advertisement, karma value, elif type, presence subscriptions, stream header, presence packet, aim transport, success packet, roster item")

Related links:

  * [Lightweight Languages 1](http://ll1.ai.mit.edu/ "Hosted by the Dynamic Languages Group at the MIT Artificial Intelligence Lab")
  * [Lightweight Languages 2](http://ll2.ai.mit.edu/ "Hosted by the Dynamic Languages Group at the MIT Artificial Intelligence Lab")
  * [Lightweight Languages 4](http://ll4.csail.mit.edu/ "Hosted by the Dynamic Languages Group at the MIT Artificial Intelligence Lab")
  * [Event-Based Programming: Taking Events to the Limit by Ted Faison &#8211; book on Amazon](http://www.amazon.com/gp/product/1590596439?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=1590596439)
  * [IM Instant Messaging Security by John Rittinghouse &#8211; book on Amazon](http://www.amazon.com/gp/product/1555583385?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=1555583385)
  * [Distributed Computing: Principles, Algorithms, and Systems by Ajay D. Kshemkalyani and Mukesh Singhal &#8211; book on Amazon](http://www.amazon.com/gp/product/0521876346?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0521876346)