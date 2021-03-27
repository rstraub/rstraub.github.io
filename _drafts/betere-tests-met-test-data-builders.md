---
layout: post
title:  "Hoe Test Data Builders tests leesbaar en flexibel maken 🔨"
author: roy_straub
categories: [Tests]
tags: [Test Data Builders, Patterns, Test Driven Development]
image: assets/images/11-hammer.jpg
description: "Ik leg in deze blog uit wat Test Data Builders zijn. Daarnaast vertel ik hoe deze je tests flexibeler en leesbaarder maken."
featured: true
hidden: true
comments: true
---

Refactoren en daarna uren je tests aanpassen?
Geen idee bij wat een test precies doet?
In deze eerste blog over Test Data Builders leg ik uit waarom deze ons helpen bij het oplossen van deze problemen. 

### Twee grote valkuilen bij tests

Als developers snappen we het belang van tests.
Ze geven ons vertrouwen.
Vertrouwen dat onze code het juiste doet.

Goede tests schrijven is een hele kunst.
Het vereist oefening en moeite.
Tests opstellen die ons het leven makkelijk maken is een grote uitdaging.

Ik zoom dit keer in op twee problemen bij het bereiken hiervan:

1. Lastig **refactoren** door duplicatie in tests
1. Tests die niet **expressief** zijn

Daarna leg ik uit hoe je deze problemen worden opgelost door _Test Data Builders_.

In het volgende blog in deze serie zal ik stap voor stap laten zien hoe je Test Data Builders toepast.

### Wanneer tests refactoring tegenwerken

Een goede developer begrijpt de waarde van refactoren.
Hij ziet het als een manier om de code te blijven verbeteren.

_Test Driven Development_ (TDD) leert ons de harmonie tussen tests en refactoring.
Het één versterkt het ander.
De praktijk leert ons dat het soms ook andersom is.

Je hebt het vast meegemaakt.
Er moet iets aan de code worden aangepast en dat is zo gepiept.
Het probleem is dat je daarna uren bezig bent alle tests weer werkend te krijgen.

_Hoe kan dat?_

Tests zijn een vorm van _koppeling_.
Dat is logisch en de bedoeling.
Hoe kunnen we er anders onze productiecode mee valideren?

Het probleem ontstaat wanneer we _signatures_ in onze productiecode aanpassen.
Als we bijvoorbeeld parameters veranderen voor methodes of constructors wordt dit op een pijnlijke manier duidelijk.
We moeten dan alle tests langs die deze code gebruiken.

In de productiecode houden we ons aan de "_Don't Repeat Yourself_" (DRY) regel.
Voor tests is dit vaak lastiger.
We moeten variaties van objecten maken.
Voor elk testgeval roepen we methodes aan.
Dat klinkt meer als "_Write everything twice_" (WET) code.

Tests kunnen refactoring dus tegenwerken doordat we te veel koppeling introduceren met duplicatie in onze tests.

### Het gevaar van nietszeggende tests

### Hoe Test Data Builders helpen

* intro
* wat zijn test data builders?
* pattern -> boek
* Builder pattern
* Sensible & safe defaults
* Domain specific language -> expressiviteit

### Hoe pas je Test Data Builders toe (losse blog?)

1. Het beginpunt
1. Maak tests data builders builders
1. Verberg de mechaniek
1. Creëer builders met factory methods
1. Verminder duplicatie voor overeenkomstige objecten
1. Definiëer test constants voor veelvoorkomende objecten
1. Bonus: Test Data Builders & Kotlin DSL's = 😍

### Wanneer pas je Test Data Builders toe?

* Complexe setup -> geneste objecten, veel argumenten
* Voornamelijk voor Value Objects (data classes of records)

* Wanneer pas je Test Data Builders NIET toe?

* Net als elk pattern nadelen
* Meer code
* Potentieel bugs in de test data builders
* Eenvoudige setup
* Vaste, gelimiteerde set?
<!-- TODO: kan scherper -->

### Conclusie 📝

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
