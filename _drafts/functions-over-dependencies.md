
Recently I've noticed a shift in how I build systems. Instead of using dependencies and dependency injection I'm using functions. What are reasons for doing so? What consequences does it have? In this answer I'll lay out the answers.

## The Impact of Language

To answer all these questions I must first explain a little about my career path, especially which technologies and paradigms I encountered. Most of my career was spent in enterprise software—large codebases that have to stay around for a while. The systems i've worked on were built on the JVM and initially I used Java and Spring Boot exclusively. Later I also built a few systems in Kotlin, after which I worked a while on some Scala codebases.

I believe the languages themselves had a profound impact on how I build systems these days, and this is due to both a social and technical factor. Each language has its own idioms, and this tends to be reflected in the community and thus the people you work together with. For instance, many Java practitioners I encounter tend to favor dependencies and dependency injection frameworks for a big portion of the workload, whereas this was not the case with Scala users. The Scala users I encountered favored using Objects and plain functions where they could, and didn't even have a dependency injection framework in relatively large codebases. 

Technically languages play a large part in this as well. Some things are possible in one language, but not in the other. Others are easy and natural in one, but awful in another. Functions for instance are more natural to use in functionally inclined languages such as Scala, or even Kotlin. That is not to say Java cannot do it, but having to wrap a plain function in a class only to make it static is not, to me at least, an intuitive way to do so. It's just what you get used to after using that same language exclusively for a long time.

This is a big reason why I am a [proponent of learning different languages]({{site.baseurl}}/learning-programming-languages-with-exercism), preferably languages that are not so related.

## Why Favor Functions?

## When is Something a Dependency?

## Preconditions

## To answer

- Change in design of my systems
- Why i favor plain functions over dependencies and dependency injection
- Consequences:
	- Simplicity -> link to simple/complicated/simple
	- Less mocks in tests? can be good or bad
- When do you make a thing a dependency? When can it be a function?
	- action or calculation?
	- interchangeable or static?
- What would this look like in code?