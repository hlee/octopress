---
layout: post
title: "ruby timeout"
date: 2012-12-09 06:56
comments: true
categories: [ruby, rescue, timeout, exception]
---

## standard timeout 
```ruby
require 'timeout'
begin
  complete_results = Timeout.timeout(1) do      
   sleep(2)
  end
rescue Timeout::Error
  puts 'Print me something please'
end
```

sometime, the code inner with begin will catch exception
such as:
```ruby
require 'timeout'
 
puts "#{Time.now}: Starting"
begin
  Timeout.timeout(5) do
    begin
      sleep 10
    rescue Exception => e
      puts "#{Time.now}: Caught an exception: #{e.inspect}"
    end
    sleep 10
  end
rescue Timeout::Error => e
  puts "#{Time.now}: Timeout: #{e}"
else
  puts "#{Time.now}: Never timed out."
end
```
so new a thread, as ruby 1.9 thread is native
```ruby
begin
  complete_results = Timeout.timeout(4) do
    Thread.new{ results = platform.search(artist, album_name) }.value
  end
rescue Timeout::Error
  puts 'Print me something please'
end 
```

##implementation

```ruby
# From lib/timeout.rb

def timeout(sec, exception=Error)
  return yield if sec == nil or sec.zero?
  raise ThreadError, "timeout within critical session" if Thread.critical
  begin
    x = Thread.current
    y = Thread.start {
      sleep sec
      x.raise exception, "execution expired" if x.alive?
    }
    yield sec
    #    return true
  ensure
    y.kill if y and y.alive?
  end
end
```
system timer only for 1.8[.](http://ph7spot.com/musings/system-timer)
