---
layout: post
title: "Introduce Some Chaos Into Your Testing"
date: 2013-10-25 19:40
comments: true
categories: Chaos Proxy Random Testing
---

{% img center /images/chaos_proxy.PNG Chaos Proxy %}

A little over a year ago, the Netflix Tech Blog posted an article revealing to the the world [Chaos Monkey](http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html). Chaos Monkey will terminate virtual machines in Netflix's AWS cloud infrastructure…in production to make sure they can handle it.  That's right, in production. I would have loved to be in the meeting where the dev ops team presented this. 

The web application I am currently testing is heavily client based, meaning that most of the data coming into the application comes from AJAX calls made directly from the browser rather than the server. As with any good web application, it has to respond well to failure, serving up nice error messages and failing gracefully. For each user story, I can test to make sure that when the feature receives failing status codes (401,403,404,500…etc), it responds appropriately, but I wanted something more, so I wrote Chaos Proxy.

{% img center /images/chaos_capture.PNG Chaos Proxy %}

Due to some frustrating corporate policy, I cannot post the source code for Chaos Proxy, but I will tell you what it does and more or less how I did it(If you know anything about C# and read up of Fiddlercore, you should be able to recreate it). Chaos Proxy is a C# console app written using Eric Lawrence's [Fiddlercore](http://fiddler2.com/fiddlercore) library. On startup, Chaos Proxy will ask you for what percentage of calls you want to fail, what status code you want to respond with, the external service's hostname you want to intercept, and the site you are testing.  After that, Chaos Proxy will intercept the calls before they ever leave your machine and return the intended status code. The intercepted calls appear in the console window so you can see which calls failed. At some point in time, I plan to add some more chaos into the mix by randomizing which status codes get returned. 

{% img center /images/chaos_chrome_capture.PNG Chaos Proxy %}

I have run it with 10, 20, and 30% failure rates during exploratory testing and have found some very interesting defects that I may not have found otherwise. I think that introducing a bit of randomness and chaos into exploratory testing is increasingly valuable. Some testers and developers fall into the trap of thinking everybody using their product has a blazing fast internet connection, a 1080p monitor, and is running chrome.  I believe that my job as a tester is to account for those poor souls who are running IE 8 on XP. API calls will fail on occasion, and my application will be ready.