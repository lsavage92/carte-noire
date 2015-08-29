---
layout:     post
title:      setTimeout and this
date:       2015-07-08 2:47:18
author:     Luke Savage
summary:    Dealing with binding issues of the 'this' keyword
categories: technical
thumbnail:  chain
tags:
- this
- setTimout
- javascript
- binding
---

Dealing with the different binding patterns of `this` while developing in Javascript can be a daunting task
for even the most veteran developers. Before we jump into looking at `window.setTimeout`, repeat after me:

> 'this' is just a reference to whatever called the function

Knowing this will help figure out what is bound to this about 90% of the time. For brevity sake, I just want to look
at one particular behavior that involves callbacks.

Take a look at the following code for a minute, assume a Dog class:

{% highlight javascript %}
Dog.prototype.eat = function(){
  this.hunger--;
};

var fido = new Dog();

setTimeout(fido.eat, 1000);
{% endhighlight %}

What do you suppose would happen?

If you are like me (and a majority of other developers), you might assume that `fido.eat()` would be called in 1000ms. But this
assumption would lead to hours of painstaking debugging.

As I said in the beginning of the post, `this` is just a reference to whatever called the function. So what is calling the function? We know
it's definitely not the `fido` instance so let's peak at an abstracted version of `setTimeout()`:

{% highlight javascript %}
var setTimeout = function(callback, delay) {
  //something to make a delay happen

  callback();
};
{% endhighlight %}

It may not be intuitively obvious just yet, but this is the answer to your woes. In the lexical scope of the `setTimeout()` function, the local
variable `callback` gets bound to a function object at runtime. In our case `callback = fido.eat()`. This assignment does *not* maintain the context of `fido` because all that is passed along to the local `callback` variable is a _function object_. In this case, when you call `setTimeout()`, it would be bound to `window` instead of `fido` like you want it to be.

The solution here is to use `bind()` to maintain your context of what `this` refers to. I won't dive deep into the why (maybe in a future post) but here's how:

{% highlight javascript %}
Dog.prototype.eat = function(){
  this.hunger--;
};

var fido = new Dog();

setTimeout(fido.eat.bind(fido), 1000);
{% endhighlight %}