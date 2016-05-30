# Automated Testing Wiki
## Purpose
This is a collection of notes and resources on testing conventions, techniques, and styles that improve the value and maintainability of automated tests. Contributions welcome! You can also fork this to use as a "style-guide" for your project's tests.

## Describing Test Cases

### Don't repeat inputs and expected outputs in test descriptions
Rather than describe the implementation, tell a story in the language of the domain. This reduces noise, decouples your test description from its implementation, and encourages thinking at a higher level of abstraction.

Instead of:
```ruby
it 'returns true for ""'

# prefer
it 'identifies the empty string as a palindrome'
```

### Strive to find (or create) domain language to describe scenarios expressively
For example, the cases for leap years can be described as typical leap years, typical common years, atypical leap years, and atypical common years. If you were developing a product where leap years were a core part of the domain, it would be useful to have language for these cases.


## General TDD Resources
* [cyber-dojo.org](http://cyber-dojo.org/) is a great place to practice test-driven development. It sets up the language and test environment for you and allows you to run tests on its servers with no setup. It also records the state of the code every time you run the tests, which is helpful for reviewing how you did.
