---
layout: post
title: "Betere tests met Test Data Builders 🔨"
author: Roy Straub
categories: [Tests]
tags: [Test Data Builders, Patterns, Test Driven Development]
image: assets/images/11-test-data-builders.jpg
description: "Onderhoudbaarheid van tests is net zo belangrijk als bij productiecode. Dit is niet eenvoudig, maar Test Data Builders helpen hierbij. Leer over wat Test Data Builders zijn en welke problemen ze oplossen."
featured: true
hidden: true
comments: true
---

Refactoren en daarna uren je tests aanpassen?
Geen idee wat een test doet?
Los het op met Test Data Builders!

## Tests en onderhoudbaarheid 🧪

De meeste developers snappen het belang van tests: ze geven vertrouwen.
Tests stellen je in staat om veilig te refactoren[^refactoring].

Deze zelfde ontwikkelaars weten dat onderhoudbare code enorm belangrijk is.
Wat minder mensen weten is dat dit voor testcode net zo cruciaal is.
Wanneer onze tests niet onderhoudbaar zijn zal dit negatieve effecten hebben. Refactoren wordt dan lastiger, wat op den duur leidt tot slechtere productiecode[^refactoring].

Twee mogelijke oorzaken van slecht onderhoudbare tests zijn:

1. Te veel **koppeling** door duplicatie in tests
1. Tests die **niet expressief** zijn

Laten we eens zien waarom deze aspecten invloed hebben op de onderhoudbaarheid van onze testcode.

## De pijn van te veel koppeling 🔗

Je hebt het vast meegemaakt, er moet iets aan de code worden aangepast en dat is zo gepiept.
Het probleem is dat je daarna uren bezig bent om tests aan te passen.

_Hoe kan dat?_

Tests zijn een vorm van _koppeling_.
Dat moet ook wel, hoe kunnen we anders onze productiecode aanroepen?
Het probleem ontstaat wanneer we _signatures_ in onze code aanpassen, zoals het introduceren van een extra parameter.
De koppeling wordt dan op een pijnlijke manier duidelijk, alle tests die dat stuk code gebruikten moet je aanpassen...

In de productiecode houden we ons aan het "[_Don't Repeat Yourself_](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)" principe, bij tests is dit vaak lastiger.
Je hebt nu bijvoorbeeld variaties van objecten nodig, waardoor je in tests vaker objecten maakt dan in de productiecode.
Dit leidt tot een _subtiele vorm van duplicatie_, namelijk de aanroep van constructors.

![tests gekoppeld aan verschillende objecten]({{ site.baseurl }}/assets/images/11-coupling-by-tests.svg)  
_Fig 2. Koppeling vanuit tests door het creëren van objecten_

Deze vorm van koppeling heeft een negatief effect op de onderhoudbaarheid van tests, maar dat is niet het enige waar we op moeten letten...

## Het belang van expressieve tests 🗣️

Leesbare code is belangrijk.
Goede developers begrijpen dat code vaker wordt gelezen dan geschreven.
Dit geldt net zo goed voor onze testcode.

Tests helpen lezers het gedrag van code te begrijpen.
Dit is waarom ze dienen als een effectieve vorm van documentatie.

Helaas kost dit, zoals zoveel in dit vakgebied, enige moeite.
Om tests het gedrag van code effectief uit te laten leggen is het belangrijk dat je hoofd van bijzaak scheidt, maar wat is hoofd- en wat is bijzaak in een test?

Simpel. Het belangrijkste in een test is _wat_ je test (het gedrag), niet het _hoe_ (de opzet).
In _listing 1_ zie je een voorbeeld van een niet-expressieve test, doordat het geteste gedrag niet van de testopzet is gescheiden.

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

_Listing 1. Slecht leesbare test, de intentie wordt verborgen door het mechanisme_

Als deze zaken niet goed van elkaar gescheiden zijn vertelt een test niet wat er gebeurd.
Dit zorgt ervoor dat lezers langer bezig zijn het te begrijpen, of erger nog dat ze het niet durven aan te passen.
Gelukkig hoeft het niet zo ver te komen, dankzij _Test Data Builders_.

## Wat zijn Test Data Builders 👷

