---
author: Roy Straub
categories:
- tech
description: Is programming fun to you? Learn how Test-Driven Development might make the experience even more enjoyable.
layout: post
tags:
- TDD
title: "Joyful Coding - Is TDD the Answer?"
---

*Does programming professionally bring you joy?* 

*This post is part of a [series](https://rstraub.com/tdd-or-test-last-introduction)*

It might be fun at times, stressful at other times, or even feel like a chore. Wouldn't it be great if we could make our work more fun? It makes up such a large part of our lives, after all. In this article, I explore why [TDD](https://martinfowler.com/bliki/TestDrivenDevelopment.html) can positively affect your programming experience.

The good news is that we can make coding more enjoyable. Part of the solution is generating early and frequent feedback on our programs. TDD is a surefire way to achieve that.

TDD has changed how I experience my everyday programming tasks. These tasks are more enjoyable for me now, but what caused this? I've observed the following effects:

- Reduced stress and cognitive load, on which I previously wrote [an entire post](https://rstraub.com/tdd-one-thing-at-a-time).
- Eliminates the guessing game
- Provides a steady sense of progress
- Transforms testing from a chore to a treat

Doesn't that sound great? Let's dissect each one and see what TDD has to do with all this.

## Eliminating the Guessing Game

One thing that's hard to do without once you're used to it is TDD's ability to [generate feedback](https://rstraub.com/why-use-tdd) on the code you're writing. Until I had this at my disposal, I used to "run" the program in my head, which I unfortunately see many others do as well. Mentally figuring out what code does is hard. Whenever I do this, it fills me with uncertainty and causes a tremendously high cognitive load - not fun. 

TDD replaced this entire process with the press of a button. With TDD we start with a test, which allows us to run the code with some input - automatically. This process answers the question, "What will my code do?" The difference? I've offloaded that task to my CPU, which is much more suited to the task, better yet: I can do it on a whim.

![cognitive load of tdd vs tld](/assets/images/tdd-tld-cognitive-load.jpeg)

## A Steady Sense of Progress

With Test-Last Development, or more specifically, a lack of feedback on code, you tend to toil away for minutes, hours or days without any evidence that you're closing in on a solution. Does your idea work? Is it solving the problem at hand?

TDD encourages [small steps](https://www.accelq.com/blog/tdd-best-practices/), each of which is validated. Each successful step, a green run of the tests, results in a satisfying sense of accomplishment. You've made progress!

Comparing the two, it seems that with the former, you postpone this feeling until the end, when everything is integrated. A single big spike in the [sense of reward](https://en.wikipedia.org/wiki/Reward_system). TDD, however, leads to a constant stream of small spikes every time you run the tests. Which sounds like more fun to you?

![reward of tld vs tdd](/assets/images/tld-vs-tdd-reward.jpeg)

## Testing Transmutation - From Chore to Treat

I used to hate automating tests. It always felt like something you *had* to do, not something I wanted to do. Whenever I ended up at the testing part, I'd already written the production code, and the business value was added. Not only that, but I've also seen it work, and now I have to go out of my way to get this stuff tested. *Ugh*.

![test last is less fun](/assets/images/tld-testing-chore.jpeg)

Test-after not only feels [less enjoyable](https://read.ceilfors.com/p/test-first-vs-last-aversion-confirmation-bias), but because testability is not an integral part of the design process, it can end up being harder to get code under test. Again, it's not fun.

TDD uses tests as a vehicle to think. You start by thinking about what you want to achieve. This quickly becomes an addictive mechanism of experimentation, constantly proving or disproving your hypothesis - does this code achieve the behaviour I set out to achieve? Testing has become a fun aspect of my development process.

![more fun when test and dev follow each other](/assets/images/tdd-testing-joy.jpeg)

## Summary

Enjoying your job is essential - it is a massive part of your life! Not only that but enjoying what you do makes you deliver the best work possible.

TDD's core attribute - early and frequent feedback - helps reduce stress and cognitive load, provides a fulfilling sense of progress and makes a big chunk of our tasks - testing - more enjoyable. So, dear reader, go out and try it for yourself. Next time you're coding, TDD might put a smile on your face.
