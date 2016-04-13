```html
<div class="welcome-message">
  <p>Welcome, #{current_user.name}</p>
</div>
```


```ruby
expect(page).to have_content "Welcome, #{user.name}"
```

Imagine changing your html to:

```html
<div class="welcome-message">
  <p>Hello again, #{current_user.name}</p>
</div>
```

Your tests will fail.

### Solution

use Internationalization

```html
<div class="welcome-message">
  <p><%= t("dashboards.show.welcome", user: current_user) %></p>
</div>
```


```ruby
expect(page).to have_content t("dashboards.show.welcome", user: user)
```

use data attributes

```html
<div class="warning" data-role="warning">
  <p>This is a warning</p>
</div>
```


```ruby
expect(page).to have_css "[data-role=warning]"
```
