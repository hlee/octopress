---
layout: post
title: "capybara webkit or selenium or watir to simulate browser behavior"
date: 2012-12-06 15:29
comments: true
categories: [ruby, selenium, capybara, webkit]
---

Sometimes we want to simulate browser behavior. The situation can be test or automation script.

##install capybara-webkit
```ruby
#capybara-webkit need qt
#ubuntu
sudo aptitude install libqt4-dev
```
##using capybara dsl
```ruby
require 'capybara'
require 'capybara/dsl'

Capybara.default_driver = :webkit

module MyModule
  include Capybara::DSL

  def login!
    within("//form[@id='session']") do
      fill_in 'Login', :with => 'user@example.com'
      fill_in 'Password', :with => 'password'
      fill_in('First Name', :with => 'John')
      fill_in('Password', :with => 'Seekrit')
      fill_in('Description', :with => 'Really Long Text...')
      choose('A Radio Button')
      check('A Checkbox')
      uncheck('A Checkbox')
      attach_file('Image', '/path/to/image.jpg')
      select('Option', :from => 'Select Box')
      end
      click_link 'Sign in'
  end
end
```
## Debugging

It can be useful to take a snapshot of the page as it currently is and take a
look at it:

```ruby
save_and_open_page
```

You can also retrieve the current state of the DOM as a string using
<tt>[page.html](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/Session#html-instance_method)</tt>.

```ruby
print page.html
```

This is mostly useful for debugging. You should avoid testing against the
contents of `page.html` and use the more expressive finder methods instead.

Finally, in drivers that support it, you can save a screenshot:

```ruby
page.save_screenshot('screenshot.png')
```

## Calling remote servers

Normally Capybara expects to be testing an in-process Rack application, but you
can also use it to talk to a web server running anywhere on the internets, by
setting app_host:

```ruby
Capybara.current_driver = :selenium
Capybara.app_host = 'http://www.google.com'
...
visit('/')
```

**Note**: the default driver (`:rack_test`) does not support running
against a remote server. With drivers that support it, you can also visit any
URL directly:

```ruby
visit('http://www.google.com')
```

By default Capybara will try to boot a rack application automatically. You
might want to switch off Capybara's rack server if you are running against a
remote application:

```ruby
Capybara.run_server = false
```

## Using the sessions manually

For ultimate control, you can instantiate and use a
[Session](http://rubydoc.info/github/jnicklas/capybara/master/Capybara/Session)
manually.

```ruby
require 'capybara'

session = Capybara::Session.new(:webkit, my_rack_app)
session.within("//form[@id='session']") do
  session.fill_in 'Login', :with => 'user@example.com'
  session.fill_in 'Password', :with => 'password'
end
session.click_link 'Sign in'
```

## XPath, CSS and selectors

Capybara does not try to guess what kind of selector you are going to give it,
and will always use CSS by default.  If you want to use XPath, you'll need to
do:

```ruby
within(:xpath, '//ul/li') { ... }
find(:xpath, '//ul/li').text
find(:xpath, '//li[contains(.//a[@href = "#"]/text(), "foo")]').value
```

Alternatively you can set the default selector to XPath:

```ruby
Capybara.default_selector = :xpath
find('//ul/li').text
```

Capybara allows you to add custom selectors, which can be very useful if you
find yourself using the same kinds of selectors very often:

```ruby
Capybara.add_selector(:id) do
  xpath { |id| XPath.descendant[XPath.attr(:id) == id.to_s] }
end

Capybara.add_selector(:row) do
  xpath { |num| ".//tbody/tr[#{num}]" }
end

Capybara.add_selector(:flash_type) do
  css { |type| "#flash.#{type}" }
end
```

The block given to xpath must always return an XPath expression as a String, or
an XPath expression generated through the XPath gem. You can now use these
selectors like this:

```ruby
find(:id, 'post_123')
find(:row, 3)
find(:flash_type, :notice)
```

You can specify an optional match option which will automatically use the
selector if it matches the argument:

```ruby
Capybara.add_selector(:id) do
  xpath { |id| XPath.descendant[XPath.attr(:id) == id.to_s] }
  match { |value| value.is_a?(Symbol) }
end
```

Now use it like this:

```ruby
find(:post_123)
```

This :id selector is already built into Capybara by default, so you don't
need to add it yourself[.](https://github.com/jnicklas/capybara)

