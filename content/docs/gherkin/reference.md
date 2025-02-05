---
title: Gherkin Reference
subtitle: "Cucumber syntax: Given, When, Then"
---

* Gherkin
  * special [keywords](#keywords) /
    * give structure and meaning / executable specifications
    * -- are translated to -- many spoken languages
    * most lines | Gherkin document -- start with -- one of the [keywords](#keywords)
    * 👁️SOME keywords need `:` 👁️
      * ⚠️if you add a `:` | keyword / NOT needed -> test(s) will be ignored ⚠️
  * Comments
    * ONLY allowed | 
      * start of a new line
      * anywhere | feature file
    * `  # Commentary` or `# Commentary`
      * == -- can start with -- >= 0 spaces
  * Block comments
    * ⚠️ NOT yet supported ⚠️
  * indentation
    * recommended, it's 2 spaces
  * each line = `keyword textWhichIsGoingToBeMatchedWithAStepDefinition` 
    * [step definition](/docs/cucumber/step-definitions)
  * _Example:_  

```gherkin
Feature: Guess the word

# 1. indentation of 2 spaces in below lines
  # The first example has two steps
  # 2.  Scenario:     keyword / needs `:`
  Scenario: Maker starts a game
    # 3. Comments ONLY allowed at the start of the line -- Uncomment next line to see the error
    #When the Maker starts a game  #Commentary NOT allowed out of the start of the line
    # 4. NOT all keywords need `:` followed   -- Uncomment next line to see the error
    #When: the Maker starts a game
    When the Maker starts a game
    Then the Maker waits for a Breaker to join

  # The second example has three steps
  Scenario: Breaker joins a game
    Given the Maker has started a game with the word "silky"
    When the Breaker joins the Maker's game
    Then the Breaker must guess a word with 5 characters
```

```gherkin
# language: es
Característica: Adivina la palabra

  Escenario: Alfredo se une al juego
    Dado Marcos ha empezado el juego con la palbra "caca"
    Cuando es el turno de Alfredo
    Entonces Alfredo puedo empezar a adivinar
```

# Keywords

* 👁️ keywords / NOT force to start the line with them 👁️
  * `Example`/`Scenario`,
  * `Background`,
  * `Scenario Outline`
  * `Rule`

```gherkin
# language: en
Feature: User Login

  Background:
    # Next line start WITHOUT a keyword
    steps are executed before each scenario in this feature.
    Given the system is online
  
  Scenario: Successful login
    # Next line start WITHOUT a keyword
    This scenario demonstrates a successful login to the system by a valid user.
    Given the user is on the login page
    When the user enters a valid username and password
    Then the user should be redirected to the dashboard

  Scenario Outline: Login with different user roles
    # Next line start WITHOUT a keyword
    This scenario outlines how different user roles access the system.
    Given the user is on the login page
    When the user logs in as <role>
    Then the user should be redirected to the <role> dashboard

    Examples:
      # Next line start WITHOUT a keyword
      The examples below illustrate the different user roles.
      | role      |
      | Admin     |
      | Moderator |
      | User      |

  Rule: Password Management
    # Next line start WITHOUT a keyword
    This rule defines the behavior related to password management.
    Background:
      Given the user is logged in
    Scenario: User changes password successfully
      This scenario shows the steps for a successful password change.
      When the user navigates to the password change page
      And the user enters a new valid password
      Then the user should see a confirmation message "Password changed successfully"

```

* primary keywords
  * [`Feature`](#feature)
  * [`Rule`](#rule) (as of Gherkin 6)
  * [`Example`](#example) (or `Scenario`)
  * [`Given`](#given), [`When`](#when), [`Then`](#then), [`And`](#and-but), [`But`](#and-but) for steps (or [`*`](#Asterisk))
  * [`Background`](#background)
  * [`Scenario Outline`](#scenario-outline) (or [`Scenario Template`](#scenario-outline))
  * [`Examples`](#examples) (or [`Scenarios`](#examples))

* secondary keywords
  * `"""` (Doc Strings)
  * `|` (Data Tables)
  * `@` (Tags)
  * `#` (Comments)

{{% note "Localisation"%}}
* Previous keywords have their equivalent / [spoken languages](#spoken-languages)
{{% /note %}}

## Feature

* `Feature: ShortTextToDescribeTheFeature`
* == high-level description of a software feature /
  * description -- could detail --
    * brief explanation
    * general acceptance criteria
  * group related scenarios
  * 👁️ first primary keyword | Gherkin document 👁️
  * free-form text underneath | new line, can be added
    * -- ignored by -- Cucumber | runtime
    * -- available for -- reporting 
    * ends | starting a line with a keyword
* 1! feature / `.feature`
* many tags are allowed to add

```gherkin
Feature: Guess the word
  # next lines are "free-form text underneath" / NOT need to start with a keyword
  The word guess game is a turn-based game for two players.
  The Maker makes a word for the Breaker to guess. The game
  is over when the Breaker guesses the Maker's word.
  # Here ends the "free-form text underneath", because the next line starts with a keyword
  Example: Maker starts a game
```

## Descriptions

* check above for `Feature`
* valid 
  * |
    * `Example`/`Scenario`,
    * `Background`,
    * `Scenario Outline`
    * `Rule`
  * write ANYTHING / line NOT start with a keyword
  * forms Markdown
  * formatters -- _Example:_ official HTML formatter --

## Rule

*TODO:
The (optional) `Rule` keyword has been part of Gherkin since v6. 

{{% note "Cucumber Support for Rule"%}}
The `Rule` keyword is still pretty new. It has been ported in a lot of Cucumber implementation already.
Yet if you encounter issues, check the documentation of your Cucumber implementation to make sure it supports it.
{{% /note %}}

The purpose of the `Rule` keyword is to represent one *business rule* that should be implemented.
It provides additional information for a feature.
A `Rule` is used to group together several scenarios
that belong to this *business rule*. A `Rule` should contain one or more scenarios that illustrate the particular rule.

For example:

```gherkin
# -- FILE: features/gherkin.rule_example.feature
Feature: Highlander

  Rule: There can be only One

    Example: Only One -- More than one alive
      Given there are 3 ninjas
      And there are more than one ninja alive
      When 2 ninjas meet, they will fight
      Then one ninja dies (but not me)
      And there is one ninja less alive

    Example: Only One -- One alive
      Given there is only 1 ninja alive
      Then he (or she) will live forever ;-)

  Rule: There can be Two (in some cases)

    Example: Two -- Dead and Reborn as Phoenix
      ...
```

## Example

* TODO:
This is a *concrete example* that *illustrates* a business rule. It consists of
a list of [steps](#steps).

The keyword `Scenario` is a synonym of the keyword `Example`.

You can have as many steps as you like, but we recommend 3-5 steps per example. Having too many steps will cause the example to lose its expressive power as a specification and documentation.

In addition to being a specification and documentation, an example is also a *test*. As a whole, your examples are an
*executable specification* of the system.

Examples follow this same pattern:

- Describe an initial context (`Given` steps)
- Describe an event (`When` steps)
- Describe an expected outcome (`Then` steps)

## Steps

* step starts with `Given`, `When`, `Then`, `And`, or `But`
* Cucumber executes 1! scenario's step / sequence you’ve written
  * -- looks for a -- matching step definition
    * -> ⚠️ step's text must be unique == != other step's text ⚠️

        ```gherkin
        # Next ones are duplicated steps, because the step's text is the same
        Given there is money in my account
        Then there is money in my account
        ```

        ```gherkin
        # Rephrase of the previous one / it's valid
        Given my account has a balance of £430
        Then my account should have a balance of £430
        ```

### Given

* uses
  * describe the initial context of the system == *scene* of the scenario == preconditions
    * typically something / happened in the *past*
    * _Example:_ create and configure objects or adding data | test database
* goal
  * **put the system in a known state**
* ❌NO user interaction | `Given`'s ❌
* several `Given` steps / -- linked with -- `And` or `But`

### When

* uses
  * describe an event
    * _Example1:_ person -- interacting with the -- system, or
    * _Example2:_ event -- triggered by -- another system
* Implementation details -- should be hidden in the -- [step definitions](/docs/cucumber/step-definitions)

### Then

* uses
  * describe an *expected* outcome / is an **observable**
    * **observable** == comes *out* of the system != behaviour deeply buried | system
      * _Examples:_ report, UI, message
      * _NOTValid:_ record | DDBB
* 👁️[step definition](/docs/cucumber/step-definitions) related -- should be an -- *assertion* 👁️

### And, But

* `And`
  * uses
    * successive `Given`'s or `Then`'s

      ```gherkin
      Example: Multiple Givens
        Given one thing
        Given another thing
        Given yet another thing
        When I open my eyes
        Then I should see something
        Then I shouldn't see something else
      ```

      ```gherkin
      # Refactor previously, replacing successive Given by And
      Example: Multiple Givens
        Given one thing
        And another thing
        And yet another thing
        When I open my eyes
        Then I should see something
        But I shouldn't see something else
      ```

* `*`
  * uses
    * == `And` == successive `Given`'s or `Then`'s

        ```gherkin
        Scenario: All done
          Given I am out shopping
          And I have eggs
          And I have milk
          And I have butter
          When I check my list
          Then I don't need anything
        ```

        ```gherkin
      # Refactor previously, replacing successive Given by *
        Scenario: All done
          Given I am out shopping
          * I have eggs
          * I have milk
          * I have butter
          When I check my list
          Then I don't need anything
        ```

## Background

* TODO:
Occasionally you'll find yourself repeating the same `Given` steps in all of the scenarios in a `Feature`.

Since it is repeated in every scenario, this is an indication that those steps
are not *essential* to describe the scenarios; they are *incidental details*. You can literally move such `Given` steps to the background, by grouping them under a `Background` section.

A `Background` allows you to add some context to the scenarios that follow it. It can contain one or more `Given` steps, which are run before *each* scenario, but after any [Before hooks](/docs/cucumber/api/#hooks).

A `Background` is placed before the first `Scenario`/`Example`, at the same level of indentation.

For example:

```gherkin
Feature: Multiple site support
  Only blog owners can post to a blog, except administrators,
  who can post to all blogs.

  Background:
    Given a global administrator named "Greg"
    And a blog named "Greg's anti-tax rants"
    And a customer named "Dr. Bill"
    And a blog named "Expensive Therapy" owned by "Dr. Bill"

  Scenario: Dr. Bill posts to his own blog
    Given I am logged in as Dr. Bill
    When I try to post to "Expensive Therapy"
    Then I should see "Your article was published."

  Scenario: Dr. Bill tries to post to somebody else's blog, and fails
    Given I am logged in as Dr. Bill
    When I try to post to "Greg's anti-tax rants"
    Then I should see "Hey! That's not your blog!"

  Scenario: Greg posts to a client's blog
    Given I am logged in as Greg
    When I try to post to "Expensive Therapy"
    Then I should see "Your article was published."
```

`Background` is also supported at the `Rule` level, for example:

```gherkin
Feature: Overdue tasks
  Let users know when tasks are overdue, even when using other
  features of the app

  Rule: Users are notified about overdue tasks on first use of the day
    Background:
      Given I have overdue tasks

    Example: First use of the day
      Given I last used the app yesterday
      When I use the app
      Then I am notified about overdue tasks

    Example: Already used today
      Given I last used the app earlier today
      When I use the app
      Then I am not notified about overdue tasks
  ...
```

You can only have one set of `Background` steps per `Feature` or `Rule`. If you need different `Background` steps for different scenarios, consider breaking up your set of scenarios into more `Rule`s or more `Feature`s.

For a less explicit alternative to `Background`, check out [conditional hooks](/docs/cucumber/api/#conditional-hooks).

## Tips for using Background

* Don't use `Background` to set up **complicated states**, unless that state is actually something the client needs to know.
  * For example, if the user and site names don't matter to the client, use a higher-level step such as
`Given I am logged in as a site owner`.
* Keep your `Background` section **short**.
  * The client needs to actually remember this stuff when reading the scenarios. If the `Background` is more than 4 lines long, consider moving some of the irrelevant details into higher-level steps.
* Make your `Background` section **vivid**.
  * Use colourful names, and try to tell a story. The human brain keeps track of stories much better than it keeps track of names like `"User A"`, `"User B"`, `"Site 1"`, and so on.
* Keep your scenarios **short**, and don't have too many.
  * If the `Background` section has scrolled off the screen, the reader no longer has a full overview of what's happening.
Think about using higher-level steps, or splitting the `*.feature` file.

## Scenario Outline

The `Scenario Outline` keyword can be used to run the same `Scenario` multiple times,
with different combinations of values.

The keyword `Scenario Template` is a synonym of the keyword `Scenario Outline`.

Copying and pasting scenarios to use different values quickly becomes tedious and repetitive:

```gherkin
Scenario: eat 5 out of 12
  Given there are 12 cucumbers
  When I eat 5 cucumbers
  Then I should have 7 cucumbers

Scenario: eat 5 out of 20
  Given there are 20 cucumbers
  When I eat 5 cucumbers
  Then I should have 15 cucumbers
```

We can collapse these two similar scenarios into a `Scenario Outline`.

Scenario outlines allow us to more concisely express these scenarios through the use
of a template with `< >`-delimited parameters:

```gherkin
Scenario Outline: eating
  Given there are <start> cucumbers
  When I eat <eat> cucumbers
  Then I should have <left> cucumbers

  Examples:
    | start | eat | left |
    |    12 |   5 |    7 |
    |    20 |   5 |   15 |
```

### Examples

A `Scenario Outline` must contain one or more `Examples` (or `Scenarios`) section(s). Its steps are interpreted as a 
template
which is never directly run. Instead, the `Scenario Outline` is run *once for each row* in
the `Examples` section beneath it (not counting the first header row).

The steps can use `<>` delimited *parameters* that reference headers in the examples table.
Cucumber will replace these parameters with values from the table *before* it tries
to match the step against a step definition.

You can also use parameters in [multiline step arguments](#step-arguments).

# Step Arguments

In some cases you might want to pass more data to a step than fits on a single line.
For this purpose Gherkin has `Doc Strings` and `Data Tables`.

## Doc Strings

`Doc Strings` are handy for passing a larger piece of text to a step definition.

The text should be offset by delimiters consisting of three double-quote marks on lines of their own:
```gherkin
Given a blog post named "Random" with Markdown body
  """
  Some Title, Eh?
  ===============
  Here is the first paragraph of my blog post. Lorem ipsum dolor sit amet,
  consectetur adipiscing elit.
  """
```
In your step definition, there’s no need to find this text and match it in your pattern.
It will automatically be passed as the last argument in the step definition.

Indentation of the opening `"""` is unimportant, although common practice is two spaces in from the enclosing step.
The indentation inside the triple quotes, however, is significant. Each line of the Doc String will be dedented according to the opening `"""`. Indentation beyond the column of the opening `"""` will therefore be preserved.

Doc strings also support using three backticks as the delimiter:

~~~gherkin
Given a blog post named "Random" with Markdown body
  ```
  Some Title, Eh?
  ===============
  Here is the first paragraph of my blog post. Lorem ipsum dolor sit amet,
  consectetur adipiscing elit.
  ```
~~~

This might be familiar for those used to writing with Markdown.

{{% note "Tool support for backticks"%}}
Whilst all current versions of Cucumber support backticks as the delimiter, many tools like text editors don't (yet).
{{% /note %}}

It's possible to annotate the DocString with the type of content it contains. You specify the content type after the
triple quote, as follows:

```gherkin
Given a blog post named "Random" with Markdown body
  """markdown
  Some Title, Eh?
  ===============
  Here is the first paragraph of my blog post. Lorem ipsum dolor sit amet,
  consectetur adipiscing elit.
  """
```

{{% note "Tool support for content types"%}} Whilst all current versions of Cucumber support content types as the
delimiter, many tools like text editors don't (yet). {{% /note %}}

## Data Tables

* allows
  * passing a list of values | 👀step definition's last argument 👀

```gherkin
Given the following users exist:
  | name   | email              | twitter         |
  | Aslak  | aslak@cucumber.io  | @aslak_hellesoy |
  | Julien | julien@cucumber.io | @jbpros         |
  | Matt   | matt@cucumber.io   | @mattwynne      |
```

### Table Cell Escaping

If you want to use a newline character in a table cell, you can write this
as `\n`. If you need a `|` as part of the cell, you can escape it as `\|`. And
finally, if you need a `\`, you can escape that with `\\`.

### Data Table API

* see [Data Table API reference](https://github.com/cucumber/cucumber-jvm/tree/main/datatable)

# Spoken Languages

The language you choose for Gherkin should be the same language your users and
domain experts use when they talk about the domain. Translating between
two languages should be avoided.

This is why Gherkin has been translated to [over 70 languages](/docs/gherkin/languages) .

Here is a Gherkin scenario written in Norwegian:

```gherkin
# language: no
Funksjonalitet: Gjett et ord

  Eksempel: Ordmaker starter et spill
    Når Ordmaker starter et spill
    Så må Ordmaker vente på at Gjetter blir med

  Eksempel: Gjetter blir med
    Gitt at Ordmaker har startet et spill med ordet "bløtt"
    Når Gjetter blir med på Ordmakers spill
    Så må Gjetter gjette et ord på 5 bokstaver
```

A `# language:` header on the first line of a feature file tells Cucumber what
spoken language to use - for example `# language: fr` for French.
If you omit this header, Cucumber will default to English (`en`).

Some Cucumber implementations also let you set the default language in the
configuration, so you don't need to place the `# language` header in every file.
