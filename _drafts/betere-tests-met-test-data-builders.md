---
layout: post
title:  "Leesbare en flexibele tests met Test Data Builders 🔨"
author: roy_straub
categories: [Tests]
tags: [Test Data Builders, Patterns, Test Driven Development]
image: assets/images/11-hammer.jpg
description: "Hoe maak je tests flexibeler en beter te lezen door Test Data Builders toe te passen"
featured: true
hidden: true
comments: true
---

Refactoren en daarna uren je tests aanpassen?
Geen idee bij wat een test precies doet?
Los het op met _Test Data Builders_!

### Twee grote valkuilen bij tests

Als developers snappen we het belang van tests.
Ze geven ons vertrouwen.
Vertrouwen in dat onze code het juiste doet.

Goede tests schrijven is een hele kunst.
Het vereist oefening en moeite.
Tests maken die ons het leven makkelijk maken is een grote uitdaging.

Ik zoom dit keer in op twee problemen bij het bereiken hiervan:

1. Lastig **refactoren** door duplicatie in tests
1. Tests die niet **expressief** zijn

Daarna leg ik uit hoe je deze problemen op kunt lossen door het toepassen van Test Data Builders.

### Waarom tests refactoring tegen kunnen werken

### Hoe Test Data Builders helpen

* intro
* wat zijn test data builders?
* pattern -> boek
* Builder pattern
* Sensible & safe defaults
* Domain specific language -> expressiviteit

### Hoe pas je Test Data Builders toe

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

### Mijn ervaring?

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
