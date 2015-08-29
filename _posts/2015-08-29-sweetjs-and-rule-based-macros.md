---
layout:     post
title:      Rule based macros? That's sweet.js!
date:       2015-08-29 4:00:00
author:     Luke Savage
summary:    Using sweet.js to create rule based macros
categories: technical
thumbnail:
tags:
- sweet
- sweet.js
- sweetjs
- macros
- javascript
---

Imagine you want to insert your own syntax into a Javascript project without the pain of writing and entire compiler to go from one syntax to another (Like Coffeescript). Sweet.js gives you the ability to define a name with the `macro` keywords, define a few patterns and then whenever you invoke the name you created in your project the pattern will be matched and expanded. This allows for some really powerful stuff, with very simple syntax.

Just to give a basic idea for what one of these might look like, here is a simple identity macro:

{% highlight javascript %}
macro myFirstMacro {
  rule { $x } => { $x }
}
{% endhighlight %}

All this says is that when you use the keyword `myFirstMacro` that you just defined, the sweet.js compiler will look for a pattern following that keyword to match `$x` which is the way sweet.js says to just expand that pattern to itself. I will show an invocation followed by what the compiler would output. Invocation:

{% highlight javascript %}
myFirstMacro "Hello, world!";
{% endhighlight %}

Output:

{% highlight javascript %}
"Hello, world!";
{% endhighlight %}

Now this may not seem very useful from this simple example but let me tweak the example just a little bit to see how this can be used.

{% highlight javascript %}
macro addTwo {
  rule { $x } => { $x + 2 }
}
{% endhighlight %}

Now if we are to invoke this macro here is the invocation and output:
{% highlight javascript %}
//Invocation
addTwo 5;

//Expanded output
5 + 2;
{% endhighlight %}

This article was meant to just be a short and sweet (hah!) intro to macros from sweet.js. If you want to dive a bit deeper take a look at hygienic macros or how you can have [recursive macros](http://jlongster.com/Sweet.js-Tutorial--2--Recursive-Macros-and-Custom-Pattern-Classes), case based macros and even override operators and keywords that Javascript already uses natively.