---
layout: post
title: "The Productive Tester"
date: 2014-07-17 19:17
comments: true
categories: Productive Automation 
---

I think we've all had the experience of somebody asking or emailing, "Hey, what's going on with DE4288?". Unless I have been looking at that defect in the last 2 minutes, I have no idea what you're talking about. For the longest time, I would open up the browser, navigate to our *cloud based agile software development tracker*, search around, eventually find what I'm looking for, and then ask you what it was you wanted. There had to be a better way! Using Automator (OS X only), I created a simple service that allows me to highlight a defect number (DE4288 for example) and it will open up Chrome and take me directly to the defect or user story. All it takes is this simple bash script:

```
	/usr/bin/open -a "/Applications/Google Chrome.app" https://rally1.rallydev.com/slm/rally.sp?#/search?keywords=$@
```
Obviously this specific example will only work with Rally, but I think the idea remains the same - Rather than just focusing on 'automating' your checks, why not automate repetitive things that annoy you.

---

My second tip uses a piece of software called Text Expander (also OS X only). Using their formatted text snippet builder, whenever I type 'bbug', a little window pops up with a form that looks like this:
	
{% img center /images/TextExpanderDefectSteps.png Steps %}

Which after I'm done, formats to something looking like this:

{% img center /images/FormattedDefect.png Steps %}

I've found this is a really nice way to have consistent looking steps to reproduce and makes sure I have at least the bare minimum defect logged for the developer.
