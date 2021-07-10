---
layout: post
title: "Improving Software Design with Role Interfaces ☕"
author: Roy Straub
categories: [Design]
tags: [Role Interface, Encapsulation, SOLID, Object Oriented Programming, Test Driven Development]
image: assets/images/14-coffeemaker.jpg
description: "Role Interfaces offer a different perspective on the Interface in Object Oriented Software. Learn what this type of Interface is about, how it differs from the traditional Header Interface and what benefits they give you."
featured: true
hidden: true
comments: true
---

Role Interfaces offer a different perspective on the Interface in OOP.
Learn what benefits this type of Interface can bring your software design.

## The purpose of the Interface 🧰

The *Interface*, a very important tool in the toolbox of every Object Oriented Programmer.
Most programmers will be familiar with it, but I recently learned to look at them in a whole new way...

Let's first have a look at what I refer to as the "traditional way" of using interfaces.

Interfaces, as we know, are powerful concepts which allow programmers to *abstract* and *encapsulate*.
You use them to define some behaviour any implementor will have to offer.
The way it is implemented is left up to the implementor to decide.

Another way to put this is that an Interface defines the **what**, not the **how**.
This generally translates to an "[Acts Like](https://www.cs.utah.edu/~germain/PPS/Topics/interfaces.html)" type of relationship between the implementor and its Interface, which brings us to the traditional view as a "Header Interface".

## The traditional view: Header Interface 🤵‍♂️

