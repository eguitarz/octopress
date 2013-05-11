---
layout: post
title: "Javascript bind method"
date: 2013-05-11 17:51
comments: true
categories: 
---
Recently I was thinking how to make my javascript codes more readable. I tried "bind" in Function object and it does help. Function object has a method "bind". It simplify codes and make them more beautiful.

## Syntax
```javascript
fun.bind(thisArg[, arg1[, arg2[, …]]])
```
- `thisArg`: the "this" context to be passed into `fun`
- `arg1`, `arg2` …: additional arguments which passes to `fun`'s scope

The purpose of `bind` is change current context easier. You don't have to create a variable like `self` to store your context.


All right, how does it help me killing my fat codes? Let's look at an example.

```javascript
var camera = { 
    owner: 'Irena',
    shoot: function() {
      console.log('shoot by ' + this.owner);
    } 
}

$(document).on('ready', function() {
  camera.shoot(); 
});

```

I don't want to write function() { … } in document ready event, since i'm calling `camera.shoot` function, it should be fed directly to event binding argument. So it becomes:

```javascript
var camera = { 
    owner: 'Irena',
    shoot: function() {
      console.log('shoot by ' + this.owner);
    } 
}

$(document).on('ready', camera.shoot);
```
Keep an eye on `camera.shoot`, there's no `()` after it. But it's not right, the result prints `shoot by undefined`. Since it's "Function Call" not "Object Method", the context became global variable, here it is `document`. To make it right, the context should be `camera` object. To solve this, I use `bind`:

```javascript
var camera = { 
    owner: 'Irena',
    shoot: function() {
      console.log('shoot by ' + this.owner);
    } 
}

$(document).on('ready', camera.shoot.bind(camera));
```
This style has three benefits:

1. No more ugly curly braces.
2. Make context of the binding function clearer.
3. Separate events binding and function definition.

For my personal opinion, I don't really like the word `bind`, I would like to see it more common.

```
Function.prototype.by = Function.prototype.bind;

var camera = { 
    owner: 'Irena',
    shoot: function() {
      console.log('shoot by ' + this.owner);
    } 
}

$(document).on('ready', camera.shoot.by(camera));
```

I love it, aren't you?


# Reference
- [MDN - Function.prototype.bind](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Function/bind)