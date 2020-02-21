---
layout: post
title: Jekyll Tutorial
date: 2020-02-19 16:22
author: Prasanth Kanna
tags: [Jekyll]
summary: A tutorial to create and host blog on Github Pages
image:  01.jpg
---

* Create a New Ogranization on Github

* Create a New Repository in that organization named:

    {% highlight markdown %}
    organization_name.github.io
    {% endhighlight %}

* Copy the Repository URL

* Open VSCode -> Press F1 -> Git: Clone -> paste repo URL -> Select Folder

* Open Terminal:

    {% highlight markdown %}
    ctrl + `
    {% endhighlight %}

* Run

    {% highlight markdown %}
    Jekyll new .

    bundle exec jekyll serve
    {% endhighlight %}
