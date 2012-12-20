---
layout: post
title: "Working with Digests and Signatures"
date: 2012-11-28 05:53
comments: true
categories: [ruby, md5, hmac sha1]
---

###MD5 digests###
MD5 is a one-way hashing algorithm for creating digest "signatures" or checksums of strings. MD5 digests are 128 bit (16 byte) signatures. MD5 is the most common method of providing checksums for files downloaded over the internet.
To create a checksum of an entire file or text convert the whole string. 


```ruby
digest = Digest::MD5.hexdigest(string_to_digest)
```

[source link](http://www.siaris.net/index.cgi/Programming/LanguageBits/Ruby/MD5.rdoc)

###hmac-sha1###

In cryptography, a hash-based message authentication code (HMAC) is a specific construction for calculating a message authentication code (MAC) involving a cryptographic hash function in combination with a secret cryptographic key. As with any MAC, it may be used to simultaneously verify both the data integrity and the authenticity of a message.

[source link](http://en.wikipedia.org/wiki/Hash-based_message_authentication_code)

In ruby its simple to generate one:

```ruby
gem install ruby-hmac

def hmac_sha1 params={}
  require 'openssl'
  secret_key = 'No telling a secret'
  OpenSSL::HMAC.hexdigest('sha1', secret_key, params)
end
```

Any questions on this, please feel free to ask. We're here to help...
