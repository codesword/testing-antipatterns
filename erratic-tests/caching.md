## Memoization

```ruby
class Post
  def self.recent
    @recent ||= order(created_at: :desc).limit(10)
  end
end
```

## Mailer
Email in queue

```ruby
expect(ActionMailer::Base.deliveries).to be_empty
```

## ActionController caching

```ruby
config.action_controller.perform_caching = true
```