Martin fowler defines the traditional view I had of interfaces as a *[Header Interface](https://martinfowler.com/bliki/HeaderInterface.html)*.
A Header Interface is an interface which defines all public behaviour of a class.
Let's have a look at an example.

![coffeemaker]({{ site.baseurl }}/assets/images/14-fancy-coffee-machine.jpg)
> A coffeemaker

Say that we are building a Software System for brewing coffee.
Part of our model is the coffeemaker. 
A coffeemaker should be able to:

* Boil water
* Grind beans
* Brew coffee
* Froth milk

A Header Interface for this would like something like fig 1:

![header interface]({{ site.baseurl }}/assets/images/14-header-interface.svg)  
*fig 1. Coffeemaker as a Header Interface*

This interface defines all public methods of a coffeemaker, a typical Header Interface.
I was used to applying Interfaces this way, for instance to adhere to the [Dependency Inversion Principle](https://stackify.com/dependency-inversion-principle/),
a common example being a [Repository](https://martinfowler.com/eaaCatalog/repository.html) or [Data Access Object](https://www.oracle.com/java/technologies/data-access-object.html).

Recently though, I have learned about using Interfaces to define (and abstract) roles in systems, with the so-called *Role Interface*.

## A different view: Role Interface 🧑‍🎤

A Role Interface abstracts and defines a specific role objects can fulfill in a system.
The language construct is exactly the same, the difference resides in the *semantics*.
As we've seen a Header Interface abstracts the entire public behaviour of some object, whereas a Role Interface only abstracts some cohesive methods belonging to a role.

Fundamental to this type of interface is the difference between objects and roles.
A role does not have to be fulfilled by a single object, nor does an object have to fulfill just one role.
This shifts the interface more towards a specific interaction a consumer and supplier have.

Sounds a bit fuzzy right?
Let's revisit our coffeemaker example.
Previously we extracted one interface (`CoffeeMaker`) defining all public behaviour.
If we adapt this to Role Interfaces we end up with fig 2:

![role interfaces]({{ site.baseurl }}/assets/images/14-role-interfaces.svg)  
*fig 2. Role Interfaces for the coffeemaker model*

You end up with more interfaces this way, but why bother?
Time to see what advantages this approach can bring.

## Advantages of the Role Interface 👍

Thankfully the advantages of the Role Interface are plentiful.
Amongst others, they give you:

* explicit roles in the model
* simpler consumer code
* increased flexibility

### Explicit Roles 🗣️

Defining interfaces for roles forces you to come up with a name to describe it.
I have found that shifting your perspective to think in roles causes you to think about the model differently, which can lead to deeper insights.

As a [Domain Driven Design](https://martinfowler.com/bliki/DomainDrivenDesign.html) proponent I recognize this as an opportunity to deepen domain knowledge and enrich the [Ubiquitous Language](https://martinfowler.com/bliki/UbiquitousLanguage.html).
To top it off explicit roles make the model more granular, which can aid in its comprehensibility.

### Unburden Consumers 😀

Ever hit the Intellisense shortcut in your IDE and felt overwhelmed?
This can indicate a violation of the [Interface Segregation Principle](https://stackify.com/interface-segregation-principle/).
Ideally a suppliers code should offer *precisely* what consuming code needs. No more, no less.

Role Interfaces are a perfect fit for upholding this principle.
Using them you can offer *fine-grained*, *cohesive* interfaces which prevent clients from being overwhelmed. 
They won't have to figure out what to use, and what not to use.
It can potentially reduce unwanted coupling too, since clients don't have to know more than they should.

### Increased Flexibility 🤸

I mentioned earlier that objects do not have to fulfill just one role or that a role should map to just one object.
This is the source of increased flexibility when using Role Interfaces.
They make it possible to shift the responsibility of who fulfills a specific role extremely easy.
Consuming code does not need to change if they talk to the interface instead of the implementor.

Looking at the coffeemaker example, the Role Interfaces make the model much more flexible.
Expressing the role of `Grinder` for instance allows the model to cope with both integrated and external bean grinders easily.

![external bean grinder]({{ site.baseurl }}/assets/images/14-bean-grinder.jpg)
> Who fulfills a role can easily be changed with Role Interfaces

When applied correctly this approach provides better cohesion than Header Interfaces.
They enable you to define a more specific *axis of change*, which in turn simplifies maintenance.
This is due to the fact that the concepts encapsulated by the roles should change for different reasons.

As always though not all is sunshine and rainbows.
Let's have a look at some disadvantages of Role Interfaces.

## Disadvantages of the Role Interface 👎

As with any solution there are consequences of using it.
The Role Interface is no exception, some of its downsides are:

* they are hard to define
* they give an extra layer of indirection
* level of granularity is hard to get right

### Hard to define 🤔

Role Interfaces are hard to get right.
In general, they express concepts which are more abstract than a class, or a Header Interface.
You need to truly understand the domain you are working in to give them an appropriate name and *express its intent effectively*.

Don't expect to get this type of abstractions right the first time.
Take advantage of working in an Agile way and incrementally improve on your model.
As you learn more about it getting the definition right will become easier.

### Level of Granularity ⚖️

Not just naming this type of interface is hard, getting the *granularity* right is also a challenge.
Just like coffee beans, we want the coarseness to be just right.
Get the grind too fine-grained or coarse and the [taste will be subpar](https://goodcoffeeplace.com/size-matters-fine-ground-vs-coarse-ground-coffee/).

![granularity is important]({{ site.baseurl }}/assets/images/14-granularity.jpg)
> The granularity of Role Interfaces should be just right

If you define Role Interfaces too fine-grained you end up with incohesive interfaces, which don't tell the whole story and make change harder.
Make them too coarse, and you risk losing the benefits of the Role Interface.

### Extra Indirection 🤯

Interfaces always give you the *cognitive overhead* of extra indirection, and the Role Interface is no exception.
If you overapply them you could end up with a nonsensical mess where you follow a trail of interfaces before finally finding an implementation.
You don't want to overwhelm or confuse readers of the code.

Always ask yourself if the tradeoff is worth it.
If you require multiple implementations the tradeoff is easy to make, though it can be worth the trouble even for one implementation.
This might be the case if the role you define makes the model more explicit or abstracts a cohesive concept.

![interface all the things]({{ site.baseurl }}/assets/images/14-all-the-things.jpg)
> Don't be like this

It is up to you to weigh the benefits and drawbacks of this solution, that's the fun part though!

## Conclusion 📝

Interfaces are the *bread and butter* of a good Object Oriented Programmer.
They encapsulate details, removing the burden from their clients.

Most interfaces a developer encounters in the wild resemble _Header Interfaces_.
The _Role Interface_ offers a different take on the interface, defining a clear collaboration between suppliers and consumers.

If you can mitigate some of its downsides the Role Interface will reward you handsomely.
They can make your Domain Model more **expressive**, **simplify clients** and make **refactoring easier**.

So dear Object Oriented Programmer, don't hesitate to use interfaces more often.
Role Interfaces can make all the difference!
