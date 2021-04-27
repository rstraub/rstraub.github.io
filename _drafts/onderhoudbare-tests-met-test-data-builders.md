---
layout: post
title:  "Hoe Test Data Builders onderhoudbaarheid van tests verbeteren 🔨"
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
Dat kan betekenen dat de tests niet onderhoudbaar zijn.
Leer hoe Test Data Builders hierbij helpen.

## Waarom onderhoudbaarheid van tests belangrijk is

Als developers snappen we het belang van tests: ze geven ons vertrouwen.
Tests stellen ons in staat om veilig te refactoren.

De meeste ontwikkelaars begrijpen het belang van onderhoudbare code.
Wat minder mensen weten is dat dit voor testcode net zo cruciaal is.
Wanneer onze tests niet onderhoudbaar zijn zal dit negatieve effecten hebben. Refactoren wordt dan lastiger, wat op den duur leidt tot slechtere productiecode.


![onderhoudbaarheid van tests en het effect op code kwaliteit]({{ site.baseurl }}/assets/images/11-test-maintenance-code-quality.svg)  
*Fig 1. Slechte onderhoudbaarheid van tests leidt tot slechtere productiecode*

Twee grote boosdoeners zijn:

1. Te veel **koppeling** door duplicatie in tests
1. Tests die **niet expressief** zijn

Laten we eens zien waarom deze aspecten invloed hebben op de onderhoudbaarheid van onze testcode.

## De pijn van te veel koppeling

Een goede developer begrijpt de waarde van refactoren.
Alleen door continu te refactoren blijft de codebase effectief.

_Test Driven Development_ (TDD) leert ons de harmonie tussen tests en refactoring.
Het één versterkt het ander, maar die relatie is niet altijd harmonieus...

Je hebt het vast meegemaakt.
Er moet iets aan de code worden aangepast en dat is zo gepiept.
Het probleem is dat je daarna uren bezig bent om tests aan te passen.

_Hoe kan dat?_

Tests zijn een vorm van _koppeling_.
Dit is niet gek, hoe kunnen we anders onze productiecode aanroepen?
Het probleem ontstaat wanneer we interfaces in onze code aanpassen.
Dit wordt op een pijnlijke manier duidelijk wanneer je bijvoorbeeld parameters aanpast.
Je moet alle tests aanpassen die deze code gebruiken.

In de productiecode houden we ons aan de "_Don't Repeat Yourself_" (DRY) regel, bij tests is dit vaak lastiger.
Je hebt nu eenmaal variaties van objecten nodig.
In de tests maken we veel vaker objecten aan dan in de productiecode.
Dit leidt tot een _subtiele vorm van duplicatie_, namelijk de aanroep van constructors.

![tests gekoppeld aan verschillende objecten]({{ site.baseurl }}/assets/images/11-coupling-by-tests.svg)  
*Fig 2. Koppeling vanuit tests door het creëren van objecten*

Deze koppeling in tests kunnen refactoring ontmoedigen.
Maar dat is niet het enige waar we op moeten letten om ze onderhoudbaar te houden...

## Het belang van expressieve tests

Leesbare code is belangrijk.
Goede developers begrijpen dat code vaker wordt gelezen dan geschreven.
Dit geldt net zo goed voor onze testcode.

Tests helpen lezers het gedrag van code te begrijpen.
Dit is waarom ze dienen als een effectieve vorm van documentatie.

Helaas kost dit, zoals zoveel in dit vakgebied, enige moeite.
Om tests het gedrag van code effectief uit te laten leggen is het belangrijk dat je hoofd van bijzaak scheidt. Maar wat is hoofd- en wat is bijzaak in een test?

Simpel. Het belangrijkste in een test is _wat_ je test (het gedrag), niet het _hoe_ (de opzet).

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
*Listing 1. Slecht leesbare test, de intentie wordt verborgen door het mechanisme*


<!-- TODO: code sample of unexpressive code -->

