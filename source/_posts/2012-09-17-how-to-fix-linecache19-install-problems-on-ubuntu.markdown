---
layout: post
title: "How to fix linecache19 install problems on ubuntu"
date: 2012-09-17 13:54
comments: true
categories: 
tags:
  - linux
  - ruby
  - bugs
  - rubygems
status: publish

---

So while attempting to install the <a href="http://rubygems.org/gems/linecache19">linecache19</a> gem under rvm on ubuntu 12.04 (aka "precise"), I ran into a problem where it took a long, long time to compile.

The fix was fairly simple:

<pre>
gem install ruby-debug19 -- --with-ruby-include=$rvm_path/src/ruby-1.9.3-p193
</pre>

where the last bit of that line should match your ruby version. I would imagine this'd work outside RVM with a different source path, too.
