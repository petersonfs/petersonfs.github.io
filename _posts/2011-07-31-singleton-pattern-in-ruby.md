---
layout: post
title: "Singleton Pattern in Ruby"
date: 2011-07-31 21:38:08 -0300
categories: ruby
permalink: singleton-pattern-in-ruby
author: Peterson Santos
---

The [Singleton](http://en.wikipedia.org/wiki/Singleton_pattern) pattern is designed so that the object is instantiated only once during each execution. And to use it in Ruby could not have an easy and elegant way, just include the module [Singleton](http://www.ruby-doc.org/stdlib/libdoc/singleton/rdoc/index.html):

{% highlight ruby %}
require 'singleton'

class Factory
  include Singleton
end
{% endhighlight %}

But careful to use, when added the module Singleton the new and allocate methods become private, to see just run:

{% highlight ruby %}
p Factory.private_methods
#=> [:new, :allocate,...]
{% endhighlight %}

To get instance of your class and check if singleton pattern works, it’s easy:

{% highlight ruby %}
sample = Factory.instance
other_sample = Factory.instance
p sample == other_sample
#=> true
{% endhighlight %}

I don’t know if other languages make’s it’s so easy.
