---
layout: post
title: "Why You Should Avoid Impl's, Abstracts and IThingies 🏷"
author: Roy Straub
categories: []
tags: []
image: assets/images/construction.jpg
description: ""
featured: true
hidden: false
comments: true
---

stuff.

## Naming is Hard, Naming Abstract Types is Even Harder

Naming is one of the few tough problems in programming as the saying goes. If you're anything like me you probably sit behind your desk, scratching your head to find a proper description almost daily.

This time I want to expose a problem I run into time and time again: badly named abstract types (interface/abstract class). I cannot recall the number of times I've encountered one of these problematic examples:
* `IThingy`,
* `AbstractThingy` or 
* `ThingyImpl`'s

Frankly, I believe we can, and should do better. This type of naming, which I consider an [anti-pattern](), is a symptom of one of these two causes:
1. An unnecessary abstraction
2. Lazy naming

The resulting problems?
* Hiding information
* Breaking encapsulation

Let's see why I consider this naming harmful, and more importantly, what you can do about it. Small tip of the veil: it involves pausing and thinking.

## Symptoms of a Deeper Cause?

Lets zoom in a bit. If we view the ill-named abstract types as the symptoms, what might be causing them? After giving it some thought, I found two causes.

Firstly, there is the case of **unnecessary abstraction**. Some programmers take the idea of "abstraction" too far and create what Martin Fowler calls [interface implementation pairs](https://martinfowler.com/bliki/InterfaceImplementationPair.html). They tend to introduce interfaces even when they don't serve a clear purpose (such as dependency inversion or polymorphism). In essence this is lazy programming, as doing this takes deliberation out of the equation. They're just following a recipe. Software design is a balancing act, where choices should be justified. As I mentioned [earlier](https://www.codecraftr.nl/interfaces-defining-roles/) interfaces always mean you incur the cost of extra cognitive load so there should be something it brings you in return.

Secondly, it sometimes simply boils down to **lazy naming**. Like mentioned naming is always hard, and the path of least resistance -the brain loves to be lazy - is to call something the first thing that comes to mind. The problem is that this is rarely the best we can come up with. If you dig deep, squint a bit more and crunch those gears a bit more you will almost certainly find a better name. Put in the extra effort now, because future you will be grateful for it.

Now that we've seen the cause, it's time to find out why I consider this naming style harmful.

## The Painful Results

The downsides of this naming pattern are twofold:
* The names are **inexpressive**
* The naming pattern **breaks encapsulation**

First of the inexpressive names. Imagine I wrote an interface `IRepository` and an implementation `Repository`. What does this tell you? 

Actually very little, and what it does tell you is not important. This naming only conveys that `Repository` implements an abstract construct. It also conveys that what it implements is an interface (because of the *I*-prefix), which is precisely what you shouldn't want to know.

Crucially, this naming expresses nothing about *what* makes the implementor stand apart. Purely looking at the class name, I have no idea what it does. Does it write to a file? A database? In memory? In the current state I'll have to look at the implementation to find out, something we should aim to avoid.

Second, and I already alluded to this, but this naming breaks encapsulation. *I*- or *Abstract*-prefixes put the abstract type in your type name. Essentially [Hungarian Notation](https://en.wikipedia.org/wiki/Hungarian_notation) at type level. Guess what happens when we want to switch from an interface to an abstract class? That's right, you need to rename the type too, even though what it represents remained the same. As a result each implementor will now need to use the new type name, potentially elavating a simple type change to a shotgun spread of changes in your diff. That's far from ideal.

Now, let's liven up this a bit with a few examples.

## Example 1: Lazy Naming

We've seen why you wouldn't want to follow this naming anti-pattern, now we'll look at some practical examples. Let's start easy.

Imagine having to write an application which grabs some settings from a csv file. Naive me would create two types: `ISettingsRepository` and `SettingsRepository`. You can clearly see that I have done a bad job conveying information to you. You're left guessing how these settings are stored and have to delve in the implementation. Bad me.

--- Code Sample (bad) ---

Now imagine that I took the previous advice to heart. I put in some elbow-grease, and proudly ask you to review my new version:
`SettingsRepository` and `CsvRepository`. Wow! These minute changes tell you a completely different story.

--- Code Sample (Better) ---

That wasn't too bad, now was it? Let's look at another common example.

## Example 2: Unnecessary Abstraction

For our second example, imagine a company tasks us writing software that simulates coffee machines in order to quickly test new production models.

As a coffee nut (hence the example!) I quickly get to work. A few hours later I come back to show you my work:

--- Class Diagram ---

I created classes for the basic components of a coffee machine: 
* the water reservoir
* the hopper
* the grinder
* the motor
* the heating element

You get the idea.

After some judicious study your eye is drawn to `IGrinder` and it's sole implementation `Grinder`. What sets `Grinder` apart, you wonder?

Suddenly you realize the company only produces machines with integrated, so-called [blade grinders](https://www.javapresse.com/blogs/grinding-coffee/blades-vs-burrs). We talk a bit, and I come back to you with a simpler version, containing just `BladeGrinder`. Turns out I got carried away in my attempts to abstract the code. Mea culpa!

## From the Trenches

If you've been programming for a few years now you've probably seen these badly named abstractions in practice, like the preceding examples. As for me, I've also seen my fair share. In my early career I regrettably also fell for this trap often enough.

Interestingly I tend to find this pitfall most for abstractions that are one-to-one (abstract and concrete type). Generally people are forced to think of what sets an implementation apart when multiple implementations are required.

Ranging from easy to spot variants like `Repository` -> `RepositoryImpl` combinations, to less obvious variants I've seen quite a few of them. Every single occurrence of this anti-pattern, bar one, was avoidable. 

I can only recall a single instance where we could not improve on the naming easily, though in hindsight I would have still tried harder. That brings me to the exceptions.

## Exceptions to the Rule?
- Technicalities (immutables/wrappers)
- Still, 99% of the time a better name is possible

## Conclusion 📝

Interfaces and abstract classes are important tools to create abstrations in code. Naming is a tough part of coding, and giving abstract types an expressive name is very demanding. Taking the shortcut and naming these types lazily can result in **hiding information** from readers or might even be a symptom of an **unnecessary abstraction**.

The antidote is to put in the effort; *stop and think*. Be kind to the future readers of your code and name interfaces and abstract classes intentionally. They will thank you for it.

_What is your opinion? Are there any other reasons to avoid this naming anti-pattern?_
