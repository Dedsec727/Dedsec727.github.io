---
layout: post
title: C++ On Visual Studio Code
date: 2020-03-07 20:55
category: 
author: Prasanth Kanna
tags: [VSCode, C++]
summary: Setting Up VSCode to Compile & Debug C++
image: cpp-on-vscode/cpp-vscode.png
---

Ever wondered to have a good IDE for C++ with beautiful dark theme and essential features? Stuck on editors like DevC++ & Codeblocks?. Well, If you are familiar with VSCode, and if you want to write some C++ Code for Competitive Coding, then this blog is for you.

[SETUP](#setup)

[DEBUG HELLO WORLD](#debug-hello-world)

## SETUP

* Install [VSCode](https://code.visualstudio.com/){:target="_blank"}
* Install [Microsoft C/C++ extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools){:target="_blank"}. You can install the C/C++ extension by searching for 'c++' in the Extensions view (Ctrl+Shift+X)
* Install [Mingw-w64](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win32/Personal%20Builds/mingw-builds/installer/mingw-w64-install.exe/download){:target="_blank"}

**Mingw-w64 Setup Settings:**

> **Version**: Latest
> 
> **Architecture**: Run Following command in cmd:
>
> {% highlight markdown %}systeminfo | findstr /c:"System Type:"{% endhighlight %}
> 
> If Output is `x86-based PC` select `i686`
>
> else if output is `x64-based PC` select `x86-64`
>
> **Threads**: posix
>
> **Exception**: seh
>
> **Build Version**: 0

## DEBUG HELLO WORLD

* Create a new folder `Hello World` and create `helloworld.cpp` in that folder. Open that folder in vscode.
  
{% highlight c++ %}
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
    vector<string> msg {"Hello", "C++", "World", "from", "VS Code", "and the C++ extension!"};

    for (const string& word : msg)
    {
        cout << word << " ";
    }
    cout << endl;
}
{% endhighlight %}

* Go to Main menu > Terminal > Configure Default Build Task > `g++.exe build active file` (if not shown, restart vscode)
* Open `helloworld.cpp` and press `ctrl + shift + B` to build
* Press F5 > Run > Add Configuration... > C++ (GDB/LLDB) > `g++.exe build and debug active file`
* Open `launch.json` just created by above step and do following steps:

1) Add following configuration: `"targetArchitecture": "x86_64"` <sup>[[2]](#references)</sup>

2) Change following configuration: `"externalConsole": true`

* Add a breakpoint and debug

## REFERENCES

* [1] [https://code.visualstudio.com/docs/cpp/config-mingw](https://code.visualstudio.com/docs/cpp/config-mingw){:target="_blank"}
* [2] [https://github.com/microsoft/vscode-cpptools/issues/2376](https://github.com/microsoft/vscode-cpptools/issues/2376){:target="_blank"}
