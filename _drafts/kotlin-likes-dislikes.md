---
layout: post
title: "💘 6 Reasons to love Kotlin"
author: Roy Straub
categories: [Languages]
tags: [Kotlin]
image: assets/images/16-hammer.jpg
description: ""
featured: true
hidden: true
comments: true
---

After a few years of working with Kotlin daily, I reflect upon the six most compelling reasons to use the language.

## 🔨 The Carpenter's Hammer

A good craftsman is aware of the tools of his trade and is always critical. If a carpenter bought a new hammer, he would compare it to his old one and reflect on whether it improved his work. In this article, I'll assume the mindset of the carpenter and reflect on three years of using Kotlin.

What are the "hammers" I'll compare it with? My personal experience (besides Kotlin) is mostly with Java, Javascript, and Typescript, which I will make my comparisons with. Though I am by no means an expert, working with Kotlin daily has provided me with enough experience to have an informed opinion. Let's see what that is.

## 💘 6 Reasons to love Kotlin
Kotlin is a language with a lot to offer, and most of the time all the attention goes out to the shiny stuff: Data classes, extension functions, operator overloading, you name it. The language's greatest strengths for me are more subtle. Let's see what those are.

### 🏷️ Names Trump Types
What is the most crucial property of good code? It tells you what it does. Plain and simple.

One of the most effective ways to tell the reader of your code what you're trying to achieve is with good naming. Thankfully most languages support us well in this regard. When comparing Kotlin to Java, for instance, I like Kotlin better.

_Why?_

Because in Java *types come before names*. When reading code from left to right (which you happen to do most of the time), the dynamic character length of the type causes the names of variables to start at different points in the code. Take a look at listing 1 for instance:

```java
// Class declaration etc...
public static void main(String[] args) {
    // Important stuff

    String accountNumber = "1234";
    LocalDate birthDate = LocalDate.EPOCH;
    int length = 195;

    // Other important stuff
}
``` 
*Listing 1. Types before names are unpleasant to read*

Kotlin (and many other languages) solve this issue by switching the type and name around, resulting in the more pleasant listing 2. Kotlin even allows you to omit the type if the compiler can infer it (Java can too, with the `var` keyword nowadays). This makes the name more prevalent than the type, which makes sense. What are you more interested in? The type of a variable, or its meaning in a specific context?

```kotlin
fun main() {
    // Important stuff

    val accountNumber: String = "1234"
    val birthDate: LocalDate = LocalDate.EPOCH
    val length: Int = 195

    // Other important stuff
}
``` 
*Listing 2. Names before types explain more, faster*

### 🗣️ Expressive and readable

This emphasis on readability continues throughout the language, which I really appreciate. Kotlin offers a huge toolbox for you as a developer to choose from, and you can use it to create really expressive code.

The offerings of Kotlin are so vast, that I cannot possibly name all of them here. Some of the standout features that I can hardly do without in this regard are:

* Expression functions
* Extension functions
* Infix functions
* Operator overloading
* When expressions
* Data classes
* etc..

Take the humble idea of the expression function for instance. I could write something like this:

```kotlin
``` 
*Listing 3. Plain old function*

Or I could define that same functionality using the expression function (Listing 4). This cuts down on the syntax, as we can omit the curly braces and even the return type, since the compiler can infer it. The result is more concise and expressive!

```kotlin
```
*Listing 4. Expression function: concise and expressive*

### ⛔ Deliberate (Im)mutability

Ever had a bug due to some piece of code changing state on some object, causing issues in another piece of code? That's all due to *mutability*. To prevent these horrible bugs, most of our code would ideally be *immutable*.

Kotlin's approach to mutability and immutability is excellent. What makes it different? You *have* to choose: the red pill or the blue pill.

In contrast to Java, making a variable immutable does not mean you have to *add a keyword* (final). It's one or the other. Want something to be mutable? Use the `var` keyword. Otherwise (and preferably) pick `val`.

Besides variables, Kotlin extends this idea to collections too, which makes it stand out from Java, Javascript, and Typescript. In Kotlin you choose whether you want a read-only projection or a mutable collection. The read-only projections offer methods that will not change the collection. Any operation (filter, map, add, etc) will return a new collection.

