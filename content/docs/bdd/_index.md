---
title: Behaviour-Driven Development
subtitle: The process Cucumber supports
weight: 1180
menu: main
iconClass: far fa-comments
---

* Behaviour-Driven Development (BDD)
  * := software development process
  * Cucumber support it

# What is BDD?

* allows
  * closing the gap between business people -- and -- technical people
  * encouraging collaboration across roles
  * working in rapid, small iterations to increase feedback
  * producing system documentation / 
    * -- is automatically checked against the -- system's behaviour
    * ⭐enables you to continue confidently ⭐
      * Reason: 🧠code -- reflects the -- documentation, & the documentation -- reflects the -- team's shared understanding  🧠
  * guiding from concept -- through to -- implementation

## BDD and agile

* BDD 
  * does NOT replace your existing agile process, BUT it enhances it
  * == set of plugins | your existing process

# Day-to-day BDD activity: _Discovery_, _Formulation_, and _Automation_

* Day-to-day BDD activity steps
  1. Discovery. if a [User Story] comes -> agreed on
     1. concrete examples
     2. expected outcomes / behaviors
  2. Formulation. document those examples / -- can be --
     1. automated
     2. checked for agreement
  3. Automation. implement the behaviour / documented example

* goal
  * each change is small
  * iterate rapidly


<figure>
  <img alt="diagram of how the practices fit together" src="bdd-practices-diagram.png" width="600px">
  <figcaption>Discovery, Formulation and Automation</figcaption>
</figure> 


## Discovery: What it _could_ do

* TODO:
> The hardest single part of building a software system is deciding precisely what to build.
>
> -- <cite>Fred Brooks, The mythical man-month</cite>

Although documentation and automated tests are produced by a BDD team, you can think of them as nice side-effects. The real goal is valuable, working software, and the fastest way to get there is through conversations between the people who are involved in imagining and delivering that software.

BDD helps teams to have the right conversations at the right time so you minimise the amount of time spent in meetings and maximising the amount of valuable code you produce.

We use structured conversations, called [discovery workshops], that focus around real-world examples of the system from the users' perspective. These conversations grow our team's shared understanding of the needs of our users, of the rules that govern how the system should function, and of the scope of what needs to be done.

It may also reveal gaps in our understanding, where we need more information before we know what to do.

The scrutiny of a discovery session often reveals low-priority functionality that can be deferred from the scope of a user story, helping the team to work in smaller increments, improving their flow.

If you're new to BDD, discovery is the right place to start. You won't get much joy from the other two practices until you've mastered discovery.

## Formulation: What it _should_ do

As soon as we have identified at least one valuable example from our discovery sessions, we can now formulate each example as structured documentation. This gives us a quick way to confirm that we really do have a shared understanding of what to build.

In contrast to traditional documentation, we use [a medium that can be read by both humans and computers](../gherkin), so that:

* We can get feedback from the whole team about our shared vision of what we're building.
* We'll be able to automate these examples to guide our development of the implementation.

By writing this executable specification collaboratively, we establish a shared language for talking about the system. This helps us to use problem-domain terminology all the way down into the code.

## Automation: What it _actually does_

Now that we have our executable specification, we can use it to guide our development of the implementation.

Taking one example at a time, we automate it by connecting it to the system as a test. The test fails because we have not implemented the behaviour it describes yet. Now we develop the implementation code, using [lower-level examples of the behaviour of internal system components](https://anarchycreek.com/2009/05/20/theyre-called-microtests/) to guide us as required.

The automated examples work like guide-rails, helping us to keep our development work on track.

When we need to come back and maintain the system later, the automated examples will help us to understand what the system is currently doing, and to make changes safely without unintentionally breaking anything.

This rapid, repeatable feedback reduces the burden of manual regression testing, freeing people up to do more interesting work, like exploratory testing.

# Learn more

Read the topics below to dig deeper and learn more about BDD.

[discovery workshops]: /docs/bdd/discovery-workshop/
[User Story]: /docs/terms/user-story/
[User Stories]: /docs/terms/user-story/
