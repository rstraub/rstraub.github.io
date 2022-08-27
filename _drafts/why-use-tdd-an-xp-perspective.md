---
layout: post
title: "Why You Should Do TDD: An XP Perspective 💎"
author: Roy Straub
categories: [Tests, Practices]
tags: [Test-Driven Development, Extreme Programming]
image: assets/images/construction.jpg
description: ""
featured: true
hidden: true
comments: true
---

Why do people apply TDD? I'll let you in on a secret: it's *not* for the tests. Let's see what Test-Driven Development is actually about.

## What are the Reasons for Doing TDD?

[Test-Driven Development][what-is-tdd] (TDD) is a controversial topic amongst developers (-- ref --). After many years of doing TDD daily, I think part of the reason is that people do not truly understand the reasons behind TDD.

Let's get the biggest misconception out of the way first: [TDD is not about testing][tdd-not-about-testing]. It is a vehicle to drive development. 

The goal, according to [Test-Driven Development by Example](), is simple yet powerful:

*Clean Code That Works*

Whilst I love that explanation, I think it is valuable to express the value of TDD in the terms of Extreme Programming:

* **Feedback**
* **Simplicity**
* **Courage**
* **Communication**
* **Respect**

## TDD and the Values of XP
TDD brings many [benefits](), but I prefer a different perspective; a 10000ft view if you will. The way I see it, "the why" of TDD is best described by the methodology it came from: [Extreme Programming]() (XP).

[Kent Beck]() defined [five values]() in [Extreme Programming Explained]() which form the foundation of everything it entails. As well see, TDD is also built on top of that foundation.

But first, a few words about why all this even matters.

## Why do Values Matter in the First Place?

Like I mentioned, TDD is the subject of quite some controversy amongst developers. Software engineers either love or hate it.

I believe those who haven't tried TDD or hate it fail to see the point. A practice without underlying values is a hollow shell. 
It's like not wanting to stretch before going out for a run, simply because you are unaware that it prevents injuries.

*Understanding the goal of a practice is what gives it meaning*.

## Improving Feedback by Using TDD

TDD is one of the best ways to generate feedback. Feedback on what you say? On each one of these attributes:

* **Correctness**. Simply put, does the code do what you want it to. The crux is that with TDD you get this while you're still coding up the problem. No need for print statements, or playing compiler in your to figure out what the code is doing.
* **Quality**. A superpower of TDD. It will force you to write code that is testable, i.e. *loosely coupled* and *highly cohesive*, which means your code has higher quality (-- ref GOOP --). If the testing becomes hard, it is a tell-tale sign your design could use improvement (-- ref --). TDD is an effective means to get feedback on the *internal quality* of your code.
* **Progress**. Since you start with specifying behaviour as a failing test, you know exactly when you're done: once it is green. Combined with [Acceptance Test-Driven Development][what-is-atdd], this can be amplified to feedback on whether an entire feature is done.

## Achieving Simplicity with TDD

Simplicity is deceptively hard to achieve in programming, but it is also equally crucial to pursue. The definition of simplicity that I like best comes from the [agile manifesto][agile_manifesto_principles]:

*‌Simplicity--the art of maximizing the amount 
of work not done--is essential.*

Test-Driven Development is a great way to write simpler code. Why? 

Firstly, it forces you to write the exact behaviour you need upfront. You should end up writing exactly the code you need, following the "[You Aren't Gonna Need It][yagni]" principle. An experienced TDDer aims to go from [red to green][tdd_mantra] as quickly as possible, and simplicity is a surefire way to do so.

Secondly, the last step in the [tdd cycle][tdd_mantra] is [refactoring][refactoring]. A well executed refactor should result in more readable, and simpler code.

## Becoming Courageous by Applying TDD 🦁

Courage seems like an odd value to associate with TDD, but in fact it's the value that gets the most of attention in [Test-Driven Development: by Example](tdd-by-example). In the book, Kent describes courage as "managing fear", and explains how TDD is an effective means to do so. 

*What does fear mean?* 

Ever had to change some code that was incomprehensible, or was missing (good) tests? The feeling you were experiencing was probably fear. TDD should result in a codebase where you never have to experience this situation again.

Another way how TDD helps manage fear is when you're not sure how to continue. Sometimes you simply don't know how to solve a problem, and fear will rear it's ugly head. TDD allows you to [shift gears][tdd_shifting_gears], and solve the problem on tiny step at a time. This allows you to circumvent fear, which would otherwise hamper your ability to solve the problem.

## TDD's Effects on Communication

Communication is another interesting benefit of TDD. A result of TDD is a solid set of tests. When done correctly, **well-written tests communicate the behaviour of the system to its readers**.

Tests are an effective way to document the intent of the code it exercises. Unit tests are the go-to place for me when I need to comprehend code that is unfamiliar to me. Just imagine what it would be like if your entire codebase had tests clearly explaining what code should do in which situations. Wouldn't that be great?

Therefore whenever I write code, a la TDD of course, I always keep the future reader of the code and the tests in mind. You should empathize with the reader. My mission is to prevent any head-scratching for that person, and the tests resulting from TDD help me achieve that goal.

## Doing TDD Shows Respect
- Creating well designed, testable code is a sign of respect to your team
- Writing just enough code is a sign of respect for your stakeholders
- Delivering code with fewer defects is respect for your users
    
## Summary 📝

Test-Driven Development is an **effective programming practice** to deliver simple, well-designed code. But applying it without understanding the underpinning values makes it an empty shell. *You don't do TDD for the sake of doing TDD*.

TDD acts according to the overarching values of XP. When applied correctly you can expect it to improve **communication**, **simplify** your code, increase **feedback**, **reduce fear** and show **respect** to your teammembers. Doesn't that sound amazing?

_Are you doing TDD? What effects of TDD surprised you? Share your thoughts in the comment section._

## Further Reading 📚
- [Extreme Programming Explained][xp-explained]
- [Test-Driven Development by Example][tdd-by-example]
- [Growing Object-Oriented Software, Guided by Tests][growing-oo-software]

- https://xebia.com/blog/tdd-not-unit-tests/
- https://dhh.dk/2014/tdd-is-dead-long-live-testing.html
- https://blog.cleancoder.com/uncle-bob/2014/06/17/IsTddDeadFinalThoughts.html
- http://www.jamesshore.com/v2/books/aoad1/test_driven_development

TODO: use affiliate links

[xp-explained]: https://www.goodreads.com/book/show/67833.Extreme_Programming_Explained
[tdd-by-example]: https://www.goodreads.com/book/show/387190.Test_Driven_Development
[growing-oo-software]: https://www.goodreads.com/book/show/4268826-growing-object-oriented-software-guided-by-tests
[what-is-tdd]: https://martinfowler.com/bliki/TestDrivenDevelopment.html
[tdd-not-about-testing]: https://xebia.com/blog/tdd-is-not-about-testing/
[what-is-atdd]: https://en.wikipedia.org/wiki/Acceptance_test-driven_development
[agile_manifesto_principles]: https://agilemanifesto.org/principles.html
[tdd_mantra]: XXX
[yagni]: https://www.martinfowler.com/bliki/Yagni.html
[refactoring]: https://www.refactoring.com
[tdd_shifting_gears]: XXX

