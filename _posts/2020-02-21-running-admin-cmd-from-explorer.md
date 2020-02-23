---
layout: post
title: Running Admin CMD From Windows Explorer
date: 2020-02-21 09:23
author: Prasanth Kanna
tags: [Batch Scripting]
summary: Have you ever wondered how to launch cmd directly from Windows Explorer without having to cd again to that folder? This blog will explain to do that and also to launch the admin cmd
image:  11.jpg
---

Have you ever wondered how to launch cmd directly from Windows Explorer without having to cd again to that folder? This blog will explain to do that and also to launch the admin cmd

[EXISTING SOLUTION](#existing-solution)

[PROBLEM WITH EXISTING SOLUTION](#problem-with-existing-solution)

[OBSERVATION](#observation)

[SOLUTION](#solution)

## EXISTING SOLUTION

The shortcut to open a cmd from a windows explorer and change the directory automatically there is:

    {% highlight markdown %}
    Ctrl-L
    cmd{% endhighlight %}

**BEHIND THE SCENES:**

> * Ctrl-L will select the windows path to the current open folder by highlighting the address bar.
> * Typing System32 apps in the address bar will run those applications. You can find the System32 apps in :
        `C:\WINDOWS\system32`
>
> * For example typing `cmd` in address bar will launch:
        `C:\WINDOWS\system32\cmd.exe /k pushd %origin%`
>
>   where `%origin%` is the path of current open folder
> * Thus cmd will automatically change its directory to the current open folder by passing the path as argument.

## PROBLEM WITH EXISTING SOLUTION

The above shortcut is quick and easy to open cmd at the current folder. But It will not opem cmd in Administrator mode.

## OBSERVATION



## SOLUTION
