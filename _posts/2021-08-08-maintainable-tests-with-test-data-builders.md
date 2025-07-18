---
author: Roy Straub
categories:
- tech
comments: true
description: Maintainability of test code is just as important as it is for production
  code. Test Data Builders help make your tests easier to maintain. Learn about what
  Test Data Builders are and how they achieve this.
featured: false
hidden: false
image: assets/images/11-test-data-builders.jpg
layout: post
tags:
- testing
- maintainability
title: "Maintainable tests with Test Data Builders"
---

Refactoring and then spend hours changing your tests? Not sure what a test does? Test Data Builders to the rescue!

## 🧪 Tests and maintenance

Most developers understand the importance of tests: they provide confidence. Tests allow you to refactor safely[^refactoring].

These developers know that maintainable code is extremely important. Fewer people know that this is just as crucial for test code. If our tests are not maintainable, this will have negative effects. Refactoring becomes more difficult, which eventually leads to worse production code[^refactoring].

![what if i told you maintainability of tests matters]({{ site.baseurl }}/assets/images/11-maintainability-meme.jpg)

Two possible causes of poorly maintainable tests are:

1. Too much **coupling** due to duplication in tests.
1. Tests which are **non-expressive**.

Let's see why these aspects affect the maintainability of our test code.

## 🔗 The pain of coupling

You've probably experienced it: something needs to be changed in the code and that's done in no time. The problem is that you spend hours adjusting tests afterwards.

_How come?_

Tests are a form of _coupling_. They have to be, how else can we call our production code? The problem arises when we modify _signatures_ in our code, such as introducing an extra parameter.
The coupling then becomes painfully clear: you have to adjust all the tests that use that piece of code.

In the production code we adhere to the "[_Don't Repeat Yourself_](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)" principle, in testing this is often more difficult. You simply need variations of objects, which is why you create objects more often in tests than in production code. This leads to a _subtle form of duplication_: creating objects.

![tests coupled to different objects]({{ site.baseurl }}/assets/images/15-coupling-tests.png)  
_Figure 1. Coupling in tests by creating objects_

This form of coupling has a negative effect on the maintainability of tests, but that's not the only thing we need to watch out for...

## 🗣️ The importance of expressive tests 

Readable code is important. Good developers understand that code is read more often than it is written, which is just as true for tests.

Tests help readers understand the behavior of code. This is why they serve as an effective form of documentation.

Unfortunately, this takes some effort. In order for tests to effectively explain the behavior of code, it is important that you separate main from side issue, but what is what in a test?

Easy. The most important thing in a test is the _what_ (the behavior), not the _how_ (the mechanism). In _listing 1_ you see an example of a non-expressive test, because the tested behavior is not separated from the test mechanism.

```java
@Test
void an_unreadable_test() {
    Country country = new Country("USA", Currency.US_DOLLAR, Language.ENGLISH);
    Author author = new Author("Oscar Wilde", country);
    Novel novel = new Novel(
            "The picture of dorian gray",
            50.00,
            author,
            Language.ENGLISH,
            Lists.newArrayList(Genre.MYSTERY)
    );
    PurchasedBook book = new PurchasedBook(novel, 1);
    Invoice invoice = new Invoice("test", country);

    invoice.addPurchasedBook(book);

    assertEquals(56.35, invoice.computeTotalAmount());
}
```

_Listing 1. Non-expressive test; intent is hidden by mechanism_

If these things aren't properly separated, a test won't tell you what's happening. This causes readers to take longer to comprehend it, or worse, they become afraid to change it.
Fortunately, it doesn't have to get that far, thanks to _Test Data Builders_.

## 👷 What are Test Data Builders 

[Test Data Builders](http://natpryce.com/articles/000714.html) are a form of the _[Builder Pattern](https://en.wikipedia.org/wiki/Builder_pattern)_, but applied to creating objects for tests[^goosgt]. These builders create objects with safe, logical default values. Like the regular builder pattern, they offer public _chainable_ methods with which the objects can be modified.

This pattern is not always applicable. It is effective for creating complex object structures, especially for _[Value Objects or Entities](https://www.martinfowler.com/bliki/EvansClassification.html)_.

Besides the advantages, there are also disadvantages. You have to write and maintain these builders yourself, so bugs can arise in them. Do not immediately make builders for everything, but make a weighted decision!

## ✨ How Test Data Builders help

Test Data Builders help decouple your test code more from your production code while increasing its expressiveness. That almost sounds like magic, but as you'll see later, it's really not.

### 🎊 Decreased coupling

Test Data Builders solve the issue of coupling by encapsulating _construction of objects_. You use the builder to create objects for your test, reducing the number of places where this occurs.
Suppose you add an argument, then all you need to do now is modify code in the builder!

![decouple tests from production code with Test Data Builders]({{ site.baseurl }}/assets/images/15-decoupling-tests.png)  
_Figure 2. Test Data Builders (TDB) decouple tests from object creation_

### 🎉 Increased expressiveness

The problem of non-expressive tests is also solved by Test Data Builders. Because they create objects with safe defaults, you only have to adjust relevant values for a test. Let's say you want to validate one property, then that's the only one you override when creating the object, the rest doesn't matter. This way you reduce technical "clutter" and the test conveys more!
Compare _listing 1_ to _listing 2_ for example.

```java
@Test
void increased_readability_by_test_data_builder() {
    Invoice invoice =
        anInvoice()
            .from(USA)
            .with(
                aPurchasedBook().of(aNovel().costing(50.0))
            ).build();

    assertEquals(56.35, invoice.computeTotalAmount());
}
```

_Listing 2. Test Data Builders expose test intent_

### 🎁 Bonus: test DSL

An additional advantage is that builder methods allow you to speak more in terms of your domain. If you compare _listing 1_ to _listing 2_ you will see that the builder methods convey more than a constructor call or setting a property. If you name the methods of the builders well, you end up with a _[Domain Specific Language](https://www.martinfowler.com/bliki/DomainSpecificLanguage.html)_ for your tests!

## 📝 Wrapping up

Tests are important for a good codebase, but if they are not maintainable they can make changes difficult. This can be due to **coupling** in tests, or tests that are **non-expressive**.

Test Data Builders provide a solution to both problems. They make it possible to build test data largely in one place and thus prevent excessive coupling. In addition, they enable you to show the intent of tests better.

As with any pattern, you should also consider the drawbacks when considering using them. If you do this right, they will make your tests more maintainable and expressive!

So next time you write a test, remember this effective solution. Make it easy on yourself and your team!

_What is your experience with Test Data Builders? Do you see any other pros or cons? Let us know in the comments!_

## 📚 Bibliography

[^goosgt]: Freeman, S., Pryce, N. (2009). Growing Object-Oriented Software, Guided by Tests (1st ed.). Addison-Wesley Professional.
[^refactoring]: Martin, F. (2018). Refactoring: Improving the Design of Existing Code (Addison-Wesley Signature Series (Fowler)) (2nd ed.). Addison-Wesley Professional.