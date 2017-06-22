---
id: 35
title: 'Authoring Iterators Using Google&#8217;s Collections Library'
date: 2008-06-23T19:23:27+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=35
permalink: /2008/06/iterators-google-collections/
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:7624:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #008000; font-style: italic; font-weight: bold;">/**
    * Removes duplicates from the elements returned by provided iterator.
    * The provided iterator must return the elements in the order elements in the order defined by the comparator.
    * The first element of a series of duplicates is returned by this iterator.
    * @param  Type of element returned by the iterator.
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #000000; font-weight: bold;">class</span> DedupingOrderedCollectionIterator<span style="color: #339933;">&lt;</span>E<span style="color: #339933;">&gt;</span> <span style="color: #000000; font-weight: bold;">implements</span> Iterator<span style="color: #339933;">&lt;</span>E<span style="color: #339933;">&gt;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> PeekingIterator<span style="color: #339933;">&lt;</span>E<span style="color: #339933;">&gt;</span> iterator<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> Comparator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">super</span> E<span style="color: #339933;">&gt;</span> comparator<span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
    * @param iterator iterates over an ordered collection
    * @param comparator implements the same comparison used to order the collection
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> DedupingOrderedCollectionIterator<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Iterator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">extends</span> E<span style="color: #339933;">&gt;</span> iterator, <span style="color: #000000; font-weight: bold;">final</span> Comparator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">super</span> E<span style="color: #339933;">&gt;</span> comparator<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">iterator</span> <span style="color: #339933;">=</span> Iterators.<span style="color: #006633;">peekingIterator</span><span style="color: #009900;">&#40;</span>iterator<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">comparator</span> <span style="color: #339933;">=</span> comparator<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">boolean</span> hasNext<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">return</span> iterator.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> E next<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">final</span> E next <span style="color: #339933;">=</span> iterator.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>iterator.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&amp;&amp;</span> comparator.<span style="color: #006633;">compare</span><span style="color: #009900;">&#40;</span>next, iterator.<span style="color: #006633;">peek</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    iterator.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #000000; font-weight: bold;">return</span> next<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> remove<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">UnsupportedOperationException</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Removes duplicates from the elements returned by provided iterator.
    * The provided iterator must return the elements in the order elements in the order defined by the comparator.
    * The first element of a series of duplicates is returned by this iterator.
    * @param  Type of element returned by the iterator.
    */
    public final class DedupingOrderedCollectionIterator&lt;E&gt; implements Iterator&lt;E&gt; {
    private final PeekingIterator&lt;E&gt; iterator;
    private final Comparator&lt;? super E&gt; comparator;
    
    /**
    * @param iterator iterates over an ordered collection
    * @param comparator implements the same comparison used to order the collection
    */
    public DedupingOrderedCollectionIterator(final Iterator&lt;? extends E&gt; iterator, final Comparator&lt;? super E&gt; comparator) {
    this.iterator = Iterators.peekingIterator(iterator);
    this.comparator = comparator;
    }
    
    public boolean hasNext() {
    return iterator.hasNext();
    }
    
    public E next() {
    final E next = iterator.next();
    while (iterator.hasNext() &amp;&amp; comparator.compare(next, iterator.peek()) == 0) {
    iterator.next();
    }
    return next;
    }
    
    public void remove() {
    throw new UnsupportedOperationException();
    }
    }</p></div>
    ;i:2;s:6970:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #008000; font-style: italic; font-weight: bold;">/**
    * Removes duplicates from the elements returned by provided iterator.
    * The provided iterator must return the elements in the order elements in the order defined by the comparator.
    * The first element of a series of duplicates is returned by this iterator.
    * @param  Type of element returned by the iterator.
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #000000; font-weight: bold;">class</span> DedupingOrderedCollectionIterator<span style="color: #339933;">&lt;</span>E<span style="color: #339933;">&gt;</span> <span style="color: #000000; font-weight: bold;">extends</span> AbstractIterator<span style="color: #339933;">&lt;</span>E<span style="color: #339933;">&gt;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> PeekingIterator<span style="color: #339933;">&lt;</span>E<span style="color: #339933;">&gt;</span> iterator<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> Comparator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">super</span> E<span style="color: #339933;">&gt;</span> comparator<span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
    * @param iterator iterates over an ordered collection
    * @param comparator implements the same comparison used to order the collection
    */</span>
    <span style="color: #000000; font-weight: bold;">public</span> DedupingOrderedCollectionIterator<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Iterator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">extends</span> E<span style="color: #339933;">&gt;</span> iterator, <span style="color: #000000; font-weight: bold;">final</span> Comparator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">super</span> E<span style="color: #339933;">&gt;</span> comparator<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">iterator</span> <span style="color: #339933;">=</span> Iterators.<span style="color: #006633;">peekingIterator</span><span style="color: #009900;">&#40;</span>iterator<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">comparator</span> <span style="color: #339933;">=</span> comparator<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">protected</span> E computeNext<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>iterator.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">final</span> E next <span style="color: #339933;">=</span> iterator.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>iterator.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&amp;&amp;</span> comparator.<span style="color: #006633;">compare</span><span style="color: #009900;">&#40;</span>next, iterator.<span style="color: #006633;">peek</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    iterator.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #000000; font-weight: bold;">return</span> next<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #000000; font-weight: bold;">return</span> endOfData<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Removes duplicates from the elements returned by provided iterator.
    * The provided iterator must return the elements in the order elements in the order defined by the comparator.
    * The first element of a series of duplicates is returned by this iterator.
    * @param  Type of element returned by the iterator.
    */
    public final class DedupingOrderedCollectionIterator&lt;E&gt; extends AbstractIterator&lt;E&gt; {
    private final PeekingIterator&lt;E&gt; iterator;
    private final Comparator&lt;? super E&gt; comparator;
    
    /**
    * @param iterator iterates over an ordered collection
    * @param comparator implements the same comparison used to order the collection
    */
    public DedupingOrderedCollectionIterator(final Iterator&lt;? extends E&gt; iterator, final Comparator&lt;? super E&gt; comparator) {
    this.iterator = Iterators.peekingIterator(iterator);
    this.comparator = comparator;
    }
    
    protected E computeNext() {
    if (iterator.hasNext()) {
    final E next = iterator.next();
    while (iterator.hasNext() &amp;&amp; comparator.compare(next, iterator.peek()) == 0) {
    iterator.next();
    }
    return next;
    }
    return endOfData();
    }
    }</p></div>
    ";}
