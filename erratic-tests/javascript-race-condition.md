One potential source of erratic tests is timing issues. When running feature specs that use JavaScript, your whole test is actually running asynchronously in the JS context. Capybara jumps through a ton of hoops to eliminate the inherent race conditions and synchronize your test and app state.

Bad
```ruby
first(".active").click
```

Good
```ruby
# If you want to make sure there's exactly one
find(".active").click

# If you just want the first element
find(".active", match: :first).click
```

Bad
```ruby
all(".active").each(&:click)
```

Good
```ruby
find(".active", match: :first)
all(".active").each(&:click)
```

Bad
```ruby
execute_script("$('.active').focus()")
```

Good
```ruby
find(".active")
execute_script("$('.active').focus()")
```

Bad
```ruby
expect(find_field("Username").value).to eq("Joe")
```

Good
```ruby
expect(page).to have_field("Username", with: "Joe")
```

Bad
```ruby
it "doesn't have an active class name" do
  expect(has_active_class).to be_false
end

def has_active_class
  has_css?(".active")
end
```

Good
```ruby
it "doesn't have an active class name" do
  expect(page).not_to have_active_class
end

def have_active_class
  have_css(".active")
end
```

When interacting with the page, use action methods like click_on instead of finder methods like find whenever possible. When verifying that elements are on the page as expected, use RSpec matchers like have_css instead of node methods like text whenever possible. 
