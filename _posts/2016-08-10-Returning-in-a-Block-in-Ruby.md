---
layout: post
title: Returning in a Block in Ruby
---

Today I came across some code that looked something like:

```ruby
def reminder_times
  User.reduce({}) do |h, user|
    return h unless user.wants_reminder?

    h[user.id] = user.preferences['reminder_time']

    h
  end
end
```

The developer wanted to build a hash of reminder times for users who wanted
a reminder. There were a couple of problems with this code.

### Return vs Break vs Next

The main problem becomes readily apparent if you try to run the code inside the
method directly in IRB. It will raise a `LocalJumpError`. This is because
`return` does not break out of and continue the block as the developer intended.
It breaks out of the method. If you run this code without a method to break out
of, you will receive a `LocalJumpError`.

Instead, the developer should have used the `next` keyword to continue looping
through the block. Alternatively, you can use `break` to exit a block. Only use
`return` if you want to exit a method.

### Reducing a Hash

The other issue was using `reduce` to build a simple hash. It didn't really make
sense to me to use `reduce` since you don't really need to cumulatively "add" to
the hash to build it. You just start with an empty hash and set key-value pairs.

### Solution

There are different ways I could have fixed the code, but I chose to go with:

```ruby
def reminder_times
  Hash.new.tap do |h|
    User.each do |user|
      next unless user.wants_reminder?

      h[user.id] = user.preferences['reminder_time']
    end
  end
end
```

(The `tap` method was just a way for me to return the new hash without having to
explicitly assign and return it.)

If I *really* wanted to use `reduce` to build a hash, I suppose I would have
done:

```ruby
def reminder_times
  User.reduce({}) do |h, user|
    h.merge({ user.id => user.preferences['reminder_time'] }) if user.wants_reminder?
  end
end
```
