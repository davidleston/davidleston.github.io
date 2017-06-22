---
id: 38
title: Processing in batches and improving maintainability
date: 2008-06-28T08:12:56+00:00
author: David
layout: post
guid: http://www.davidleston.com/?p=38
permalink: /2008/06/processing-in-batches-and-improving-maintainability/
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:6772:"
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000066; font-weight: bold;">void</span> process<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> List<span style="color: #339933;">&lt;</span>Foo<span style="color: #339933;">&gt;</span> foos<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">final</span> ArrayList<span style="color: #339933;">&lt;</span>bar<span style="color: #339933;">&gt;</span> batch <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;</span>bar<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span>batchSize<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Foo foo <span style="color: #339933;">:</span> foos<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>isValid<span style="color: #009900;">&#40;</span>foo<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">final</span> Bar transformed <span style="color: #339933;">=</span> transform<span style="color: #009900;">&#40;</span>foo<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    batch.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>transformed<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>batch.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">%</span> batchSize <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    processBatch<span style="color: #009900;">&#40;</span>batch<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    batch.<span style="color: #006633;">clear</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    processBatch<span style="color: #009900;">&#40;</span>batch<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">// returns true if we want to process this Foo, otherwise returns false</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">boolean</span> isValid<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Foo foo<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">// makes a Bar out of a Foo</span>
    <span style="color: #000000; font-weight: bold;">private</span> Bar transform<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Foo foo<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> processBatch<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> ArrayList<span style="color: #339933;">&lt;</span>Bar<span style="color: #339933;">&gt;</span> bars<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    openTransaction<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">for</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Bar bar <span style="color: #339933;">:</span> bars<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    executeQuery<span style="color: #009900;">&#40;</span>bar<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    closeTransaction<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">void process(final List&lt;Foo&gt; foos) {
    final ArrayList&lt;bar&gt; batch = new ArrayList&lt;bar&gt;(batchSize);
    
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
    
    private void processBatch(final ArrayList&lt;Bar&gt; bars) {
    openTransaction();
    for(final Bar bar : bars) {
    executeQuery(bar);
    }
    closeTransaction();
    }</p></div>
    ;i:2;s:7775:
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000066; font-weight: bold;">void</span> process<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> List<span style="color: #339933;">&lt;</span>Foo<span style="color: #339933;">&gt;</span> foos<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">final</span> Iterator<span style="color: #339933;">&lt;</span>Foo<span style="color: #339933;">&gt;</span> validFoos <span style="color: #339933;">=</span> Iterators.<span style="color: #006633;">filter</span><span style="color: #009900;">&#40;</span>foos.<span style="color: #006633;">iterator</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, isValid<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">final</span> Iterator<span style="color: #339933;">&lt;</span>Bar<span style="color: #339933;">&gt;</span> bars <span style="color: #339933;">=</span> Iterators.<span style="color: #006633;">transform</span><span style="color: #009900;">&#40;</span>validFoos, transform<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">final</span> Iterator<span style="color: #339933;">&lt;</span>Iterator<span style="color: #339933;">&lt;</span>Bar<span style="color: #339933;">&gt;&gt;</span> batches <span style="color: #339933;">=</span> Iterators.<span style="color: #006633;">partition</span><span style="color: #009900;">&#40;</span>bars, batchSize, <span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">while</span><span style="color: #009900;">&#40;</span>batches.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">Iterator</span> batch <span style="color: #339933;">=</span> batches.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    processBatch<span style="color: #009900;">&#40;</span>batch<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> Predicate isValid <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Predicate<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">// returns true if we want to process this Foo, otherwise returns false</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">boolean</span> apply<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Foo foo<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> Function transform <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Function<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">// makes a Bar out of a Foo</span>
    <span style="color: #000000; font-weight: bold;">public</span> Bar apply<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Foo foo<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> processBatch<span style="color: #009900;">&#40;</span>Iterator<span style="color: #339933;">&lt;</span>Bar<span style="color: #339933;">&gt;</span> bars<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    openTransaction<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">while</span><span style="color: #009900;">&#40;</span>bars.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">final</span> Bar bar <span style="color: #339933;">=</span> batch.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    executeQuery<span style="color: #009900;">&#40;</span>bar<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    closeTransactioin<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">void process(final List&lt;Foo&gt; foos) {
    final Iterator&lt;Foo&gt; validFoos = Iterators.filter(foos.iterator(), isValid);
    final Iterator&lt;Bar&gt; bars = Iterators.transform(validFoos, transform);
    final Iterator&lt;Iterator&lt;Bar&gt;&gt; batches = Iterators.partition(bars, batchSize, false);
    
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
    
    private void processBatch(Iterator&lt;Bar&gt; bars) {
    openTransaction();
    while(bars.hasNext()) {
    final Bar bar = batch.next();
    executeQuery(bar);
    }
    closeTransactioin();
    }</p></div>
    ";}
categories:
  - Programming
---
Here&#8217;s a common pattern:

<pre lang="java" line="1">void process(final List&lt;Foo> foos) {
    final ArrayList&lt;bar> batch = new ArrayList&lt;bar>(batchSize);

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

private void processBatch(final ArrayList&lt;Bar> bars) {
    openTransaction();
    for(final Bar bar : bars) {
        executeQuery(bar);
    }
    closeTransaction();
}
</pre>

We have some code duplication: `processBatch` appears twice in `process`. Also, we&#8217;re iterating over two collections in order to process each Bar: we&#8217;re iterating over `foos` in `process` and `bars` in `processBatch`. With the help of [Google Collections](http://code.google.com/p/google-collections/), we can do better:

<pre lang="java" line="1">void process(final List&lt;Foo> foos) {
    final Iterator&lt;Foo> validFoos = Iterators.filter(foos.iterator(), isValid);
    final Iterator&lt;Bar> bars = Iterators.transform(validFoos, transform);
    final Iterator&lt;Iterator&lt;Bar>> batches = Iterators.partition(bars, batchSize, false);

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

private void processBatch(Iterator&lt;Bar> bars) {
    openTransaction();
    while(bars.hasNext()) {
        final Bar bar = batch.next();
        executeQuery(bar);
    }
    closeTransactioin();
}
</pre>

You may want to look at the [Javadoc for the Iterators class in Google Collections](http://google-collections.googlecode.com/svn/trunk/javadoc/index.html?com/google/common/collect/Iterators.html "com.google.common.collect.Iterators") to better understand what&#8217;s happening here.

We removed the duplicate code. And while we still have two loops, one in `process` and one in `processBatch`, these loops are iterating over the same collection: `foos`. In addition, `process` has fewer lines of code. Granted, we have more lines of code elsewhere, but a real `process` method is likely to be more complex. By reducing the number of code blocks (braces) in `process`, we&#8217;re making it easier to read and maintain.