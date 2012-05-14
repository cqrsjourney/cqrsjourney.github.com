---
layout: post
title: "Specing out end-to-end scenarios"
date: 2012-05-14 11:18
comments: true
categories: 
- requirements
- acceptance tests
- SpecFlow
---

## From mockups to features 
To spec out the scenarios for our [conference management system](http://cqrsjourney.github.com/blog/2012/03/30/Sample-Application-Overview), we’ve started with conversations with the domain experts. We’ve envisioned the user interactions with the system and captured them in mockups, like the one below:

<img src="/images/posts/Mockup-conf-mgmt.png" alt="Conference management mockup" border="0" />

Mockups helped us in many ways:

1.	Explaining our ideas in terms of UI interactions to the graphic designers.
2.	Having discussions with the developers in terms of desired functionality.
3.	Establishing, discussing and refining terms from our [ubiquitous language](https://github.com/mspnp/cqrs-journey-wiki/wiki/Ubiquitous-language).
4.	Evolving our understanding of stories via “what if” scenarios rooted in the mockups.
5.	Becoming a foundation for the future formulation of the acceptance tests.

Based on these we’ve proceeded to develop acceptance tests using [SpecFlow](http://www.specflow.org/). SpecFlow provides an integrated experience for writing and executing tests in the BDD ([Behavior-Driven Development](http://en.wikipedia.org/wiki/Behavior_Driven_Development)) style within Visual Studio. The resulting tests helped us capture, distill and refine the requirements in an unambiguous way. Here’s an example of a SpecFlow acceptance test (Feature):

<img src="/images/posts/Feature-conf-mgmt.png" alt="Conference management Feature sample in SpecFlow" border="0" />

The initial step was to write the project specifications as Feature files using the [Gherkin](ttp://en.wikipedia.org/wiki/Behavior_Driven_Development#Application_examples_in_the_Gherkin_language) language syntax. They served well for the purpose of evolving and discussing the stories among developers and domain experts. However in that form, they could not be executed. So, from the testing perspective they would need to be executed manually if we wanted to verify whether the implemented functionality has, in fact, met our expectations.

## From features to executable specs

Later on, we added the underlying plumbing to make sure that those features/acceptance tests can actually execute against our system-under-test. 

<img src="/images/posts/Executable-specs-test-run.jpg" alt="Executable spec test run" border="0" />

We used two different approaches, both of which are valuable.

Because our application is a web application, for testing directly via the UI, we used [WatiN](http://watin.sourceforge.net), an open source library for automating Web browser testing. These tests help us gain confidence that the key end-to-end happy paths through the system work. They are fragile, however and require substantial maintenance effort.

Another approach for sub-scenarios is to use subcutaneous testing (or testing just beneath the UI) by directly calling the controllers (i.e. _Features\Registration\All Features end to end\SelfRegistrationEndToEndWithInfrastructure.feature_). This way we avoid coupling with the UI but
it may appear to be more complex since it requires some internal knowledge of how the system is implemented. With time, however, it became much easier to use this approach and we were able to reuse a lot of infrastructure as well as internal reuse of the parts of the test actions (these are actually called Step Definitions in SpecFlow).

## From executable specs to exploratory testing

Of course, having the executable specs in place by no means preclude other types of testing. We recognize that good end-to-end acceptance testing requires breadth, depth, variability of actions and data, and rich scenarios, both plausible and implausible. While we value test automation for some of the scenarios, we also have professional testers on our team who are performing exploratory testing, performance testing, content testing etc. They too use the executable specs in their arsenal of tools and artefacts. The executable specs inform them of the goals of the system and some concrete scenarios.

## Finding your way around

The SpecFlow Feature files with the business specifications were structured in the following way. All the end-to-end scenarios were grouped in a subfolder similar to _"Features\Registration\All Features end to end”_ so that we could provide a quick overview of the epic (Registration in this case) and two basic reconnaissance paths through the system: one happy path and one sad (failure) path.

Then, in separate folders we grouped the variations of each scenario within the same epic – for example _“Features\Registration\Individual Reservation”_ exercises logic for scenarios specifically for individual reservations with various seat type selections. This way we can easily separate the full end-to-end acceptance tests from more fine-grained integration tests with various permutations for each underlying scenario.

Regarding the implementation details, there are some general support classes that provide many shared infrastructure functions used in most of the preconditions and assertions throughout the [Step Definitions](https://github.com/techtalk/SpecFlow/wiki/Step-Definitions).

As a test runner we used [xUnit.net](http://xunit.codeplex.com) underneath, which is supported by SpecFlow and integrates nicely with some well-known external tools like ReSharper, CodeRush, and TestDriven.NET.

## Getting involved

One of the ways that you can get involved with us is to review and refine the existing acceptance tests or contribute new tests for existing scenarios or even planned (and not yet implemented) scenarios.

## Final note

SpecFlow is just one tool in our testing armory. It is particularly useful as a way to help capture requirements from our Domain Experts in addition to verifying the behavior of the system.

