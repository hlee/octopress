---
layout: post
title: "ruby selenium-webdriver watir-webdriver"
date: 2011-10-26 08:12
comments: true
categories: [selenium-webdriver, rspec]
---

There are many other Selenium gems out there, but this is the only official, maintained gem. If you're looking for a slightly higher level API built on the same technology, you may want to check out [watir-webdriver](http://watirwebdriver.com/) or [capybara](https://github.com/jnicklas/capybara).
## example code
```ruby
require "selenium-webdriver"

driver = Selenium::WebDriver.for :firefox
driver.navigate.to "http://google.com"

element = driver.find_element(:name, 'q')
element.send_keys "Hello WebDriver!"
element.submit

puts driver.title

driver.quit

# execute arbitrary javascript
puts driver.execute_script("return window.location.pathname")

# pass elements between Ruby and JavaScript
element = driver.execute_script("return document.body")
driver.execute_script("return arguments[0].tagName", element) #=> "BODY"

# wait for a specific element to show up
wait = Selenium::WebDriver::Wait.new(:timeout => 10) # seconds
wait.until { driver.find_element(:id => "foo") }

# switch to a frame
driver.switch_to.frame "some-frame" # name or id
driver.switch_to.frame driver.find_element(:id, 'some-frame') # frame element

# switch back to the main document
driver.switch_to.default_content

# repositionning and resizing browser window:
driver.manage.window.move_to(300, 400)
driver.manage.window.resize_to(500, 800)
driver.manage.window.maximize

# get an attribute
class_name = element.attribute("class")

# is the element visible on the page?
element.displayed?

# click the element
element.click

# get the element location
element.location

# scroll the element into view, then return its location
element.location_once_scrolled_into_view

# get the width and height of an element
element.size

# press space on an element - see Selenium::WebDriver::Keys for possible values
element.send_keys :space

# get the text of an element
element.text
```

## SSL Certificates

The Firefox driver ignores invalid SSL certificates by default. If this is not the behaviour you want, you can do:
```ruby
profile = Selenium::WebDriver::Firefox::Profile.new
profile.secure_ssl = true

driver = Selenium::WebDriver.for :firefox, :profile => profile
```
There is an edge case where the default SSL certificate check will not work correctly. WebDriver assumes that the certificate is untrusted whenever there's a problem, which means a certificate from a trusted issuer but with a hostname mismatch (e.g. a production certificate in a test environment) will not be correctly ovverriden. See UntrustedSSLCertificates for more on why this is. To work around it, tell the Firefox driver to not assume the issuer is untrusted:
```ruby
profile = Selenium::WebDriver::Firefox::Profile.new
profile.assume_untrusted_certificate_issuer = false
driver = Selenium::WebDriver.for :firefox, :profile => profile
```
Not that Profile#secure_ssl remains set to the default value of true in the above example[.](http://code.google.com/p/selenium/wiki/RubyBindings)

