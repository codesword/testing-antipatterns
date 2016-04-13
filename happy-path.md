## Happy paths

Happy path tests validate the expected behavior of the system under test. They follow the well-trodden execution path of everything going right. In a functional test, the happy path is the same -- or close to -- the use case. In a unit test, it's the same but smaller -- because your unit obeys the Single Responsibility Principle, you're testing its single responsibility.

Actually, happy path tests aren't an antipattern. The antipattern is when the developer stops at happy path tests. Happy path tests don't test the parts of the system most likely to fail (the sad paths).

When writing tests, you need to cover the following cases

- validity (or domain): asserts the correct behavior for data that isn't valid (or is out of the domain)
- boundary: asserts that the implementation works correctly at the boundaries of the domain.

```ruby
context "find factorial of number" do
  it "factorial of 5 is 120" do
    result = factorial(5)
    expect(result).to eq 120
  end
end
```

With test like this, the factorial method defined below will make the test pass.

```ruby
def factorial(num)
  120
end
```
One solution to this is to have multiple happy paths.

```ruby
context "find factorial of number" do
  it "factorial of 5 is 120" do
    result = factorial(5)
    expect(result).to eq 120
  end

  it "factorial of 5 is 120" do
    result = factorial(6)
    expect(result).to eq 5040
  end
end
```
In this case, the method below will make all tests pass.

```ruby
def factorial(num)
  return 1 if num == 1
  num * factorial(num - 1)
end
```

However we didn't handle different boundries eg factorial of 0 is 1 or validity eg what happens if we pass in string instead of numbers, pass in a negative number etc

The test below is testing both validity and boundry
```ruby
context "find factorial of number" do
  it "evaluate the factorial of 5" do
    result = factorial(5)
    expect(result).to eq 120
  end

  it "evaluate the factorial of 6" do
    result = factorial(6)
    expect(result).to eq 5040
  end

  it "evaluate the factorial of 0" do
    result = factorial(0)
    expect(result).to eq 1
  end

  it "raises an exception for inputs that are negative" do
    expect(factorial(-2)).to raise_error(ArgumentError, "Input must be positive")
  end

  it "raises an exception for inputs that are not integers" do
    expect(factorial("2")).to raise_error(ArgumentError, "Input must be a fixnum/integer")
  end
end
```

The above test will force us to define the factorial method like the one below so that our test can pass.

```ruby
def factorial(num)
  raise ArgumentError, "Input must be a fixnum/integer" unless num.class == Fixnum
  raise ArgumentError, "Input must be positive" if num < 0
  return 1 if num == 0
  num * factorial(num - 1)
end
```
