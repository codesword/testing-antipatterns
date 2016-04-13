```ruby
# spec/support/env_helper.rb

module EnvHelper
  def with_env(variable, value)
    old_value = ENV[variable]
    ENV[variable] = value
    yield
  ensure
    ENV[variable] = old_value
  end
end

RSpec.configure do |config|
  config.include EnvHelper
end
```

You can use this in a test, like so:

```ruby
require "spec_helper"

feature "User views the form setup page", :js do
  scenario "after creating a submission, they see the continue button" do
    with_env("POLLING_INTERVAL", "1") do
      form = create(:form)

      visit setup_form_path(form, as: form.user)

      expect(page).not_to have_css "[data-role=continue]"

      submission = create(:submission, form: form)

      expect(page).to have_css "[data-role=continue]"
    end
  end
end
```
