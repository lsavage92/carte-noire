---
layout:     post
title:      Classical, prototypal and psuedoclassical inheritance
date:       2015-06-08 9:16:00
author:     Luke Savage
summary:    Top level differences between classical, prototypal and psuedoclassical inheritance
categories: jekyll
thumbnail:  arrows-v
tags:
- inheritance
- prototypal
- classical
- psuedoclassical
- javascript
---

If you are familiar with both class-based object oriented languages and prototypal OO languages then you know what I mean when I say that inheritance
works quite differently in those different paradigms. I want to take a minute to look at a quick, top-level overview of what makes Javascript's
inheritance pattern so different from languages like C++ and Java.

An object (in the programming sense of the word) is a virtual abstraction of a real-world object. And a class (as seen in C++ and Java) is a generalization about different objects. In class-based OO languages you have to have a Class first to create an object. Checkout the following diagram:

```
|--------------------------------------|----------------------------------|
|    Human    |   Superclass of Man    | Generalization of generalization |
|-------------|------------------------|----------------------------------|
|    Man      |  Class of lukeSavage   |  Generalization of abstraction   |
|-------------|------------------------|----------------------------------|
|  lukeSavage | Variable holding object|      Real world abstraction      |
|-------------|------------------------|----------------------------------|
| Luke Savage |   Real World Person    |                -                 |
|-------------|------------------------|----------------------------------|
```

This gives us a pretty good idea of what it means to be an object and a class within class-based OO languages. In prototypal languages, you do not need a class first to create an object. We can just create empty objects like `var obj = {}` (technically they go up the prototype chain to the Object.prototype, but that's a different story). Now let's look at the same diagram but in Javascript:

```
|-------------------------------------------------------------------------|
|   Object    |   Prototype of Human   | Generalization of generalization |
|-------------|------------------------|----------------------------------|
|    Human    |   Prototype of Man     | Generalization of generalization |
|-------------|------------------------|----------------------------------|
|    Man      | Prototype of lukeSavage|  Generalization of abstraction   |
|-------------|------------------------|----------------------------------|
|  lukeSavage | Variable holding object|      Real world abstraction      |
|-------------|------------------------|----------------------------------|
| Luke Savage |   Real World Person    |                -                 |
|-------------|------------------------|----------------------------------|
```

It may not seem much different from a glance at these two diagrams because the pattern of generalization seems the same. The key difference is actually in how you implement one versus the other. As I had stated previously, in C++, Java and similar languages, you _must_ have a class first for the object to get it's properties from and prototypal languages do not need such a class.

If you have previously worked with class-based OO languages but are now working in Javascript there is another inheritance pattern called psuedoclassical. [Psuedoclassical](http://javascript.info/tutorial/pseudo-classical-pattern) is essentially the same as prototypal inheritance but has a thin layer of interface over it in order to make it feel more like classical. It is important to note that it is _still_ inheriting through a prototype chain, but the layout is meant to make it feel more familiar.