categories:
  - Programming
---
Let&#8217;s implement an iterator.

<pre lang="java" line="1">/**
 * Removes duplicates from the elements returned by provided iterator.
 * The provided iterator must return the elements in the order elements in the order defined by the comparator.
 * The first element of a series of duplicates is returned by this iterator.
 * @param  Type of element returned by the iterator.
 */
public final class DedupingOrderedCollectionIterator&lt;E> implements Iterator&lt;E> {
    private final PeekingIterator&lt;E> iterator;
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
}</pre>

First, if you&#8217;re confused about the generic wildcards, watch [Josh Bloch&#8217;s presentation entitled **Effective Java Reloaded**](http://www.youtube.com/watch?v=pi_I7oD_uGI) and watch for the reference of &#8220;producer extends, consumer super&#8221; (aka PECS) or reference [Josh Bloch&#8217;s second edition of Effective Java](http://www.amazon.com/gp/product/0201310058?ie=UTF8&tag=davidleston-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0201310058 "Effective Java(TM) Programming Language Guide (The Java Series) by Joshua Bloch").

Second, using [Google&#8217;s PeekingIterator](http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/PeekingIterator.html "Javadoc for com.google.common.collect.PeekingIterator<E>") often reduces the code you need to deal with iterators.

Third, when implementing an iterator, you usually have to worry about what happens when `next()` is called when `hasNext()` would return false. What exception are you supposed to throw? And I keep coding the same implementation for `remove()` and always forget what exception it&#8217;s supposed to throw.  [Google&#8217;s AbstractIterator](http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/AbstractIterator.html "com.google.common.collect.AbstractIterator<T>") to the rescue!

Here&#8217;s the same iterator written with com.google.common.collect.AbstractIterator<T>:

<pre lang="java" line="1">/**
 * Removes duplicates from the elements returned by provided iterator.
 * The provided iterator must return the elements in the order elements in the order defined by the comparator.
 * The first element of a series of duplicates is returned by this iterator.
 * @param  Type of element returned by the iterator.
 */
public final class DedupingOrderedCollectionIterator&lt;E> extends AbstractIterator&lt;E> {
    private final PeekingIterator&lt;E> iterator;
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
}</pre>

AbstractIterator allows you to write concise iterators with consistent behavior.