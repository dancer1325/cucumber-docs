---
title: Writing better Gherkin
subtitle: "Some guidelines to writing better Gherkin"
---


# Describe behaviour

* scenarios -- should describe --
  * the intended behaviour of the system == "what" == *functional requirement*
    * Reason: 🧠if the implementation of a feature changes -> ONLY need to change the process steps behind the scenes 🧠
  * ⚠️NOT the implementation ⚠️ == "how" == *procedural reference*
    * *procedural* -- belongs to -- implementation details

* _Example:_ authentication Scenario
  * behavior

    ```
    When "Bob" logs in              
    ```

  * implementation

    ```
      Given I visit "/login"
      When I enter "Bob" in the "user name" field
        And I enter "tester" in the "password" field
        And I press the "login" button
      Then I should see the "welcome" page
    ```

* 👁️ questions to wonder | writing a feature clause 👁️
  * “if the implementation changes -> Will this wording need to change?”
    * if the answer is “Yes” -> reword

# Consider a more declarative style

* Declarative tests
  * == describes the behaviour != implementation details 
    * == hides the details of the implementation
    * steps
      * express the idea
      * NO exact values specified
  * allows
    * scenarios
      * easier to maintain
      * less brittle
    * "living documentation"
  * _Example:_

    ```
    Feature: Subscribers see different articles based on their subscription level
     
    Scenario: Free subscribers see only the free articles
      Given Free Frieda has a free subscription
      When Free Frieda logs in with her valid credentials
      Then she sees a Free article
    
    Scenario: Subscriber with a paid subscription can access both free and paid articles
      Given Paid Patty has a basic-level paid subscription
      When Paid Patty logs in with her valid credentials
      Then she sees a Free article and a Paid article
    ``` 

* Imperative tests
  * more precise 
    * steps
    * inputs
    * expected results
  * harder to read
  * tied to the current UI
    * -> more work to maintain
      * Reason: 🧠 if implementation changes -> tests need to be updated 🧠
  * _Example:_

    ```
    Feature: Subscribers see different articles based on their subscription level 
    
    Scenario: Free subscribers see only the free articles
      Given users with a free subscription can access "FreeArticle1" but not "PaidArticle1" 
      When I type "freeFrieda@example.com" in the email field
      And I type "validPassword123" in the password field
      And I press the "Submit" button
      Then I see "FreeArticle1" on the home page
      And I do not see "PaidArticle1" on the home page
    
    Scenario: Subscriber with a paid subscription can access "FreeArticle1" and "PaidArticle1"
      Given I am on the login page
      When I type "paidPattya@example.com" in the email field
      And I type "validPassword123" in the password field
      And I press the "Submit" button
      Then I see "FreeArticle1" and "PaidArticle1" on the home page  
    ```
