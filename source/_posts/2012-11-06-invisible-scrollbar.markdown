---
layout: post
title: "Invisible scrollbar"
date: 2012-11-06 20:00
comments: true
categories: css
---
You want to hide your scroll bar, but you still want to keep the scrolling ability. Then you're gonna need an invisible scroll bar, this article might quite fit your needs.

There is no any javascript are required to make this work. The concept is dead simple. You need 2 divs. One is "wrapper", another is "content". You put your context into "content", and there sure do will have a scroll bar there. Set the "content" size, and set the "wrapper" size, make the "wrapper"'s size a bit smaller than "content". For more accuracy, which is "wrapper"'s width minus "content" scroll bar's width.

Last step is set "wrapper"'s `overflow-x: hidden`, and `overflow-y: auto`. That's all. Period.

For the code please refer to 
[https://gist.github.com/4024297](https://gist.github.com/4024297)