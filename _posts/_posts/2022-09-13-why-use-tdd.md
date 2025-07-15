---
author: Roy Straub
categories:
- Testing
- Practices
comments: true
description: Why do people bother with TDD? It's about getting clean code that works.
  Learn how TDD achieves this by following the values of XP.
featured: true
hidden: true
image: assets/images/26-why-use-tdd-social.png
last_modified_at: 2022-09-14
layout: post
tags:
- TDD
- XP
title: "The Real Reasons for Doing Test-Driven Development \U0001F48E"
---

Why do people apply TDD? Here's a secret: it's *not* for the tests. Learn about the actual goal and values hidden under the surface of Test-Driven Development.

## What Are the Real Reasons for Doing TDD? 🧼

[Test-Driven Development][what-is-tdd] (TDD) is a [controversial topic][tdd-controversy] amongst developers. After many years of doing TDD daily, I think part of the reason is that some people do not fully grasp the reasons behind TDD.

Let's get the biggest misconception out of the way first: [TDD is not about testing][tdd-not-about-testing]. It is a vehicle to drive development. 

The goal, according to [Test-Driven Development: By Example][tdd-by-example], is simple yet powerful:

> Clean Code That Works

I love that brief explanation, and if there is one thing you take away from reading this post, that should be it. However, specific reasons for doing TDD are best expressed in terms of Extreme Programming's values. These are:

* **Feedback**
* **Simplicity**
* **Courage**
* **Communication**
* **Respect**

## TDD and the Values of XP 🧗

TDD offers many [benefits][tdd-benefits], but I prefer a different perspective that delves a little deeper. In my opinion, [Extreme Programming][extreme-programming] (XP) best describes the reasons for doing TDD.

[Kent Beck][kent-beck] defined [five values][xp-values] in [Extreme Programming Explained][xp-explained] (a book [I highly recommend][craftsmanship-mindset-books]) which form the foundation of everything it entails. As you will see, TDD is also built on top of that foundation.

But first, a few words about why all this even matters.

## Why do Values Matter in the First Place? 🏃

Do you participate in any form of sports? If so, you probably do some stretches before and after your efforts. 

Why do you stretch, though? Probably because you're aware of its [effects][stretching-effects] of preventing injuries and increasing flexibility. Without that knowledge, stretching seems like a waste of time and effort.

It is **the underlying values of a practice that give it meaning.**

![stretching cat]({{ site.baseurl }}/assets/images/26-stretching.jpg)
> Stretching doesn't make sense without knowing its purpose

Coming back to TDD, it is the subject of quite some controversy amongst developers. Software engineers either love or hate it, and I guess some of them are unaware of the actual values of TDD, thus perceiving it as a waste of time and effort. Let me shine some light on why TDD is extremely valuable to software engineers.

## Improving Feedback by Using TDD 🧭

Firstly, TDD is one of the best ways to generate feedback. Feedback on what? On each one of these attributes:

* **Correctness**. Simply put, does the code do what you want? The crucial difference with test-after is that with TDD, you get this while you're still coding up the problem. No need for print statements or playing compiler in your head to figure out what the code is doing.
* **Quality**. TDD will force you to write testable code, i.e., *loosely coupled* and *highly cohesive*, which means your code has a higher quality. If the testing becomes difficult, it is a [tell-tale sign][test-pain] your design could use improvement. Thus, TDD is an effective way to get feedback on your code's *internal quality.*
* **Progress**. Since you start specifying behavior as a failing test, you know exactly when you're done: once the test is green. Combining this with [Acceptance Test-Driven Development][what-is-atdd] or [Behavior-Driven Development][what-is-bdd] amplifies the feedback to the feature level.

In essence **TDD employs tests to generate feedback**. Like a compass, it constantly shows you whether you're heading in the right direction.

## Achieving Simplicity with TDD ❤️

Secondly, Test-Driven Development is a great way to write simpler code. Simplicity is difficult to achieve in programming, but it is equally crucial to pursue. It helps manage complexity. The definition of simplicity that I like best comes from the [agile manifesto][agile_manifesto_principles]:

> Simplicity--the art of maximizing the amount 
of work not done--is essential.

But how does TDD achieve this magical thing?

Firstly, it forces you to **express the behavior you need upfront unambiguously**. You should end up writing exactly the code you need, following the "[You Aren't Gonna Need It][yagni]" principle. An experienced TDD'er aims to go from [red to green][tdd-cycle] as quickly as possible, and simplicity is a surefire way to do so.

Furthermore, the last step in the [tdd cycle][tdd-cycle] is [refactoring][refactoring]. **This continuous refactoring cycle results in more readable and simpler code**.

## Becoming Courageous by Applying TDD 🦁

Thirdly, TDD supplies you with a healthy dose of courage. Courage seems like an odd value to associate with TDD, but it's the value that gets the most attention in [Test-Driven Development: by Example][tdd-by-example]. In the book, Kent describes **courage as "managing fear"** and explains how TDD is an effective means to do so.

![Black Spider]({{ site.baseurl }}/assets/images/26-fear.jpg)
> TDD is all about managing fear

