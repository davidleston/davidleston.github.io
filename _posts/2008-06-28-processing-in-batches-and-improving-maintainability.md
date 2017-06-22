---
id: 38
title: Processing in batches and improving maintainability
date: 2008-06-28T08:12:56+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=38
permalink: /2008/06/processing-in-batches-and-improving-maintainability/
categories:
  - Programming
---
Here's a common pattern:

```java
void process(final List<Foo> foos) {
    final ArrayList<bar> batch = new ArrayList<bar>(batchSize);

    for (final Foo foo : foos) {
        if (isValid(foo)) {
            final Bar transformed = transform(foo);
            batch.add(transformed);
            if (batch.size() % batchSize == 0) {
                processBatch(batch);
                batch.clear();
            }
        }
    }
    processBatch(batch);
}

// returns true if we want to process this Foo, otherwise returns false
private boolean isValid(final Foo foo) {
    return true;
}

// makes a Bar out of a Foo
private Bar transform(final Foo foo) {
    return null;
}

private void processBatch(final ArrayList<Bar> bars) {
    openTransaction();
    for(final Bar bar : bars) {
        executeQuery(bar);
    }
    closeTransaction();
}
```

We have some code duplication: `processBatch` appears twice in `process`. Also, we're iterating over two collections in order to process each Bar: we're iterating over `foos` in `process` and `bars` in `processBatch`. With the help of [Google Collections](http://code.google.com/p/google-collections/), we can do better:

```java
void process(final List<Foo> foos) {
    final Iterator<Foo> validFoos = Iterators.filter(foos.iterator(), isValid);
    final Iterator<Bar> bars = Iterators.transform(validFoos, transform);
    final Iterator<Iterator<Bar>> batches = Iterators.partition(bars, batchSize, false);

    while(batches.hasNext()) {
        final Iterator batch = batches.next();
        processBatch(batch);
    }
}

private final Predicate isValid = new Predicate() {
    // returns true if we want to process this Foo, otherwise returns false
    public boolean apply(final Foo foo) {
        return true;
    }
};

private final Function transform = new Function() {
    // makes a Bar out of a Foo
    public Bar apply(final Foo foo) {
        return null;
    }
};

private void processBatch(Iterator<Bar> bars) {
    openTransaction();
    while(bars.hasNext()) {
        final Bar bar = batch.next();
        executeQuery(bar);
    }
    closeTransactioin();
}
```

You may want to look at the [Javadoc for the Iterators class in Google Collections](http://google-collections.googlecode.com/svn/trunk/javadoc/index.html?com/google/common/collect/Iterators.html "com.google.common.collect.Iterators") to better understand what's happening here.

We removed the duplicate code. And while we still have two loops, one in `process` and one in `processBatch`, these loops are iterating over the same collection: `foos`. In addition, `process` has fewer lines of code. Granted, we have more lines of code elsewhere, but a real `process` method is likely to be more complex. By reducing the number of code blocks (braces) in `process`, we're making it easier to read and maintain.