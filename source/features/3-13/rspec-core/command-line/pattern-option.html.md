# `--pattern` option

When you run RSpec without giving it specific file names, it determines which
  files to load by applying a pattern to the provided directory arguments or
  `spec` (if no directories are provided). By default, RSpec uses the following
  pattern:

      "**{,/*/**}/*_spec.rb"

  Use the `--pattern` option to declare a different pattern.

## Background

_Given_ a file named "spec/example_spec.rb" with:

```ruby
RSpec.describe "two specs" do
  it "passes" do
  end

  it "passes too" do
  end
end
```

_And_ a file named "spec/example_test.rb" with:

```ruby
RSpec.describe "one spec" do
  it "passes" do
  end
end
```

## By default, RSpec runs matching spec files

_When_ I run `rspec`

_Then_ the output should contain "2 examples, 0 failures".

## The `--pattern` flag makes RSpec run files matching the specified pattern and ignore the default pattern

_When_ I run `rspec -P "**/*_test.rb"`

_Then_ the output should contain "1 example, 0 failures".

## The `--pattern` flag can be used to pass in multiple patterns, separated by commas

_When_ I run `rspec -P "**/*_test.rb,**/*_spec.rb"`

_Then_ the output should contain "3 examples, 0 failures".

## The `--pattern` flag accepts shell style glob unions

_When_ I run `rspec -P "**/*_{test,spec}.rb"`

_Then_ the output should contain "3 examples, 0 failures".
