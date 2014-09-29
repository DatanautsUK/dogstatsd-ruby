
dogstatsd-ruby
==============

A client for DogStatsD, an extension of the StatsD metric server for Datadog.

[![Build Status](https://secure.travis-ci.org/DataDog/dogstatsd-ruby.png)](http://travis-ci.org/DataDog/dogstatsd-ruby)

Quick Start Guide
-----------------

First install the library:

    gem install dogstatsd-ruby

Then start instrumenting your code:

``` ruby
# Load the dogstats module.
require 'statsd'

# Create a stats instance.
statsd = Statsd.new('localhost', 8125)

# Increment a counter.
statsd.increment('page.views')

# Record a gauge 50% of the time.
statsd.gauge('users.online', 123, :sample_rate=>0.5)

# Sample a histogram
statsd.histogram('file.upload.size', 1234)

# Time a block of code
statsd.time('page.render') do
  render_page('home.html')
end

# Send several metrics at the same time
# All metrics will be buffered and sent in one packet when the block completes
statsd.batch do |s|
  s.increment('page.views')
  s.gauge('users.online', 123)
end

# Tag a metric.
statsd.histogram('query.time', 10, :tags => ["version:1"])
```

You can also post events to your stream. You can tag them, set priority and even aggregate them with other events.

Aggregation in the stream is made on hostname/event_type/source_type/aggregation_key.

``` ruby
# Post a simple message
statsd.event("There might be a storm tomorrow", "A friend warned me earlier.")

# Cry for help
statsd.event("SO MUCH SNOW", "Started yesterday and it won't stop !!", :alert_type => "error", :tags => ["urgent", "endoftheworld"])
```



Documentation
-------------

Full API documentation is available
[here](http://www.rubydoc.info/github/DataDog/dogstatsd-ruby/master/frames).


Feedback
--------

To suggest a feature, report a bug, or general discussion, head over
[here](http://github.com/DataDog/dogstatsd-ruby/issues/).


Change Log
----------

- 1.4.1
    - Fixed bug in message separator when batching metrics
- 1.4.0
    - Added support for metrics batching
- 1.3.0
    - Added support for submitting events.
- 1.2.0
    - Added global tags.
    - Added ability to set `namespace` and `tags` from `Statsd#initialize`.
- 1.1.0
    - Added `sets` metrics.
- 1.0.0
    - Initial release.


Credits
-------

dogstatsd-ruby is forked from Rien Henrichs [original Statsd
client](https://github.com/reinh/statsd).

Copyright (c) 2011 Rein Henrichs. See LICENSE.txt for
further details.