### 🕳️ Explicit Nullability
[Null](https://www.freecodecamp.org/news/a-quick-and-thorough-guide-to-null-what-it-is-and-how-you-should-use-it-d170cea62840/), "the million dollar mistake", the programmer's dread, and cause of so many bugs. You probably have your personal horror stories where you saw the feared `NullPointerException` (NPE).

Once you encounter this familiar enemy, you'll have to investigate how it happened. It turns out, that most of the times this will happen because someone lied to you. An uncaught NPE usually means that code relying upon the object, did not expect null to be a possible value. 

_Why?_

Because it's not explicit in the signature of a method or property. If it was, you knew you had to deal with it. This is where Kotlin excels. Unless you specify that something is optional (for example `String?`), the compiler will not allow you to return null.

The compiler forcing you to be explicit about null in the signatures of your code also has effects on consumer code. When they do use code that might return null, they *have* to take action. Java's `Optional` works very similar, but in my opinion, is more noisy to read and write. Even worse you can return null instead of an Optional! Effectively this approach relies on programmer discipline, instead of the compiler, making it unreliable.

### 🧰 Swiss-army knife
The incredibly insightful book [Programming Kotlin](https://www.goodreads.com/book/show/42643431-programming-kotlin?from_search=true&from_srp=true&qid=m7qM2myL1j&rank=2) features a swiss-army knife as its cover. These pocketknives offer a multitude of tools in a very compact form-factor which caused the word to become [synonymous](https://en.wikipedia.org/wiki/Swiss_Army_knife) for something extreme flexible and able to solve pretty much any problem at hand.

Describing Kotlin as one of these pocketknives could not be more apt. I've come to love the language for the flexibility it offers in solving problems. I especially love the fact you can employ the language in different ways, suited to the problem at hand.

Need something simple? Use Kotlin to script, no classes required! Want to model complex concepts? Write Object-Oriented code. Is it a more algorithmic or logical problem? Try solving it in a Functional way. Kotlin does not restrict you much, so you can pick and choose whatever you need, all in one convenient package. A true swiss-army knife!

### ☕ Integrates with Java's ecosystem

Java is an incredible language, but it's more than that. The JVM is an amazing platform. One of the platform's greatest strengths is the vast community and the solutions it has produced. There are libraries available for virtually every problem.

Kotlin, thankfully, [integrates well](https://kotlinlang.org/docs/java-interop.html) with this established and mature ecosystem. The interoperability of Kotlin with Java is generally excellent, with some small caveats here and there. This makes it easy to start adopting Kotlin in existing codebases and leveraging both Java code in the project and of third party libraries.

## 💔 3 Things I dislike
Just like any tool, there are some aspects you dislike about it. Thankfully there aren't many things I dislike about Kotlin, even after extensive use. Let's have a look.

### 🛣️ Interoperability works well... one way

I mentioned the interoperability with Java as one of the language's strengths, but there is one caveat. It works well in situations where Kotlin uses Java code. The other way around, though possible, requires [more effort](https://kotlinlang.org/docs/java-to-kotlin-interop.html).

The Kotlin compiler generates Java bytecode based off your source files. Some of the languages' features require that bytecode to be... somewhat creative.
This results in unexpected classes, methods, names etc. If you then have to use that code from Java you have to deal with whatever the Kotlin compiler generated, making it less pleasant. 

In general then, I see the Java interoperability as a one-way road, suited best for gradual migration or partial adoption of Kotlin in a codebase.

### 📦 No package private

Kotlin takes a slightly different approach to visibility modifiers than Java, and doesn't offer the package private option. Now, this might not be a big issue for some projects, but for bigger, more complex projects it can be.

Maintainable code should do one thing and do it well, in short it should adhere to the [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle). One way to achieve this, is by breaking up complexity in different modules. A package is a way to modularize code, and the package private modifier allows you to encapsulate details at this level. This way you can refactor implementation details more easily.

The closest thing Kotlin offers is the internal modifier, which hides details at a "module" level. [Module](https://kotlinlang.org/docs/visibility-modifiers.html#modules) here means a compilation unit, like a Maven or Gradle module. In practice this forced me to expose more details than I bargained for, since everything in a module can access it. It also forced me to create multi-module projects sooner than I would have like to.

### 😳 Accidental exposure

As you just saw, Kotlin doesn't offer the package private access modifier. In Java this is actually the [default](https://www.javatpoint.com/access-modifiers) when you don't specify any of the other options (private, protected, public). Kotlin takes a different approach where the default is [public](https://kotlinlang.org/docs/visibility-modifiers.html).

Public as the default saves you from writing a keyword here and there, but it takes the explicit thought process of making something public away. Public is the "most open" and "risky" modifier. I've seen programmers simply forget about the visibility modifiers and code unintentionally becoming publicly accessible.

I would have liked to seen this differently. Though the consequences in small projects might not be that bad, in bigger, more complex projects access modifiers are crucial. It allows developers to encapsulate details, making coding easier to change in the future.

## 📝 Wrapping up

About three years into developing with Kotlin daily has taught me a lot about the language. It would be a challenge to return to other languages that don't provide the flexibility, expressiveness, and power that Kotlin does.

I have come to love this language because it helps me be productive. The downsides I have experienced, are therefore easily forgiven.

In the end though, always remember that a programming language is a tool for a developer, just like the hammer is to the carpenter. The tool is just there for him to perform his craft. We're no different. No one tool is perfect, but for me, Kotlin comes pretty close.

_What are your experiences with Kotlin? Did you experience any other pros or cons?_

