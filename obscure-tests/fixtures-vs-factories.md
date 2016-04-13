Fixtures are Rails' default way to prepare and reuse test data. Do not use fixtures.

Let’s take a look at a simple fixture:

```
# users.yml
dan:
  name: Dan
  role: developer
  location: San Francisco

phil:
  name: Phil
  role: designer
  location: Boston
```
You can use it in a test like this:

```ruby
describe User do
  describe "something" do
    it "is composed of first and last name" do
      user = users(:dan)
      # some other code
    end
  end
end
```
There are a few problems with this test code:

It is not clear where the user came from and how it is set up. This is a mystery guest
In practice these shortcomings are addressed by comment essays:

```ruby
describe Dashboard do
  fixtures :all

  describe "#show" do
    before do
      # User with preferences to view posts about kittens
      # and in the group with special access to Burmese cats
      # with 4 friends that like ridgeback dogs.
      @user = users(:kitten_fan)
    end
  end
end
```

Factories to the rescue. In rails, we use factory girl to maintain simple definition in a single place.

```ruby
FactoryGirl.define do
  factory :user do
    first_name "Marko"
    last_name  "Anastasov"
    phone "555-123-6788"
  end
end
```

Now your test can set the related attributes before checking for the expected outcome:

```ruby
describe User do
  describe "#full_name" do

    it "is composed of first and last name" do
      user = build(:user, first_name: "Johnny", last_name: "Bravo")
      user.full_name.should eql("Johnny Bravo")
    end
  end
end
```
