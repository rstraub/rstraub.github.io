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

Ints, Doubles, Strings. We work with primitives all the time, but did you know they can hurt your Software Design? Meet the Microtype.

## Introduction

Primitives are the basic building blocks of the languages we work with, and the programs we write. The truth is, we tend to rely on them too much.

Overusing primitives can lead to problems. Thankfully, with a little elbow grease we can leverage primitives in a much better way, by creating so-called _Microtypes_.

TODO: bruggetje

## Primitive Obsession

Overusing primitives is actually a code smell, called [Primitive Obsession](https://refactoring.guru/smells/primitive-obsession). A tell for this code smell is having a primitive instead of a small type representing a (domain) concept.

Among others this code smell can lead to **bugs**, **duplication**, **low cohesion** and an **inexpressive model**. I'll show examples of this later, don't worry. 

One easily overlooked way to solve this is smell is by defining a _Microtype_.

## A Micro-What Now? 📜

[Microtypes](https://codebox.net/pages/microtypes-in-java) are custom classes which wrap a single primitive, and are therefore quite small (hence the name). They embody the third rule of _[Object Calisthenics](https://developerhandbook.stakater.com/content/architecture/object-calisthenics.html#_3-wrap-all-primitives-and-strings)_.

Effectively they are very small _[Value Objects](https://www.martinfowler.com/bliki/ValueObject.html)_; Their identity is defined entirely by their attribute (the primitive they wrap). Being Value Objects, Microtypes should be *immutable* and its *equality* should be based on it's attribute, not its reference.

Let's set the scene before diving into some examples.

## Running Example: Coffee Roasters

Imagine that your writing a piece of software for a coffee roaster, and the model includes `Coffee`. It represents a bag of coffeebeans that will be sold to a customer.

It needs to contain information about the type of bean used, the intensity (1-5) and the weight of the bag (in grams). A first take might look like this:

<script src="https://gist.github.com/rstraub/613128eb37038b442e0b8c4744761f56.js"></script>

This does get the job done, albeit barely. I think we can do better!

## Preventing Bugs

Using primitives all over the place can become a way for subtle, semantic bugs to creep into the code. For instance if we look at `Coffee`, both intensity and weight are represented using an `Int`.

It's all too easy for client code to pass mix up these two representations, and the compiler won't catch this issue because it cannot distinguish them purely by semantics.

<script src="https://gist.github.com/rstraub/ae548759ef09e5606e8b24e4805894ba.js"></script>
_Listing 2. Switching intensity and weight causes a bug_

Running the code above results in:
```
Coffee(type=ARABICA, intensity=1000, weight=2)
```
Ouch, that might end up causing some serious problems!

By defining a Microtype for weight, the compiler will yell at us if we mix up the concepts. How's that for early feedback!

<script src="https://gist.github.com/rstraub/6818d8d58a50d2ad3276f7d301e9ebab.js"></script>

_Listing 3. Preventing semantic bugs with a Microtype_

## Combat Duplication

There are some rules concerning the weight of coffee. For instance, it should never be a negative number, or maybe we need to convert between grams and kilograms.

Without a dedicated type, this logic might pop up anywhere in the code where the logic is needed:

<script src="https://gist.github.com/rstraub/eac7a99c2dcc92872f7aebe762c45d2a.js"></script>

_Listing 4. Duplication because the validation logic doesn't have a natural "home"_

When we have a Microtype for weight, it is the natural place to define this validation. The duplication is gone, even better any instances of `Weight` we use are validated. The code is more maintainable! 

<script src="https://gist.github.com/rstraub/0035b92683e8115e1037f3f3488d26bc.js"></script>

_Listing 5. The Microtype handles validation, resulting maintainable code_

## Improving Cohesion

The duplication problem also closely relates to a [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)) problem. Without a type for weight, logic regarding weight can pop up all over the place. 

The `Coffee` class might validate that weight is not a negative number. Some service orchestrating a use case might do some conversion of weight from grams to kilograms. Logic becomes disparate, lowering cohesion of other classes... Bad.

The dedicated Microtype is a natural "home" to place all these kinds of business rules (and future ones, too). It itself has high cohesion, and might improve cohesion of other classes by relieving them of containing weight logic.

<script src="https://gist.github.com/rstraub/d03941347b1f807a4dfa14f5da3a7e95.js"></script>

_Listing 6. Microtype containing weight related logic_

## Codifying a Rich Model

Leaving the concepts of weight and intensity as simple primitives deprives our model of depth. 

One of the staples of Domain-Driven Design is to practice Model-Driven Design. Your code should express the Ubiquitous Language. If we model these concepts as mere primitives, it can end up making it implicit. We want the opposite: an expressive, explicit model. Just compare the information the primitive and Microtype versions convey.

<script src="https://gist.github.com/rstraub/d7df7a823ac1ca968760baee64cae127.js"></script>

_Listing 7. Primitives might result in an implicit model_

In the primitive version I'm left making assumptions on what weight means. Is it grams? Kilograms? Pounds? With the Microtype, I instantly see that weight is measured in grams. It captures, and expresses knowledge about the domain in code!

<script src="https://gist.github.com/rstraub/af6efde29baa559da05179c12b7e1f83.js"></script>

_Listing 8. Microtypes improve expressiveness of the model_

## When to Employ Microtypes
* Rules regarding specific piece of data
* Represents a (non-trivial / relevant) concept

## Downsides of microtypes
* Uses more memory
* Wrapping primitives can be clunky (construction / calculations)

## Conclusion
* Define microtypes instead of leaning on primitives for too long

---

Generally you want to wrap primitives if you are writing (business) logic that operates on the primitive and/or custom validation rules apply. Another big tell for me is if the primitive represents a significant concept in the domain. 
