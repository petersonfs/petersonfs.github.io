---
layout: post
title: "Using Redis as Rails Cache Store"
date: 2011-09-09 21:38:08 -0300
categories: ruby
permalink: using-redis-as-rails-cache-store
author: Peterson Santos
---

If you want to use redis as your cache store, i recommend you checkout the Redis Store, see the github repo:

[https://github.com/jodosha/redis-store.](https://github.com/jodosha/redis-store)

It provides a lot of features, to powerful your application like:

* Namespaced Rack::Session
* Rack::Cache
* i18n
* Cache Redis stores for Ruby web frameworks

### How to setup?

First step it’s add gem in your Gemfile and run bundle command to install:

{% highlight bash %}
gem "redis-store", "~> 1.0.0.1"
{% endhighlight %}

{% highlight bash %}
bundle install
{% endhighlight %}

It’s almost done, the last step is change how your Rails application will store the cache.
Go to config/environments/production.rb and change to something like this:

{% highlight bash %}
config.cache_store = :redis_store
{% endhighlight %}

Now you are ready! From now all rails cache will be stored on Redis.
