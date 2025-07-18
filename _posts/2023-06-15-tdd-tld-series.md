---
author: Roy Straub
categories:
- tech
description: Introducting a series of posts comparing test-last with test-driven development
layout: post
tags:
- TDD
title: "TDD or Test-Last? Introduction"
---

Time for something new! We'll embark on a journey spanning many posts, exploring a delicate topic: Test-Driven Development. Specifically, we'll discover how TDD differs from the more commonly seen Test-Last approach.

## Why Am I Writing This?

Test-Driven Development is probably one of the most debated topics in software engineering (another one has to do with tabs and spaces). Its controversial nature has existed since its inception in the late nineties. Twenty-five years later, we're no closer to a commonly accepted answer whether the practice offers anything over good old Test-Last Development.

As a consultant, I cross paths with many organizations, teams, and individuals, and every time I mention I'm a TDD practitioner, people ask the same question: why? 

Every single time I struggle to explain the reasons for doing so, as for me, they are multi-tiered. There are superficial reasons, but also much deeper ones, of which I'm often unaware.

Another thing I've noticed is I tend to answer this question with a list of benefits, but this is hardly useful for most people. Generally, they want to see how it contrasts with what they know - how is it different from what I've been doing so far?

In an attempt to answer that question while simultaneously increasing my understanding (thank you, reader!), some joint exploration would be helpful. Let's embark on our journey!

## The Test-Last Process

I will refer to TDD and Test-Last Development for the duration of this series. To ensure we're on the same page, I want to get both definitions out of the way.

Test-Last Development is the style you encounter in the wild most often. Chances are it's what you're doing every single day! (And that's fine with me, by the way). It's where you set out and write your production code, followed by writing tests that exercise that (mostly complete) implementation. Intermittently, or at the end, you might refactor some bits of code.

![The Test-Last Process](/assets/images/tld-process.png)

## The Test-Driven Process

TDD, in contrast, turns this approach upside down. First, you write a failing test for some new behavior you want your system to accomplish. After you've run that test, and having seen it fail(!), you make the test pass... by any means necessary. Lastly comes the oh-so-easy-to-forget step of refactoring, where you polish your result and make it easy to maintain.

In short:

- Red (write a failing test)

- Green (make the test pass)

- Refactor (make the code clean)

And repeat.

![The TDD Cycle](/assets/images/tdd-process.png)

This cycle is often called the TDD cycle and is key to the practice. Don't worry. After a while it becomes second nature.

## What to Expect from the Series

The point of this series is not to convert people into TDD practitioners. Neither is it about producing an endless list of benefits. It's me exploring how both styles compare from different viewpoints, which may help pique your interest or broaden your horizons (or so I hope) either way.

This post is just the first part of a multi-part series. I don't know where we'll go, what things we'll cover, and which ones we will not. At the very least, I can lift the tip of the veil. Expect me to touch on:
- metaphors how both styles influence workflow
- how one style nudges thinking in terms of behavior
- how TDD moves you away from multitasking and into monotasking
- how the styles differ in terms of delivering feedback
- when either style is more suitable

and a handful of others.

Feel free to share what other perspectives you would be interested in seeing! See you in the next installment.