---
layout: post
title: "Minimal compass integration for Rails 3.1"
date: 2011-08-31 21:38:08 -0300
categories: ruby
permalink: minimal-compass-integration-for-rails-3-1
author: Peterson Santos
headline: "A simple example of compass integration with rails 3.1"
---

If you like to use the [compass](http://compass-style.org), and want integrate it with Rails 3.1 asset pipeline are necessary to make some settings:

#### config/application.rb

{% highlight ruby %}
module Compass
  RAILS_LOADED = true
end

if defined?(Bundler)
  Bundler.require(:default, :assets, Rails.env)
end

module MyPrecious
  class Application < Rails::Application
    config.assets.enabled = true
    # that's it!
    config.sass.load_paths << Compass::Frameworks['compass'].stylesheets_directory
  end
end
{% endhighlight %}

#### Gemfile

{% highlight ruby %}
group :assets do
  gem 'sass-rails', '~> 3.1.0'
  gem 'coffee-rails', '~> 3.1.0'
  gem 'uglifier'
  gem 'compass'
end
{% endhighlight %}

### Note

These instructions are only valid until Compass version 0.12 goes stable. Then the hack won’t be necessary.

Skips all of the nasty and bloated old Compass Rails integration. No need for that confusing “config/compass.rb” file, either.

Note that this will only work for simple stylesheets and probably needs extra configuration for stuff like sprites.
