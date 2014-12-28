---
layout: post
title: "Webdriver Screenshots in CI"
date: 2013-07-22 11:11
comments: true
categories: Testing Automation CI TeamCity SpecFlow
---

Flaky tests are annoying.  Flaky tests are infuriating when they are run in continuous integration and you can't see why it's falling without bugging the SCM guys.  There are a few ideas to help alleviate this problem.

1. First and foremost, have a test infrastructure in place that allows you to write stable tests. Whether that means using the page-object pattern or ensuring you and your developers are on the same page with regards to stable html tags for you to key off of.
1. Have some good logging in place that you can dig into to figure it why it failed. If a test fails, hopefully you have a log of what happened before the test failed, when the test failed, and some sort of stack-trace.
1. On test failure, take a screenshot of the browser. After implementing this into my test suite and CI build, my anxiety over flaky tests has been greatly reduced. Being able to see the state of the browser at the time of failure has allowed me to quickly diagnose and treat a flaky test.

Implementing the screenshot capability into SpecFlow was surprisingly easy.  First off, I added a little static method to a WebDriver extensions class that looks like this: 

{% codeblock lang:c# %}
	public static void TakeScreenshot(this IWebDriver driver, string filename)
	        {
	            Screenshot ss = ((ITakesScreenshot)driver).GetScreenshot();
	            ss.SaveAsFile(filename, System.Drawing.Imaging.ImageFormat.Png);
	        }
{% endcodeblock %}

It takes in a webdriver driver instance and a string for the screenshot filename. In my SpecFlow hooks, I added an AfterScenario hook that looks like this:

{% codeblock lang:c# %}
    [AfterScenario]
    public static void AfterScenario()
    {
    	//Check to see if there were any errors in the scenario and if there were, take a screenshot of the browser
        if (ScenarioContext.Current.TestError != null)
        {
            driver.TakeScreenshot(ScenarioContext.Current.ScenarioInfo.Title.ToString() + ".png");
        }
    }
{% endcodeblock %}

It's just that simple.  I set the file name as the scenario title so I can easily identify them.  By default, the screenshots are saved to either the bin/debug or bin/release folder. In TeamCity, I had our SCM team save any .png files in the bin/release folder and save those as artifacts.

