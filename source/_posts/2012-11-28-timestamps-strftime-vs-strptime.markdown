---
layout: post
title: "Timestamps strftime vs strptime"
date: 2012-11-28 06:20
comments: true
categories: [ruby, timestamp, strftime, strptime]
---


###strftime###

Formats date according to the directives in the given format string. The directives begins with a percent (%) character. Any text not listed as a directive will be passed through to the output string.

[source link](http://apidock.com/ruby/DateTime/strftime)

```ruby
puts Time.now.strftime("%FT%T%:z")

#  %F - The ISO 8601 date format (%Y-%m-%d)
#  %T - 24-hour time (%H:%M:%S)
#  %:z - hour and minute offset from UTC with a colon (e.g. +09:00)
#  output: 2012-11-28T06:29:36-05:00
```

###strptime###

Parses the given representation of date and time with the given template, and creates a date object.

[source link](http://apidock.com/ruby/DateTime/strptime/class)

```ruby
format = "%m/%d/%Y %H:%M:%S"
date_time = "11/28/2012 16:39:11.642"

date_obj = DateTime.strptime(date_time, format)
```


Any questions on this, please feel free to ask. We're here to help...
