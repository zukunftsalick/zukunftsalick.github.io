---
layout: post
published: true
title: Method dispatch in Ruby
author: Pedro Pimentel
date: 2009-12-15 17:38:11.000000000 +08:00
cover: http://farm6.staticflickr.com/5489/11723537295_ba713114a7_b.jpg 
categories:
- ruby
tags:
- ruby
- dispatcher
- interpreter
- mri
- method
---
Some days ago I was asked how the dispatcher works in ruby and I was caught in surprise I didn't know how to explain the method dispatching in the language we love (Ruby). That question was kept still in my mind for a few days but while listening to some workmates discussing about singleton classes in ruby the answer came to my mind in a blink of eyes reminding me from a university class which I had a long time ago about how method dispatching works in dynamic languages like Ruby.

So with that information in mind and some googling to confirm it I came out with a simple explanation of how the dispatching works in Ruby and decided it's worth sharing you.

Essentially for each method call in ruby, the language interpreter checks in the inheritance hierarchy of the classes of the receiver (in our case "<em>my_string</em>") to determine which method should be executed.

An example:

<pre code="ruby">
  my_string = Hash.new # => {}
  my_string.size  # => 0
</pre>

The code above is pretty simple but what's important is happening beneath of it. The language interpreter is assigning the variable <em>my_string</em> with an instance of the Hash class then it's calling the method <em>size</em>.

The Hash class is where our interpreter will start searching for the <em>size</em> method, if the interpreter doesn't find the method in the Hash class, it'll continue to search in the Hash parent class, which in our case (Ruby) is the topmost class . It can be the case the interpreter don't find  the method <em>size</em>, so it'll throw  <em>method missing</em> exception. In our example, the Hash class contains the â€œ<em>size</em>â€ method and successfully returns.

If you want to know how MRI's (Matz's Ruby Interpreter) implements method dispatch, I recommend you to take a look in<a title="Patrick Farley" href="http://www.klankboomklang.com/2007/09/14/method-dispatch/" target="_blank"> this blog post by Patrick Farley</a>, where he explains the Ruby source code responsible for handling method dispatch.

For even further information on this matter there is this huge and excelent <a title="Russ Olsen" href="http://www.jroller.com/rolsen/entry/ruby_spin_up_where_did" target="_blank">post from Russ Olsen</a>, author of the book Design Patterns in Ruby.
