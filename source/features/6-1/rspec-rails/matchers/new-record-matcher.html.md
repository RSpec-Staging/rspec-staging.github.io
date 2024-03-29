# `be_a_new` matcher

The `be_a_new` matcher accepts a class and passes if the subject is an
  instance of that class that returns false to persisted?

  You can also chain `with` on `be_a_new` with a hash of attributes to specify
  the subject has equal attributes.

## An example spec with four be_a_new possibilities

_Given_ a file named "spec/models/widget_spec.rb" with:

```ruby
require "rails_helper"

RSpec.describe Widget do
  context "when initialized" do
    subject(:widget) { Widget.new }

    it "is a new widget" do
      expect(widget).to be_a_new(Widget)
    end

    it "is not a new string" do
      expect(widget).not_to be_a_new(String)
    end
  end

  context "when saved" do
    subject(:widget) { Widget.create }

    it "is not a new widget" do
      expect(widget).not_to be_a_new(Widget)
    end

    it "is not a new string" do
      expect(widget).not_to be_a_new(String)
    end
  end
end
```

_When_ I run `rspec spec/models/widget_spec.rb`

_Then_ the examples should all pass.
