---
author: Roy Straub
categories:
- tech
description: Learn how Object-Oriented and Functional Programming stand apart, and more crucially how to make them coexist.
layout: post
tags:
- OOP
- FP
- software design
title: "Object-Oriented vs Functional Programming—Why Not Both?"
---

Good. Bad. Right. Wrong. This. That. People love [binary oppositions](https://en.wikipedia.org/wiki/Binary_opposition), and Software Engineering is full of them. One such opposition is the discussion of object-oriented vs functional programming. However, I’d argue it doesn’t have to be either/or. With care, we can have the best of both worlds, but to do so we need to understand the strengths and weaknesses of both paradigms.

## Object-Oriented Programming

[Object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming)(OOP) has been a mainstay ever since the 1970s and 1980s and remains a popular paradigm to this day, found in languages like Java, C#, Python, etc.

It sets itself apart by modeling your software as ‘objects’, which bring together data and possible interactions with it. A major aim is to hide the internals and expose them only via its functions.

The paradigm aligns well with our natural way of thinking in terms of things, or ‘objects.’ When we perceive the world around us we tend to classify things as objects—we see a large brown thing with leaves and categorize it as a tree. In programming, this works too, especially for rich domains. 

OOP has advantages and disadvantages. Like any tool, its effectiveness [depends](https://rstraub.com/it-depends) on how we employ it and in what context. Over the years, however, I’ve found OOP’s strengths to be as follows: 
- **Capturing natural concepts in code**. This is very useful in rich domains (such as the previous example), as it aligns well with our language and reasoning in objects and subjects. This is a major part of [Domain-Driven Design](https://martinfowler.com/bliki/DomainDrivenDesign.html), specifically [Ubiquitous Language](https://martinfowler.com/bliki/UbiquitousLanguage.html).
- **Bringing data and logic together**. Done well, this creates high [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)) (things that change together belong together), which makes change easier. It can also reduce [coupling](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29), which is perhaps the [biggest reason](https://tidyfirst.substack.com/p/surprise-factory-coupling-why-software) for making software hard to adapt. 
- **Hiding internals**. Functions that follow the [Tell, Don’t Ask principle](https://martinfowler.com/bliki/TellDontAsk.html), allow you to hide much of the internal complexities from the rest of the codebase.

However, there are also downsides:
- **‌Not everything is an object.** Real-world applications consist of more than object-like concepts such as processes. Having access to only Objects to model software might feel like putting a circle into a square hole.
- **Mutability.** Mutable state adds time as a dimension of complexity to the equation—what did an object look like at a specific point in time?
- **Side Effects.** Mutating state, as well as many other interactions interleaved in code makes the outcome of it dependent on *when* it is called. This makes it harder to reason about the program.
- **Verbosity.** When all you need is a function, wrestling it into an object form can result in more code than needed.

Let’s explore some Object-Oriented code. Imagine we’re creating software for train logistics. The code needs to couple and decouple train sets from an entire train. Here’s some object-oriented code to solve the problem:

```python
class Train:
    def __init__(self, composition):
        self.composition = composition

    def couple(self, train_set):
        self.composition.append(train_set)

    def decouple(self):
        self.composition.pop()

    def length(self):
        lengths = [train_set.length for train_set in self.composition]
        return sum(lengths)

    def weight(self):
        weights = [train_set.weight for train_set in self.composition]
        return sum(weights)


class TrainSet:
    def __init__(self, weight, length):
        self.weight = weight
        self.length = length
```

And we’d use it like this:

```python
def test_couple_increases_weight_length():
    train = Train([TrainSet(1000, 150)])

    train.couple(TrainSet(500, 75))

    assert train.weight() == 1000 + 500
    assert train.length() == 150 + 75
    assert len(train.composition) == 2


def test_decouple_decreases_weight_length_and_trainsets():
    train = Train([TrainSet(1000, 150), TrainSet(500, 75)])

    train.decouple()

    assert train.weight() == 1000
    assert train.length() == 150
    assert len(train.composition) == 1
```

Let’s analyze it. We express a train as a `Train` object with its composition as a property. Both `length` and `weight` can be calculated properties, which are preferable. It’s then quite natural to create interactions with that object, expressing them as `couple` and `decouple` a train set. Both affect the length, weight, and composition of the entire train. Consider this code sample our starting point for further comparison.

Functional programming has an entirely different philosophy, bringing with it a completely different set of advantages and disadvantages. Let’s see what those are.

## Functional Programming

[Functional programming](https://en.wikipedia.org/wiki/Functional_programming)(FP) is on the rise, despite its origins tracing back to the 1950s, and there are good reasons for that. Done well, FP can make codebases easier to grasp and less prone to complex bugs.

The [paradigm differs](https://www.geeksforgeeks.org/difference-between-functional-programming-and-object-oriented-programming/) from OOP in that it treats [functions as first-class citizens](https://en.wikipedia.org/wiki/First-class_function), emphasizes the use of functions, [immutability](https://en.wikipedia.org/wiki/Immutable_object) and isolating [side-effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science)). FP aligns well with calculations—inputs and outputs.

I’ve learned most about FP from the excellent book [Grokking Simplicity](https://grokkingsimplicity.com). A crucial perspective the author offers is that functional programming is all about identifying and separating *Actions, Calculations, and Data*.

- **Actions** depend on when they’re used, such as database queries, API calls, and reading files. 
- **Calculations** always give the same result given the same inputs—it doesn’t matter when you call them. 
- **Data** is inert and can be interpreted as is—usually describes some event. 

These **ACDs** of functional programming have permanently changed how I read and write code. They have caused me to be on the lookout for this distinction and pull them apart in code. 

Functional programming has a whole other set of benefits compared to OOP:
- **Natural fit for processing**. We tend to think of calculations more naturally as functions, which makes FP a good fit for processing data.
- **Simplicity by locality**. FP can simplify code by increasing its *locality*. Locality means ‘Can I understand this code without considering any other context?’ FP achieves this with immutability and isolating side effects. For instance, mutability forces you to consider who holds references to the same data, and both mutability and side effects force you to think on a temporal axis—when something is used.
- **Composability.** Pure functions compose exceptionally well, often surprising you with new ways of being useful. The Linux command line is a great example. Tools like `ls`, `grep`, and `sed`, are simple in isolation, but can form surprisingly powerful new combinations by chaining them together.
- **Testability.** Not having to deal with time as a dimension, as well as dealing with inputs and outputs makes testing functional code simple.

The downsides I’ve experienced are:
- **Functions are not our natural way of thinking,** especially not for concepts we see as ‘objects’ in real life. A Tree is neither a function nor data to me, but rather an object.
- **Operating upon data**, rather than the data and logic being self-contained. When done carelessly, this might decrease cohesion and increase coupling, making future changes to the code harder.
- **Effort up front, payoff later.** Code that adheres to the FP principles can be hard to design—it can feel counterintuitive. You need the state changed, but you have to out of your way to do so. You need to query a database here, why not do so where you need it? The effort is moved forward in the process. Once you’ve put in the effort, the code will remain easier to reason about, and easier to debug for the rest of its lifetime.
- **Learning curve**. FP is sometimes known for its steep learning curve, not helped by complex terminology such as Monads, Monoids, Applicatives, etc, originating from [Category Theory](https://en.wikipedia.org/wiki/Category_theory). These concepts obscure the essence of ideas, which are relatively simple at their core.

Time for some code—functional programming style. We’ll consider the same example as before: coupling and decoupling train sets on a train. 

```python
def couple_train(train, train_set):
    return train + (train_set,)


def decouple_train(train):
    return train[:-1]


def train_length(train):
    lengths = map(lambda train_set: train_set["length"], train)
    return sum(lengths)


def train_weight(train):
    weights = map(lambda train_set: train_set["weight"], train)
    return sum(weights)

```

And we’d use it as such:

```python
def test_couple_increases_weight_length_and_trainsets():
    train = ({"length": 150, "weight": 1000},)

    coupled = couple_train(train, {"length": 75, "weight": 500})

    assert train_length(coupled) == 150 + 75
    assert train_weight(coupled) == 1000 + 500
    assert len(coupled) == 2
    
def test_decouple_decreases_weight_length_and_trainsets():
    train = ({"length": 150, "weight": 1000}, {"length": 75, "weight": 500})

    decoupled = decouple_train(train)

    assert train_length(decoupled) == 150
    assert train_weight(decoupled) == 1000
    assert len(decoupled) == 1
```

Compared to the OOP example we’ve expressed the behavior as calculations operating on immutable data. For instance, instead of a mutable [list](https://docs.python.org/3/library/stdtypes.html#lists), we’ve used a [tuple](https://docs.python.org/3/library/stdtypes.html#tuples) instead. Another crucial difference is found in the usage of the code: we assign results of functions to new variables `coupled` and `decoupled`. No more mutating state in place. We win in predictability, but we lose the clearly expressed concepts.

Could we do better? I believe so, but first, we should consider how we look at programming paradigms.

## The Toolbox

There always seems to be discussion around ‘which paradigm is best’ or ‘why this paradigm is better than that one.’ But what if we look at it differently? Time to break the binary opposition.

Imagine your skillset as a software engineer as a toolbox. Every skill is neatly stored in one of its drawers. Now, let’s say that you’re handed a new screwdriver. Instead of throwing out your other tools, you would let them coexist and pick the appropriate tool for the job. Sometimes using them together to get a job done neither one could have achieved alone.

Each paradigm is an addition to your toolbox, not a replacement. This is why [I advocate exploring different languages](https://rstraub.com/learning-programming-languages-with-exercism). As we’ve seen, each paradigm has its advantages and disadvantages, and each shines in different situations. Adding a tool to our collection makes us more flexible and enables us to synthesize entirely new things out of their coexistence.

More and more languages are becoming multi-paradigm, supporting different paradigms to varying degrees. Individual languages will lean more towards one or the other. For instance Scala—by default—is more functionally inclined than Java. A language being multi-paradigm can be likened to a language giving you a bigger toolbox to choose from. You can leverage FP for data processing, and OOP for rich domain modeling and join the two to get the best of both worlds. 

What would a union of the best of both worlds look like to me? 
- **Rich Domain Modeling** in the application’s core.
- **Objects for concepts, functions for processing**
- **Immutability as the default**
- **Isolation of side effects**, sometimes referred to as ‘pushing side effects to the edge of the world’.

We can model software using objects but still encourage locality by making them immutable and side-effect-free. Functional Object-Oriented Programming (FOOP?):

```python
@dataclass(frozen=True)
class TrainSet:
    weight: int
    length: int


@dataclass(frozen=True)
class Train:
    composition: tuple[TrainSet, ...]

    def couple(self, train_set):
        return Train(self.composition + (train_set,))

    def decouple(self):
        return Train(self.composition[:-1])

    def length(self):
        lengths = map(lambda ts: ts.length, self.composition)
        return sum(lengths)

    def weight(self):
        weights = map(lambda ts: ts.weight, self.composition)
        return sum(weights)
```

Used like this:

```python
def test_couple_increases_weight_length():
    train = Train(
        (TrainSet(1000, 150),)
    )

    coupled = train.couple(TrainSet(500, 75))

    assert coupled.weight() == 1000 + 500
    assert coupled.length() == 150 + 75
    assert len(coupled.composition) == 2


def test_decouple_decreases_weight_length_and_trainsets():
    train = Train((TrainSet(1000, 150), TrainSet(500, 75)))

    decoupled = train.decouple()

    assert decoupled.weight() == 1000
    assert decoupled.length() == 150
    assert len(decoupled.composition) == 1
```

Comparing this solution to the OOP and FP example, we’ve hit upon the Goldilocks zone for a problem like this. [Frozen data classes](https://docs.python.org/3/library/dataclasses.html) make the objects immutable after creation, making them easy to reason about, whilst clearly capturing the concepts of `Train` and `TrainSet`. We compute new states by returning new `Train` instances from `couple` and `decouple`. This changes the interaction for client code, as now `Train` is returned from those methods.

This happens to be the programming style I gravitate towards in programming languages supporting both OOP and FP. At least for the core of non-trivial programs solving complex domain problems.

Concluding we can see that no tool is inherently good or bad. Good code can be written in any language or paradigm, but the same holds for the inverse. In the end, it isn’t the tool that decides the outcome. That responsibility lies with the one who wields it.

## Summary

As much as we’d like reality to be black and white, it is more nuanced than that. In this case that turns out to be a great outcome: 

*We don’t have to choose either Object-Oriented Programming or Functional Programming. We can have the best of both.* 

Used well together, these paradigms allow you to synthesize something better than either one could have done by itself. The sum of the whole is greater than its parts.

*The code samples are available on [Github](https://github.com/rstraub/codecraftr-samples/tree/main/python/samples/functional_vs_oop).*
