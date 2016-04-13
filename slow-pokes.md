## Slow Pokes

As applications grow, test suites naturally and necessarily get slower. The longer the test suite, the less you will run it. The more often you can run your tests, the more valuable they are because you can catch bugs faster than you otherwise would have. As a baseline, after every line of code that you write, try to run its respective test. Always run your entire test suite before submitting pull requests and after rebasing. As you can imagine, this leads to running your tests frequently. If it’s a chore to run your tests you aren’t going to run them, and they quickly become out of date. At that point, you may as well not have written them in the first place.

### How to write fast test suites
Here are some things to think about when trying to write a fast test suite:

- Use profiling to find the slowest tests(rspec --profile)
- Have a fast spec_helper
- Use an application preloader(spring)
- Only persist what is necessary
- Move sad paths out of feature specs
- Don't hit external APIs
- Delete tests
