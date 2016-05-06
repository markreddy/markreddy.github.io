---

title: Language Agnostic Unit Test Principles
description: "What make a good unit test"
tags: [unit test]
comments: true
image:
  feature: texture-feature-01.jpg
---

After spending a few days churning out unit tests for a recent project of mine, I took a step back and asked myself: *What are the properties of good unit tests?* <br><br>
Tests are seen as something of a burden that devs have to do to keep business happy, but in reality they can save countless hours of debugging and ensure the behaviour of a system is not changed (for the worst) when new code is introduced.<br><br>
So here are my, principles / properties of a good test: <br><br>
**Automatic:** Invoking of tests as well as checking results for PASS/FAIL should be automatic. <br><br>
**Thorough:** As in Coverage; Although bugs tend to cluster around certain regions in the code, ensure that you test all key paths and scenarios, even the most innocent looking code can turn sour if the system does not feed it the right input. There are several tools that analyse untested lines of code so leverage them to find the gaps. <br><br>
**Repeatable:** Tests should produce the same results every time they are run, they should not depend on uncontrollable params. <br><br>
**Independent:** Tests should be isolated, not relying on data in DBs or external modules, think mocking frameworks here. Within the suite itself, no assumptions about order of test execution should be made, you should be able to pick and choose which test to run regardless. This clean slate approach to each test ensures that when a test fails, it should pinpoint the exact location of the problem. <br><br>
**Professional:** In the long run you’ll have as much test code as production (if not more), therefore follow the same standard of good-design for your test code. Well factored methods/classes with intention revealing names, no needless duplication, etc. Tests are documentation, they point out the corner cases that can cripple a system, therefore should be highly readable. <br><br>
**Speed:** Good tests should run Fast. Any test that takes over half a second to run, needs to be worked upon. The longer the test suite takes for a run, the less frequently a developer will choose to run it. <br><br>
Some other more obvious guidelines, that may cut out some of the bloat:
* Don’t test code that you don’t own (e.g. third-party libs).
* Don’t go about testing getters and setters.
* Keep an eye on cost-to-benefit ratio or defect probability.
* Write your tests in an Arrange/Act/Assert style.