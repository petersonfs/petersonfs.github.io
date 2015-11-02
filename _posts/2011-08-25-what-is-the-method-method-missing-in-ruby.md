---
layout: post
title: "What is the method method_missing in Ruby?"
date: 2011-08-25 21:38:08 -0300
categories: ruby
permalink: what-is-the-method-method-missing-in-ruby
author: Peterson Santos
headline: "Do you really know how 'method_missing' works? Check it out :)"
---

If you began studying ruby and went looking for some gems, probably should have seen a method called “method_missing” and should probably not have understood anything (at least i didn’t understand the first time). So will a brief explanation of what it’s and how it can help in our implementation.

### Definition

It’s callback method you can implement that gets called when a object tries to call a method that’s missing. Take a look in a sample, that show how it works:

{% highlight ruby %}
# Create class without method_missing and see your behavior
#
class Person; end

person = Person.new
puts person.walk
# => undefined method ‘walk’ for #<Person:0x007fd7108491c8>

# Create a class and implement the method missing and see your behavior
#
class Person
  def method_missing(method, *args)
    "Hello i'm a method missing"
  end
end

person = Person.new
puts person.walk
# => Hello i'm a method missing
{% endhighlight %}

### Real examples

If you study or work with ruby, probably you should heard about the ruby on rails. With ruby on rails we can create the find methods dynamically, like this:

{% highlight ruby %}
class Person < ActiveRecord::Base
  attr_accressor :first_name, :last_name, :age
end

person.find_by_first_name("Peterson")
person.find_by_last_name("Ferreira")
person.find_by_age(22)
{% endhighlight %}

Notice that we don’t have implemented the above methods in the class called Person, and still managed to call them. But the example above we use only with ActiveRecord, let’s go implement our own dynamics methods and see how method_missing works:

{% highlight ruby %}
class Person
  attr_accessor :first_name, :last_name, :age, :match

  def initialize(first_name, last_name, age)
    @first_name, @last_name, @age = first_name, last_name, age
  end

  def find(params = {})
    params.each do |name, value|
      puts "#{value}"
    end
  end

  def method_missing(method, *args)  
    # Get the first word later expression: find_by_
    # and call the method find with right parameters
    # else delegate the responsability for ancestor
    if method.to_s =~ /^find_by_(.*)$/
      find($1.to_sym => args.first)
    else
      super
    end
  end

  def respond_to?(method, include_private = false)
    if method.to_s =~ /^find_by_(.*)$/
      true
    else
      super
    end
  end
end

person = Person.new("Peterson", "Ferreira", 2)

person.find_by_first_name("Peterson")
person.find_by_last_name("Ferreira")
person.find_by_age(22)
{% endhighlight %}

### Little tip

* Everytime you implement the method method_missing, for maintain the consistency of your API implement the same logic in method respond_to?.
* You can implement the logic of matcher in separated class to DRY your code.
