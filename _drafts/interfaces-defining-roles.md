---
layout: post
title: "How to improve software design using Role Interfaces"
author: Roy Straub
categories: [Design]
tags: [Role Interface, Encapsulation, SOLID, Object Oriented Programming, Test Driven Development]
image: assets/images/construction.jpg
description: "Role Interfaces offer a different perspective on the Interface in Object Oriented Software. Learn what this type of Interface is about, how it differs from the traditional Header Interface and what benefits they give you."
featured: true
hidden: true
comments: true
---

Role Interfaces offer a different perspective on the Interface in OOP.
Learn what benefits this type of Interface can bring your software design.

## Defining the traditional "Header Interface"

The *Interface*, a very important tool in the toolbox of every Object Oriented Programmer.
Most programmers will be familiar with it, but I recently learned to look at them in a whole new way...

Let's first have a look at what I refer to as the "traditional way" of using interfaces.

Interfaces, as we know, are powerful concepts which allow programmers to *abstract* and *encapsulate*.
You use them to define some behaviour any implementor will have to offer.
The way it is implemented is left up to the implementor to decide.

Another way to put this is that an interface defines the **what**, not the **how**.
This generally translates to an "[Acts Like](https://www.cs.utah.edu/~germain/PPS/Topics/interfaces.html)" type of relationship between the implementor and its interface.

- Defines actions an object can do
- "Acts like"
- Header interface
- Swapping implementations / Dependency inversion principle

## Object oriented programming and roles

- What is a role to begin with?
- Object oriented oriented programming is about messaging
- Collaborations
- CRC cards

## What is a Role Interface

- Interface describing a role an object can play
- Consumer driven contracts
- Example of traditional "header interface" vs role interface
- Object is not its role
- Aids in testability / mocking
- No implementation needed to finish the consumer

## Disadvantages of the Role Interface

- Harder to define crisply
- Extra layer of indirection
- Getting the granularity right is hard -> wrong means overwhelming or confusing clients
- Mapping 1 to 1 interface and class? blasphemy!

## Advantages of the Role Interface

- Explicit contract for collaboration
- Naming roles can enhance the domain model / ubiquitous language
- Need to know basis, less coupling / easier for clients
- Interface segregation principle
- Roles can be fulfilled by others / refactoring responsibilities becomes easier

## Conclusion 📝

Interfaces are the bread and butter of a good Object Oriented Programmer.
They encapsulate details, removing the burden from their clients.

Most interfaces a developer encounters in the wild resemble _Header Interfaces_.
The _Role Interface_ offers a different take on the interface, defining clearly the collaboration it has with its clients.

If you can mitigate some of its downsides the Role Interface will reward you handsomely.
They can make your Domain Model more **expressive**, **simplify clients** and make **refactoring easier**.
To top it off your codebase will even become more **testable**.

So dear Object Oriented Programmer, don't hesitate to use interfaces more often.
Role Interfaces can make all the difference!

## References

https://martinfowler.com/articles/consumerDrivenContracts.html
https://martinfowler.com/bliki/RoleInterface.html
https://martinfowler.com/bliki/UbiquitousLanguage.html
https://en.wikipedia.org/wiki/Class-responsibility-collaboration_card
https://www.cs.utah.edu/~germain/PPS/Topics/interfaces.html
https://stackify.com/dependency-inversion-principle/
https://stackify.com/interface-segregation-principle/

Maybe useful
https://en.wikipedia.org/wiki/Mixin
https://en.wikipedia.org/wiki/Delegation_pattern
https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html
https://martinfowler.com/bliki/InterfaceImplementationPair.html
https://blog.cleancoder.com/uncle-bob/2016/01/04/ALittleArchitecture.html