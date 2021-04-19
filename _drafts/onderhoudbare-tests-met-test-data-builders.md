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

## Het belang van onderhoudbaarheid van tests

Als developers snappen we het belang van tests: ze geven ons vertrouwen.
Tests stellen ons in staat om veilig te refactoren.

De meeste ontwikkelaars begrijpen het belang van onderhoudbare code.
Wat minder mensen weten is dat dit voor testcode net zo cruciaal is.
Wanneer onze tests niet onderhoudbaar zijn zal dit negatieve effecten op de productiecode hebben. Kortgezegd: 

_Tests met een slechte onderhoudbaarheid zullen leiden tot een niet onderhoudbare codebase._

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
*Koppeling door tests door het creëren van objecten*

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

<!-- TODO: code sample of unexpressive code -->

Als dit niet goed van elkaar gescheiden is, verteld een test niet wat er gebeurd.
Dit zorgt ervoor dat lezers langer bezig zijn het te begrijpen, of erger nog dat ze het niet durven aan te passen.

## Hoe Test Data Builders helpen

* intro
* wat zijn test data builders?
* pattern -> boek
* Builder pattern
* Sensible & safe defaults

![ontkoppel tests van productiecode met Test Data Builders]({{ site.baseurl }}/assets/images/11-decoupling-with-tdb.svg)  
*Test Data Builders ontkoppelen tests bij het creëren van objecten*


* Domain specific language -> expressiviteit

<!-- TODO: expressive code sample -->
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
