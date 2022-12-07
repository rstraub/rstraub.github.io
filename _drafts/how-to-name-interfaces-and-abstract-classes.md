---
layout: post
title: "How to Properly Name Interfaces, Abstract Classes and Their Implentations 🏷"
author: Roy Straub
categories: [Software Design]
tags: [OOP, Naming]
image: assets/images/construction.jpg
description: "Naming Abstract Types and their implementations is difficult. Learn why you should avoid names like IAbstractions, ThingyImpl or AbstractThing."
featured: true
hidden: false
comments: true
---

Naming Abstract Types and their implementations is difficult. Learn why you should avoid names like IAbstractions, ThingyImpl or AbstractThing.

## Naming is Hard, Naming Abstract Types is Even Harder

Naming is one of the few truly tough problems in programming as the saying goes. If you're anything like me you probably sit behind your desk, scratching your head to find a proper description almost daily.

This time I want to expose a problem I run into time and time again: badly named abstract types (interface/abstract class). I cannot recall the number of times I've encountered one of these problematic examples:
* `IThingy`,
* `AbstractThingy` or 
* `ThingyImpl`'s

Frankly, I believe we can, and should do better. This type of naming, which I consider an harmful, is a symptom of one of these two causes:
1. An unnecessary abstraction
2. Unexpressive naming

Let's see what the problem with this type of naming is, and more importantly, what you can do about it. Small tip of the veil: it involves pausing and thinking.

## Think: What Purpose Does the Abstraction Have?

Firstly, there is the case of **unnecessary abstraction**. Some programmers take the idea of "abstraction" too far and create what Martin Fowler calls [interface implementation pairs](https://martinfowler.com/bliki/InterfaceImplementationPair.html). They tend to introduce interfaces when they don't serve a clear purpose or anticipate for a future scenario that might not happen. Either way it violates the [YAGNI principle](https://www.martinfowler.com/bliki/Yagni.html). Introducing abstractions should always be done deliberately.

Software design is a balancing act, where choices should be justified. As I mentioned [earlier](https://www.codecraftr.nl/interfaces-defining-roles/), interfaces always mean you incur the cost of extra cognitive load due to adding indirection. There should always be a positive effect to offset that cost.

Next time you see (or write) something like an `IService` and `ServiceImpl` think twice about the purpose of the abstraction. Sometimes you simply might not need it!

## Think, Again: Come Up With a Better Name

Secondly, this naming pattern might occur due to **lazy naming**. Naming is always hard, and the path of least resistance - the brain loves to be lazy - is to call something the first thing that comes to mind. 

The problem is that this is rarely the best we can come up with. If you dig deep, and put in a bit more effort you will almost certainly find a better name. Make the investment, and try to come up with a better name. Future you will be grateful for it.

For example you might encounter a `Repository`/`RepositoryImpl` combination. What does this tell you? 

Very little, and what it does tell you is not the important aspect. This naming only conveys that `RepositoryImpl` implements an abstract construct `Repository`. 

Crucially, these names express nothing about *what* makes the implementor stand apart. Purely looking at the class name, I have no idea what it does. Does it write to a file? A database? In memory? In the current state I'll have to look at the implementation to find out, something we should aim to avoid.

The solution is easy, name the implementor by what makes it special. A name like `InMemoryRepository`, or `FileRepository` tells me much more at a glance.

## From the Trenches

Let's have a look at what this looks like in practice. A great example is [Java's collection API](https://docs.oracle.com/javase/7/docs/api/java/util/Collections.html). Just as a reminder, it looks like this:

![Java Collections API Diagram]({{ site.baseurl }}/assets/images/27-java-collections.jpg)

*Figure 1. Java Collections API, by Ramlmn, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0), via Wikimedia Commons*

So, what do you see? Are there any `ISets` or `ListImpls` in this hierarchy? 

No. All the interfaces (yellow) have meaningful names like `Set`, `List` or `Queue`. All the classes (purple) implementing them put relevant information in their name. A `TreeSet`, `LinkedList` or `PriorityQueue` instantly let me know what I can expect from using them.

At this point some of you might point at the abstract classes (blue) in this hierarchy, such as `AbstractQueue`. Well spotted! This brings us to the exceptions.

## Exceptions to the Rule?

There are certain reasons where you could prefix your abstract type, but it should be your absolute last resort. They can be useful in:

- **Skeletal implementations of abstract types.** The `AbstractQueue` is a great example of this. It implements an interface (`Queue`), but offers some basic setup for implementing a new type of queue, hence it is a *skeleton implementation class*. In these situations there is no better name to come up with as that is its only purpose, and the interface is already named `Queue`. According to [Effective Java](https://www.goodreads.com/book/show/34927404-effective-java), the abstract prefix in this instance has simply become convention, but other names like `SkeletalQueue` might have been more optimal.
- **Libraries and technical limitations**, such as [Immutables](https://immutables.github.io). For technical reasons, when using this library you need to create an abstract type, which the annotation processor uses to generates a concrete class. The concrete and abstract type mean the same thing, but of course the names must be unique. Thus you end up with something like `Queue` and `QueueImpl`.

Keep in mind these should be the exception to the rule. Always think long and hard before resorting to pre- or postfixing your abstract types this way. Most of the time there are better options.

## Conclusion 📝

Interfaces and abstract classes are important tools to create abstrations in code. Naming is a tough part of coding, and giving abstract types an expressive name is very demanding. Taking the shortcut and naming these types lazily can result in **hiding information** from readers or might even be a symptom of an **unnecessary abstraction**.

The antidote is to put in the effort; *stop and think*. Be kind to the future readers of your code and name interfaces and abstract classes intentionally. They will thank you for it.

_What is your opinion? Are there any other reasons to avoid this naming anti-pattern?_
