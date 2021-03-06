# HashKit

[![Build Status](https://travis-ci.org/Sage/hash_kit.svg?branch=master)](https://travis-ci.org/Sage/hash_kit)
[![Maintainability](https://api.codeclimate.com/v1/badges/3ffb56b92ca96c783093/maintainability)](https://codeclimate.com/github/Sage/hash_kit/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/3ffb56b92ca96c783093/test_coverage)](https://codeclimate.com/github/Sage/hash_kit/test_coverage)
[![Gem Version](https://badge.fury.io/rb/hash_kit.svg)](https://badge.fury.io/rb/hash_kit)

Welcome to your HashKit! HashKit is a toolkit for working with Ruby Hashes.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'hash_kit'
```

And then execute:

```bash
$ bundle
```

Or install it yourself as:

```bash
$ gem install hash_kit
```

## Usage


#HashKit::Helper

This is class contains helper methods for working with Ruby hashes.

## #indifferent!(hash)

This method is called to make a hash allow indifferent access to key values. Allowing a valid key to be accessed by either a string or symbol.
```ruby
hash = { 'key1' => 'value1', key2: 'value2' }

helper.indifferent!(hash)

value1 = hash[:key1] #This will return 'value1'
value2 = hash['key2'] #This will return 'value2'
```

## #symbolize

This method is called to convert all keys within a hash into symbols to allow consistent usage of hashes within your Ruby application.

```ruby
hash = helper.symbolize(hash)
```

## #stringify

This method is called to convert all keys within a hash into strings to allow consistent usage of hashes within your Ruby application.

```ruby
hash = helper.stringify(hash)
```

## #to_hash

This method is called to convert a object instance into a hash.

```ruby
    hash = helper.to_hash(obj)
```

## #from_hash

This method is called to convert a hash into an object.

```ruby
#class definition

class TestEntity
  attr_accessor :text, :numeric, :time
end
```

```ruby
obj = helper.from_hash(hash, TestEntity)
```


Additionally an array of HashKit::TransformItems can be specified to allow mapping from nested hashes into child entities, and nested arrays of hashes into nested arrays of entities.

Example:

```ruby
#class definitions

class TestEntity
  attr_accessor :text, :numeric, :time
end

class ComplexEntity
  attr_accessor :nested_entity, :nested_entity_array
end
```

```ruby
# transform method

# transform item definitions
transform1 = HashKit::TransformItem.new.tap do |t|
  t.key = :nested_entity
  t.klass = TestEntity
end
transform2 = HashKit::TransformItem.new.tap do |t|
  t.key = :nested_entity_array
  t.klass = TestEntity
end
transforms = [transform1, transform2]

# hash definition
hash = {
  nested_entity: { text: 'abc', numeric: 5 },
  nested_entity_array: [
    { text: 'abc', numeric: 5 },
    { text: 'abc', numeric: 5 }
  ]
}

#to hash call
obj = helper.from_hash(hash, ComplexEntity, transforms)
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/sage/hash_kit. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

This gem is available as open source under the terms of the
[MIT licence](LICENSE).

Copyright (c) 2018 Sage Group Plc. All rights reserved.
