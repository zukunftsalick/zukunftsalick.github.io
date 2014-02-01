---
layout: post
status: publish
published: true
title: How to Run Just one Test Method from your Terminal
author: Pedro Pimentel
author_login: admin
author_email: zukunft@gmail.com
author_url: http://
wordpress_id: 75
wordpress_url: http://www.pedropimentel.com/?p=75
date: 2008-10-01 22:45:07.000000000 +08:00
categories:
- rails
- ruby
- hints
tags:
- ruby test
comments: []
---
Many times I found myself running all tests just after modifying just one test method. Depending on the size of your project and its test ratio, it can be a very boring waiting for it to finish.

It can be even worse: Imagine you have other tests failing. How can you improve your productivity ?Â  Just use the "-n method_name" parameter for the method you want to test.
<pre lang="bash">ruby path_to_your_test_case -n method_you_want_to_test</pre>
A real example, I want to test the "test_should_do_stuff" method inside my "stuff_controller_test.rb":
<pre lang="bash">ruby test/functional/stuff_controller_test.rb -n test_should_do_stuff</pre>
Worth remember that stills load your fixtures and preforms setup, it only won't execute the other test methods.
