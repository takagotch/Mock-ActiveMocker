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



```

```
bundle
gem install active_mocker
rake active:mocker:build
```

```
```
