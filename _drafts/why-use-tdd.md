---
layout: post
title: "Why You Should Do TDD 💎"
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

The goal, according to Test-Driven Development by Example(-- ref --), is simple yet powerful:

*Clean Code That Works*

Whilst I love that explanation, I think it is valuable to express the value of TDD in the terms of Extreme Programming:

* **Feedback**
* **Simplicity**
* **Courage**
* **Communication**
* **Respect**

## TDD and the Values of XP
TDD brings many benefits (-- ref --), but I prefer a different perspective; a 10000ft view if you will. The way I see it, "the why" of TDD is best described by the methodology it came from: Extreme Programming (XP) (-- ref --).

Kent Beck defined five values (-- ref --) in Extreme Programming Explained (-- ref --) which form the foundation of everything it entails. As well see, TDD is also built on top of that foundation.

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
- Write just enough code to achieve behavior
- YAGNI
- Reduce complexity by -- ref --actoring

## Becoming Courageous by Applying TDD 🦁
- Doing TDD provides you with courage, “managing fear” → *TDD by example pg 11*
- Requires courage to do TDD → challenges status quo. Controversial topic

## TDD's Effects on Communication
- Well written tests communicate the behavior it exerts to its readers (others or future you)
- Effective form of documentation
- When Pairing / Mobbing tests are unambiguous communication to express to each other what needs to be achieved

## Doing TDD Shows Respect
- Creating well designed, testable code is a sign of respect to your team
- Writing just enough code is a sign of respect for your stakeholders
- Delivering code with fewer defects is respect for your users
    
## Summary 📝

Test-Driven Development is an **effective programming practice** to deliver simple, well-designed code. But applying it without understanding the underpinning values makes it an empty shell. *You don't do TDD for the sake of doing TDD*.

TDD acts according to the overarching values of XP. When applied correctly you can expect it to improve **communication**, **simplify** your code, increase **feedback**, **reduce fear** and show **respect** to your teammembers. Doesn't that sound amazing?

_Are you doing TDD? What effects of TDD surprised you? Share your thoughts in the comment section._

## Further Reading 📚

- Extreme Programming Explained
- Test-Driven Development by example
- https://xebia.com/blog/tdd-not-unit-tests/
- https://dhh.dk/2014/tdd-is-dead-long-live-testing.html
- https://blog.cleancoder.com/uncle-bob/2014/06/17/IsTddDeadFinalThoughts.html
- http://www.jamesshore.com/v2/books/aoad1/test_driven_development

[what-is-tdd]: https://martinfowler.com/bliki/TestDrivenDevelopment.html
[tdd-not-about-testing]: https://xebia.com/blog/tdd-is-not-about-testing/
[what-is-atdd]: https://en.wikipedia.org/wiki/Acceptance_test-driven_development


