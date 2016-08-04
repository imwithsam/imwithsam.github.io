---
layout: post
title: Redis Keyspace Notifications Using Ruby and Heroku
---

I recently worked on a Slack Bot written in Ruby using Redis for its
conversational state machine. I wanted users to receive a notification anytime
the conversation timed out (when the Redis key expired). The ideal solution was
for Redis to let me know whenever this happened. Luckily, as of v2.8, we have
[Redis Keyspace Notifications](http://redis.io/topics/notifications)!

The documentation on using Redis and Keyspace Notifications with Ruby and Heroku
is surprisingly sparse so I had to do a bit of research and experimentation to
get this to work. I hope this post saves some of you out there some time.

### Configuration

The Redis Keyspace Notifications feature is disabled by default. You can enable
it via the `CONFIG SET` command for `notify-keyspace-events`. If you're using
the [redis-rb](https://github.com/redis/redis-rb) library, it can
be programmatically configured like this:

```ruby
r = Redis.new
r.config(:set, 'notify-keyspace-events', 'xE')
```

(You can verify your all of your configuration settings using `r.config(:get,
'*')`.)

If you refer to the configuration table in the [Redis Keyspace
Notifications](http://redis.io/topics/notifications) docs you'll see that `xE`
will enable notifications for expired keyevent events, which is exactly what I
was looking for. You may need to change this setting for your purposes. Setting
it to `KEA` will enable notifications for all events. It's useful to set it to
this initially to make sure you're picking up event notifications and to see
exactly what kind of data you're getting back.

### Pattern Subscribe

After you've configured `notify-keyspace-events` you'll need to subscribe to
listen for the events. `PSUBSCRIBE` will subscribe the client to a glob-style
pattern. This is useful because keyevent events will publish to a channel named
something like

```
__keyevent@0__:expired
```

where `0` is the database instance and `expired` is the event. (Note that the
event is `expired`, and not `expire` as you might assume from the Redis
documentation.) Using this pattern, you can subscribe just to Redis key
expiration events.

```ruby
r.psubscribe('__keyevent@*__:expired') do |on|
  on.pmessage do |pattern, channel, message|
    puts "pattern: #{pattern}"
    puts "channel: #{channel}"
    puts "message: #{message}"
  end
end
```

The message is the Redis key that expired. I initially tested this by setting up
a key to expire after 10 seconds then running the above code. e.g.

```
r.set('my_key', 'my_value', ex: 10)
```

And voila, it's just that easy!

I just put my code into a rake task and set it up to run as a separate worker
process in my Procfile.

### Heroku Redis vs Redis Cloud

My code worked fine on Development, but would blow up on the Redis config line
on Acceptance and Production. We were using the Heroku Redis add-on. At the time
of writing, Heroku Redis did not support configuring Keyspace Notifications.
After experimenting with different Redis add-ons, I was finally able to get the
configuration set using the Heroku **Redis Cloud** add-on.
