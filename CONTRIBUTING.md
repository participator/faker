# Contributing to Faker

Have a fix for a problem you've been running into or an idea for a new feature you think would be useful? Bug reports and pull requests are welcome on GitHub at https://github.com/faker-ruby/faker.

<br>
We love pull requests. Here's what you need to do:

<br>

- [Ensure that you have a working environment](#setting-up-your-environment)
- [Check that everything works](#make-sure-everything-works)
- [Prepare to submit a PR](#prepare-to-submit-a-pr)
- Push to your fork and submit a pull request.
- [Github Flow for contributors and collaborators](#github-flow-for-contributors-and-collaborators)
- [Syntax/Good practices](#syntaxgood-practices)
  - [Documentation](#documentation)
  - [Code Styles](#code-styles)
  - [YAML](#yaml)
- [Tips](#tips)

<br>

## Setting Up Your Environment:
1. Fork the repo and clone your fork onto your machine

1. Setup the project's dependencies `bin/setup`

<br>

## Make Sure Everything Works
1. Run the tests. We only take pull requests with passing tests, and it's great to know that you have a clean slate: `bundle && bundle exec rake`

1. We are using [RuboCop](https://github.com/bbatsov/rubocop) because we love static code analyzers.
    * Ways to run RuboCop:
        - `bundle exec rubocop`
        - `bundle exec rake` would run the test suite and after that it runs the Ruby static code analyzer.

<br>

## Prepare and Submit a PR
1. Add a test for your change. If you are adding functionality or fixing a bug, we need a test! We use [Minitest](https://github.com/seattlerb/minitest) in this project. *Only PRs for refactoring or documentation changes do not require new tests.*

1. Make the test pass. Always use `sample`, `shuffle`, and `rand` from the Base class (just like the rest of the code) rather than `Array#sample`, `Array#shuffle` and `Kernel#rand` to preserve the deterministic feature.

1. We care about code coverage and use `SimpleCov` to analyze the code and generate test coverage reports. It's possible to check the test coverage by running  `open coverage/index.html`. Please make sure to not decrease our `current % covered` and add appropriate test cases when necessary.

1. When adding a new class, add a new yaml file to `lib/locales/en` rather than adding translations to `lib/locales/en.yml`.  For example, if you add Faker::MyThing, put your translations in `lib/locales/en/my_thing.yml`.  See [the locale README](./lib/locales/en/README.md) for more info.

1. When removing a method, don't forget to deprecate it. You can `extend Gem::Deprecate` and use the `deprecate` method to accomplish this task.

1. Methods with optional arguments should use keyword rather than positional arguments. An exception to this could be a method that takes only one optional argument, and it's unlikely that that method would ever take more than one optional argument.

1. Push to your fork and submit a pull request.

<br>

## Github Flow for contributors and collaborators

For those of you with commit access, please check out Scott Chacon's blog post about [github flow](http://scottchacon.com/2011/08/31/github-flow.html)

> * Anything in the main branch is deployable
> * To work on something new, create a descriptively named branch off of main (ie: new-oauth2-scopes)
> * Commit to that branch locally and regularly push your work to the same named branch on the server
> * When you need feedback or help, or you think the branch is ready for merging, open a pull request
> * After someone else has reviewed and signed off on the feature, you can merge it into main

If you're reviewing a PR, you should ask yourself:
> * Does it work as described? A PR should have a great description.
> * Is it understandable?
> * Is it well implemented?
> * Is it well tested?
> * Is it well documented?
> * Is it following the structure of the project?

<br>
<br>

## Syntax/Good practices:

### Documentation
Include [YARD] style docs for all methods that includes:
- A short description of what the method generates
- Descriptions for all params (`@param`)
- The return type (`@return`)
- At least one example of the output (`@example`)
- The version that the method was added (`@faker.version`)
  - Set as `next` for new methods or methods with new features 

```ruby
##
# Produces a random string of alphabetic characters, (no digits)
#
# @param char_count [Integer] The length of the string to generate
#
# @return [String]
#
# @example
#   Faker::Alphanumeric.alpha #=> "kgdpxlgwjirlqhwhrebvuomdcjjpeqlq"
#   Faker::Alphanumeric.alpha(number: 10) #=> "zlvubkrwga"
#
# @faker.version next
def alpha(number: 32)
    # ...
end
```
<br>

### Code Styles
Please follow these guidelines when adding new code:
* Two spaces, no tabs.
* No trailing whitespace. Blank lines should not have any space.
* Prefer `&&`, `||` over `and`, `or`.
* `MyClass.my_method(my_arg)` not `my_method( my_arg )` or `my_method my_arg`.
* `a = b` and not `a=b`.
* In general, follow the conventions you see used in the source already.
* **ALL SHALL OBEY THE RUBOCOP**

<br>

### YAML
Please use dash syntax for yaml arrays:
```Yaml
# this is preferred
a_things:
  - small_thing
  - big_thing
  - other_thing


# instead of these
b_things: [small_thing, big_thing, other_thing]
c_things: [
  small_thing,
  big_thing,
  other_thing,
]

```

- If in doubt, use `bundle exec rake reformat_yaml['lib/path/to/file.yml']` to reformat the yml.

<br>

## Tips

* Use the `rake console` task to start a session with Faker loaded.
* Use `bundle exec yard server -r` to launch the YARD Doc server

[YARD]: (https://www.rubydoc.info/gems/yard/file/README.md)
