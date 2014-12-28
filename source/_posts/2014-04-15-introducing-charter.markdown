---
layout: post
title: "Introducing Charter"
date: 2014-04-15 16:15
comments: true
categories: charter sbtm exploratory testing
---

**tl;dr A command line tool for creating a test charter exported in markdown or html.**

Work has been looking to formalize our exploratory testing efforts and the idea of exploratory test charters was brought up. From there, I read up on Session Based Testing and found it intriguing. I started looking for something to help me in my session based testing efforts: something lightweight, unobtrusive, and exports the charter in a useful format. When I didn't find anything that I thought would fit my needs, I starting writing Charter. It's a simple command line tool for creating and exporting test charters in Markdown or HTML. I took this as an opportunity to brush up on my Ruby skills and create something that perfectly met my needs. Charters are saved in a folder with any defect screenshots associated with the charters. My team uses the Github wiki with our repository so I have my charters saving to a folder in the wiki repository so they are publicly accessible if needed. Tags can be added to charters and Charter will find all charters with a given tag. Charter is currently OS X only with no immediate plans to verify if it works on Windows yet. Take a look and try Charter out for yourself! I would love some feedback!

You can find the source on Github [here](https://github.com/markgrossman/Charter) and as a Ruby gem [here](https://rubygems.org/gems/charter).

##Installation  
 Charter was created as a Ruby gem and is available through Rubygems.org. Installation is as simple as:  
  <code>[sudo] gem install charter</code>
 	
After installing the gem, create a ~/.charterrc file and add the following:
	{% codeblock lang:yaml %}
		---
		session_folder: "/Where/The/Charters/Will/Save/To"
		tester: Your Name Here
	{% endcodeblock %}
##Usage
	charter [global options] command [command options] [arguments...]

Creating a new charter is as easy as <code>charter start "My charter title here"</code>. This will create a new charter in the folder specified in your ~/.charterrc file.

<code>charter purpose "This is my purpose!"</code> : What do you hope to accomplish with this charter  
<code>charter env "Windows 7"</code> : Add a environment description  
<code>charter scenario "Scenario goes here"</code> or <code>charter s "Scenario goes here"</code> : Add a scenario  
<code>charter bug "This is my bug"</code> or <code>charter bug -s "My bug"</code> : Add a bug with or without a screenshot  
<code>charter note</code> : Add a note  
<code>charter tag "Login"</code> : Add a tag to the charter  
<code>charter finish</code> or <code>charter finish -e</code> : Remove any remaining placeholders and optionally export the charter in HTML  
<code>charter find Login</code> : Find all charters with a given tag

See an example charter [here](/charter-example)
