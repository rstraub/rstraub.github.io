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

Overusing primitives can lead to problems, like duplication, low cohesion or even code that's not expressive. Thankfully, with a little elbow grease we can leverage primitives in a much better way, by creating so-called _Microtypes_.

But first, let's see why primitives can cause us a headache sometimes.

## Primitive Obsession

Imagine that your writing a piece of software for a bank, and the model includes a representation of an IBAN (International Bank Account Number). A logical first thought might be to represent that as a string. Seems like a good fit!

Is it really, though? I think we can do better.

Expressing the IBAN can lead to issues like:
* **Duplication.** For instance, validating the IBAN is required wherever you receive one. It can be tempting to write validation logic for each use case that works with the IBAN, and thus duplicating logic.
* **Low Cohesion.** Another consequence of operating on a primitive is that there is no real "home" for any logic that belongs to the concept we're trying to represent. This means validation logic might live in one part of the code and logic that extracts the country code from an IBAN might live in another. That's waiting for problems to happen!
* **Unexpressive model.** One of the staples of Domain-Driven Design is to practice Model-Driven Design. Your model should express the ubiquitous language. Now, what happens if, in the domain of banking, we express a core concept like a bank account as a primitive? That's right, we make our model implicit. Of course there might be mentions of `iban` or `accountNumber` in the code, but then you rely on developers providing consistent names to represent the same concept and lose out on all the benefits an explicit model gives us.

This overusing of primitives where an object might be a better fit is actually a well-defined code smell called _[Primitive Obsession](https://refactoring.guru/smells/primitive-obsession)_. It can manifest itself in a variety of ways, but I think that a single piece of data, for instance a single string for an IBAN, is a very deceiving one that can be easily overlooked.

Frankly, we can do better. We can start creating Microtypes.


## A Micro-What Now? 📜

[Microtypes](https://codebox.net/pages/microtypes-in-java) are custom classes which wrap a single primitive, and are therefore quite small (hence the name). I also consider classes wrapping a single collection or array a microtype. They embody the third rule of _[Object Calisthenics](https://developerhandbook.stakater.com/content/architecture/object-calisthenics.html#_3-wrap-all-primitives-and-strings)_.

Effectively they are very small _[Value Objects](https://www.martinfowler.com/bliki/ValueObject.html)_; Their identity is defined entirely by their attribute (the primitive they wrap). Being Value Objects, Microtypes should be *immutable* and its *equality* should be based on it's attribute, not its reference.

Let's continue our example of the banking software. Our Microtype could look something like this:

```kotlin
```
Listing 1. IBAN as a full-blown class (Microtype)

Great! Looks simple enough. But how do I know when to create a Microtype? Let's see.

## To type, or not to (micro)type

Generally you want to wrap primitives if you are writing (business) logic that operates on the primitive and/or custom validation rules apply. Another big tell for me is if the primitive represents a significant concept in the domain. 

When concepts consist of multiple pieces of data it is quite easy to spot a potential class. Take an `Address` for example. It could be modelled as a single string, but it's easy to imagine a class with `zipcode`, `street`, `city` etc.

Spotting a class when it consists of one piece of data is usually harder. In most contexts you wouldn't think twice about using anything other than a string to represent a phonenumber, right?

I already mentioned the potential problems of keeping the phonenumber around as "just" a string. Let's have a look at the potential benefits of defining a Microtype to represent it.

## The joys of microtypes

Defining a Microtype **consolidates the concept** in your conceptual model. Contrast having a class for a bank account number to relying exclusively on developers consistently naming arguments and properties:

```kotlin

```
Listing 2. Difference between representing an IBAN as a string or class

* Place for logic
* Reduce duplication
* Value objects & Standalone classes (immutable and supple)

## Downsides of microtypes
* Uses more memory
* Wrapping primitives can be clunky (constructors / cannot use directly as values)

## A Microtype in Practice
* IBAN
* Validation -> num check
* get Country code
* get BBAN

## Conclusion
* Define microtypes instead of leaning on primitives for too long