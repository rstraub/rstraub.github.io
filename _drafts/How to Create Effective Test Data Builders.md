# How to Create Effective Test Data Builders

## Test Data Builders don't build themselves

A while ago I wrote about the [Test Data Builder (TDB) pattern](https://www.codecraftr.nl/maintainable-tests-with-test-data-builders/), and how it can improve the readability and maintainability of your test code. This provided a nice introduction into the topic, but there is still much to discuss, hence this post.

To delve into the topic of Test Data Builders a bit deeper, this post, together with the previous one, will be part of a series. This time we'll take a look at how to actually create the Test Data Builders in ways that maximize their effectiveness. Unfortunately they don't build themselves!

## An Example... From the Books

Let's take a bit of a hands-on approach and gradually improve on some tests in desperate need for some improvement. 

Imagine we're tasked with developing software for a library system. As part of a new feature request, we need to determine the correct cost of membership. This demands some explanation.

`Memberships` can be of different tiers:
- `Casual`
- `Regular`
- `Ultimate`

These tiers determine the amount of material a `Member` is allowed to loan, and is part of what determines the price of membership.

Members have a Membership, and some characteristics of the `Person` who owns the membership. A notable characteristic for our example is their `Age`, as both elderly (65+) and children (<18) get a notable discount. Isn't that nice!

So, now that you know enough about the (fictional) feature we're supposed to build, let's look at some code.

## A Test in Dire Need of Improvement

As I explained in an [earlier post](https://www.codecraftr.nl/why-use-tdd/), one of the best ways to get to a great result is by using our tests to drive the implementation. A first take on a test for calculating membership cost for an adult with a regular membership might look like this:

Listing 1. First iteration on membership cost calculation test

What do you see here? That's right, it's hard to make out the essence of the test. A big chunk of the code is creating the objects, distracting us from the story the test is telling us: how cost for membership is calculated.

There's some work to be done here. 

## A Side-by-Side Comparison

## Analyzing the Builder Code

## Conclusion

In this second part of the Test Data Builder series, we looked at how to create effective Test Data Builders.

First, you create a builder for the objects you need in your tests, followed by initializing the builder with safe defaults. After doing that we can optimize them for readability by making builders composable and creating some static factory methods.

The result should be test code that is stripped down to its bare essentials, clearly conveying the story it's telling to its readers. The only code left in the test should be essential to the test case itself!

Join me in the next installment, when we look in detail how to use Test Data Builders to write amazing test code.