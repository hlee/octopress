---
layout: post
title: "generate random string in ruby"
date: 2012-11-28 22:39
comments: true
categories: [ruby, random, string] 
---

Sometimes we need to generate a 'n' character random string.

Here are a few:

- **Only upper case alphabets [A-Z]**

```ruby
value = ""; 
8.times{value  << (65 + rand(25)).chr} >>}
#or
(0...8).map{65.+(rand(26)).chr}.join
(0...8).map{ ('A'..'Z').to_a[rand(26)]  }.join
```

- **Lower case and upper case [a-zA-Z]**

```ruby
value = ""; 
8.times{value << ((rand(2)==1?65:97) + rand(25)).chr} >>}
#or
o =  [('a'..'z'),('A'..'Z')].map{|i| i.to_a}.flatten
string  =  (0...50).map{ o[rand(o.length)]  }.join
```

- **Using SecureRandom provided by ActiveSupport**

```ruby
require 'active_support/secure_random'
random_string = ActiveSupport::SecureRandom.hex(16)

# outputs: 5b5cd0da3121fc53b4bc84d0c8af2e81
```

- SecureRandom also has methods for: 

base64

1. hex
2. random_bytes
3. random_number

[see:](http://api.rubyonrails.org/v3.0.9/classes/ActiveSupport/SecureRandom.html)

- **It is also important to avoid Ambiguity**

```ruby
# Generates a random string from a set of easily readable characters
def generate_activation_code(size = 6)
  charset = %w{ 2 3 4 6 7 9 A C D E F G H J K M N P Q R T V W X Y Z}
  (0...size).map{ charset.to_a[rand(charset.size)] }.join
end
```

- **Random URL Friendly Strings**

```ruby
rand(36**length).to_s(36)
```

- **One more example with SecureRandom**

```ruby
require 'securerandom'
s = SecureRandom.urlsafe_base64(20)
```


- **Creating a Random string with arguments**

```ruby
def random_string(length=10)
  chars = 'abcdefghjkmnpqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ23456789'
  password = ''
  length.times { password << chars[rand(chars.size)] }
  password
end
```


- **This example works Only in ruby 1.9**

```ruby
[*('A'..'Z')].sample(8).join
#Generate a random 8 letter string (e.g. NVAYXHGR)

([*('A'..'Z'),*('0'..'9')]-%w(0 1 I O)).sample(8).join
#Generate a random 8 character string (e.g. 3PH4SWF2), excludes 0/1/I/O. Ruby 1.9
ALPHABET = ('a'..'z').to_a
10.times.map{ ALPHABET.sample }.join
10.times.inject(''){|s| s << ALPHABET.sample }
```

- **Here's one using digest sha1**

```ruby
require 'sha1'
srand
seed = "--#{rand(10000)}--#{Time.now}--"
Digest::SHA1.hexdigest(seed)[0,8]
```

- **Here are more examples to help**

- Example 1

```ruby
rand(2**256).to_s(36)[0..7]
#Add ljust if you are really paranoid about the correct string length:
rand(2**256).to_s(36).ljust(8,'a')[0..7]
characters = ('a'..'z').to_a + ('A'..'Z').to_a
# Prior to 1.9, use .choice, not .sample
(0..8).map{characters.sample}.join
(0...8).collect { |n| value  << (65 + rand(25)).chr }.join()
```


- Example 2

```ruby
def generate_random_string(length=6)
  string = ""
  chars = ("A".."Z").to_a
  length.times do
    string << chars[rand(chars.length-1)]
  end
  string
end
```


- Example 3
```ruby
chars = [*('a'..'z'),*('0'..'9')].flatten
#Single expression, can be passed as an argument, allows duplicate characters:
Array.new(len) {|i| chars.sample}.join
```


- Example 4

```ruby
def token(length=16)
  chars = [*('A'..'Z'), *('a'..'z'), *(0..9)]
  (0..length).map {chars.sample}.join
end
```

- Example 5
```ruby
''.tap {|v| 4.times { v << ('a'..'z').to_a.sample} }
```

- Example 6
```ruby
class String

  def self.random(length=10)
    ('a'..'z').sort_by {rand}[0,length].join
  end

end
```

- Example 7
```ruby
(('a'..'z').to_a + ('A'..'Z').to_a + (0..9).to_a).sample(8).join

([(48..57),(65..90),(97..122)]).sample(8).collect{|x|x.chr}""
```

- Example 8
```ruby
def secure_random_string(length = 32, non_ambiguous = false)
  characters = ('a'..'z').to_a + ('A'..'Z').to_a + ('0'..'9').to_a

  %w{I O l 0 1}.each{ |ambiguous_character| 
    characters.delete ambiguous_character 
  } if non_ambiguous

  (0...length).map{
    characters[ActiveSupport::SecureRandom.random_number(characters.size)]
  }.join
end
```

- Example 9 
```ruby
SecureRandom.base64(15).tr('+/=lIO0', 'pqrsxyz')
# ruby 1.8 and unix
random_string = `openssl rand -base64 24`
```

[.](http://stackoverflow.com/questions/88311/how-best-to-generate-a-random-string-in-ruby)
