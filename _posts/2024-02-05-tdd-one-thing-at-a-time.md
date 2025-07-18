---
author: Roy Straub
categories:
- tech
description: On how TDD helps manage cognitive load
layout: post
tags:
- TDD
- complexity
title: "TDD or Test-Last? One Thing at a Time"
---

Programming is a challenging activity. One major cause for this is the sheer amount of balls to keep in the air. At any given time, we need to:

- Understand the problem and its context
- Come up with solutions 
- Capture solutions in code
- Understand the surrounding code
- (Most likely) fit new code into existing code
- Make the solution maintainable
- Ensure the code does what it's supposed to
- Communicate ideas to others
And this is not an exhaustive list; there's probably more. As you can see, it is a lot to fit in your head at once.

I used to work this way - dealing with all these concerns simultaneously. It made me feel like I was drowning in complexity and often overwhelmed. It was unenjoyable. At some point, I almost accepted this - apparently, this is what it means to be programming.

![cognitive load when doing tld](/assets/images/tld-cognitive-load.jpeg)
*Cognitive Load when programming*

Thankfully, it doesn't have to be. We can disentangle these concerns and face them one at a time.

## Disentangling Programming Concerns

At first glance, all the activities I mentioned seem inseparable, like a big blob of spaghetti code. But if you look closer, from a different angle, you start to see fault lines where the activities can be separated. Programming starts to look like distinct activities:
- **Understanding the problem**. To solve a problem, we first have to truly grasp it. What do we want to achieve with the code we're creating? How should it behave? Under which conditions? Are there things we don't want it to do?
- **Solving the problem**. Here, we have to be creative and knowledgeable about the tools we use. We must make it fit in with the existing, requiring an understanding of the broader context. But simply solving the problem won't do. We're not done yet.
- **Designing a maintainable solution**. In most cases, we need the ability to evolve the code. This means we must apply structure and make the solution understandable to ourselves and [others](https://rstraub.com/empathy-the-key-to-great-code). We introduce design to our software.

Following this insight, it makes sense to separate the activities. That is precisely what TDD helps with.

## TDD to Separate Concerns

At the core of TDD is [its mantra](https://www.codecademy.com/article/tdd-red-green-refactor): *red, green, refactor*. You go from one phase to the next in tiny [iterations](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html) on a scale of mere seconds or minutes. Each phase forces us to look at the problem "wearing a different hat."

- **Red** is where we express our understanding of the problem in a failing test, one piece at a time. We're fleshing out the problem piecemeal, [specifying behavior](https://rstraub.com/stop-testing-implementations) we want of the system. This is where we wear the tester hat.
- **Green** is where we crack our knuckles and let the keyboard sing. All we care about is solving that small piece of the puzzle we just captured our understanding of. It doesn't matter what the result looks like. We're just trying to get to the finish line - making the test pass. Simply put, we wear the hacker's smudgy baseball cap here.
- **Refactor** is where we zoom out and take the potential mess we made in the previous step and forge it into something we can work with. Here, we put on our proper engineering hat.

I like to explain the cycle like this: 
> first, *make sure we build the right thing*, then *build the thing*, and lastly, *build the thing right*.

![tdd separates cognitive load](/assets/images/tdd-cognitive-load.jpeg)
*‌Cognitive load is reduced by separating activities*

As you can see, these distinct phases have different goals. Instead of "juggling" all three concerns simultaneously, TDD strongly nudges us towards delineating them in a sequence of steps. It's like moving from keeping three balls in the air to just one while simply holding the remaining ones in hand.

## Conclusion

*Do you need TDD to do this?* 

Not necessarily, but like [I mentioned previously](https://rstraub.com/tdd-or-test-last-exploring-metaphors), TDD does nudge you in the right direction.

TDD can help to separate concerns in the act of programming. It has helped me do so, and made coding a more enjoyable experience in the process. It drastically lowered the [cognitive load](https://en.wikipedia.org/wiki/Cognitive_load) I had to deal with. TDD permanently changed how I see the act of programming - distinct concerns to cycle through.
