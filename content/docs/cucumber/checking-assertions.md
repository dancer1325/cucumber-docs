---
title: Checking Assertions
subtitle: "How to determine success or failure"
---

* assertions should be done | `Then` steps
* Cucumber does NOT come with an assertion library

# Java

## JUnit 5

* if you use [cucumber-junit-platform-engine](https://github.com/cucumber/cucumber-jvm/tree/main/cucumber-junit-platform-engine) -> choose any assertion library
  * _Example:_
    * [AssertJ](https://assertj.github.io/doc/)
    * [Hamcrest](http://hamcrest.org/JavaHamcrest/)
    * [JUnit Jupiter](https://junit.org/junit5/docs/current/user-guide/#writing-tests-assertions)

## JUnit 4

* TODO:
When using JUnit 4 to run Cucumber we recommend using [JUnit 4](https://junit.org/junit4/)'s `assert*` methods.

If you are using Maven, add the following to your `pom.xml`:

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>{{% version "junit" %}}</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-junit</artifactId>
    <version>{{% version "cucumberjvm" %}}</version>
    <scope>test</scope>
</dependency>
```

{{% note "Cucumber version"%}}
Make sure to use the same version for `cucumber-junit` that you are using for `cucumber-java` or `cucumber-java8`.
{{% /note %}}

Below is an example using `assertEquals`:

```java
import static org.junit.Assert.*;

public class Example {

    @Then("the result should be {int}")
    public void the_result_should_be(int expectedResult) {
        assertEquals(expectedResult, result);
    }
}
```

For more examples of how to use JUnit assertions, see the [JUnit Wiki](https://github.com/junit-team/junit4/wiki/Assertions).

## TestNG

You can also use [TestNG](https://testng.org/doc/)'s assertions'.

If you are using Maven, add the following to your `pom.xml`:
```xml
<dependency>
    <groupId>org.testng</groupId>
    <artifactId>testng</artifactId>
    <version>{{% version "testng" %}}</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-testng</artifactId>
    <version>{{% version "cucumberjvm" %}}</version>
    <scope>test</scope>
</dependency>
```

TestNG assertions are similar JUnit.
For a more extensive example of how to use TestNG with Cucumber, see the [calculator-java-testng example](https://github.com/cucumber/cucumber-jvm/tree/main/examples/calculator-java-testng).

For more information on how to use TestNG assertions, see the [TestNG documentation](https://testng.org/doc/documentation-main.html#success-failure).

# JavaScript

## Node.js

We recommend using Node.js' built-in [assert](https://nodejs.org/dist/latest-v8.x/docs/api/assert.html) module.

```javascript
const assert = require('assert')

Then('the result should be {word}', function (expected) {
  // this.actual is typically set in a previous step
  assert.equal(this.actual, expected)
})
```

## Other Assertion Libraries

You can use any other assertion library if you wish. Here is an example using [Chai](https://www.chaijs.com/):

```javascript
const { expect } = require('chai')

Then('the result should be {word}', function (expected) {
  expect(this.actual).to.eql(expected)
})
```

# Ruby

## RSpec

We recommend using [RSpec](https://rspec.info/) for assertions.

Add the `rspec-expectations` gem to your `Gemfile`.
Cucumber will automatically load RSpec's matchers and expectation methods to be
available in your step definitions. For example:

```ruby
Given /^a nice new bike$/ do
  expect(bike).to be_shiny
end
```

If you want to configure RSpec, you'll need to also add the `rspec-core` gem
to your `Gemfile`. Then, you can add to your `features/support/env.rb`
configuration, such as:

```ruby
RSpec.configure do |config|
  config.expect_with :rspec do |c|
    c.syntax = :expect
  end
end
```

Realize that tests/assertions/expectations either “pass” or “fail” (raise an error), and that “fail” is **not** the same as `false`.
Anything besides “fail” is a pass.

When, in RSpec, `something.should_be 0` and it is not, then what is returned is an error exception, not a Boolean value.
In Cucumber, one writes `fail if false` and not only `false`.
This is because `false` might be the expected successful outcome of a test, and thus not an error.

Sometimes however, we wish to test how our application handles an exception and therefore do not want that exception
to be handled by Cucumber. For that situation use the `@allow-rescue` [tag](/docs/cucumber/api/#tags).

## Test::Unit

If you prefer to use `Test::Unit`'s `assert` methods you can mix them into
your `World`.

```ruby
require 'test/unit/assertions'

World(Test::Unit::Assertions)
```
