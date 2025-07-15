---
author: Roy Straub
categories:
- Craftsmanship
comments: true
description: Battleship is a fun and nostalgic game, even more so when you try to
  program it! Learn about the Battleship Codekata and give it a go yourself.
featured: false
hidden: false
image: assets/images/18-battleship.webp
layout: post
tags:
- CodeKatas
- Battleship
title: ⚗️ Concocting the Battleship Codekata
---

B1. _Miss._ A2. _Hit._ That's right, it's Battleship! I created a Codekata for this nostalgic game. Learn all about it in this post.

## ✒️ Why Create a Codekata?
I recently played Battleship for the first time in my life (yes I know, shame on me) and had a great time doing so. In my spare time, I love doing Codekatas, and since I am currently learning Scala even more so (Katas are great to learn languages).

My thoughts started racing about Battleship and all of a sudden the idea came to mind to create a little program for it. Programming a game makes for great exercise. Thus the Battleship Kata was born. 

One of the things I love about creating a Codekata is how you're already invested in the idea behind it. You're probably quite motivated to give solving it a go!

Codekatas are fun, especially the relatable ones like [Mastermind](https://codingdojo.org/kata/Mastermind/), [Minesweeper](https://codingdojo.org/kata/Minesweeper/) or [Bowling](https://kata-log.rocks/bowling-game-kata). I find these very enjoyable precisely because they are very _visual_ and _evocative_. They also require little explanation since you probably are familiar with the rules.

Let's see how the Battleship Codekata holds up to these traits.

## 🚢 The Battleship Codekata
Two players play [Battleship](https://en.wikipedia.org/wiki/Battleship_(game)). Each player has a grid where he places his five ships, after which they take turns shooting until a player has lost all ships. That's the game in a nutshell. Sounds like fun, right?

The Codekata consists of explanations of the rules, some hints, and ideas to make solving it more challenging. If you want to give it a go, you can find it on my [github](https://github.com/rstraub/battleship-kata).

The rules are quite simple, but capturing them in a program makes for some interesting practice. Though I haven't completed a solution myself, I do have a work in progress (which you can find [here](https://github.com/rstraub/battleship-kata-scala)). There are similarities with the Reversi and Minesweeper Kata, which are games also centering around a grid. 

Let's look at some of the challenges I noticed while doing this Kata.

## 🥵 Challenges of the CodeKata
The Battleship Kata is challenging (and interesting!) in two regards for me. 

First is how you model the game, especially the _Grid_ in your program. This is a great lesson about the separation of [_Model_ and _View_](https://martinfowler.com/eaaDev/SeparatedPresentation.html) as the representation in your program doesn't need to match reality. Maybe you don't even need a grid, but work with just ships!

Secondly, deciding which object knows which, and who is responsible for negotiating between them is an interesting problem. There's no clear-cut answer and each solution has its consequences.

Challenges bring forth learning, what can you learn from this Codekata?

## 🎓 Lessons to be Learned
Like all [Codekatas]({{site.baseurl}}/improving-with-codekatas/), what you learn from doing one is entirely up to you. That being said, some Katas are more suitable than others for learning a specific concept.

The Battleship Kata is especially suited to learn:  
* **Baby Steps.** You might be tempted to write all the code for the Grid so can start placing ships and taking shots, but how can you make small incremental steps to get to your goal?  
* **Modelling.** Which objects should do what and know who? How can you express the model as expressively as possible? You can even apply _Tactical Patterns_ from Domain-Driven Design here, like Aggregates or Value Objects.  
* **Simple Design.** What is the bare minimum of code, whilst retaining readability and expressiveness you can use to solve this problem.  
* **(Clean) Architecture.** How will you separate the model from the means of delivering input and output, such as a command-line interface? 

These are just some takeaways you can have from this Kata, but there are probably tons more lessons here!

## 🔮 Future Plans
The Battleship Kata is publicly available because I hope that other people will enjoy solving it as much as I am. Check it out and give it a shot (pun intended).

I also intend to post it to Codekata catalogs like [kata-log.rocks](https://kata-log.rocks/index.html) and [codingdojo.org](https://codingdojo.org/) in the hope of making it more known. Hopefully people will even contribute, making the Kata even better!

_What do you think? Does the Battleship Kata sound interesting to you? Do you have ideas about it? Let me know in the comments below!_