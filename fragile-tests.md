## Fragile Tests

When it becomes difficult to make trivial changes to your code without breaking tests, your test suite can become a burden. Fragile code comes from coupling. The more coupled your code, the harder it is to make changes without having to update multiple locations in your code. We want to write test suites that fully cover all functionality of our application while still being resilient to change.

### Causes of fragile tests

- [Coupling to the DOM](fragile-tests/coupling-to-dom.md)
- [Stubbing and mocking](fragile-tests/dangers-of-stubbing.md)
- [Relying on an objects that are created far from the test case itself](fragile-tests/far-away-objects.md)
- [Testing implementation details](fragile-tests/implementation-details.md)
