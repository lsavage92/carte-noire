---
layout:     post
title:      Separation of concerns with Backbone.js
date:       2015-07-16 9:13:00
author:     Luke Savage
summary:    Overview of MVC architecture with Backbone.js as an example
categories: technical
thumbnail:  unlink
tags:
- backbone.js
- backbone
- javascript
- MVC
---

After getting my feet wet with Backbone.js I felt it necessary to talk about what the heck these MVC frameworks are and why they do what they do. To begin, MVC stands for Model-View-Controller. This describes the architecture behind the framework and how these different 'units' interact with each other. I'm going to go over each aspect of the MVC architecture and give small code examples to show formatting, but if you're interested in how it works from behind the scenes I would check out the API docs for [Backbone.js](http://http://backbonejs.org/), they are fantastic!

The models of a particular application are the data structures. In a particular model, you would never have any sort of onscreen rendering or DOM manipulations happening. This is purely where the 'state' of your program lives and breeds. Here's a small code example from backbone of what this would look like:

{% highlight javascript %}
var thisModel = Backbone.Model.extend({
  initialize: function(){
    //What happens when this model is created
  },

  someTrigger: function(){
    //Not all models have this trigger function, but it's important for discussion
    this.trigger('myEvent', this);
  }
});
{% endhighlight %}

Woah! What's all this `.extend({})` business and why are you passing it a key-value pairs in a hash? The `extend()` method in Backbone allows you to instantiate a psuedoclassical inheritance pattern within your application without having to do it yourself. Not only that, but because `thisModel` is now a subclass of `Backbone.Model`, it gains access to a lot of really handy methods. Hey, thanks Backbone! This means if I wanted to create a new instance of `thisModel` I would simply do as follows

{% highlight javascript %}
var myModel = new thisModel();
{% endhighlight %}

And just like that, we have a model!

So if we don't render our data to the browser in our models, you can easily assume that will happen in our views. Views in Backbone are used to render our data to the browser by _communicating_ with our models. In short, it is what you will see when you load up an application that was made with Backbone. The code to create a view is not much different from a model and goes as follows:

{% highlight javascript %}
var thisView = Backbone.View.extend({
  initialize: function(){
    //What happens when this view is created
  },

  render: function(){
    //how you would like your view to display the data in the model
  }
});
{% endhighlight %}

At this point you may be wondering how `thisView` would communicate with `thisModel` and the answer is by associating itself with a particular instance of `thisModel`. Let's look at another code example, assuming we fleshed out our above model and view:

{% highlight javascript %}
var myModel = new thisModel();

var myView = new thisView({model: myModel});
{% endhighlight %}

This brings up a few important points about Backbone. One is that just by passing in an object with properties in it, you can extend that model/view to have access to those properties. Two is that by passing in an object that specifies a key of `model` as we show above you can _bind_ a particular model instance with a particular view instance. This binding relationship is what allows you to seperate the concerns of data vs. rendering and as we will see shortly, you also seperate interactions from the user as well. It is this very pattern that gives Backbone its... well backbone!

I want to briefly note that Views come packaged with a special property called `.$el`. Looks like it would be jQuery right? That's because it is! When you are doing your rendering you have access to both the `.$el` property (which defaults to a `<div>`) and you can use Underscores templating to create html templates to be loaded inside your `.$el`.

In the interest of brevity, let's move onto controllers. Now, controllers are where you'll find the funny bone in Backbone (I'm chock full of these puns right now). Technically speaking, there is no `Backbone.Controller` that you can use to create a controller like you would a model or a view. Instead, in Backbone.js when you want a controller you can implement controller-esque features straight into your views. If we take our view from earlier and wanted to add some controller functionality to it we could do something like this:

{% highlight javascript %}
var thisView = Backbone.View.extend({
  initialize: function(){
    //What happens when this view is created
  },

  events: {
    'click': function(){
      //do something to the update the model
    }
  }

  render: function(){
    //how you would like your view to display the data in the model
  }
});
{% endhighlight %}

By adding events to your view, you can capture them and have the view communicate that the user wants something to happen to the model. Conversely, when the data in the model changes, native API events fire off that you can listen for from a view and update the rendering accordingly.

Backbone.js is huge and it would be a lofty attempt to try and fit it all into a single blog post. I hope that this 'jumpstart to Backbone' is helpful in claryfing how the framework is used at its most basic level.
