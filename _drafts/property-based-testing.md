- Properties
- Generators
- Shrinking
## Research
### Comprehensive guide
https://dev.to/keploy/property-based-testing-a-comprehensive-guide-lc2 provides a global, but superficial overview

> Unlike traditional testing, which focuses on specific examples, PBT uses generalized properties to define expected behaviors, enabling the discovery of edge cases and unexpected issues.

### In praise of pbt
https://news.ycombinator.com/item?id=26680060 ->
https://increment.com/testing/in-praise-of-property-based-testing/ -> from the author of Hypothesis Python lib

> Example-based tests hinge on a single scenario. Property-based tests get to the root of software behavior across multiple parameters.

> We often treat our tests as specifications, but in reality they are stories.

> Shrinking, in particular, is one of the big benefits of using property-based testing libraries over fixture libraries with random generation.

To recap, adopting property-based testing will:
- Bridge the gap between what we claim to be testing and what we’re actually testing.
- Reveal the assumptions that we made during testing and development, and check if they are violated.
- Expose subtle inconsistencies in our code that would be hard to detect with example-based testing.

shrinking attempts to brings back a failing test to simpler params

- highlights where pbt shines and differs from traditional example based testing 
- AI summary
	- Property-based testing removes extraneous details, making tests cleaner and more robust by allowing unimportant details to vary.
	- Traditional example-based tests make stronger claims than they can demonstrate, while property-based tests express exact circumstances for expected passes. (AI summ)
	- Property-based testing focuses on generalizing scenarios to better specify software behavior and uncover bugs missed by traditional example-based testing.

### Moving from traditional to pbt
https://hypothesis.works/articles/incremental-property-based-testing/ -> how to move from traditional tests to pbt

### Beginners guide to pbt

https://www.thesoftwarelounge.com/the-beginners-guide-to-property-based-testing/
- some nice heuristics
### Books
https://pragprog.com/titles/fhproper/property-based-testing-with-proper-erlang-and-elixir/ book about the subject, going in more depth