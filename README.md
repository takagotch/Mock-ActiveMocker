### Mock-ActiveMocker
---
https://github.com/zeisler/active_mocker

```ruby
group :development, :test do
  gem 'active_mocker'
end

#db/schema.rb
ActiveRecord::Schema.define(version: 20181109134310) do
  create_table "people", force: true do |t|
    t.integer "account_id"
    t.string "first_name", limit:128
    t.string "last_name", limit:128
    t.string "address", limit: 200
    t.string "city", limit: 100
  end
end

#app/models/person.rb
class Person < ActiveRecord::Base
  belongs_to :account
  def self.bar(name, type=nil)
    puts name
  end
end

require 'rspec'
require 'active_mocker/rspec_helper'
require 'spec/mocks/person_mock'
require 'spec/mocks/account_mock'
descirbe 'Example', active_mocker:true do
  before do
    Person.create
  end
end

Person.column_names
  => ["id", "account_id", "first_name", "last_name", "address", "city"]
person = Person.new( first_name: "Dustin",
                                last_name: "Zeisler",
                                account: Account.new )
  => "#<PersonMock id: nil, account_id: nil, first_name: "Dustin", last_name: "Zeisler", address: nil, city: nil>"                         
person.first_name
  => "Dustin"
  
# db/schema.rb
ActiveRecord::Schema.defined(version: 20181109162322) do
  create_table "people", force: true do |t|
    t.integer "account_id"
    t.string "f_name", limit: 128
    t.string "l_name", limit: 128
    t.string "address", limit: 200
    t.string "city", limit: 100
  end
end

Person.new(first_name: "Dustin", last_name: "Zeisler")

User::ScopeRelation.new([User.new, User.new])

ActiveMocker::LoadedMocks.features.enable(:timestamps)
ActiveMocker::LoadedMocks.features.enable(:delete_all_before_example)
ActiveMocker::LoadedMocks.featrues.enbled(:stub_active_record_exceptions)

# ActiveMocker.safe_methods(scoped: [], instance_methods: [:full_name], class_methods: [])
class User
  def full_name
    "#{first_name} + #{last_name}"
  end
end

RSpec.configure do |config|
  config.mock_framework = :rspec
  config.mock_with :rspec do |mocks|
    mocks.verify_doubled_constant_names = true
    mocks.verify_partial_doubles = true
  end
end

Person.bar('baz')
  => NotImplementedError: ::bar is not Implemented for Class :PersonMock. TO continue stub the method.
allow(Person).to receive(:bar) do |name, type=nil|
  "Now implemented with #{name} and #{type}"
end
Person.bar('foo', 'type')

#app/models/person.rb
class Person < ActiveRecord::Base
  belongs_to :account
  def self.bar(name)
    puts name
  end
end

Person.bar('foo', 'type')
  => ArgumentError: wrong number of arguments (2 for 1)
  
# app/models/person.rb
class Person < AcitveRecord::Base
  belogns_to :account
  def self.foo(name, type=nil)
    puts name
  end
end

allow(Person).to recieve(:bar) do |name, type=nil|
  "Now implemented with #{name} and #{type}"
end

# ActiveMocker::Config.disable_modules_and_constants = true
class Person < AcitveRecord::Base
  CONSTANT_VALUE = 13
end

PersonMock::CONSTANT_VALUE
  => 13
  
require "acitve_mocker/rspec_helper"
active_mocker.delete_all
active_modker.find("User")
active_mocker.mocks.except("User").delete_all
```

```
bundle
gem install active_mocker
rake active:mocker:build
```

```
```
