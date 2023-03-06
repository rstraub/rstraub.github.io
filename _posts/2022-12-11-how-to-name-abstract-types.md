---
author: Roy Straub
categories:
- Software Design
comments: true
description: Naming abstract types and their implementations is challenging. Learn
  why you should avoid names like IRepository, RepositoryImpl, and AbstractRepository.
featured: true
hidden: true
image: assets/images/27-naming-abstract-types.jpg
layout: post
tags:
- OOP
- Naming
title: "How to Name Interfaces, Abstract Classes, and Their Implementations \U0001F3F7"
---

Naming abstract types and their implementations is challenging. Learn why you should avoid names like IRepository, RepositoryImpl, and AbstractRepository.

## Naming Is Hard, Naming Abstract Types Is Even Harder 🥵

As the saying goes, naming is one of the few truly tough problems in programming. If you're anything like me, you probably sit behind your desk, scratching your head to find a fitting name every day.

This time I want to look at a problem I repeatedly encounter: badly named abstract types and their implementations (interface/abstract class). You've probably experienced one of these problematic examples yourself:
* `IRepository`,
* `AbstractRepository` or 
* `RepositoryImpl`'s

We can and should do better. This type of naming tends to be a symptom of one of these two causes:
1. An unnecessary abstraction
2. Unexpressive naming

Let's see what the problem with this type of naming is and, more importantly, what you can do about it.

## Think: What Purpose Does the Abstraction Have? 🤔

Firstly, there is the case of **unnecessary abstraction**. Some programmers take the idea of "abstraction" too far and put interfaces in front of nearly everything. These tend to miss a purpose or anticipate a future scenario that might not happen, a clear violation of the [YAGNI principle](https://www.martinfowler.com/bliki/Yagni.html). Introducing abstractions should always be done deliberately.

Software design is a delicate balancing act where choices must be justified. As I mentioned [earlier](https://www.codecraftr.nl/interfaces-defining-roles/), interfaces always mean you incur the cost of extra cognitive load due to adding indirection. There should always be a positive effect to offset that cost.

Next time you see (or write) an `IService` and `ServiceImpl` think about the purpose of the abstraction. You might not need it!

## Think, Again: Come up with a Better Name 💡

Secondly, this naming pattern might occur due to **lazy naming**. Naming is always hard, and the path of least resistance - the brain loves to be lazy - is to call something the first thing that comes to mind. 

The problem is that this is rarely the best we can come up with. If you dig deep and put in more effort, you will find a better name. Future you will be grateful for it.

For example, you might encounter a `Repository`/`RepositoryImpl` combination. What does this tell you? 

Very little. It only conveys that `RepositoryImpl` implements an abstract construct `Repository`. Crucially, these names express nothing about *what* makes the implementor stand apart. Purely looking at the class name, I have no idea what it does. Does it write to a file? A database? In memory? Currently, you would have to look at the implementation to find out, which is bad.

The solution is easy; name the implementor by what makes it unique. A name like `InMemoryRepository`, or `FileRepository` tells me much more at a glance.

## From the Trenches 🕵️

Let's look at a real-life example, in this case [Java's collection API](https://docs.oracle.com/javase/7/docs/api/java/util/Collections.html). As a reminder, it looks like this:

![Java Collections API Diagram]({{ site.baseurl }}/assets/images/27-java-collections.png)

*Figure 1. Java Collections API, by Ramlmn, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0), via Wikimedia Commons*

Do you see any `ISets` or `ListImpls` in this hierarchy? 

No. All the interfaces (yellow) have meaningful names like `Set`, `List` or `Queue`. All the classes (purple) implementing them put relevant information in their name. A `TreeSet`, `LinkedList` or `PriorityQueue` instantly tells you what to expect from them.

Some of you might point at the abstract classes (blue) in this hierarchy, such as `AbstractQueue`. There is a reason for this, but it is an exception to the rule.

## Exceptions to the Rule? 🚨

In some situations, you could prefix your abstract type, but it should be your last resort. They can be useful in:

- **Skeletal implementations of abstract types.** The `AbstractQueue` is an excellent example of this. It implements an interface (`Queue`), but offers the basic setup for implementing a new type of queue. Hence it is a *skeleton implementation class*. In these situations, there is no better name to come up with as that is its sole purpose, and the interface is already named `Queue`. According to [Effective Java](https://www.goodreads.com/book/show/34927404-effective-java), the abstract prefix in this instance has become convention, but other names like `SkeletalQueue` might have been more optimal.
- **Libraries and technical limitations**. For example, when using a library like [Immutables](https://immutables.github.io) you end up with an abstract type and concrete type for every thing you wish to represent. Both types mean the same thing, but the names must be unique, so you end up with types such as `Queue` and `QueueImpl`.

Keep in mind these should be the exception to the rule. Always think long and hard before resorting to pre- or postfixing your abstract types this way. Most of the time, there are better options.

## Conclusion 📝

Interfaces and abstract classes are important tools for creating abstractions in code. Expressively naming abstract types an expressive name is demanding, and not doing so hides the true meaning of types from readers. Also, think hard if the abstract type is necessary. Sometimes, you could do without it.

The antidote is simple, not easy: *stop and think*. Be kind to the future readers of your code and name interfaces and abstract classes intentionally. They will be grateful for it.

_What is your opinion? What is your preferred way to name these types, and why?_