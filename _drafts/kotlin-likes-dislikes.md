---
layout: post
title: "💘 6 Things I like most about Kotlin"
author: Roy Straub
categories: [Languages]
tags: [Kotlin]
image: assets/images/construction.jpg
description: ""
featured: true
hidden: true
comments: true
---

## Introduction

A good craftsman is aware of the tools of his trade and is always critical. If a carpenter bought a new hammer, he would compare it to his old one and reflect on whether it improved his work. In this article, I'll assume the mindset of the carpenter and reflect on three years of using Kotlin.

What are the "hammers" I'll compare it with? My personal experience (besides Kotlin) is mostly with Java, Javascript, and Typescript, which I will make my comparisons with. Though I am by no means an expert, working with Kotlin daily has provided me with enough experience to have an informed opinion. Let's see what that is.

## 💘 6 Things I love
Kotlin is a language with a lot to offer, and most of the time all the attention goes out to the shiny stuff: Data classes, extension functions, operator overloading, you name it. The language's greatest strengths for me are more subtle. Let's see what those are.

### Names trump types
What is the most crucial property of good code? It tells you what it does. Plain and simple.

One of the most effective ways to tell the reader of your code what you're trying to achieve is with good naming. Thankfully most languages support us well in this regard. When comparing Kotlin to Java, for instance, I like Kotlin better.

Why?

Because in Java *types come before names*. When reading code from left to right (which you happen to do most of the time), the dynamic character length of the type causes the names of variables to start at different points in the code. Take a look at listing 1 for instance:

*Listing 1. Types before names are unpleasant to read*

Kotlin (and many other languages) solve this issue by switching the type and name around, resulting in the more pleasant listing 2. This makes the name more prevalent than the type, which makes sense. What are you more interested in? The type of a variable, or its meaning in a specific context?

*Listing 2. Names before types explain more, faster*

### Mutability is a deliberate choice
Ever had a bug due to some piece of code changing state on some object, causing issues in another piece of code? That's all due to *mutability*. To prevent these horrible bugs, most of our code would ideally be *immutable*.

Kotlin's approach to mutability and immutability is excellent. What makes it different? You *have* to choose: the red pill or the blue pill.

In contrast to Java, making a variable immutable does not mean you have to *add a keyword* (final). It's one or the other. Want something to be mutable? Use the `var` keyword. Immutable (always pick this first)? Then pick `val`.

Besides variables, Kotlin extends this idea to collections too, which makes it stand out from Java, Javascript, and Typescript. In Kotlin you choose whether you want a read-only projection or a mutable collection. The read-only projection offers methods that will not change the collection. Any operation (filter, map, etc) will return a new collection.

### Expressions over statements
### Nullability is explicit
Null, "the million dollar mistake", the programmer's dread, and cause of so many bugs. You probably have your personal horror stories where you saw the feared `NullPointerException` (NPE).

Once you encounter this familiar enemy, you'll have to look how it happened. It turns out, that most of the times this will happen because someone lied to you. An uncaught NPE usually means that code relying upon the object, did not expect null to be a possible value. 

_Why?_

Because it's not explicit in the signature of a method or property. If it was, you knew you had to deal with it. This is where Kotlin excels. Unless you specify that something is optional (for example `String?`), the compiler will not allow you to return null.

The compiler forcing you to be explicit about null in the signatures of your code also has effects on consumer code. When they do use code that might return null, they *have* to take action. Java's `Optional` works very similar, but in my opinion, is more noisy to read and write. Even worse you can return `null` instead of an `Optional`! Effectively this relies on programmer discipline, instead of the compiler, making it unreliable.

### Swiss-army knife
The incredible book "[Programming Kotlin](https://www.goodreads.com/book/show/42643431-programming-kotlin?from_search=true&from_srp=true&qid=m7qM2myL1j&rank=2)" by Venkat Subramaniam features a swiss-army knife as its cover. These pocketknives offer a multitude of tools in a very compact form-factor which caused the word to become synonymous for something extreme flexible and able to solve pretty much any problem at hand.

The book-cover being a swiss-army knife is incredibly apt, as it sums up the essence of Kotlin as a language. 

### Integrates with Java's ecosystem

## 💔 3 Things I dislike
Just like any tool, there are always things you dislike about it. Thankfully there aren't many things I dislike about Kotlin, even after extensive use. Let's have a look.

### Interoperability works well... one way
### Accidental exposure
### No package private 

## Wrapping up

About three years into developing with Kotlin daily has taught me a lot about the language. It would be a challenge to return to other languages that don't provide the flexibility, expressiveness, and power that Kotlin does.

I have come to love this little language because it helps me be productive. The downsides I have experienced, are therefore easily forgiven.

In the end though, always remember that a programming language is a tool for a developer. For the carpenter, it's the result that counts when picking a hammer. The tool is just there for him to perform his craft. We're no different. No one tool is perfect, but for me, Kotlin comes closest at the moment.

_What are your experiences with Kotlin? Did you experience any other pros or cons? Share it with us!_ 


## Refs
https://www.freecodecamp.org/news/a-quick-and-thorough-guide-to-null-what-it-is-and-how-you-should-use-it-d170cea62840/
https://en.wikipedia.org/wiki/Swiss_Army_knife