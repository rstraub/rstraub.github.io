---
layout: post
title:  "Interfaces defining roles"
author: Roy Straub
categories: [Design]
tags: [Role Interface, Test Driven Development]
image: assets/images/construction.jpg
description: "Role interfaces"
featured: true
hidden: true
comments: true
---

Defining roles with interfaces

## Defining the traditional interface
* Defines actions an object can do
* "Acts like"
* Header interface
* Swapping implementations / Dependency inversion principle

## Object oriented programming and roles
* What is a role to begin with?
* Object oriented oriented programming is about messaging
* Collaborations
* CRC cards

## What is a Role Interface
* Interface describing a role an object can play
* Consumer driven contracts
* Example of traditional "header interface" vs role interface
* Object is not its role
* Aids in testability / mocking
* No implementation needed to finish the consumer

## Disadvantages of the Role Interface
* Harder to define crisply
* Extra layer of indirection
* Getting the granularity right is hard -> wrong means overwhelming or confusing clients
* Mapping 1 to 1 interface and class? blasphemy!

## Advantages of the Role Interface
* Explicit contract for collaboration
* Naming roles can enhance the domain model / ubiquitous language
* Need to know basis, less coupling / easier for clients
* Roles can be fulfilled by others / refactoring responsibilities becomes easier

## Conclusion


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