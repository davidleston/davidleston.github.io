---
id: 75
title: Eventual Consistency taster
date: 2015-04-17T20:35:42+00:00
author: David
layout: post
guid: http://davidleston.com/?p=75
permalink: /2015/04/eventual-consistency-taster/
categories:
  - Other
---
If I send an update to one system, then a minute later send that update to another system, my system will be inconsistent for that minute. Not quite. In my system there's only one application that creates new data. Think of that application as the author of a novel. Updates to the novel are sent to other applications in the system. Applications receive updates at different times. Any application that's reading page 42 of the novel has read the same 42 pages that any other application has or will read. When at page 42, that application's understanding of the novel is consistent with all other applications' understanding when they're 42 pages into the novel. Eventual consistency does not mean inconsistent. With a commerce web site, is it acceptable for a confirmation email to be sent after we update the storefront? It depends on how long after. Eventually consistent systems can have applications receiving data milliseconds or hours apart. First I need to understand what an acceptable delay is for each system. Then, I can work out the resources necessary to meet that goal. For example, I might want the storefront to show a new order within 100 milliseconds, a confirmation email to be sent within 10 seconds, and the "monthly statement" application needs to know by the end of the month.

With this explanation of eventual consistency, each application reads all pages in the same order. In order to gain greater performance, I might be able to split the story into multiple novels to be read in parallel. Imagine a customer has sent two payments. By applying the customer's payments in the order they were sent, a transactional history is created that is coherent with the history that would have been created had payments been applied synchronously. Do I need to apply payments from different customers in the order they were sent? If after looking at my domain, I determine there's no need, then I can process different customers' payments in parallel. In effect, I’ve split one novel into multiple novels that can be read in parallel. For any given novel, each application must have the same understanding of the novel with each page. But applications have no need to have the same understanding of novel A when on page 10 of novel B.