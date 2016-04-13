## Obscure tests

When you’re having trouble understanding the behavior a test is verifying, then we have a testing anti-pattern called obscure tests
A common cause of Obscure Test is the Mystery Guest.

We have a mystery guest when test reader is not able to see the cause and effect between fixture and verification logic because part of it is done outside the Test Method.

The impact is:
- Tests don’t fulfill the role of Tests as Documentation.
- You may have Erratic Tests which result in tests that don’t pass during every test run or pass in the test environment but not in production.

In the test code of Rails applications, the Mystery Guest is usually one of following culprits:
- [a Rails fixture](obscure-tests/fixtures-vs-factories.md)
- [an instance variable defined at the top of a long context block, or nested up multiple context blocks](obscure-tests/instance-variable.md)
- [RSpec DSL Puzzle](obscure-tests/rspec-dsl-puzzle.md)
- [Irrelevant information in factories](obscure-tests/irrelevant-informaion.md)
- a variable without an Intention Revealing Name
