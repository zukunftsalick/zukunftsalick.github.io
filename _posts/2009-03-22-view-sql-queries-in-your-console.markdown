---
layout: post
status: publish
published: true
title: View sql queries in your console
author: Pedro Pimentel
author_login: admin
author_email: zukunft@gmail.com
author_url: http://
wordpress_id: 123
wordpress_url: http://www.pedropimentel.com/?p=123
date: 2009-03-22 18:45:02.000000000 +08:00
categories:
- rails
- hints
tags:
- rails
comments:
- id: 94
  author: Matias
  author_email: matiasleidemer@gmail.com
  author_url: ''
  date: '2009-03-23 09:17:23 +0800'
  date_gmt: '2009-03-23 12:17:23 +0800'
  content: I guess it only works for the Rails &gt;= 2.2, right?
- id: 95
  author: Pedro Pimentel
  author_email: zukunft@gmail.com
  author_url: http://
  date: '2009-03-23 17:47:59 +0800'
  date_gmt: '2009-03-23 20:47:59 +0800'
  content: |-
    Hello Matias!
    I didn't try in older versions of Rails. I'm not sure.
- id: 174
  author: Mario Olivio Flores
  author_email: mario@orbitalvoice.com
  author_url: http://orbitalvoice.com
  date: '2011-08-02 22:37:38 +0800'
  date_gmt: '2011-08-03 01:37:38 +0800'
  content: "Alternatively, two other ways in rails 2 &amp; 3:\r\n\r\nhttp://stackoverflow.com/questions/1344232/how-can-i-see-the-sql-that-will-be-generated-by-a-given-activerecord-query-in-rub#answer-1576221"
---
Don't you think it's really irritating when, in the console, you are testing your model's methods and everytime you need to check how each SQL query was formed you need to go to another tab to visualize the log ???

Your frustation is over. Just add the following lines in your .irbrc file:

<pre lang="ruby">
def log_to
  ActiveRecord::Base.logger = Logger.new($stdout)
  ActiveRecord::Base.connection_pool.clear_reloadable_connections!
end
</pre>

You can change the method's name to whatever suits your needs. After that, every time you are in your application's console you just type <em>log_to</em> and you're ready to go:

<pre lang="bash">
>> log_to
=> []
>> MyModel.count
  SQL (1.8ms) SELECT count(*) as count_all FROM "mymodels"
=> 10
</pre>

This hint I got it from <a title="Pratik Naik" href="http://m.onkey.org/">Pratik Naik</a> while doing pair programming with him at the company I work.
