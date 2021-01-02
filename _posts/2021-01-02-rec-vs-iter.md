---
layout: post
title: Recursion vs Iteration
date: 2021-01-02 16:46
category: 
author: Prasanth Kanna
tags: [Algorithms]
image: rec-vs-iter/rec-vs-iter.jpeg
---

Consider the following example:

{% highlight js %}
// Recursion
const gcdRec = (a,b) => a === 0 ? b : gcd(b % a, a);

// Iteration
const gcdIter = (a,b) => {
    let r;
    while (a !== 0){
        r = b % a;
        b = a;
        a = r;
    }
    return b < 0 ? -b : b;
}
{% endhighlight %}

What do you think is efficient? Use `console.time` on both the functions and find out. Based upon your system, the results can vary.

But theoretically **Iteration approach is more efficient than Recursion approach** due to following reasons:

* Function call overhead
* Increasing memory to store return values
* Call stack overflow on large numbers (If number of recursive calls are higher, then the code will crash)
