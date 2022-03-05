---
layout: post
title: "The Might of Microtypes"
author: Roy Straub
categories: [Craftsmanship, Software Design]
tags: [OOP, Refactoring]
image: assets/images/construction.jpg
description: ""
featured: true
hidden: true
comments: true
---

Ints, Doubles, Strings. We work with primitives all the time, but did you know they can hurt your Software Design? Microtypes can help!

## Problematic Primitives 

Primitives are the basic building blocks of the languages we work with, and the programs we write. The truth is, we tend to rely on them too much.

Overusing primitives can lead to problems. Thankfully, with a little elbow grease we can leverage primitives in a much better way, by creating so-called _Microtypes_.

First, let's see which problems might arise from fixating on primitives.

## Primitives a Code Smell?

Overusing primitives is actually a code smell, called [Primitive Obsession](https://refactoring.guru/smells/primitive-obsession). A tell for this code smell is operating upon primitives extensively, when the primitive represents a significant concept.

Consequences of this code smell can be **bugs**, **duplication**, **low cohesion** and an **implicit model**. I'll show examples of this later, don't worry. 

One easily overlooked way to solve this smell is by defining a _Microtype_.

## A Micro-What Now?

[Microtypes](https://codebox.net/pages/microtypes-in-java) are custom classes which wrap a single primitive, and are therefore quite small (hence the name). They are also commonly referred to as Value Classes or Value Objects. 

Being _[Value Objects](https://www.martinfowler.com/bliki/ValueObject.html)_, the identity of a Microtype is defined entirely by their attribute. Furthermore, Microtypes should be *immutable* and its *equality* should be based on it's attribute, not its reference.

Let's set the scene before diving into some examples.

## Example: Coffee Roasters

Imagine that your writing a piece of software for a coffee roaster, and the model includes `Coffee`. It represents a bag of coffee beans that will be sold to a customer.

It needs to contain information about the type of bean used, the intensity (1-5) and the weight of the bag (in grams). A first take might look like this:

<script src="https://gist.github.com/rstraub/613128eb37038b442e0b8c4744761f56.js"></script>

This does get the job done, albeit barely. I think we can do better!

## Bug Prevention

Using primitives all over the place can become a way for subtle, semantic bugs to creep into the code. For instance if we look at `Coffee`, both intensity and weight are represented using an `Int`.

It's all too easy for client code to pass mix up these two representations, and the compiler won't catch this issue because it cannot distinguish them by semantics.

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

## Combat Duplication

There are business rules concerning the weight of coffee. For instance, it cannot be a negative number, and we need to convert the weight to kilograms in order to determine the price for the bag of coffee beans.

Without a dedicated type, this logic might pop up anywhere in the code where the it is needed:

<script src="https://gist.github.com/rstraub/eac7a99c2dcc92872f7aebe762c45d2a.js"></script>

_Listing 4. Duplication because weight logic doesn't have a "home"_

When we have a Microtype for weight, it is the logical place to define this validation. The duplication is gone, and any instances of `Weight` we use are validated. This makes the code more maintainable! 

<script src="https://gist.github.com/rstraub/0035b92683e8115e1037f3f3488d26bc.js"></script>

_Listing 5. The Microtype contains the logic, removing duplication_

## Improving Cohesion

The duplication problem also closely relates to a [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)) problem. Without a type for weight, logic regarding weight can pop up all over the place. 

The `Coffee` class might validate that weight is not a negative number. Some service orchestrating a use case might do some conversion of weight from grams to kilograms. Logic becomes disparate, lowering cohesion in other classes... Bad.

As we just saw, a dedicated Microtype is a natural "home" to place these business rules (and future ones, too). It itself has high cohesion, and improves cohesion of other classes by relieving them of containing weight logic.

<script src="https://gist.github.com/rstraub/d03941347b1f807a4dfa14f5da3a7e95.js"></script>

_Listing 6. Microtype containing weight related logic_

## Expressing the Domain Model

Leaving the concepts of weight and intensity as simple primitives deprives our model of _depth_. 

One of the staples of Domain-Driven Design is that your code should capture and express the Ubiquitous Language. If we model these concepts as mere primitives, it can end up making them implicit. 

We want the opposite: an expressive and explicit model. Just compare the information the primitive (listing 7) and Microtype versions (listing 8) convey.

<script src="https://gist.github.com/rstraub/d7df7a823ac1ca968760baee64cae127.js"></script>

_Listing 7. Primitives might result in an implicit model_

<script src="https://gist.github.com/rstraub/af6efde29baa559da05179c12b7e1f83.js"></script>

_Listing 8. Microtypes make the model expressive and explicit_

In the primitive version I'm left making assumptions on what represents weight. Is it grams? Kilograms? Pounds? With the Microtype, I instantly see that weight is measured in grams. It captures knowledge about the domain in code!

## Are Microtypes a Silver Bullet?

So, should you go and wrap every single primitive you find? 

That's probably not a good idea. 

Primitives are **heavily optimized**, and using objects everywhere might cause a serious performance hit. This is especially true with high volume use cases. 

Some languages (like [Kotlin](https://kotlinlang.org/docs/inline-classes.html), [Scala](https://docs.scala-lang.org/overviews/core/value-classes.html), and in the future maybe even [Java](https://openjdk.java.net/jeps/8277163)) offer solutions to this problem in the form of a _Value Class_. This allows you to use a custom type at compile-time, and make use of the primitive at runtime.

Another downside to using Microtypes (or Value Classes) everywhere, is that they can be **clunky**. You have to construct them, and to do anything with their values requires you to introspect the object, or define custom methods (like `plus`, `minus`, etc).

Though the extra code problem is hard to solve, at least languages can help with making it read nice. Kotlin and Scala allow you to define operators for your types, so you can do:

<script src="https://gist.github.com/rstraub/2cb0e94cfc95219a8bde7f308fa7c6fa.js"></script>

_Listing 9. Operator overloading_

Also strategically using extensions functions can work miracles too. For instance you could make construction easier with an extension on `Int`:

<script src="https://gist.github.com/rstraub/576ff11ac25d39d22a36a0c3e990be35.js"></script>

_Listing 10. Extension functions to construct Weights_

My advice is to use Microtypes diligently. Use them where they help make your code more **expressive** and **maintainable**. You get most of your money's worth if they capture a domain concept.

## Conclusion

Primitives are _essential_ in creating software. Can you imagine writing programs without Ints, Strings or Booleans? They are **generic programming constructs** however, and that comes with problems.

A solution to those problems are Microtypes. Small classes that wrap a primitive and give it **specific meaning** and **purpose**. Though they have their own pro's and cons, they can improve your software if used correctly.

Think twice next time you express a concept with a primitive, a Microtype might serve you better!

_What's your take on Microtypes? Do you see other pro's or cons? Share your thoughts in the comments below!_
