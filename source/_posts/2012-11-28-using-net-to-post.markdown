---
layout: post
title: "Using NET to Post API Calls With or Without Secure Connections"
date: 2012-11-28 06:45
comments: true
categories: [ruby, net]
---

Using Net module is the best and the eaiest ways to post data or make api calls
to urls. Here's an example



```ruby

def post_using_net(url, params={})
  uri = URI.parse(url)
  http = Net::HTTP.new(uri.host, uri.port)
  http.use_ssl = true
  http.verify_mode = OpenSSL::SSL::VERIFY_NONE
  response = http.post(uri.request_uri, params.to_query)
  response
end
```


for connections that does not use ssl i.e (https) the following can be removed


```ruby
  http.use_ssl = true
  http.verify_mode = OpenSSL::SSL::VERIFY_NONE

```


Net also handles get, put and delete, to make it work for muliple requests,
just use a send to make calls to the methods

```ruby
def send_using_net(method, url, params={})
  uri = URI.parse(url)
  http = Net::HTTP.new(uri.host, uri.port)
  http.use_ssl = true
  http.verify_mode = OpenSSL::SSL::VERIFY_NONE
  response = http.send method, [uri.request_uri, params.to_query]
  response
end
```

Any questions on this, please feel free to ask. We're here to help...
