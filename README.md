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



## General TDD Resources
* [cyber-dojo.org](http://cyber-dojo.org/) is a great place to practice test-driven development. It sets up the language and test environment for you and allows you to run tests on its servers with no setup. It also records the state of the code every time you run the tests, which is helpful for reviewing how you did.
