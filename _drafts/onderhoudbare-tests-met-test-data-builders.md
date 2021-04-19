---
layout: post
title:  "Hoe Test Data Builders onderhoudbaarheid van tests verbeteren 🔨"
author: Roy Straub
categories: [Tests]
tags: [Test Data Builders, Patterns, Test Driven Development]
image: assets/images/11-hammer.jpg
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
Hij ziet het als een manier om de code te blijven verbeteren.

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

<!-- TODO graphic -->

In de productiecode houden we ons aan de "_Don't Repeat Yourself_" (DRY) regel, bij tests is dit vaak lastiger.
Je hebt nu eenmaal variaties van objecten nodig.
In de tests maken we veel vaker objecten aan dan in de productiecode.
Dit leidt tot een _subtiele vorm van duplicatie_, namelijk de aanroep van constructors.

Tests kunnen refactoring tegenwerken doordat we te veel koppeling introduceren met duplicatie in onze tests.

## Het gevaar van nietszeggende tests

Leesbare code is belangrijk.
Goede developers begrijpen dat code vaker wordt gelezen dan geschreven.
Dit geldt net zo goed voor onze testcode.

Één van de voordelen van tests is dat ze kunnen dienen als documentatie.
Ze beschrijven wat het gedrag is van onze code.

Om tests als effectieve documentatie te laten werken is het belangrijk dat we hoofd van bijzaak scheiden.
Dit wordt vaak de "_Signal to noise_" ratio genoemd.
We willen veel vertellen met weinig ruis.

Onze tests zijn geschreven met de constructen van de programmeertaal.
Als we geen extra stappen zetten leidt dit tot enorm veel ruis.

Een voorbeeld hiervan is de setup van een test.
Je moet objecten maken en state goedzetten om een bepaald scenario na te bootsen.
Maar al die technische zaken leiden ons af van de hoofdzaak:
wat de productiecode moet doen onder welke omstandigheden.

Als we de hoofd- en bijzaken niet goed van elkaar scheiden krijgen we tests die niet duidelijk aangeven wat er precies wordt getest.
Je ziet dan niet wat belangrijk is en wat niet.
Erger nog de test vertelt je niet meer hoe de code zich zou moeten gedragen.

## Hoe Test Data Builders helpen

* intro
* wat zijn test data builders?
* pattern -> boek
* Builder pattern
* Sensible & safe defaults
* Domain specific language -> expressiviteit

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
