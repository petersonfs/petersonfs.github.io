---
layout: post
title: "Ruby wrapper for Getclicky API"
date: 2011-08-18 21:38:08 -0300
categories: ruby
permalink: ruby-wrapper-for-getclicky-api
author: Peterson Santos
---

I participated in a project where it was necessary to connect to Getclicky API, so i decided to do a gem, and i’ll show you how it’s easy to use.

### Install Getclicky

The getclicky is available at [rubygems](https://rubygems.org/gems/getclicky), to install, you can just run the command below:

{% highlight bash %}
gem install getclicky
{% endhighlight %}

If you want to use with Ruby on Rails, remember to add the gem in yout Gemfile:

{% highlight bash %}
source :rubygems

gem "rails", "3.0.9"
gem "getclicky", "0.1.0"
{% endhighlight %}

### Setup your client

To access data from of Getclicky API, you need pass the site id and secret key in each request, and to configure it’s very easy, look:

{% highlight ruby %}
Getclicky.configure do |config|
  config.site_id = "32020"
  config.sitekey = "2e05fe2778b6"
end
{% endhighlight %}

### Client interface

To retrieve data it’s easy, you can call any type listed in getclicky documentation, i’ll show some examples:

{% highlight ruby %}
getclicky = Getclicky::Client.new

p getclicky.pages()
# => ...
p getclicky.tweets()
# => ...
p getclicky.visitors()
# => ...
{% endhighlight %}

In each method you can pass optional parameters acording the getclicky documentation, look:

{% highlight ruby %}
getclicky = Getclicky::Client.new

p getclicky.visitors(:date => "last-7-days", :daily => 1)
# => ...
p getclicky.item(:date => "last-7-days", :item => "google.com")
# => ...
p getclicky.visitors_list(:domain => "google.com")
# => ...
{% endhighlight %}

By default getclicky API returns XML, but you can change adding :output in parameter like this:

{% highlight ruby %}
getclicky = Getclicky::Client.new

## JSON
p getclicky.visitors(:output => :json, :date => "last-7-days", :daily => 1)
# => [{ "type": "visitors", "dates": [{"date": "2011-08-18" ...

## CSV
p getclicky.visitors(:output => :csv, :date => "last-7-days", :daily => 1)
# => # visitors # 2011-08-18 Item,Value,Value Percent...

## PHP
p getclicky.visitors(:output => :php, :date => "last-7-days", :daily => 1)
# => a:1:{s:8:"visitors";a:7:{s:10:"2011-08-18";
{% endhighlight %}

To handle all requests i use the gem called [Httparty](https://github.com/jnunemaker/httparty), and it’s very good becouse made easy work with the http protocol, that’s it!
