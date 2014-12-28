---
layout: post
title: "Partially Automate Exploratory Testing on OSX"
date: 2013-07-06 19:30
comments: true
categories: Testing Automation Exploratory
---
I found Trish Koo's [blog](http://trishkhoo.com/2012/09/using-ruby-and-automator-to-partially-automate-your-exploratory-testing-on-osx/) on how to automate the input of test data while doing exploratory testing enlightening.  A lot of the blog/twitter chatter recently has been about test automation and specifically doing too much automating, at least on the GUI level. As a new tester, I sometimes have to remind myself that some things don't need to be automated.  That being said, anything that can help relieve the pain of manual testing is always helpful. I don't know about how you do quick exploratory testing, but any time I come across a text field, odds are I'm going to fill it with some variation of "test". While I found her solution helpful, having to use a keyboard shortcut to copy data to my clipboard, then use another to paste the data, is too much work for me. For the past couple of months, I have been playing with TextExpander and I thought I could add a snippet to input test data. I started by finding some test data and putting it in a .txt file, one item per line.  From there, riffing on Trish's code, I added the following snippet:
	
	{% codeblock lang:ruby %}
		#!/usr/bin/env ruby -wKU

		dict = File.open('/<PathToYourFile>/File.txt')
		lines = dict.readlines
		word = lines[rand(lines.size)]
		puts word
	{% endcodeblock %}

I've found this solution helps speed up my manual testing in addition to adding more realistic data to the database.
