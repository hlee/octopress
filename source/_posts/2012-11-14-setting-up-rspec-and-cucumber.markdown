---
layout: post
title: "Setting up RSpec and Cucumber"
date: 2012-11-14 09:04
comments: true
categories: [rspec, cucumber, rails, tableish]
---

##Including RSpec in your code:##


**Add the following in your Gemfile**
File: Gemfile
```ruby
group :test, :development do
  gem "rspec-rails", "~> 2.0"
end
```

```sh
bundle
```

**Installing RSpec**
```sh
rails g rspec:install
```

**Configuring RSpec**

File: config/application.rb

```ruby
config.generators do |g|
  g.test_framework :rspec
  g.integration_tool :rspec
end
```

Now adding a new scaffold or resource will automatically include the RSpecs to help
test the code

```sh
rails g scaffold book title author
rake db:migrate
RAILS_ENV=test rake db:migrate
```

**Running the Specs**

```sh
rspec spec
```

You can also specify the file name and the line number for running individual
specs


##Including Cucumber in your Code##

**Add the following in your Gemfile**
File: Gemfile

```ruby
group :test, :development do
  gem 'cucumber-rails', require: false
end
```

**Installing Cucumber**

```sh
rails g cucumber:install
```

**For learners who are looking to setup the cucumber for the first time**

Use [Traing Wheels](https://github.com/cucumber/cucumber-rails-training-wheels)

File: Gemfile
```ruby
gem "cucumber-rails-training-wheels", :group => :test
```
**Installing Cucumber**
rails generate cucumber_rails_training_wheels:install

**Set up Cucumber Training Wheels before Scaffolding**

```sh
rails generate cucumber_rails_training_wheels:feature post title:string body:text number:integer published:boolean
rails generate scaffold post title:string body:text number:integer published:boolean
```

**Testing the Features**

```sh
cucumber features
```

**If you face Issues with Tableish in your features**

Replace:
```ruby
tableish('table tr', 'td,th')
```
With:
```ruby
find('table').all('tr').map { |row| row.all('th, td').map { |cell| cell.text.strip } }
```


Any questions on this, please feel free to ask. We're here to help...
