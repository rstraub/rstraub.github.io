---
layout: post
title:  "Leesbare en flexibele tests met Test Data Builders 🔨"
author: roy_straub
categories: [Tests]
tags: [Test Data Builders, Patterns, Test Driven Development]
image: assets/images/11-hammer.jpg
description: "Test Data Builders"
featured: true
hidden: true
comments: false
---

Refactoren en daarna uren je tests aanpassen?
Geen idee bij wat een test precies doet?
Los het op met _Test Data Builders_!

### Twee grote valkuilen bij tests

1. Lastiger refactoren door duplicatie in tests
1. Nietszeggende tests

* post outline

### Waarom Test Data Builders helpen

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

### Wanneer pas je Test Data Builders NIET toe?

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
