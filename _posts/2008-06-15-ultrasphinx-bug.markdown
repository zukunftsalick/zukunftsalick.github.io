---
layout: post
status: publish
published: true
title: Ultrasphinx bug?
author: Pedro Pimentel
author_login: admin
author_email: zukunft@gmail.com
author_url: http://
wordpress_id: 49
wordpress_url: http://www.pedropimentel.com/2008/06/15/ultrasphinx-bug/
date: 2008-06-15 17:28:06.000000000 +08:00
categories:
- rails
- ruby
tags:
- rails
- gsoc
- ultrasphinx
comments:
- id: 28
  author: Eduardo
  author_email: nosachamos@gmail.com
  author_url: ''
  date: '2008-07-12 16:01:14 +0800'
  date_gmt: '2008-07-12 19:01:14 +0800'
  content: "hehehe esse foi um fix rÃ¡pido, no dia seguinte tava arrumado :D\r\n\r\ncara,
    ainda to engatinhando em rails, tenho dedicado umas 2 horas por semana pra isso...
    to vendo que nÃ£o Ã© suficiente. o que tu recomenda?"
---
It seens Ultrasphinx plugin for Ruby on Rails doesn't know how to deal with Decimal data type from MySQL.

You can use a Decimal column for indexing, but when you need to make thecolumn sortable it comes the problem. As you know, faceting is on for numeric and date fields and to add the sortable feature to it, we need to pass a hash with
<pre>{:sortable =&gt; true}
</pre>
Ok, then you run rake tasks to rebuild your configuration file and indexes and try to sort the search by the Decimal column and we got an error saying our column isn't sortable.

You can check isn't generating the _sortable sufix by looking the ultrasphinx configuration file. All other sortable fields have their _sortable sufix added to ti, except by the decimal field.

I'll report it as soon as possible to Evan Weaver, the plugin's owner, or maybe try to fix it by myself.

<strong>Updated: June, 16</strong>

I fixed by addingÂ  'decimal' =&gt; 'float' in the TYPE_MAP inside the fields.rb file of ultrasphinx plugin.
