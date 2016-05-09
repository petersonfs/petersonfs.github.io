---
layout: post
title: "Understanding Include and Extend in Ruby"
date: 2011-08-13 21:38:08 -0300
categories: ruby
permalink: understanding-include-and-extend-in-ruby
author: Peterson Santos
headline: "Checkout the article to understand how 'include' and 'extend' works in ruby"
---

In Ruby has a couple of ways to combine the methods of two classes. Classes are collections of related methods and data members. Two classes can combine their methods using the include or extend statements. Both of these statements are specialized for a different purpose, the include add instance methods to your class, and extend add class methods. Look’s the example below:

{% highlight ruby %}
module Person
  def walk
    puts "Walking..."
  end
end

class Woman
  include Person
end

class Man
  extend Person
end

# Class methods
Woman.walk
# => undefined method ‘walk’ for Woman:Class
Man.walk
# => Walking...

# Instance methods
Woman.new.walk
# => Walking...
Man.new.walk
# => undefined method ‘walk’ for #
{% endhighlight %}

## Understanding

#### Include

Behind the scenes, when we include a module in a class, that Ruby does is put the module constants, methods, and module variables in the instance of the class if the module has not been included in one of the ancestors.
To help us Ruby already has some methods to work around the include:


{% highlight ruby %}
# +include?+
# Returns true if a module was included in the class or one of yours ancestors
p Woman.include?(Person)
# => true
p Man.include?(Person)
# => false

# +included+
# Included it's a callback that's called everytime you include a module
module Person
  def walk
    puts "Walking..."
  end

  def self.included(mod)
    puts "#{self} included in #{mod}"
  end
end

class Children
  include Person
end
# => Person included in Children

# +included_modules+
# Returns an array of modules included
p Children.included_modules
# => [Person, Kernel]
{% endhighlight %}

#### Extend

Behind the scenes, when we use the extend, the Ruby simply add class methods to our object.
We have two callbacks that run when a module has extended, the both work’s equal:

{% highlight ruby %}
module Person  
  def self.extend_object(object)
     puts "#{self} added to #{object}"
     super
  end

  def self.extended(object)
     puts "#{self} added to #{object}"
     super
  end
end

class Baby
  extend Person
end
# => Person added to Baby
# => Person added to Baby
{% endhighlight %}

### Conclusion

Use include for instance methods and extend to class methods. Then we can reuse a lot of code and we can modularize our code, and include or extend as we want in a way that only the ruby can do.