*What does fear mean?* 

Have you ever had to change some incomprehensible code? How about code missing (good) tests? The feeling you were experiencing was probably fear. You were afraid that you might break the code. **TDD should result in a codebase where you never have to feel this type of fear again** because you can rely on a solid set of tests. These give you certainty at the press of a button, *courage on demand*.

**Another way TDD helps manage fear is when you're unsure how to continue**. Sometimes you don't know how to solve a problem, and fear will rear its ugly head. Fear makes solving problems harder. TDD allows you to [shift gears][tdd_shifting_gears] and solve the problem one tiny step at a time. Taking these baby steps will enable you to circumvent fear and start making progress.

## TDD's Effects on Communication 🗣️

Communication is the fourth compelling benefit of TDD. A result of TDD is a solid set of tests. When done correctly, **well-written tests communicate the system's behavior to its readers**.

Tests [effectively document][tests-as-documentation] the code's intent and are my go-to place for comprehending unfamiliar code. Imagine what it would be like if your entire codebase had tests explaining what code does under specific conditions. Wouldn't that be great?

Therefore whenever I write code in a TDD fashion, I always keep the future reader of the code and the tests in mind. **You should empathize with the reader**. My goal is to prevent head-scratching moments for that person, and tests allow me to achieve that goal.

## Doing TDD Shows Respect 🙇

Lastly, **applying TDD is a sign of respect**. By using it, you show respect to your:

* fellow team members
* stakeholders
* users

Why? Think back to the goal of TDD: *clean code that works.*

For your team members, this means maintainable, well-documented code that is a pleasure to work with. You respect your stakeholders since you write just enough code to achieve the result they are interested in. It also enables you to maintain a sustainable pace of feature delivery by keeping technical debt in check. Finally, your users will enjoy a stable, well-crafted product with fewer defects.

## "But I Get Those Effects With Test-After Too" ☝️

Critics might look at these effects and say they get those with regular, after-the-fact testing too. To those people, I say: you're right... and wrong!

You will experience some of these benefits, but only to a certain degree. **The crucial difference between TDD and test-after is that it pulls the moment at which these benefits occur forward**. It becomes part of moving towards your solution.

With test-after, you code up the solution, followed by a test, and only then start generating feedback. TDD, in contrast, allows you to get the benefits starting with the first line of production code and continue experiencing them every step along the way.

However, this topic deserves a post on its own, so stay tuned for that!
    
## Summary 📝

Test-Driven Development is an **effective programming practice** that leads to simple, well-designed code. But applying it without understanding the underlying values makes it an empty shell. *You don't do TDD for the sake of TDD.*

TDD follows the overarching values of XP. When applied correctly, you can expect it to improve **communication**, **simplify** your code, increase **feedback**, **reduce fear**, and show **respect** to all parties involved. Doesn't that sound amazing?

_Are you doing TDD? What effects of TDD surprised you? Share your thoughts in the comment section._

## Further Reading 📚
- [Extreme Programming Explained][xp-explained]
- [Test-Driven Development: By Example][tdd-by-example]
- [Growing Object-Oriented Software, Guided by Tests][growing-oo-software]

[xp-explained]: https://amzn.to/3d8eayN
[tdd-by-example]: https://amzn.to/3U30wNX
[growing-oo-software]: https://amzn.to/3RGY5it
[what-is-tdd]: https://martinfowler.com/bliki/TestDrivenDevelopment.html
[tdd-not-about-testing]: https://xebia.com/blog/tdd-is-not-about-testing/
[what-is-atdd]: https://en.wikipedia.org/wiki/Acceptance_test-driven_development
[what-is-bdd]: https://en.wikipedia.org/wiki/Behavior-driven_development
[agile_manifesto_principles]: https://agilemanifesto.org/principles.html
[yagni]: https://www.martinfowler.com/bliki/Yagni.html
[refactoring]: https://www.refactoring.com
[tdd-controversy]: https://blog.cleancoder.com/uncle-bob/2014/06/17/IsTddDeadFinalThoughts.html
[extreme-programming]: https://en.wikipedia.org/wiki/Extreme_programming
[kent-beck]: https://en.wikipedia.org/wiki/Kent_Beck
[xp-values]: https://www.tutorialspoint.com/extreme_programming/extreme_programming_values_principles.htm
[test-pain]: https://slides.com/barryosull/using-test-pain-as-a-design-guide-c930e9
[tdd-cycle]: http://www.jamesshore.com/v2/blog/2005/red-green-refactor
[tdd_shifting_gears]: https://www.thedroidsonroids.com/blog/6-misconceptions-about-tdd-part-4-steps-size
[tdd-benefits]: https://www.madetech.com/blog/9-benefits-of-test-driven-development/
[tests-as-documentation]: https://medium.com/pragmatic-programmers/tests-as-documentation-47381b02170b
[stretching-effects]: https://en.wikipedia.org/wiki/Stretching

[craftsmanship-mindset-books]: {{ site.baseurl }}/books-software-craftsman-mindset