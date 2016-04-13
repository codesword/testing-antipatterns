````ruby
# app/models/item.rb
class Item < ActiveRecord::Base
  def self.unique_names
    pluck(:name).uniq.sort
  end
end

# spec/models/item_spec.rb
describe Item, ".unique_names" do
  it "returns a list of sorted, unique, Item names" do
    create(:item, name: "Gamma")
    create(:item, name: "Gamma")
    create(:item, name: "Alpha")
    create(:item, name: "Beta")

    expected = Item.pluck(:name).uniq.sort

    expect(Item.unique_names).to eq expected
  end
end
```

The implementation of the method under test is `pluck(:name).uniq.sort`, and
we're testing it against `Item.pluck(:name).uniq.sort`.

Instead of testing the implementation of the code, we should test it's behavior.
A better test would look like this:

```ruby
describe Item, ".unique_names" do
  it "returns a list of sorted, unique, Item names" do
    create(:item, name: "Gamma")
    create(:item, name: "Gamma")
    create(:item, name: "Alpha")
    create(:item, name: "Beta")

    expect(Item.unique_names).to eq %w(Alpha Beta Gamma)
  end
end
```
