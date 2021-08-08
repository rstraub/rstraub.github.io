---
layout: post
title: "🔨 Maintainable tests with Test Data Builders"
author: Roy Straub
categories: [Tests]
tags: [Test Data Builders, Patterns, Test Driven Development]
image: assets/images/11-test-data-builders.jpg
description: "Maintainability of test code is just as important as it is for production code. Test Data Builders help make your tests easier to maintain. Learn about what Test Data Builders are and how they achieve this."
featured: true
hidden: true
comments: true
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

In the production code we adhere to the "[_Don't Repeat Yourself_](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)" principle, in testing this is often more difficult. You simply need variations of objects, which is why you create objects more often in tests than in production code. This leads to a _subtle form of duplication_: invoking constructors.

![tests coupled to different objects]({{ site.baseurl }}/assets/images/11-coupling-by-tests.svg)  
_Figure 1. Coupling in tests by creating objects_

This form of coupling has a negative effect on the maintainability of tests, but that's not the only thing we need to watch out for...

## 🗣️ The importance of expressive tests 

Readable code is important. Good developers understand that code is read more often than it is written, which is just as true for tests.

Tests help readers understand the behavior of code. This is why they serve as an effective form of documentation.

Unfortunately, this takes some effort. In order for tests to effectively explain the behavior of code, it is important that you separate main from side issue, but what is what in a test?

Easy. The most important thing in a test is the _what_ (the behavior), not the _how_ (the setup). In _listing 1_ you see an example of a non-expressive test, because the tested behavior is not separated from the test mechanism.

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

_Listing 1. Non-expressive test, intent is hidden by mechanism_

If these things aren't properly separated, a test won't tell you what's happening. This causes readers to take longer to comprehend it, or worse, they become afraid to change it.
Fortunately, it doesn't have to get that far, thanks to _Test Data Builders_.

## Wat zijn Test Data Builders 👷

[Test Data Builders](http://natpryce.com/articles/000714.html) zijn een vorm van het _[Builder Pattern](https://en.wikipedia.org/wiki/Builder_pattern)_, maar dan toegepast op het maken van objecten voor tests[^goosgt].
Deze builders maken objecten aan met veilige, logische default waarden.
Ze bieden, zoals de gewone builder, publieke _chainable_ methodes aan waarmee de objecten aangepast kunnen worden.

Dit pattern is niet altijd toepasbaar.
Het is effectief bij complexe objectstructuren, vooral voor _[Value Objects of Entities](https://www.martinfowler.com/bliki/EvansClassification.html)_.

Naast de voordelen zijn er toch nadelen.
Je moet deze builders zelf schrijven en onderhouden.
Er kunnen dus ook bugs in je builders ontstaan.
Ga niet gelijk overal builders voor maken, maar maak een afweging!

## Hoe Test Data Builders helpen ✨

Test Data Builders helpen je testcode meer te ontkoppelen van je productiecode en tegelijkertijd de expressiviteit ervan te verhogen.
Dat klinkt bijna als magie, maar zoals je straks zult zien, is het in essentie eenvoudig.

### Minder koppeling 🎊

Test Data Builders lossen het koppelingprobleem op door _constructie van objecten te encapsuleren_.
Je gebruikt de builder om objecten voor je test te maken, waardoor het aantal plekken waar dit gebeurt teruggebracht wordt.
Stel dat je een argument toevoegt, dan hoef je nu alleen nog maar code in de builder aan te passen!

![ontkoppel tests van productiecode met Test Data Builders]({{ site.baseurl }}/assets/images/11-decoupling-with-tdb.svg)  
_Fig 2. Test Data Builders ontkoppelen tests van de creatie van objecten_

### Verhoogde Expressiviteit 🎉

Het expressiviteitsprobleem wordt ook opgelost door Test Data Builders.
Doordat ze objecten aanmaken met veilige defaults hoef je alleen relevante waardes voor een test aan te passen.
Stel dat je één property wilt valideren, dan is dat de enige die je overschrijft bij het maken van het object, de rest doet er niet toe.
Op deze manier verminder je technische "clutter" en vertelt de test meer!
Vergelijk _listing 1_ maar eens met _listing 2_.

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

_Listing 2. Test Data Builders maken de intentie van een test duidelijker_

### Bonus: Test DSL 🎁

Een bijkomend voordeel is dat je met builder methodes meer kunt spreken in de termen van je domein.
Als je _listing 1_ met _listing 2_ vergelijkt dan zie je dat de builder methodes meer zeggen dan een constructoraanroep of het zetten van een property.
Benoem je de methodes van de builders goed, dan eindig je met een _[Domain Specific Language](https://www.martinfowler.com/bliki/DomainSpecificLanguage.html)_ voor je tests!

## Conclusie 📝

Tests zijn belangrijk voor een goede codebase, maar als ze niet onderhoudbaar zijn kunnen ze aanpassingen juist lastig maken.
Dit kan komen door **koppeling** in tests, of door tests die **niet expressief** zijn.

Test Data Builders bieden een oplossing voor beide problemen.
Ze maken het mogelijk om testdata grotendeels op één plek op te bouwen en voorkomen daarmee onnodige koppeling.
Daarnaast zorgen ze voor tests die duidelijker laten zien welk gedrag getest wordt.

Zoals met elk pattern moet je ook de nadelen meenemen in de overweging om ze toe te passen.
Doe je dit goed dan zullen ze je tests flexibeler en expressiever maken!

Denk de volgende keer bij het schrijven van een test dus aan deze effectieve oplossing.
Maak het jezelf en je team gemakkelijk!

_Wat zijn jouw ervaring met Test Data Builders? Zie jij nog andere voor- of nadelen? Deel het!_

## Referenties 🌐

[^goosgt]: Freeman, S., Pryce, N. (2009). Growing Object-Oriented Software, Guided by Tests (1st ed.). Addison-Wesley Professional.
[^refactoring]: Martin, F. (2018). Refactoring: Improving the Design of Existing Code (Addison-Wesley Signature Series (Fowler)) (2nd ed.). Addison-Wesley Professional.
