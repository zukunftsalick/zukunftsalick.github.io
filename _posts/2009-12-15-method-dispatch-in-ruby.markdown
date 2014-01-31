---
layout: post
status: publish
published: true
title: Method dispatch in Ruby
author: Pedro Pimentel
author_login: admin
author_email: zukunft@gmail.com
author_url: http://
wordpress_id: 194
wordpress_url: http://www.pedropimentel.com/?p=194
date: 2009-12-15 17:38:11.000000000 +08:00
categories:
- ruby
tags:
- ruby
- dispatcher
- interpreter
- mri
- method
comments:
- id: 131
  author: clayton
  author_email: clayton@integrumtech.com
  author_url: http://www.integrumtech.com
  date: '2009-12-16 01:20:17 +0800'
  date_gmt: '2009-12-16 04:20:17 +0800'
  content: I always love learning new little things about Ruby internals, especially
    something that I take for granted.
- id: 134
  author: CÃ¡ssio Marques
  author_email: cassiommc@gmail.com
  author_url: http://cassiomarques.wordpress.com
  date: '2009-12-16 20:38:52 +0800'
  date_gmt: '2009-12-16 23:38:52 +0800'
  content: "Before searching the parent classes, the interpreter will search in the
    'ghost' or 'eigenclass' of the object upon which the method is being called.\r\n\r\nNice
    post :)"
- id: 136
  author: Pedro Pimentel
  author_email: zukunft@gmail.com
  author_url: http://
  date: '2009-12-16 20:52:30 +0800'
  date_gmt: '2009-12-16 23:52:30 +0800'
  content: |-
    Thanks for the complement CÃ¡ssio.
    A good example to illustrate what you said is when you call methods from a singleton class.
- id: 172
  author: garge
  author_email: miah-101@live.com
  author_url: http://www.youroutdoorcenter.com
  date: '2011-06-12 19:12:29 +0800'
  date_gmt: '2011-06-12 22:12:29 +0800'
  content: '[...] Method dispatch in Ruby | Pedro Pimentel [...]'
- id: 176
  author: Charlie Fuson
  author_email: Dionne_Makarewicz@yahoo.com
  author_url: ''
  date: '2012-06-24 23:07:30 +0800'
  date_gmt: '2012-06-25 02:07:30 +0800'
  content: Full range of Jersey Euro 2012 , I love it at Soccer !
- id: 179
  author: london 2012
  author_email: Tomika_Dubourg@hotmail.com
  author_url: ''
  date: '2012-08-06 14:09:27 +0800'
  date_gmt: '2012-08-06 17:09:27 +0800'
  content: Most Business Knows How to Use Google ,But Most DO Not Know How their Businesses
    SHOULD Utilize Google to its Benefit \
---
<p style="text-align: center;"><a href="http://www.pedropimentel.com/wp-content/uploads/2009/12/pomegranate.jpg"><img class="size-medium wp-image-195 aligncenter" title="pomegranate" src="http://www.pedropimentel.com/wp-content/uploads/2009/12/pomegranate-311x450.jpg" alt="pomegranate" width="311" height="450" /></a></p>

Some days ago I was asked how the dispatcher works in ruby and I was caught in surprise I didn't know how to explain the method dispatching in the language we love (Ruby). That question was kept still in my mind for a few days but while listening to some workmates discussing about singleton classes in ruby the answer came to my mind in a blink of eyes reminding me from a university class which I had a long time ago about how method dispatching works in dynamic languages like Ruby.

So with that information in mind and some googling to confirm it I came out with a simple explanation of how the dispatching works in Ruby and decided it's worth sharing you.

Essentially for each method call in ruby, the language interpreter checks in the inheritance hierarchy of the classes of the receiver (in our case "<em>my_string</em>") to determine which method should be executed.

An example:
<pre lang="ruby">  my_string = Hash.new # => {}
  my_string.size  # => 0</pre>
The code above is pretty simple but what's important is happening beneath of it. The language interpreter is assigning the variable â€œ<em>my_string</em>â€ with an instance of the Hash class then it's calling the method â€œ<em>size</em>â€.

The Hash class is where our interpreter will start searching for the â€œ<em>size</em>â€ method, if the interpreter doesn't find the method in the Hash class, it'll continue to search in the Hash parent class, which in our case (Ruby) is the topmost class . It can be the case the interpreter don't find  the method â€œ<em>size</em>â€, so it'll throw a â€œ<em>method missing</em>â€ exception. In our example, the Hash class contains the â€œ<em>size</em>â€ method and successfully returns.

If you want to know how MRI's (Matz's Ruby Interpreter) implements method dispatch, I recommend you to take a look in<a title="Patrick Farley" href="http://www.klankboomklang.com/2007/09/14/method-dispatch/" target="_blank"> this blog post by Patrick Farley</a>, where he explains the Ruby source code responsible for handling method dispatch.

For even further information on this matter there is this huge and excelent <a title="Russ Olsen" href="http://www.jroller.com/rolsen/entry/ruby_spin_up_where_did" target="_blank">post from Russ Olsen</a>, author of the book Design Patterns in Ruby.
