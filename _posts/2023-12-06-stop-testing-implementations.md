---
author: Roy Straub
categories:
- tech
description: Why you should test behaviour, not structure
layout: post
tags:
- testing
- maintainability
title: "Stop Testing Implementations"
---

One class, one test. 

Some of you might agree with this statement, and I used to as well. I no longer do, and have been flagellated for breaking this “rule”.

We should stop fixating on a test per class, method, function, or whatever technical construct of your choosing - to make a goal or necessity to have a one to one relation between tests and technical construct.

Instead we should orientate tests around behaviour. Doing so decouples the behaviour specified in the test from the implementation which accomplishes it. This allows the implementation to be emergent and fluid. The test isn’t coupled to the shape of the solution but to the behaviour demanded by it.

The payoffs? 

- Flexibility. We increase the ability to restructure the implementation whilst keeping our safety net intact.

- Decoupling. Implementation and specification (test) don’t have to change at the same rate. This makes refactoring cheaper, as we don’t necessarily have to change both sides of the equation.

- Comprehension. Letting go of testing implementation and expressing behaviour leads to tests becoming a specification of the system. Not in a technical sense, but a functional one. They contain less noise in their story explaining the system.

How did we end up with this 1:1 relationship between tests/classes? It is easy and obvious. Orientating around behaviour necessitates deeper insight and deliberation, similar to packaging code by concern as opposed to type does. It’s easy to throw all views one package, but much harder to group them by their rate of change (cohesion). 

Another reason might be that [unit tests](https://www.martinfowler.com/bliki/UnitTest.html) have always been an ambiguous term. People look for absolute rules, such as one class, one test or mock all collaborations. The harsh truth is that [it depends](https://rstraub.com/it-depends). Hard rules are useful until you develop a better sense of judgment acquired by gaining experience, beyond that they prevent the best outcomes from tradeoffs.

The key takeaway is this. Stop seeing tests as verification of your implementation. Start seeing them as the specification of behaviour (part of) your system should accomplish and reap the benefits.
