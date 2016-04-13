Consider this setup

```ruby
context 'user account exists with a matching Facebook uid' do
  setup do
    @user = create(:user, fb_user_id: 1234567, profile_url: "http//..", name: "some name")
  end
  ...
end
```

The right approach

```ruby
context 'user account exists with a matching Facebook uid' do
  setup do
    @uid  = 1234567
    @user = create(:user, fb_user_id: @uid)
  end
  ...
end
```
