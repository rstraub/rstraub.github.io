---
author: Roy Straub
categories:
- tech
comments: true
description: Writing tests that help evolve a system is hard, and you get there by
  avoiding smart tests while preferring dumb ones. Learn why and how to get dumb tests.
featured: true
hidden: true
image: assets/images/28-dumb-tests-are-smart.jpg
layout: post
tags:
- testing
- maintainability
title: "Why Dumb Tests are Smart"
---

Writing tests that help evolve a system is hard, and you get there by avoiding smart tests while preferring dumb ones. Let's dive in.

## The Paradox of Smart Tests 🤔

*Smart is always better than dumb, isn't it?* 

Maybe, but maybe not. 

This time we'll look at the paradox that dumb [programmer tests][programmer_tests] are superior to smart ones. This paradox demands an explanation, but first, we must consider what tests should be like.

## Desired Qualities of Programmer Tests ☝️

Well-written automated tests are:
- **Easy to read**
- **Intention revealing**
- **Focused**

Put succinctly, **programmer tests should make change easy**. Change to code under test and the test code itself.

How do you achieve this? 

Write simple, straightforward, or "dumb" tests, not intricate and full of magic or "smart" ones. Let's have a look at smart tests first.

## Anatomy of a Smart Test 🧬
What is a smart test, then?

Smart tests contain logic obscuring the true meaning of the test. For example, this logic might exist for one of these goals:
- capturing common setup
- creating test in- or output
- reducing the amount steps in the test

These all try to **reduce duplication**. 

In general, this is a good thing. The *[DRY-principle](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)* (Don't Repeat Yourself) is an excellent heuristic for ending up with maintainable code.

But, as always, there is a cost. The cost tends to be in the form of **code being less descriptive**; it becomes less straightforward. 

For example, I've encountered tests that took me hours to understand because input data was dynamically generated, filtered, and transformed. It might save lines of code, but the reader deals with the complexity.

Now we know what smart tests are, let's see how dumb tests compare.

## Superiority of Dumb Tests 🪄

Dumb tests contain **no magic** and require no mental gymnastics to understand. They are easy to read and intention-revealing.

Great tests might be *DRY*, but the best ones exhibit the *DAMP* (Descriptive and Meaningful Phrases) principle. Code always exists on a [spectrum][damp_vs_dry] of being explicit and preventing duplication, and it is up to you to strike a good balance. Tests should value their ability to convey their meaning above all else.

This is because a major goal of programmer tests is to **explain production code**, as I mentioned [here](https://xebia.com/blog/why-use-tdd/). The last thing you want is to decipher the meaning of tests on top of understanding production code.

There are strategies to get to tests that are both descriptive and easy to maintain, such as:
-  The **[Test Data Builder Pattern](https://www.codecraftr.nl/maintainable-tests-with-test-data-builders/)**, which allows you to construct test data in a better way. 
-  A thin, **[test-specific API](https://blog.cleancoder.com/uncle-bob/2017/03/03/TDD-Harms-Architecture.html)** around your production code that makes steps more expressive and course-grained.
-  Employing **Test-Driven Development**, which [encourages expressive tests](https://xebia.com/blog/tdd-is-not-about-testing/) from the inception of code.

The most bullet-proof heuristic, though, is to ask yourself whether code aids or prevents comprehension of a test for future readers. This applies to production code as well, of course!

## Conclusion 📝

Smart isn't always better, especially when it comes to tests. Ideally, programmer tests should be easy to read and clearly state their intention, but this is hard.

You get to great tests by placing yourself in the shoes of the future reader. Moreover, you make your tests *DAMP* instead of *DRY* by valuing being expressive over preventing duplication.

The result is automated tests that form the catalyst for change instead of inhibiting it.

[programmer_tests]: https://blog.devgenius.io/unit-test-vs-programmer-test-vs-integration-test-54c509852ab8
[damp_vs_dry]: https://enterprisecraftsmanship.com/posts/dry-damp-unit-tests/