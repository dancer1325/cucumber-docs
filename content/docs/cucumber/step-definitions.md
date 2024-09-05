---
title: Step Definitions
subtitle: Connecting Gherkin steps to code
polyglot:
 - java
 - javascript
 - ruby
 - kotlin
 - scala

weight: 1
---

* Step Definition
  * := {{% stepdef-body %}} + [expression](#expressions) / -- links it to -- >= 1 [Gherkin steps](/docs/gherkin/reference#steps)
  * if Cucumber executes a [Gherkin step](/docs/gherkin/reference#steps) | scenario -> will look for a matching *step definition*
  * _Example:_ let's Gherkin scenario

    ```gherkin
    Scenario: Some cukes
      Given I have 48 cukes in my belly       // Gherkin step
    ```

    {{% block "java" %}}
    
    ```java
    package com.example;
    import io.cucumber.java.en.Given;
    
    public class StepDefinitions {
        @Given("I have {int} cukes in my belly")        // Step definition / matches with the previous Gherkin step
        public void i_have_n_cukes_in_my_belly(int cukes) {
            System.out.format("Cukes: %n\n", cukes);
        }
    }
    ```
    
    Or, using Java8 lambdas:
    
    ```java
    package com.example;
    import io.cucumber.java8.En;
    
    public class StepDefinitions implements En {
        // Step definition / matches with the previous Gherkin step
        public StepDefinitions() {
            Given("I have {int} cukes in my belly", (Integer cukes) -> {
                System.out.format("Cukes: %n\n", cukes);
            });
        }
    }
    ```
    {{% /block %}}

    {{% block "kotlin" %}}
    
    ```kotlin
    package com.example
    import io.cucumber.java8.En
    
    class StepDefinitions : En {
        // Step definition / matches with the previous Gherkin step -- via -- lambda expressions
        init {
            Given("I have {int} cukes in my belly") { cukes: Int ->
                    println("Cukes: $cukes")
            }
        }
    
    }
    ```
    
    {{% /block %}}

    {{% block "scala" %}}
    
    ```scala
    package com.example
    import io.cucumber.scala.{ScalaDsl, EN}
    
    class StepDefinitions extends ScalaDsl with EN {
    
        Given("I have {int} cukes in my belly") { cukes: Int =>
            println(s"Cukes: $cukes")
        }
    
    }
    ```
    
    {{% /block %}}

    {{% block "ruby" %}}
    
    ```ruby
    Given('I have {int} cukes in my belly') do |cukes|
      puts "Cukes: #{cukes}"
    end
    ```
    
    {{% /block %}}

    {{% block "javascript" %}}
    
    ```javascript
    const { Given } = require('cucumber')
    
    Given('I have {int} cukes in my belly', function (cukes) {
      console.log(`Cukes: ${cukes}`)
    });
    ```
    {{% /block %}}

# Step definition's Expressions

* types
  * [Cucumber Expression](/docs/cucumber/cucumber-expressions) 
  * [Regular Expression](https://en.wikipedia.org/wiki/Regular_expression)
    * == {{% expression-parameter %}}
      * is transformed
      * -- are passed as -- arguments to the step definition's {{% stepdef-body %}}
    * _Examples:_ 

    {{% block "java" %}}
    
    ```java
    @Given("I have {int} cukes in my belly")  // regular expression / pass expression parameter
    public void i_have_n_cukes_in_my_belly(int cukes) {
        println("Cukes: $cukes");
    }
    ```
    {{% /block %}}

    {{% block "kotlin" %}}
    
    ```kotlin
    Given("I have {int} cukes in my belly") { cukes: Int ->
            println("Cukes: $cukes")
    }
    ```
    {{% /block %}}

    {{% block "scala" %}}
    
    ```scala
    Given("I have {int} cukes in my belly") { cukes: Int =>
        println(s"Cukes: $cukes")
    }
    ```
    {{% /block %}}

    {{% block "ruby" %}}
    
    ```ruby
    Given(/I have {int} cukes in my belly/) do |cukes|
    end
    ```
    {{% /block %}}

    {{% block "javascript" %}}
    
    ```javascript
    Given(/I have {int} cukes in my belly/, function (cukes) {
    });
    ```
    {{% /block %}}

# State management

* == store state | instance variables
* allows
  * transferring state from a step definition -- to a -- subsequent step definition 

{{% block "javascript" %}}
{{% warn "❌NO arrow functions❌" %}}
* if you use arrow functions -> create a variable / represent state outside of the steps

```javascript
let cukesState;

Given('I have {int} cukes in my belly', cukes => {
  cukesState = cukes
})
```
{{% /warn %}}
{{% /block %}}

# Scope

* Step definitions
  * -- are NOT linked to a particular -- feature file or scenario
  * -- sensitive part is --
    * 's expression
      * Reason: 🧠 way to match 🧠
    * ❌ NOT ❌
      * 's file,
      * 's class
      * 's package name

# Snippets

* uses
  * Cucumber encounters a [Gherkin step](/docs/gherkin/reference#steps) / NOT matching step definition
* suggest step definitions / matching [Cucumber Expression](/docs/cucumber/cucumber-expressions)
  * _Example:_ Gherkin step / NO matching step definition
    
    ```gherkin
    Given I have 3 red balls
    ```

    {{% block "java" %}}
    
    ```java
    @Given("I have {int} red balls")
    public void i_have_red_balls(int int1) {
    }
    ```
    {{% /block %}}

    {{% block "kotlin" %}}
    
    ```kotlin
    @Given("I have {int} red balls") { balls: Int ->
    }
    ```
    {{% /block %}}

    {{% block "scala" %}}
    
    ```scala
    Given("I have {int} red balls") { balls: Int =>
    }
    ```
    {{% /block %}}

    {{% block "ruby" %}}
    
    ```ruby
    Given('I have {int} red balls') do |int1|
    end
    ```
    {{% /block %}}

    {{% block "javascript" %}}
    
    ```javascript
    Given("I have {int} red balls", function (int1) {
    });
    ```
    {{% /block %}}
 
    * _Example2:_ Previous / another parameter type WITHOUT matching step definition

    {{% block "java" %}}
    
    ```java
    @Given("I have {int} {color} balls")
    public void i_have_color_balls(int int1, Color color) {
    }
    ```
    {{% /block %}}

    {{% block "kotlin" %}}
    
    ```kotlin
    @Given("I have {int} {color} balls") { balls: Int, color: Color ->
    }
    ```
    {{% /block %}}}

    {{% block "scala" %}}
    
    ```scala
    Given("I have {int} {color} balls") { (balls: Int, color: Color) =>
    }
    ```
    {{% /block %}}

    {{% block "ruby" %}}
    
    ```ruby
    Given('I have {int} {color} balls') do |int1, color|
    end
    ```
    {{% /block %}}

    {{% block "javascript" %}}
    
    ```javascript
    Given("I have {int} {color} balls", function (int1, color) {
    });
    ```
    {{% /block %}}
