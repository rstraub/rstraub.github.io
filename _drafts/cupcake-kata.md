---
layout: post
title: "Cupcake Code Kata"
author: Roy Straub
categories: []
tags: []
image: assets/images/construction.jpg
description: ""
featured: false
hidden: true
comments: true
---

Code and Sweets. Sounds great doesn't it? Let's see what a code kata combining them can teach you.

## Code Kata With a Topping of Design Patterns 

Any form of mastery demands practice, and this code kata can help master a few specific skills too.

[The Cupcake kata](https://codingdojo.org/kata/cupcake/) is aimed at improving your proficiency at Design Patterns (though it could be solved without them). What sets it apart is that is does so by offering a fun little puzzle as the context for applying them.

Curious what the puzzle is about? Read on.

## Sweet. Cupcakes

The Cupcake Kata's challenge is twofold.

Firstly you're tasked to write code that can produce *descriptions* and *prices* for different types of confectionaries, namely cupcakes and cookies. 

But there's a twist: different sorts of toppings can be sprinkled on top of the confectionary. The description, and price vary according to the confectionary and toppings it has. To top it off (pun intended) the order in which they are added to the cupcake or cookie matters: i.e. nuts on a chocolate cupcake is different from chocolate on a nut cupcake.

Secondly your program should support *bundles* of confectionaries. 

For instance an order can contain a bundle of two chocolate cupcakes, and a bundle of three cookies. Bundles can even contain other bundles. Similar to confectionaries, bundles can also be asked for their description, and total price.

*How would you solve this problem?*

Let's dive into the solution I came up with.

## The Solution

Solving this code kata was interesting (and fun!), and I ran into some unforeseen design consequences. The model of the program ended up looking like this:

-- image --
*Figure 1. Model for the cupcake program*

Look closely at the model in figure 1, and you will spot two patterns:
1. Decorator
2. Composite

Did you see them? No? Don't worry, let's look at the first one.

In order to solve the first part of the challenge, toppings influencing the price and description of a confectionary, I ended up applying the **Decorator Pattern**. Each `Topping` can decorate a `Confectionary`, adding its price and description to the decorated object.

Let's consider an example: a sugar coated chocolate cupcake. This product is built like this: 

```java
new Sugar(new Chocolate(new Cupcake()))
```

Asking this object for its price works like this:

* Ask price of sugar chocolate cupcake
* sugar asks price of chocolate
* chocolate asks price of cupcake, which replies `$1.00`
* chocolate returns the price of the cupcake and itself: `$1.00 + $0.10 = $1.10`.
* sugar replies the price of the chocolate cupcake and itself: `$0.15 + $1.10 = $1.25`

Ask it for its description and it will evaluate in a similar fashion to return `🧁 with 🍫 and 🍬`.

I solved the second part of the challenge, creating bundles of confectionaries (and other bundles), with the **Composite Pattern**.

This requirement called for an overarching interface for both bundles and cookies/cupcakes: `Product`. Any product could be asked its `description` and `price`:

```java
sealed public interface Product permits Bundle, Confectionary {
  String description();
  double price();
}
```

A side effect of this requirement was that a distinction between `Bundle` and `Cookie` & `Cupcake` was needed. Otherwise you could sprinkle nuts on a bundle! 

I defined a `Confectionary` *marker interface*, implemented by `Topping`, `Cookie` and `Cupcake`. After that `Topping` was only allowed to decorate a `Confectionary`, not a `Product`.

Whew, crisis averted! Time to let `Bundle` contain other products. 

I represented that as a `Map` of `descriptions`, corresponding to `Product`s. That way I could ask descriptions and prices for each distinct product in a bundle, whether it be `Bundle` or `Confectionary`. Using that information, it was easy to determine the price and description for the bundle itself.

That sums up what I think are the interesting parts of the solution! Want to take a closer look? The code can be found on [Github](https://github.com/rstraub/cupcake-kata-java).

## Learnings

* pattern vocabulary is powerful
* implementing composite / decorator
* Dusting off some Java & Java 17 features

We do code kata's in order to learn, so what can you learn from doing this one?

What you learn from a kata depends on your prior knowledge, so this is what it taught me:

* Context, consequences, and implementation of the Composite & Decorator Pattern.
* Power of a pattern language

Though I have read the GoF book, its been a while since I consciously implemented Composite or Decorator, so my knowledge about them was spotty. This kata really pushes you in the direction of both, and seeing them solve a problem makes them sink in that much more.

The real lesson, for me at least, was the power of the design pattern language. Just because the kata description mentions two patterns you immediately form a *high level mental model* of the solution, instead of discussing classes in isolation. To me, this is where the real value of any pattern lies.

As a little bonus I implemented this kata in Java 17, thus it also helped me dust of some of my Java skills, and allowed me to try my hand at some of the more recent language construct such as sealed classes and interfaces. 

Don't forget: code kata's are a great way to experiment with new technology!

## Wrapping Up 📝

The Cupcake code kata is a simple exercise to flex your Design Patterns muscles, especially the Composite and Decorator.

Besides being fun to solve, this Kata can be a great tool to teach junior coders about Design Patterns, and their value in a hands-on way.

Have a few minutes to spare in your day? Why not give the [Cupcake kata](https://codingdojo.org/kata/cupcake/) a shot yourself!

_How would/did you solve this Code Kata? Share your solution in the comments below._
