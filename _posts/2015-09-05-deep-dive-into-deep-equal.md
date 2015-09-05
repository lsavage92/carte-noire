---
layout:     post
title:      Deep dive into deepEqual
date:       2015-09-05 9:16:00
author:     Luke Savage
summary:    Extending the Jasmine testing framework to include deepEqual and notDeepEqual
categories: technical
thumbnail:  anchor
tags:
- Jasmine
- Tape
- testing
- equality
- deepEqual
---
# Introduction
This post isn't really about deep equality itself, I just really liked the title. I want to talk about the [Jasmine](http://jasmine.github.io/) testing framework and how to extend it to include deep equality functionality like our good friend [Tape](https://github.com/substack/tape).

In the world of Tape you can simply test for deep equality with an assertion like `t.deepEqual(myValue, expectedValue);` which is fantastic. The wonderful developers of Tape wrote their own module to test for deep equality but even though I love Tape, we will not be using that module to extend Jasmine.

Why you ask? Well mostly because it doesn't work for the current project I am working on that allows you to write framework agnostic tests in really small comments within the file you wish to test ([SpeckJS](https://www.npmjs.com/package/speckjs)). Enough self-promotion, let's make Jasmine better!

# The Good Part
In order to extend Jasmine to have both `deepEqual` and `notDeepEqual` we are going to need a way to test for this. I chose to use the [node.js assert module](https://nodejs.org/api/assert.html). Simply require this in your test file and we will then have access to the two methods we need: `assert.deepEqual()` and of course `assert.notDeepEqual()`.

Let's start with some code and try it out:

{% highlight javascript %}
var assert = require('assert');

describe('deep equality', function(){
  it('should deepEqual like a boss', function(){
    var pass = assert.deepEqual(ourObject, expectedObject);
    expect(pass).toBe(true);
  });
});
{% endhighlight %}

You might be thinking, "but wait Luke, assert.deepEqual() doesn't return a boolean!". And you are absolutely right about that. This was the first roadblock to using this module, but there is an easy workaround.

First, we have to think about what _is_ the result of that function call? As it turns out, if the two objects are deeply equal, then nothing happens and it returns undefined. However, if they are not equal then it throws an error. This should definitely make a light bulb appear above your head. Here's how I did it:

{% highlight javascript %}
var assert = require('assert');

describe('deep equality', function(){
  it('should deepEqual like a boss', function(){
    var pass;
    try {
      pass = true;
      assert.deepEqual(ourObject, expectedObject);
    } catch(e) {
      pass = false;
    }
    expect(pass).toBe(true);
  });
});
{% endhighlight %}

# Conclusion
As a result, the exception is now suppressed and handled with this block. If the two objects pass the test, then pass is `true` and all is well. Otherwise if they are not equal, the exception is thrown and pass is set to false which causes the test to fail.

After this it should be obvious how to implement `notDeepEqual` as well. I hope this helps and maybe next time you'll just use Tape ;).