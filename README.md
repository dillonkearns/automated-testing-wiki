# Automated Testing Wiki
## Purpose
This is a collection of notes and resources on testing conventions, techniques, and styles that improve the value and maintainability of automated tests. Contributions are welcome! You can also fork this to use as a "style-guide" for your project's tests.

This guide strives to be opinionated, but sensible and reasonably uncontroversial. That is, any suggestions given here are backed by an explanation of how they add to tests' value and/or maintainability (please open a pull request if that's not the case!). It is language agnostic, and uses ruby syntax since it reads like pseudocode.

## Describing Test Cases

### Don't repeat inputs and expected outputs in test descriptions
Rather than describe the implementation, tell a story in the language of the domain. This reduces noise, decouples your test description from its implementation, and encourages thinking at a higher level of abstraction.

```ruby
# avoid
it 'returns true for ""'

# prefer
it 'identifies the empty string as a palindrome'
```

### Strive to find (or create) domain language to describe scenarios expressively
For example, the cases for leap years can be described as typical leap years, typical common years, atypical leap years, and atypical common years. If you were developing a product where leap years were a core part of the domain, it would be useful to have language for these cases.

### Be concise
Decreasing noise makes the intent more clear.
* Avoid implicit words
  ```ruby
  # avoid - the "should" doesn't express anything new, every test implicitly describes what "should" happen
  it 'should give an error if first name is missing'

  # prefer
  it 'gives an error when first name is missing'
  ```

## Assertions

### Separate independent assertions into their own tests
This clarifies the intent of the test, makes tests more maintainable because they are shorter and because test cases are clearly separated, and provides more granular failure messages (one failure doesn't get buried by another).

*Note: There are some proponents of having only one assertion per test case. You may or may not arrive at that principle. What's essential is that tests have one well-defined reason to fail.*

```ruby
# avoid - if the first case fails, you won't know the status of the other cases
it 'identifies phrases as palindromes' do
  expect('race car').to be_truthy
  expect('Amor, Roma!').to be_truthy
  expect('taco    cat').to be_truthy
end

# prefer - you'll know if there's a problem with punctuation, but extra whitespace is working
it 'identifies a palindrome phrase' do
  expect('race car').to be_truthy
end

it 'identifies a palindrome phrase with punctuation' do
  expect('Amor, Roma!').to be_truthy
end

it 'identifies a palindrome phrase with multiple spaces between words' do
  expect('taco    cat').to be_truthy
end
```

## Agile Testing Pyramid
#### Acceptance
* Purpose: Verify that the system is wired through properly.
* How: Exercise minimal paths as realisitcally as possible. Rely on lower-level tests for the logic's correctness.
* Pros: Gives you confidence that your system works end-to-end.
* Cons: Slow, brittle, can be non-deterministic.

#### Unit
* Purpose: Drive out a modular, maintable, minimal code design incrementally. Comprehensively test logic of an independent unit.
* How: Focus on one small slice of functionality at a time, avoiding anticipating the next steps as you do each small step.
* Keys to success: Factor out tiny pieces, favoring stateless objects, minimal dependencies, and other techniques to make units easier to test and understand.
* Pros: Fast to write and execute.
* Cons: Does not prove that pieces interact together. Note that most beginners have a tendency to write too many realistic tests, and too few unit tests.

## Dogma
Above all, rely on your judgement and that of our teams. Don't be absolute in your approach, instead use the **best** solution depending on your goals. Best can change over time as well. You may be told or read in a book that you must always test this way but it is your team that can decide what's best for that project. A good example is multiple asserts. Despite the general rule to avoid multiple asserts, there are situations where this does make sense. [Multiple Asserts Are Ok] (https://www.industriallogic.com/blog/multiple-asserts-are-ok/).

## General TDD Resources
* [cyber-dojo.org](http://cyber-dojo.org/) is a great place to practice test-driven development. It sets up the language and test environment for you and allows you to run tests on its servers with no setup. It also records the state of the code every time you run the tests, which is helpful for reviewing how you did.
