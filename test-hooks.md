## Test Hooks

They are methods in production code that only run when in testing mode.

### Example
```ruby
class ApplicationController < ActionController::Base
  unless Rails.env.test?
    before_filter :require_login
  end
end
```
