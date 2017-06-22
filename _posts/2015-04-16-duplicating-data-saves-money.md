---
id: 70
title: Duplicating data can save money
date: 2015-04-16T21:28:22+00:00
author: David
layout: post
guid: http://davidleston.com/?p=70
permalink: /2015/04/duplicating-data-saves-money/
categories:
  - Programming
---
I have lots of records in my database. One application writes these records, many applications read these records. So I put them all in one database, and have all the applications access that database. Simple. But then I run into some problems.

**Dependencies**

There are times I need to change the schema. If I change the name of a column, I have to deploy all the applications simultaneously. I avoid releasing applications simultaneously. By spreading out releases, I can detect and fix a defect in one application, then prevent that defect in other applications. Spreading out releases also flattens the demand for QA and hotfixes. Also, getting all the applications to a deployable state at the same time is quite the coordination effort.

To avoid the need to deploy all the applications simultaneously, I can make backwards compatible changes. If I want to rename a column, I first duplicate that column, update the applications one by one, then drop the original column. To make sure both columns don&#8217;t stick around for a long time, I need to release applications that I might not otherwise release and ensure that supporting the new column name is prioritized in the backlog for each of the applications. If I want to make a change that isn&#8217;t backwards compatible, I still need to release all the applications simultaneously.

I could create multiple copies of the table. Each time I version the schema, I create a new table. After all applications have migrated off an old version, I can remove it. This requires maintaining a list of which applications are using which versions. And after a while I&#8217;m likely to be close to one copy per application.

Dependency management impacts development cost, the most expensive part of my application. Though this alone is enough to convince me to have one copy per application, I explore operational costs below.

**Availability**

Two applications + each with its own copy of data = twice the price. Not exactly. I pay for servicing requests for the data. If one application has greater availability requirements than the other, then one application can use a highly-available solution (e.g. Amazon RDS) while another uses a less-expensive lower-availability solution (e.g. small EC2 instance with cold standby). Additionally, once I reach a certain scale it&#8217;s cheaper to scale out than up, and at higher scales, scaling out is my only economically viable option (RDS scales to 30,000 IOPS).

**Read Latency**

Two applications are likely be have different access patterns for any short window of time. By serving each application with a different database, you achieve greater cache locality. If each application only stores the fields and records it needs, then relevant data will be more tightly packed. Latency can be further improved by storing calculated values in place of raw data (i.e. the sum of order line items instead of the individual line items). Additionally, by segmenting my load onto separate databases, I can serve load less latency-sensitive load from less expensive storage.

**Write Latency**

Not all columns and indexes are used by all applications. Imagine I have one application where I want to insert new data as quickly as possible &#8211; where milliseconds matter. If this application stores a subset of all fields and maintains a subset of all indexes, write speeds will be faster. I can send new data to this application first, then all other applications. Imagine a new order is received with 10,000 line items. If I improve write time of each line item by 10 milliseconds, I’ve improved the order insert time by 100 seconds. I&#8217;ve reduced the amount of time the customer has to wait to see the order in the UI by nearly two minutes &#8211; reducing support calls and improving customer satisfaction.