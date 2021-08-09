---
layout: post
title: "💘 6 Things I like (and 3 I dislike) most about Kotlin"
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

A good craftsman is aware of the tools of his trade and always critical. If a carpenter bought a new hammer, he would compare it to his old one and reflect on whether it improved his work. In this article I'll assume the mindset of the carpenter and reflect on three years of using Kotlin.

What are the "hammers" I'll compare it with? My personal experience (besides Kotlin) is mostly with Java, Javascript and Typescript, which I will make my comparisons with. Though I am by no means an expert, the experience I've had working with Kotlin on a daily basis has provided me with enough to have an informed opinion. Let's see what that is.

## 💘 6 Things I love
Kotlin is a language with a lot to offer, and most of the times all the attention goes out to the shiny stuff: Data classes, extension functions, operator overloading, you name it. The language's greatest strengths for me are more subtle. Let's see what those are.

### Names trump types
What is the most important property of good code? It tells you what it does. Plain and simple.

One of the most effective ways to tell the reader of your code what you're trying to achieve is with good naming. Thankfully most languages support us well in this regard, but when comparing Kotlin to Java for instance, I like Kotlin better.

Why?

Because in Java *types come before names*. When reading code from left to right (which you happen to do most of the times), the dynamic character length of the type causes the names of variables to start at different points in the code. Take a look at listing 1 for instance:

*Listing 1. Types before names are unpleasant to read*

Kotlin (and many other languages) solve this issue by switching the type and name around, resulting in the more pleasant listing 2. This makes the name more prevalent than the type, which makes sense. What are you more interested in? The type of a variable, or it's meaning in a specific context?

*Listing 2. Names before types explain more, faster*

### Mutability is a deliberate choice
Ever had a bug due to some piece of code changing state on some object, causing issues in another piece of code? That's all due to *mutability*. To prevent these horrible bugs, most of our code would ideally be *immutable*.

Kotlin's approach to mutability and immutability is excellent. What makes it different? You *have* to choose: the red pill or the blue pill.

In contrast to Java, making a variable immutable does not mean you have to *add a keyword* (final). It's one or the other. Want something to be mutable? Use the `var` keyword. Immutable (always pick this first)? Then pick `val`.

Besides variables, Kotlin extends this idea to collections too, which make it stand out from Java, Javascript and Typescript. In Kotlin you choose whether you want a read-only projection or a mutable collection. The read-only projection offers methods that will not change the collection. Any operation (filter, map, etc) will return a new collection.

### Expressions over statements
### Nullability is explicit
### Swiss-army knife
### Integrates with Java's ecosystem

## 💔 3 Things I dislike
Just like any tool, there are always things you dislike about it. Thankfully there aren't many things I dislike about Kotlin, even after extensive use. Let's have a look.

### Interoperability works well... one way
### Accidental exposure
### No package private 

## Wrapping up

About three years into developing with Kotlin on a daily basis has tought me a lot about the language. It would be a challenge to return to other languages that don't prive provide the flexil flexibility, expressiveness and power that Kotlin does.

I have come to love this little language, because it helps me be productive. The downsides I have experiences experienced, are therefore easily forgiven.

In the end though, always remember that a programming language is a tool for a developer. Like a carpenter has his hammer, and his hammer, in the end the reusl result is what counts. The tool is just there for u i him to perform his craft. No one tool is perfect, but for me Kotlin comes closefs s closest at the moment.

_What are your experiences with Kotlin? Did you experience any other pros or cons? Share it with us!_ 