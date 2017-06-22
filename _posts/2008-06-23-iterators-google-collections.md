---
id: 35
title: Authoring Iterators Using Google's Collections Library
date: 2008-06-23T19:23:27+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=35
permalink: /2008/06/iterators-google-collections/
categories:
  - Programming
---
Let's implement an iterator.

```java
/**
 * Removes duplicates from the elements returned by provided iterator.
 * The provided iterator must return the elements in the order elements in the order defined by the comparator.
 * The first element of a series of duplicates is returned by this iterator.
 * @param  Type of element returned by the iterator.
 */
public final class DedupingOrderedCollectionIterator<E> implements Iterator<E> {
    private final PeekingIterator<E> iterator;
    private final Comparator<? super E> comparator;

    /**
     * @param iterator iterates over an ordered collection
     * @param comparator implements the same comparison used to order the collection
     */
    public DedupingOrderedCollectionIterator(final Iterator

<? extends E> iterator, final Comparator

<? super E> comparator) {
        this.iterator = Iterators.peekingIterator(iterator);
        this.comparator = comparator;
    }

    public boolean hasNext() {
        return iterator.hasNext();
    }

    public E next() {
        final E next = iterator.next();
        while (iterator.hasNext() && comparator.compare(next, iterator.peek()) == 0) {
            iterator.next();
        }
        return next;
    }

    public void remove() {
        throw new UnsupportedOperationException();
    }
}
```

First, if you're confused about the generic wildcards, watch [Josh Bloch's presentation entitled **Effective Java Reloaded**](http://www.youtube.com/watch?v=pi_I7oD_uGI) and watch for the reference of "producer extends, consumer super" (aka PECS) or reference [Josh Bloch's second edition of Effective Java](http://www.amazon.com/gp/product/0201310058?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0201310058 "Effective Java(TM) Programming Language Guide (The Java Series) by Joshua Bloch").

Second, using [Google's PeekingIterator](http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/PeekingIterator.html "Javadoc for com.google.common.collect.PeekingIterator<E>") often reduces the code you need to deal with iterators.

Third, when implementing an iterator, you usually have to worry about what happens when `next()` is called when `hasNext()` would return false. What exception are you supposed to throw? And I keep coding the same implementation for `remove()` and always forget what exception it's supposed to throw.  [Google's AbstractIterator](http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/AbstractIterator.html "com.google.common.collect.AbstractIterator<T>") to the rescue!

Here's the same iterator written with com.google.common.collect.AbstractIterator<T>:

```java
/**
 * Removes duplicates from the elements returned by provided iterator.
 * The provided iterator must return the elements in the order elements in the order defined by the comparator.
 * The first element of a series of duplicates is returned by this iterator.
 * @param  Type of element returned by the iterator.
 */
public final class DedupingOrderedCollectionIterator<E> extends AbstractIterator<E> {
    private final PeekingIterator<E> iterator;
    private final Comparator<? super E> comparator;

    /**
     * @param iterator iterates over an ordered collection
     * @param comparator implements the same comparison used to order the collection
     */
    public DedupingOrderedCollectionIterator(final Iterator

<? extends E> iterator, final Comparator

<? super E> comparator) {
        this.iterator = Iterators.peekingIterator(iterator);
        this.comparator = comparator;
    }

    protected E computeNext() {
        if (iterator.hasNext()) {
            final E next = iterator.next();
            while (iterator.hasNext() && comparator.compare(next, iterator.peek()) == 0) {
                iterator.next();
            }
            return next;
        }
        return endOfData();
    }
}
```

AbstractIterator allows you to write concise iterators with consistent behavior.