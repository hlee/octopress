---
layout: post
title: "Passing Command Line Arguments to Rake Tasks"
date: 2012-11-28 08:02
comments: true
categories: [ruby, rake, 'command line'] 
---
Sometimes, we need to rake tasks that inserts a paticular user entered value into multiple databases.

We'd like to be able to pass this value into the rake task from the command line, or from another rake task, how can We do this?


```ruby
require 'rake'

task :my_task, :arg1, :arg2 do |t, args|
  puts "Args were: #{args}"
end
```

You can invoke it by using the following:

```ruby
task :invoke_my_task do
  Rake.application.invoke_task("my_task[1, 2]")
end
```

or if you prefer this syntax...

```ruby
task :invoke_my_task_2 do
  Rake::Task[:my_task].invoke(3, 4)
end
```

A task with prerequisites passes its arguments to it prerequisites(tasks)

```ruby
task :with_prerequisite, :arg1, :arg2, :needs => :my_task
```

or just a...

```ruby
task :with_prerequisite, [:arg1, :arg2] => :my_task
```

To specify default values, we take advantage of args being a Rake::TaskArguments object

```ruby
task :with_defaults, :arg1, :arg2 do |t, args|
  args.with_defaults(:arg1 => 1, :arg2 => 2)
  puts "Args with defaults were: #{args}"
end
```

Here are a few usages:

```sh
> rake my_task[1,2]
Args were: {:arg1=>"1", :arg2=>"2"}

> rake "my_task[1, 2]"
Args were: {:arg1=>"1", :arg2=>"2"}

> rake invoke_my_task
Args were: {:arg1=>"1", :arg2=>"2"}

> rake invoke_my_task_2
Args were: {:arg1=>3, :arg2=>4}

> rake with_prerequisite[5,6]
Args were: {:arg1=>"5", :arg2=>"6"}

> rake with_prerequisite_2[7,8]
Args were: {:arg1=>"7", :arg2=>"8"}

> rake with_defaults
Args with defaults were: {:arg1=>:default_1, :arg2=>:default_2}

> rake with_defaults['x','y']
Args with defaults were: {:arg1=>"x", :arg2=>"y"}
```


[For more information...](http://rake.rubyforge.org/files/doc/rakefile_rdoc.html)

[.](http://stackoverflow.com/questions/825748/how-do-i-pass-command-line-arguments-to-a-rake-task)

Any questions on this, please feel free to ask. We’re here to help…