Als dit niet goed van elkaar gescheiden is, verteld een test niet wat er gebeurd.
Dit zorgt ervoor dat lezers langer bezig zijn het te begrijpen, of erger nog dat ze het niet durven aan te passen.
Gelukkig hoeft het niet zo ver te komen, dankzij _Test Data Builders_.

## Wat zijn Test Data Builders

Test Data Builders zijn een vorm van het _Builder Pattern_[^builder], maar dan toegepast op het maken van objecten ter gebruik in tests.
Deze vorm van builders wordt beschreven in het boek "Growing Object Oriented Software Guided by Tests", wat invloedrijk is in TDD-sferen.
<!-- TODO: expressive code sample -->

* intro
* wat zijn test data builders?
* pattern -> boek
* Builder pattern
* Sensible & safe defaults


* Domain specific language -> expressiviteit

## Hoe Test Data Builders helpen

Test Data Builders kunnen helpen om je testcode meer te ontkoppelen van je productiecode en tegelijkertijd de expressiviteit ervan te verhogen.
Dat klinkt bijna als magie, maar zoals je straks zult zien, is het in essentie eenvoudig.

Het probleem met koppeling lossen de Test Data Builders op door, net als andere "Creational Design Patterns", constructie van objecten te encapsuleren.
Je gebruikt dus de builder om een object in je test te maken.
Op deze manier breng je het aantal plekken terug waar constructors worden aangeroepen, wat voor minder problemen zorgt wanneer we die objecten refactoren.
Stel dat je een argument toevoegd, dan hoef je nu alleen nog maar code in de builder aan te passen!

![ontkoppel tests van productiecode met Test Data Builders]({{ site.baseurl }}/assets/images/11-decoupling-with-tdb.svg)  
*Fig 3. Test Data Builders ontkoppelen tests van de creatie van objecten*

Het tweede probleem lossen Test Data Builders ook elegant op.
Doordat ze objecten aanmaken met veilige defaults, hoef je met builder methodes, alleen relevante waardes voor je test te zetten.
Stel dat je alleen één property wilt valideren, dan is dat de enige die je overschrijft bij het maken van het object.
De rest doet er niet toe.
Zo wordt de technische "clutter" verminderd.

Een bijkomend voordeel is dat je met builder methods meer kunt spreken in de termen van je domein.
Als je figuur **X** en **Y** vergelijkt dan zie je dat een builder methode iets kan vertellen over de semantiek.
Een constructoraanroep of een property zetten kan dit veel minder.
Benoem je de methodes van de builders goed, dan eindig je met een zeer effectieve test _Domain Specific Language_.
De test zal dan precies vertellen wat er gebeurd!

**Fig.. code listing**
## Wanneer pas je Test Data Builders toe?

* Complexe setup -> geneste objecten, veel argumenten
* Voornamelijk voor Value Objects (data classes of records)

* Wanneer pas je Test Data Builders NIET toe?

* Net als elk pattern nadelen
* Meer code
* Potentieel bugs in de test data builders
* Eenvoudige setup
* Vaste, gelimiteerde set?
<!-- TODO: kan scherper -->

## Conclusie 📝

Tests zijn belangrijk voor een goede codebase.
Als ze niet goed worden geschreven kunnen ze aanpassingen aan de code juist lastig maken.
Dit kan komen door duplicatie of onduidelijke omschrijvingen in tests.

Test Data Builders bieden een oplossing voor beide problemen.
Ze maken het mogelijk om testdata grotendeels op één plek op te bouwen en voorkomen daarmee onnodige duplicatie.
Daarnaast zorgen ze voor tests die duidelijker laten zien wat er wordt gevalideerd.

Zoals met elk pattern moet je ook de nadelen meenemen in de overweging om ze toe te passen.
Doe je dit goed dan zullen ze testcode flexibeler en expressiever maken!

Denk de volgende keer bij het schrijven van een test dus aan deze effectieve oplossing.
Maak het jezelf en je team makkelijk!

_Wat zijn jouw ervaring met Test Data Builders? Zie jij nog andere voor- of nadelen? Deel het met ons!_
