---
layout: page
title: "Advisory Board Meeting Notes, November 23, 2011"
date: 2011-11-23 13:58
comments: true
sharing: true
footer: true
---
Here are then notes from Project Liike's first advisory board meeting. The goal of the meeting was to introduce the project and its objectives, as well as soliciting some initial feedback about the project's intent.

Comments and discussion are welcome.

## Goals for project

In order to provide clarification and to encourage solidarity, members on the board asked the [project team](/team "the official team members") to provide a terse and focused statement about the project's objective. After the meeting concluded, the team summarized the objective as:

{% blockquote %}
The primary objective of Project Liike is to harvest a set of guidance for web developers who need to extend existing web applications to include a mobile experience. The mobile experience will be built upon HTML5 as the platform because we anticipate these applications running on devices that do not even exist yet. We will achieve this by building a reference application under the real-world challenge of balancing value and available resources. 
{% endblockquote %}

## Deliverables

What are the actual deliverables for Project Liike?

* **Reference Implementation** or RI, this is essentially an end-to-end sample application. It's the primary code deliverable from the project. We will build this application based on the [Extending Existing Apps scenario](/scenarios/extending-existing-apps.html). The application will be driven by a set of forthcoming user stories. Additionally, we will be utilizing assets from p&p's [Project Silk](http://silk.codeplex.com/) as the existing web application.

* **Patterns &amp; How-To's** as we identify and encounter problems during the development we'll catalog them. The outcome will be similar to Brad Frost's [Mobile Web Best Practices](http://mobilewebbestpractices.com/). However, our intent is not to replace or overshadow existing works but rather to compliment and credit. 

 	* _Patterns_ are more formal abstractions that include a problem, a solution (typically independent of a particular technology), a sample implementation of the solution, and guidance about when the pattern is appropriate.
	
	* _How To's_ will be articles focusing on how to perform a specific tasks (e.g., delivering the appropriate content to a feature phone from an ASP.NET application).

* **Target Topics** will be more general articles discussing a higher level context and project decisions. Some topics we have already proposed are:

	* When is [jQuery mobile](http://jquerymobile.com/) the best solution? and why are we not using it in Liike?
	* When is [PhoneGap/CallBack](http://phonegap.com/) appropriate to use? and why are we not using it in Liike?
	* What is the spectrum of choices for building applications for mobile devices? Native, mobile web, and things in between.

## Schedule

The project has officially started, but we are still ramping up. We have have an extended break for the second half of December, then we will run full time from January through March.

We will be having regular advisory board meetings begins in January, one every other week.

The project team is employing an iterative development/design process. We will demonstrate the reference application at each advisory board meeting and present any new guidance for review.

## Discussion

The advisory board had a healthy discussion about the nature, intent, and expectations of the project. To summarize:

<dl>
<dt>What is the specific objective of this project?</dt>
<dd>In addition to what has already been published on this site, we attempted to summarize the objective. See above, under Goals.</dd>

<dt>How does Project Liike differ from Mobile ★ Boilerplate and Mobile Web Best Practices?</dt>
<dd>
<ul>
<li>
<strong><a href="http://html5boilerplate.com/mobile">Mobile ★ Boilerplate</a></strong> is specifically meant to be a reusable template. There is excellent guidance packed into it. However, Liike is meant to provide higher level guidance exploring the how's and why's of building a mobile experience. Project Liike is not aiming to create a reusable asset to solve a specific problem, rather (in the words of one of the advisors) we hope to "teach developers how to fish, and not simply give them a fish".</li>
<li>
<strong><a href="http://mobilewebbestpractices.com/">Mobile Web Best Practices</a></strong> does have some similarities to Project Liike as noted above. The primary difference is that our guidance will center about our reference application.</li>
</ul>
</dd>
<dt>Project Liike seems shy about producing "reusable components"? Is this a good thing or a bad thing?</dt>
<dd>Firstly, there may have been some confusion over the term "reusable components". There will definitely be plenty of source code for developers to examine and reuse as they will. However, we are not _planning_ to produce a library or framework as part of Project Liike. If that happens as a natural side-effect, that's okay. We don't know exactly what problems we'll be encountering in this project, and we believe it would be presumptuous for us to plan to build a library or framework. This topic will continue to be discussed by the advisors and the project team.</dd>
</dl>
