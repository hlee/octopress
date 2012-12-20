---
layout: post
title: "learn by practice extend and include"
date: 2010-03-25 18:07
comments: true
categories: [ruby, extend, include, metaprogram]
---
Here is some examples to help understand extend and include
```ruby
module M_A
  def test
    puts true
  end
end

module M_B
  def test
    puts false
  end
end

class A
  include M_A
  def meta_class
    class << A; self; end;
  end
end
A.test
A.new.test
A.instance_methods.grep /test/
A.new.meta_class.singleton_methods.grep /test/
class A
  include M_B
end
A.new.test

class B
  def B.meta_class
    class << B; self; end;
  end
  class << self
    def meta_class2
      class << B; self; end;
    end
  end
end

B.extend M_A
B.test
B.new.test
B.singleton_methods.grep /test/
B.meta_class.instance_methods.grep /test/
```
So class have singleton_methods, that should live in the meta_class and that method should be a instance method there
extend just put test method to meta class. then later one will cover the first one

result
```ruby

1.9.3p327 :048 > A.test
NoMethodError: private method `test' called for A:Class
    from (irb):48
    from /home/rharrington/.rvm/rubies/ruby-1.9.3-p327/bin/irb:16:in `<main>'
1.9.3p327 :049 > A.new.test
false
 => nil 
1.9.3p327 :050 > A.instance_methods.grep /test/
 => [:test] 
1.9.3p327 :051 > A.new.meta_class.singleton_methods.grep /test/
 => [] 
1.9.3p327 :052 > B.extend M_A
 => B 
1.9.3p327 :053 > B.test
true
 => nil 
1.9.3p327 :054 > B.new.test
NoMethodError: private method `test' called for #<B:0x0000000088c5e8>
    from (irb):54
    from /home/rharrington/.rvm/rubies/ruby-1.9.3-p327/bin/irb:16:in `<main>'
1.9.3p327 :055 > B.singleton_methods.grep /test/
 => [:test] 
1.9.3p327 :056 > B.meta_class.instance_methods.grep /test/
 => [:test] 


```

