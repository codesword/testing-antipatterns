```ruby
describe "#value" do
  it "is the difference between up and down votes" do
    link = double(upvotes: 10, downvotes: 3)
    score = Score.new(link)
    expect(score.value).to eq 7 end
  end
end
```

Here, we’ve replaced the dependency on Link and are constructing a double that responds to the following interface:
- upvotes
- downvotes

What happens if we change the upvotes and downvotes methods in the Link class to positive_votes and negative_votes? Well our test will break.
