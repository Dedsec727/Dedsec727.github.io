---
layout: post
title: Rust Over Other Languages
date: 2020-05-31 15:33
category: 
author: Prasanth Kanna
tags: [Rust]
image: rust_over_other_languages/rust-logo.jpg
---

Rust is getting soo popular that it is one of the highest paying languages in the world, ranking 4th after Perl, Scala & Go.
What made Rust that much popular? What are the advantages of Rust over other languages? This blog compares some promising
features of Rust with good old C++, that make Rust stand out. This blog does not point out differences, rather it focuses
on how rust is perfect at handling some typical errors in C++

## No Increment & Decrement Operators

Consider the following C++ code:

{% highlight c++ %}
int i = 0;
int j = i++;
{% endhighlight %}

Problem: General misconception in the above code, unless you are a cpp pro, is assuming that j is going to be assigned 1
while i also becomes 1. Since the above code is a post increment, meaning the increment will happen after assigning i to j.
Even though this small piece of code may seem to be pretty easy by even a beginner, but mishandling pre increment
 and post increments can lead to serious bugs.

Rust handles this by completely avoiding increments and decrement operators. So if you have to increment a variable you have to do this explicitly:

{% highlight rust %}
let i: i32 = 0;
i = i + 1;
let j = i;
{% endhighlight %}

The above code seems good enough right? But actually it won't compile.

In rust every variable is mutable by default. You cannot modify a variable once you initialize it. So i the above code
both i and j are mutable, so we cannot increment i. We need to explicitly specify that i is mutable using mut keyword.

{% highlight rust %}
let mut i: i32 = 0;
i = i + 1;
let j = i;
{% endhighlight %}

The above nudge is really useful. If one part of our code operates on the assumption that a value will never change and another part of our code changes that value, it’s possible that the first part of the code won’t do what it was designed to do. The cause of this kind of bug can be difficult to track down after the fact, especially when the second piece of code changes the value only sometimes.

## Double Free Error

When two data pointers, suppose s1 & s2, point to same memory location, and when you try to delete/drop them from memory, they will both try to free the same memory. This is known as a double free error and is one of the memory safety bugs. Freeing memory twice can lead to memory corruption, which can potentially lead to security vulnerabilities.

Consider following C++ code:

{% highlight c++ %}
string *s1 = new string("Hello");
string *s2 = s1;

delete s1;
delete s2;
{% endhighlight %}

Problem: The above code compiles perfectly in C++. You will only know about Double Free error during runtime while using a debugger.
Else it will be very hard to track this error and it can lead to memory corruption.

Rust handles this error by moving ownership of s1 to s2 and making s1 invalid. Consider following Rust code:

{% highlight rust %}
let s1 = String::from("Hello");
let s2 = s1;

drop(s1);
drop(s2);
{% endhighlight %}

The above code will not even compile, as we are trying to drop a moved object s1.
Not just dropping s1, but also trying to use s1 later won't compile the code

If you’ve heard the terms shallow copy and deep copy while working with other languages, Rust uses move instead of shallow copy

## Data Race

(To be continued...)
