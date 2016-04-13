```ruby
it "sets submitted at to the current time" do
  form = Form.new
  form.submit
  expect(form.reload.submitted_at).to eq Time.now
end
```

The best way to ensure that the time is what you think it is, is to stub it out
with a known value. Rails 4.1 introduced the `travel_to` helper, which allows
you to stub the time within a block:

```ruby
it "sets submitted at to the current time" do
  form = Form.new

  travel_to Time.now do
    form.submit
    expect(form.reload.submitted_at).to eq Time.now
  end
end
```
