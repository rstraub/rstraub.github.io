---
author: Roy Straub
categories:
- tech
comments: true
description: Ints, Doubles, Strings. We work with primitives all the time, but did
  you know they can hurt your Software Design? Learn how to solve this issue using
  the Microtype.
featured: false
hidden: false
image: assets/images/20-coffee-beans.jpg
layout: post
tags:
- OOP
- software design
- refactoring
title: "The Might of Microtypes"
---

Ints, Doubles, Strings. We work with primitives all the time, but did you know they can hurt your Software Design? Microtypes can help!

## 🚩 Primitives Turn Problematic 

Primitives are the basic building blocks of the languages we work with, and the programs we write. The truth is, we tend to rely on them too much.

Overusing primitives can lead to problems. Thankfully, with a little elbow grease we can leverage primitives in a much better way, by creating so-called _Microtypes_.

First, let's see which problems might arise from fixating on primitives.

## 🦨 Overusing Primitives a Code Smell?

Overusing primitives is a code smell, called [Primitive Obsession](https://refactoring.guru/smells/primitive-obsession). A tell for this code smell is operating upon primitives extensively, when the primitive represents a significant concept.

Consequences of this code smell can be **bugs**, **duplication**, **low cohesion** and an **implicit model**. I'll show examples of these problems later in this post. 

One easily overlooked way to solve this smell is by defining a _Microtype_.

## 🔬 Introducing the Microtype

[Microtypes](https://codebox.net/pages/microtypes-in-java) are custom classes which wrap a single primitive, and are therefore very small (hence the name). They are also commonly referred to as Value Classes or Value Objects. 

Being _[Value Objects](https://www.martinfowler.com/bliki/ValueObject.html)_, the identity of a Microtype is defined entirely by their attribute. Furthermore, Microtypes should be *immutable* and its *equality* should be based on it's attribute, not its reference.

Let's set the scene before diving into some examples.

## ☕ Example: Coffee Roasters

Imagine that your writing a piece of software for a coffee roaster, and the model includes `Coffee`. It represents a bag of coffee beans that will be sold to a customer.

It needs to contain information about the type of bean used, the intensity (1-5) and the weight of the bag (in grams). A first take might look like this:

<script src="https://gist.github.com/rstraub/613128eb37038b442e0b8c4744761f56.js"></script>
_Listing 1. First iteration for Coffee_

This does get the job done, but reeks of Primitive Obsession. Next, we'll look at how Microtypes help out.

## 🪲 Bug Prevention

Using primitives all over the place can become a way for subtle, semantic bugs to creep into the code. For instance if we look at `Coffee`, both intensity and weight are represented using an `Int`.

It's all too easy for clients to mix up intensity and weight. The compiler won't catch this issue because it cannot distinguish them by semantics alone.

<script src="https://gist.github.com/rstraub/ae548759ef09e5606e8b24e4805894ba.js"></script>
_Listing 2. Switching intensity and weight causes a bug_

Running the code above results in:
```
Coffee(type=ARABICA, intensity=1000, weight=2)
```
Ouch, that is some very strong coffee. Not quite what we intended!

By defining a Microtype for weight, the compiler will yell at us if we mix up the concepts. How's that for early feedback!

<script src="https://gist.github.com/rstraub/6818d8d58a50d2ad3276f7d301e9ebab.js"></script>

_Listing 3. Preventing semantic bugs with a Microtype_

## 📍 Combat Duplication

There are business rules concerning the weight of coffee. For instance, it cannot be a negative number, and we need to convert the weight to kilograms in order to determine the price for the bag of coffee beans.

Without a dedicated type, this logic might pop up anywhere in the code where the it is needed:

<script src="https://gist.github.com/rstraub/eac7a99c2dcc92872f7aebe762c45d2a.js"></script>

_Listing 4. Duplication because weight logic doesn't have a "home"_

When we define a Microtype for weight, it is the logical place to define this validation. The duplication is gone, and any instances of `Weight` we use are validated. This makes the code more maintainable! 

<script src="https://gist.github.com/rstraub/0035b92683e8115e1037f3f3488d26bc.js"></script>

_Listing 5. The Microtype contains the logic, removing duplication_

## 📦 Improving Cohesion

The duplication problem also closely relates to a [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)) problem. Without a specific type logic regarding weight can pop up all over the place. 

The `Coffee` class might validate that weight is not a negative number. Some service orchestrating a use case might do some conversion of weight from grams to kilograms. Logic becomes disparate, lowering cohesion in other classes... _Bad_.

As we just saw, a dedicated Microtype is a natural "home" to place these business rules (and future ones, too). It itself has high cohesion, and improves cohesion of other classes by relieving them of containing weight logic.

<script src="https://gist.github.com/rstraub/d03941347b1f807a4dfa14f5da3a7e95.js"></script>

_Listing 6. Microtype containing weight related logic_

## 🗣️ Expressing the Domain Model

Expressing the concepts of weight and intensity as primitives deprives our model of _depth_. 

One of the tenets of Domain-Driven Design is that your code should capture and express the Ubiquitous Language. If we express these concepts as mere primitives, it can end up making the model _implicit_. 

We want the opposite: an _expressive_ model. Just compare the primitive (listing 7) to the Microtype versions (listing 8).

<script src="https://gist.github.com/rstraub/d7df7a823ac1ca968760baee64cae127.js"></script>

_Listing 7. Primitives might result in an implicit model_

<script src="https://gist.github.com/rstraub/af6efde29baa559da05179c12b7e1f83.js"></script>

_Listing 8. Microtypes make the model expressive and explicit_

In the primitive version you're left making assumptions on what represents weight. Is it grams? Kilograms? Pounds? With the Microtype, you instantly see that weight is measured in grams. It captures knowledge about the domain in code!

## ⚖️ Microtypes: a Silver Bullet?

So, should you go and wrap every single primitive you find? 

That's probably a bad idea. 

Primitives are **heavily optimized**, and using objects everywhere might cause a serious performance hit. This is especially true with high volume use cases. 

Some languages (like [Kotlin](https://kotlinlang.org/docs/inline-classes.html)) offer solutions to this problem in the form of a _Value Class_. This allows you to use a custom type at _compile-time_, and make use of the primitive at _runtime_.

Another downside is that Microtypes can be **clunky** to work with. They have to be constructed, and using them requires accessing their attribute, or defining custom methods (like `plus`, `minus`, etc).

Though the extra code problem is hard to solve, some languages help make it read nicely by allowing you to define custom operators. For `Weight` that might look like this:

<script src="https://gist.github.com/rstraub/2cb0e94cfc95219a8bde7f308fa7c6fa.js"></script>

_Listing 9. Operator overloading_

Strategically using extension functions can work miracles too. For instance you could make `Weight` construction easier with an extension on `Int`:

<script src="https://gist.github.com/rstraub/576ff11ac25d39d22a36a0c3e990be35.js"></script>

_Listing 10. Extension functions to construct Weights_

My advice is to use Microtypes _diligently_. Use them where they make your code more **expressive** and **maintainable**. You get most of your money's worth if they capture a domain concept.

## 📝 Wrapping Up

Primitives are _essential_ in creating software. Can you imagine writing programs without Ints, Strings or Booleans? They are **generic programming constructs** however, and that comes with problems.

A solution to those problems are Microtypes: small classes that wrap a primitive and give it **meaning** and **purpose** in a certain context. Though they have their own pro's and cons, they can improve your software when used correctly.

Think twice next time you express a concept with a primitive, a Microtype might serve you better!

_What's your take on Microtypes? Do you see other pro's or cons? Share your thoughts in the comments below!_