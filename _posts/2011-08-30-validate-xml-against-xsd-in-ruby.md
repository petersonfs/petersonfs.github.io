---
layout: post
title: "Validate XML against XSD (Schema) in Ruby"
date: 2011-08-30 21:38:08 -0300
categories: ruby
permalink: validate-xml-against-xsd-in-ruby
author: Peterson Santos
---

I began this week to do a small project where one of its features is to validate a given xml against an schema. In the ruby ecosystem we have several options for working with xml, and i chose nokogiri, where he met my needs very well.

### What is Nokogiri ?

Is an HTML, XML, SAX, and Reader parser. Among Nokogiri’s many features is the ability to search documents via XPath or CSS3 selectors. [See more](http://nokogiri.org/Nokogiri.html)

### Install Nokogiri

The nokogiri is available at [rubygems](http://rubygems.org/gems/nokogiri), to install, just run the command below:

{% highlight bash %}
gem install nokogiri
{% endhighlight %}

### Validate against a XSD Document (Schema)

The class below it’s a simple abstraction to validate the xml against xsd, look:

{% highlight ruby %}
require "nokogiri"

class ValidateXml
  attr_accessor :document, :schema

  def initialize(document_path)
    read_document(document_path)
  end

  def validate(schema_path)
    read_schema(schema_path)
    @schema.validate(@document)
  end

  private
  def read_schema(schema_path)
    @schema = Nokogiri::XML::Schema(File.read(schema_path))
  end

  private
  def read_document(document_path)
    @document = Nokogiri::XML(File.read(document_path))
  end
end
{% endhighlight %}

To validate your xml against xsd, call the method validate, and pass the path for xsd, like below:

{% highlight ruby %}
xml = ValidateXml.new("document.xml")

p xml.validate("schema.xsd")
# => [#]
{% endhighlight %}

The method validate will return the object [Nokogiri::XML::SyntaxError](http://nokogiri.rubyforge.org/nokogiri/Nokogiri/XML/SyntaxError.html), then you can iterate through error messages, like this:

{% highlight ruby %}
xml = ValidateXml.new("document.xml")

xml.validate("schema.xsd").each do |error|
  puts error.message
end
# => Element 'review': This element is not expected. Expected is ( pub_date ).
{% endhighlight %}

The examples used are hosted in: [http://msdn.microsoft.com/en-us/library/ms764613](http://msdn.microsoft.com/en-us/library/ms764613)

To see the power of nokogiri, look the official documentation site at: [http://nokogiri.org](http://nokogiri.org)
