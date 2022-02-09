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

It needs to contain information about the type of bean used, the intensity (1-10) and the weight of the bag (in grams). A first take might look like this:

TODO: sample code

This does get the job done, albeit barely. I think we can do better!

## Preventing Bugs

Using primitives all over the place can become a way for subtle, semantic bugs to creep into the code. For instance if we look at `Coffee`, both intensity and weight are represented using an `Int`.

It's all too easy for client code to pass mix up these two representations, and the compiler won't catch this issue because it cannot distinguish them purely by semantics.

By defining types for intensity (an enum) and one for weight (a class), the compiler will yell at us if we mix up the concepts. How's that for early feedback!

## Combat Duplication

There are some rules concerning the weight of coffee. For instance, it should never be a negative number.

Without a dedicated type, this validation logic might pop up anywhere in the code where input representing weight enters the system.

When we define a type for weight, it becomes the sole place where this validation is defined. The code is more maintainable!

## Improving Cohesion

The duplication problem also closely relates to a [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)) problem. Without a type for weight, logic regarding weight can pop up all over the place. 

The `Coffee` class might validate that weight is not a negative number. Some service orchestrating a use case might do some conversion of weight from grams to kilograms.

Logic becomes disparate, and muddles the responsibilities of other classes... Bad.

The dedicated Microtype is a natural "home" to place all these kinds of business rules (and future ones, too!). It itself has high cohesion, and relieves other classes from containing its logic.

## Codifying a Rich Model

Leaving the concepts of weight, intensity and bean as simple primitives deprives our model of depth. 

One of the staples of Domain-Driven Design is to practice Model-Driven Design. Your model (code) should express the Ubiquitous Language. If we model these concepts as mere primitives, it can end up making it implicit. We want the opposite: an expressive, explicit model. Just compare the information the primitive and Microtype versions convey. 

In the primitive version I'm left making assumptions on what their semantics are. With the Microtype, I instantly see that weight is measured in grams, intensity goes from one to ten, and I see which bean options are available. It captures knowledge about the domain in code!

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
