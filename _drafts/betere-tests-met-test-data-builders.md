---
layout: post
title:  "Test Data Builders"
author: roy_straub
categories: [Tests]
tags: [Test Data Builders, Patterns, Test Driven Development]
image: assets/images/construction.jpg
description: "Test Data Builders"
featured: true
hidden: true
comments: false
---

Iets met builders.

### Twee grote valkuilen bij tests

1. Lastiger refactoren door duplicatie in tests
1. Nietszeggende tests

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

### Conclusie

* Tabel met voor en nadelen?
* Takeaways