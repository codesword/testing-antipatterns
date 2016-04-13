## What is an Anti-pattern

An antipattern is a recurring negative solution to a problem:
- Because it's a solution to a problem, it tends to stick around after it's implemented. If it didn't solve a problem, it would be thrown out.
- Because it recurs, it gets implemented -- and reimplemented -- by developers in a wide variety of settings.
- Because it's negative, it's not the optimal solution

The combination of these three elements is what makes antipatterns so troublesome.

Learning `rspec`, `jasmine` etc is the easiest part of testing. Writing good tests is the hard part. In this workshop, I am going to presents some common testing antipatterns and show how to resolve them.

These are some of the antipatterns we will be discussing today:

-  Tests that only check for the expected result, not the boundaries and exceptions - [Happy Path](happy-path.md)
- Test that runs incredibly slow. When developers kick it off, they have time to go to the bathroom, grab a smoke, or worse, kick the test off before they go home at the end of the day - [Slow pokes](slow-pokes.md)
-  Tests that are hard to figure out what is being tested - [Obscure Tests](obscure-tests.md)
-  Tests that break when they shouldn't - [Fragile Tests](fragile-tests.md)
-  Tests that pass and fail without you changing anything - [Erratic Tests](erratic-tests.md)
-  Test code that is not well refactored as the production code - [Second Class Citizen](second-class-citizen.md)
-  Tests that require branches in production code - [Test Hooks](test-hooks.md)
