---
layout: post
title: "retry and retry code blocks"
date: 2011-12-26 06:20
comments: true
categories: [block, retry, rescue]
---
## simple way to rescue and retry several
```ruby
tries = 0
begin
  # some routine
rescue
  tries += 1
  retry if tries <= 3
  puts "no dice!"
end
#or
3.times do
  begin
    ...
  rescue
    ...
  end
  break
end
```

## with_rescue

```ruby
class Integer
  def times_try
    n = self
    begin
      n -= 1
      yield
    rescue
      raise if n < 0
      retry
    end
  end
end

begin
  3.times_try do
    #some routine
  end
rescue
  puts 'no dice!'
end

```

if you don't want to define

```ruby
begin
  #your code
rescue
  retry if _r = (_r || 0) + 1 and _r < 4
  raise
end
```

```ruby
with_rescue(ProtocolError, :limit => 5) do |try|
  if try == 0
    self.send('HTTP/1.1')
  else
    self.send('HTTP/1.0')
  end
end
```

## Retry Block Code

```ruby
# Options:
# * :tries - Number of retries to perform. Defaults to 1.
# * :on - The Exception on which a retry will be performed. Defaults to Exception, which retries on any Exception.
#
# Example
# =======
#   retryable(:tries => 1, :on => OpenURI::HTTPError) do
#     # your code here
#   end
#
def retryable(options = {}, &block)
  opts = { :tries => 1, :on => Exception }.merge(options)

  retry_exception, retries = opts[:on], opts[:tries]

  begin
    return yield
  rescue retry_exception
    retry if (retries -= 1) > 0
  end

  yield
end
```

us it as

```ruby

retryable(:tries => 5, :on => OpenURI::HTTPError) do
  open('http://example.com/flaky_api')
  # Code that mashes up stuff for your "social networking" site.
end
```

Here are the <tt>[Kernel#retryable specs (pastie)](http://pastie.caboo.se/138570)</tt>[.](http://blog.codefront.net/2008/01/14/retrying-code-blocks-in-ruby-on-exceptions-whatever/)

