---
layout: post
title: "rspec test failed after changing to capybara-webkit"
date: 2012-12-09 06:03
comments: true
categories: [rspec, capybara-webkit]
---
## problem as
written some RSpec test for my rails 3.2 application and because I was annyoed by the Browser popping up ich tried to change from firefox to capybara-webkit. After this all tests still run, except one. The line that is failing is:
```ruby
expect { click_button "Create" }.to change(Answer, :count).by(count)
```

solution is easy, The simplest way to resolve this is to wait before checking:
```ruby
expect { click_button "Create"; sleep 2 }.to change(Answer, :count).by(count)
```
There is a race condition here between Capybara sending the click action to the server and your test checking the database.
