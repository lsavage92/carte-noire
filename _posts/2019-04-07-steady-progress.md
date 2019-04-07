---
layout:     post
title:      Steady Progress
date:       2019-04-07 12:30:00
author:     Luke Savage
summary:    Introduced to game development
categories: game development
thumbnail:  aviato
tags:
- game development
- C#
- Unity
- Unity3D
---
# Introduction
Its been about one week since I chose to follow a [few passions](http://http://lukesavage.me/personal/2019/03/31/reaching-beyond/) and I'm happy to say that I have worked on 2 out of the 3 areas of focus almost every day of last week. I spent most of my time on game development because that has been the most interesting so far. This has been a refreshing exploration so far and I'm finding myself having trouble sitting down to write this blog instead of programming more! But, this blog is also part of my goals so ... here I am :). I want to try to make sure my posts are organized so this one will focus on what I have learned in game development and I will have other posts for Elixir and Web Workers (Surprise!). 

This last week I went through 3 basic Unity3D tutorials: [Unity Interactive Tutorials](https://unity3d.com/learn/tutorials/s/interactive-tutorials), [Roll-A-ball](https://unity3d.com/learn/tutorials/s/roll-ball-tutorial) and [Space Shooter](https://unity3d.com/learn/tutorials/s/space-shooter-tutorial). My understanding of Unity, game objects, scenes and adding behavior with C# has grown quickly from these tutorials! I'm starting to feel like I will soon be able to tackle a game of my own. After a _few_ more tutorials and extending some of the games I've built so far that is...

## Unity Interactive Tutorials
These tutorials were great. I found them analogous to a phantom tutorial on a web application. I don't have a ton to say about it other than it's quick, easy and a good first step towards approaching the Unity editor and beginning to understanding how components and scene objects fit together.

## Roll-A-Ball
I have actually done part of this tutorial before but gave up because ¯\_(ツ)_/¯. This time I was far more determined! It only took a few hours but after that the game was complete. The Roll-A-Ball tutorial is the clear next step from the Interactive Tutorials. It introduced a few more topics to me including the camera, physics, vectors and scripting.

It was in this tutorial that I got my first good taste of C#. I was pleasantly surprised with how easy it was to understand and write. It's been years since I have written in Java/C/C++ or anything that resembles C# but still found it very natural to write in and even found it enjoyable!

The amount of code for this project was very small but that experience was huge to me. I was absolutely blown away at how _little_ code you need to write some game logic. Feelings of nostalgia washed over me as I was taken back to the days when web development was new to me and the day came where I felt the same awe that _it's possible_ to build _anything_ given the right time and resources. This feeling is at the heart of what I love about software engineering <3.

## Space Shooter
This was a significantly more involved game than Roll-A-Ball but still completely understandable if you have prior code experience. I probably spent about 5 times as much time on this tutorial than the Roll-A-Ball one and it was fun the whole time! This introduced some more concepts to me such as lighting, prefabs, audio, textures and materials. It also continued to expand on C# and how your scripts all connect.

I was very curious to how you tie all these siloed behaviors together into a cohesive game. It seems that you _need_ a game object in order to have a script affect the behavior of the game. So you create an empty game object called `Game Controller` in order to have the overarching game logic. I'm not _entirely_ sure yet but it seems that there is a whole lot of using `GetComponent<T>()` and `Instantiate` going on in games in order to tie behavior together and create objects/enemies/etc.

## Conclusion
I had a hell of a lot of fun making these simple games last week and I can't wait to continue. These posts aren't going to be super interesting until I start to dive into the deep end and start developing without the tutorials holding my hand. See you next week!