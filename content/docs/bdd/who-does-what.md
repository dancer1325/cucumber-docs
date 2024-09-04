---
title: Who Does What?
subtitle: Roles and responsibilities in a BDD team
---

* Who should be writing [Gherkin](/docs/gherkin/) documents & [step definitions](/docs/cucumber/step-definitions)?
  * -- depends on --
    * team structure,
    * skills,
    * culture,
    * ...

# The Three Amigos

* := meeting /
  * user stories -- are turned into, via Gherkin scenarios, -- cleaned oned
  * intervene
    * **The product owner**
      * -- responsible for -- deciding scoping
    * **The tester**
      * -- responsible for -- generating
        * Scenarios,
        * edge cases
    * **The developer**
      * -- responsible for --
        * adding Steps to the Scenarios
        * thinking of the details / each requirement

# Writing Gherkin

* TODO:
To start with, when the language and style used in the scenarios
is still being established, it is recommended that the entire team collaborate on writing the Gherkin.
Later, it can be efficiently done by a pair: a developer (or someone who is responsible for the
automation) and a tester (or someone who is responsible for quality) as long as their
output is actively reviewed by the product owner (or business representative).

# Writing Features

Cucumber tests are written in terms of “Features”. Each feature consists of one or more “Scenarios”.

Let’s start with an example Feature file:

```Gherkin
Feature: Explaining Cucumber
  In order to gain an understanding of the Cucumber testing system
  As a non-programmer
  I want to have an overview of Cucumber that is understandable by non-geeks

  Scenario: A worker seeks an overview of Cucumber
    Given I have a coworker who knows a lot about Cucumber
    When I ask my coworker to give an overview of how Cucumber works
    And I listen to their explanation
    Then I should have a basic understanding of Cucumber
```

Note that the scenarios do not go into the details of what the software
(or, in this case, the coworker) will do. It stays focused on the perspective of
the person the Feature is intended to serve (in this case, “a non-programmer”).

Every feature file has a single feature description at the top, but can have any
number of scenarios.

The `Feature` line names the feature. This should be a short label.

`In order to` presents the reason/justification for having the feature. In
general, this should match to one of the project’s core purposes or “business
values” such as:

- Protect revenue
- Increase revenue
- Manage cost
- Increase brand value
- Make the product remarkable
- Provide more value to your customers

`As a` describes the role of the people/users being served by the feature.

`I want` is a one sentence explanation of what the Feature is expected to do.

So, those three lines cover Why, Who, and What. Then, the document gets into the “How” with scenarios.

# Scenarios

You can have any number of scenarios for a feature.

If you have lots and lots of scenarios in one feature, you might
actually be describing *more* than one feature. When that happens, we recommend
splitting up the document into separate Feature definitions (The definition of
“lots and lots” here is subjective, and it's up to you to determine when it's time to split up a feature).

The first line provides a short description of what the scenario is intended to
cover. If you can’t describe your scenario in a single sentence (and not a
run-on sentence), then it’s probably trying to cover too much, and should be
split into multiple scenarios.

That is followed by some combination of “Steps”—lines that begin with the
keywords `Given`, `When`, and `Then` (typically in that order).

You can have many lines that use the same keyword (e.g., `Given there is something` followed by `Given I have another thing`). To increase the readability, you can substitute the keywords `And` or `But` (e.g., `Given there is something` followed by `And I have another thing`).

In general, any `Given` step line should describe only one thing. If you have
words like “and” in the middle of a step, you are probably describing more than
one step, and should split it into multiple steps.

For example:

```gherkin
	When I fill in the "Name" field and the "Address" field
```

Becomes:

```gherkin
	When I fill in the "Name" field
	And I fill in the "Address" field
```

Cucumber features are best served by consistency. Don't say the same thing in
different ways — say it the same way every time.

For example:

```gherkin
	Given I am logged in
```

and

```Gherkin
	Given I have logged in to the site
```

have identical meaning, so it’s better to pick one and use the same line in
every Scenario where you need to be logged in.
