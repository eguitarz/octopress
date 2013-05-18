---
layout: post
title: "Browser atanomy"
date: 2013-05-18 16:48
comments: true
categories: 
---

Recently, I'm interested in browser behaviors, here's the note after I read a nice article [How browser work](http://taligarsiel.com/Projects/howbrowserswork1.htm).

- Browser components
![](images/layers.png)

##Components - UIs
- UI: Elements except main window. (Address bar, bookmark…)
- UI Backend: Generic elements in main window. (Checkbox, input…)

##Components - engines
- Browser engine: Rendering engine interface.
- Rendering engine: draw requested content.
- JS interpreter: run JS.

##Components - backends
- Networking: platform independent network interface.
- Data Persistence: data storage.

#Render engine
Main flow:
1. Parsing HTML and build dom tree.
2. Render with styling info.
3. Layout and positioning.
4. Painting.
![](images/flow.png)

##Render engine of Safari & Gecko

- Safari parser flow

![](images/webkitflow.png)

- Gecko parser flow

![](images/mozillaflow.jpg)

Basically equal, but Gecko has a Content Sink process to making DOM elements.

#What does parser do?
![](images/parser.png)

It breaks the content into lexers (tokenizers), and constructing the parse tree via Syntax rule, then translates result to machine code.

##HTML parser

HTML is NOT a context free grammar which means it's more difficult to implement.

![](images/htmlparser.png)

![](images/htmlparserflow.gif)


##CSS parser
CSS is a context free grammar which means it could be build via parser generator by providing token definition and syntax.

![](images/cssparser.png)

##The order of parsers
###Scripts
Synchronous, top to bottom, only one script could be parsed/executed at a time, excepts \<script defer\> or \<script async\>(HTML5).


###Speculative parsing
While executing script, another thread will fetch the rest scripts in document, for optimization.


###Style sheets
Asynchronous. Firefox blocks scripts until all css are parsed. Webkit does only when the scripts access unsafe css.

# It's not the end
Next topic will talk about render tree and Layout.