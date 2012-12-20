---
layout: post
title: "how to use observer and call back"
date: 2012-11-12 15:07
comments: true
categories: [rails3] 
---
* Add configuration

```ruby
#config/application.rb
config.active_record.observers = :order_observer
```


* Create a Observer Class

```ruby
    class OrderObserver < ActiveRecord::Observer
      def after_update(order)
        order.update_column('type_state', "UPDATED")
      end
    end 
```
or we can use the way to register

```ruby
    #config/application.rb
    config.active_record.observers = :notification_observer

    class NotificationObserver < ActiveRecord::Observer
      observe :account, :balance

      def after_update(order)
        order.update_column('type_state', "UPDATED")
      end
    end 
```

Any questions on this, please feel free to ask. We're here to help...
