---
layout:     post
title:      Machine Learning Basics
date:       2019-04-07 12:30:00
author:     Luke Savage
summary:    An understanding check from 2 weeks of ML
categories: python
thumbnail:  robot
tags:
- python
- ml
- machine learning
- tensorflow
- google
---

It's been a couple of weeks since I began studying machine learning with the [Google Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course) and it has been a blast! The first few days were tough due to a lot of new vocabulary and a harsh reminder that I have not done any kind of real math in a while. However, this discomfort was quickly squashed by some math review and some diligent note taking (Shoutout to [desmos](https://www.desmos.com/) for helping me remember graph shapes). After that initial hurdle, it quickly became a lot of fun and soon enough my mind started to wonder what I could do with these skills once I have more confidence in using these tools. For now, I'd like to review some of what I have learned so far about machine learning in general.

The biggest surprise to me right up front is that a machine learning "model" is simply just a math equation. I don't know how this escaped me but I guess _Machine Learning_ always sounded so magical :). So far I have only explored regression models, which are models that predict continuous values. This could be something like predicting median housing values for certain geographic regions, predicting high school grades for certain income levels, etc. This is in contrast to classification models which predict discrete values. A classifier would be a model that can tell a cat from a dog in a picture or tell the letter 'A' from 'T'. Since I only have worked with regression models so far that will be what I discuss in this post.

The TL;DR of a regression model is: try a linear regression equation (line of best fit), calculate loss (error rate) and adjust model hyperparameters to improve the model. A few things to unpack here so let's start with loss. Loss is the distance between a given labeled example and your model (line of best fit). Here is a picture to help visualize what loss is and the difference between high loss (left) and low loss (right) for the same data set.

![loss example](https://developers.google.com/machine-learning/crash-course/images/LossSideBySide.png)

Forgetting about models for a second, if you had the model on the left of the image above, how would you adjust it to be more like the model on the right? First, what does the equation of a line look like?

```y = mx + b```

In machine learning they change the name of slope to _weight_ and y-intercept to `bias`. So instead it looks something like this:

```y' = wx + b```

Just like in math class, to change the lines position in the coordinate plane, you would alter slope and the y-intercept of the equation. But how do we know which model will have the lowest loss? This is when it gets math-y so I'm going to gloss over a few  things here. Basically you have an equation that calculates loss (in this case L2 loss) and then average that loss over a given batch of examples (mean squared loss/error). If we mapped out every possible `w` value and calculated the loss we would have a parabola for the given loss equation used in this course. This gets more complicated with more complex problems. Our goal, is to find the model that sits at the minimum of that parabola. This is done through a process called gradient descent.

![gradient descent example](https://developers.google.com/machine-learning/crash-course/images/GradientDescentGradientStep.svg)

Once we are reasonably sure we are at the minimum of the parabola, we have our model! I'm going to go ahead and stop here for this post. I am further along than this but I have not been writing blog posts so next post I want to begin to step into tensorflow and explain how it can help us discover models with minimal loss for data sets and how to properly train the models!