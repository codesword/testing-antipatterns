```ruby
describe Post do
  let(:user) { build_stubbed(:user) }
  let(:title) { "Example Post" }
  subject(:post) { build_stubbed(:post, user: user, title: title) }

  # a lot of other specs

  context "with an author" do
    let(:user) { build_stubbed(:user, name: "Willy") }

    it "returns the author's name" do
      expect(post.author_name).to eq("Willy")
    end
  end
end
```

This test case overrides the user locally, but relies on the post created in the subject block to use this local user object.

The fix is to bring that context in our test, and build the needed objects within the test:

```ruby
context "with an author" do
  it "returns the author's name" do
    author = build_stubbed(:user)
    post = build_stubbed(:post, user: author)

    expect(post.author_name).to eq(author.name)
  end
end
```
