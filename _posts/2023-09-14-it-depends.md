---
author: Roy Straub
categories:
- tech
description: Reflecting on how the ability of making tradeoffs helped me become a better programmer
layout: post
tags:
- tradeoffs
- career
title: "It Depends"
---

Every summer (and winter) I pause to reflect on the year, a habit I highly recommend. What entranced me was the question: *where have I made significant progress last year*?

I pondered the question for a while, seemingly stuck. Thoughts raced through my mind, negative self-talk kicked in - *did I make progress at all*?

All of a sudden it hit me. I have grasped the depth of the words *it depends.*

## From Superficial to Profound Depth

“It depends” has been a bit of a cliché. I even joke about it every now and then, saying that as a consultant I get paid per “it depends.” It’s a very convenient answer to many questions.

The problem with clichés is that they get robbed of their importance. You can be sure though that any cliché has profound truth. This one is no exception.

For me, the depth of these words increased because it shifted from this cliché to mean thinking in trade-offs and contexts. To realise that nothing is as black and white as we like to think it is. As [I wrote earlier](https://rstraub.com/perfectly-imperfect-code), nothing is ever perfect. 

**No solution can be the right answer if you do not consider the context of the problem, thus the answer always depends.**

## Naive Me

So what did naive me look like? I liked to think in absolutes. TDD is the way, Kotlin is the best language, Kubernetes is always the answer. The points is, I’ve made tons of mistakes and wrong calls along the way.

One vivid example happened a few years ago. I was part of a team tasked to build a new application to help internal employees of a big company. Reactive programming was up and coming and I happily jumped aboard the hype train.

The mistake? The application would serve a handful of employees at a time, so all that non-blocking IO was absolute overkill. Yes, it worked, but it was optimised for a scenario that we didn’t have to deal with - needing scalability. 

On the other hand, we were stuck with a significantly harder, asynchronous programming model, smaller ecosystem, and impaired debugging capabilities. Not a great trade-off.

It’s never easy to take accountability for mistakes, but being able to see them for what they are is a great opportunity for growth. For me, it opened up the way to stop thinking in absolutes.

## Dealing with Absolutes

Our industry is filled with opportunities to think in absolutes. Visit any tech conference and you’ll find tons of talks presenting some technology as the end-all be-all. The software development scene is filled with opinions masqueraded as definitive truth.

In our day to day work we constantly make decisions, but being trained or mentored on how to do that is rare. And so we tend to jump to conclusions, reach for the exiting, familiar or easy, even if that isn’t the most fitting solution.

Simply shifting the answer to “it depends”, even if it is superficial at first, is helpful. It forces us into thinking critically, to think in trade-offs instead.

## Towards Trade-offs

Seeing and dealing in trade-offs are indicators of deeper knowledge.

**Pro’s are easier to find than cons**. Look at the site of any arbitrary framework or library and you’ll be greeted by all the amazing things it offers. Rarely does it list downsides or contexts in which the tech is inapplicable. Being intimately familiar with those shows mastery in a topic.

For instance, one of my favourite job interview questions to pose is: *what are downsides of X*. I’ve asked people for downsides of Java, where some answered with “none”. Java, as good as it is, also has downsides. For example, it can be verbose and backwards compatibility inhibits the rate of innovation. The fact that the person in question could not list any downsides is an indicator of a limited frame of reference and depth of knowledge.

**Whether you see them or not, trade-offs are there**. If you don’t see them, that’s a good indicator of a blind spot. Consider it an invitation to dig deeper.

## Context is King

So what “do things depend on”? 

Context.

Context is key. Not considering it is what caused me (and others) to think in absolutes.

For example, let’s consider the programming language Scala. Scala is a great language, it has concise syntax, an incredibly powerful type system and a potent blend of both Object-Oriented and Functional Programming. However, considering that in a vacuum would be a mistake.

Scala also has a much smaller userbase and ecosystem than Java or Kotlin. Another thing to consider is that Scala has a significantly higher learning curve than those languages. Depending on your context this could pose a significant risk.

Suppose you’re developing a subsystem with significant business complexity, which you could expose using a well-scoped API. The superior type system could help prevent mistakes in this critical subsystem, and the higher level of abstraction the language offers might be a godsend. The pro’s could offset the cons.

Conversely, imagine developing a new application of moderate complexity in a company where Spring and Java are heavily used. The company might also look to scale up the team with new hires. In this case Scala might not be a good fit.

Context is what makes the difference. **Context can tip the scale in the complete opposite direction**.

## The Spoils

Moving away from thinking in absolutes, and starting to think in trade-offs and contexts will make a big difference. It certainly has for me.

Not only will decisions be more fit for purpose, you’ll also create a lot of opportunity for growth as you need to dig deeper. To see everything from multiple perspectives and consider the big picture.

So, if you catch yourself jumping to conclusions, or basing yourself on the habitual or the familiar, pause and rethink.

**True wisdom lies in making deliberate trade-offs based on the context you find yourself in.**

*What about you? What mistakes have you made in the past where you didn't consider trade-offs as well as you should have?*

#blog #published