Test Data Builders zijn een vorm van het _[Builder Pattern](https://en.wikipedia.org/wiki/Builder_pattern)_, maar dan toegepast op het maken van objecten voor tests[^goosgt].
Deze builders maken objecten aan met veilige, logische default waarden.
Ze bieden, zoals de gewone builder, publieke _chainable_ methodes aan waarmee de objecten aangepast kunnen worden.

Dit pattern heeft, zoals alle patterns, gevallen waar het wel en niet toepasbaar is.
Het is effectief bij complexe objectstructuren, vooral voor _[Value Objects of Entities](https://www.martinfowler.com/bliki/EvansClassification.html)_.

Verder zijn er, naast de genoemde voordelen, ook nadelen.
Je moet deze builders zelf schrijven en onderhouden, er kunnen dus ook bugs in je builders ontstaan.
Ga dus niet gelijk voor alles builders maken, maar maak een afweging!

## Hoe Test Data Builders helpen ✨

Test Data Builders helpen je testcode meer te ontkoppelen van je productiecode en tegelijkertijd de expressiviteit ervan te verhogen.
Dat klinkt bijna als magie, maar zoals je straks zult zien, is het in essentie eenvoudig.

### Minder koppeling 🎊

Test Data Builders lossen het koppelingprobleem op door _constructie van objecten te encapsuleren_.
Je gebruikt de builder om objecten voor je test te maken, waardoor je het aantal plekken waar objecten worden gemaakt terugbrengt.
Stel dat je een argument toevoegt, dan hoef je nu alleen nog maar code in de builder aan te passen!

![ontkoppel tests van productiecode met Test Data Builders]({{ site.baseurl }}/assets/images/11-decoupling-with-tdb.svg)  
_Fig 3. Test Data Builders ontkoppelen tests van de creatie van objecten_

### Verhoogde Expressiviteit 🎉

Het expressiviteitsprobleem wordt ook opgelost door Test Data Builders.
Doordat ze objecten aanmaken met veilige defaults hoef je alleen relevante waardes voor een test te overschrijven.
Stel dat je alleen één property wilt valideren, dan is dat de enige die je overschrijft bij het maken van het object, de rest doet er niet toe.
Op deze manier wordt de technische "clutter" verminderd en vertel je meer met je test!
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

_Listing 2. Test Data Builders helpen de intentie van een test te verduidelijken_

### Bonus: Test DSL 🪅

Een bijkomend voordeel is dat je met builder methods meer kunt spreken in de termen van je domein.
Als je _listing 1_ met _listing 2_ vergelijkt dan zie je dat de builder methode meer zeggen dan een constructoraanroep of het zetten van een property.
Benoem je de methodes van de builders goed, dan eindig je met een _[Domain Specific Language](https://www.martinfowler.com/bliki/DomainSpecificLanguage.html)_ voor je tests!

## Conclusie 📝

Tests zijn belangrijk voor een goede codebase, maar als ze niet onderhoudbaar zijn kunnen ze aanpassingen aan de code juist lastig maken.
Dit kan komen door **koppeling** in tests, of door tests die **niet expressief** zijn.

Test Data Builders bieden een oplossing voor beide problemen.
Ze maken het mogelijk om testdata grotendeels op één plek op te bouwen en voorkomen daarmee onnodige koppeling.
Daarnaast zorgen ze voor tests die duidelijker laten zien welk gedrag getest wordt.

Zoals met elk pattern moet je ook de nadelen meenemen in de overweging om ze toe te passen, doe je dit goed dan zullen ze je tests flexibeler en expressiever maken!

Denk de volgende keer bij het schrijven van een test dus aan deze effectieve oplossing.
Maak het jezelf en je team gemakkelijk!

_Wat zijn jouw ervaring met Test Data Builders? Zie jij nog andere voor- of nadelen? Deel het!_

## Referenties 🌐

[^goosgt]: Freeman, S., Pryce, N. (2009). Growing Object-Oriented Software, Guided by Tests (1st ed.). Addison-Wesley Professional.
[^refactoring]: Martin, F. (2018). Refactoring: Improving the Design of Existing Code (Addison-Wesley Signature Series (Fowler)) (2nd ed.). Addison-Wesley Professional.
