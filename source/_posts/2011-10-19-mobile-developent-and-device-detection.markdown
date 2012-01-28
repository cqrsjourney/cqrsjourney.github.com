---
layout: post
title: "Mobile Development: Detecting Devices &amp; Features"
date: 2011-10-19 16:01
comments: false
categories: [mobile,web]
---

_Take this post cum granlis salis. I'm trying to figure this stuff out and I'm thinking out loud._

## Background

Whenever a browser makes a request, it includes a string identifying itself to the server. We commonly refer to this as the *user agent string*. This string identifies the browser and the platform and the version and a great deal more such nonsense.

{% img right /images/posts/tower-babel.jpg %}

This sounds great in theory. We should be able to use this data to optimize what's being sent to the (mobile) browser. However, there's been something of a [sordid history for user agent strings](http://webaim.org/blog/user-agent-string-history/ "History of the browser user-agent string by Aaron Andersen"). In retrospect, we've realized that [user agent sniffing](http://en.wikipedia.org/wiki/User_agent#User_agent_sniffing) is a tool that has often hurt more than it has helped.

We've learned to _favor feature detection over browser detection_ (or device detection). Take a look at [modernizr](http://www.modernizr.com/) and [haz.io](http://haz.io/) for more on the that front.  The success of feature detection has also resulted in a shift from server logic to client logic. We detect features on the client but we detect user agent strings on the server, before we send anything to the client.

How does all this play into the mobile web? One of the key mobile features we are interested in is _screen size_. Luckily for us, the W3C has blessed us with [media queries](http://www.w3.org/TR/css3-mediaqueries/). In a nutshell, media queries allow you to conditionally apply CSS based properties of the display device. This has given rise to something known as [Responsive Web Design](http://www.alistapart.com/articles/responsive-web-design/). Responsive Web Design is about having a single set of markup whose layout can _respond_ to the device's display capabilities. Unfortunately, there are a few [rough edges](http://www.webdesignshock.com/responsive-design-problems/) with this approach.

## Moving Backwards…
In the mobile world, client-side feature detection has a few drawbacks. It requires extra code to be sent to the browsers and it takes additional processing on the client. It's also likely that you'll end up sending more than is really needed (or that you'll need to make additional requests).

One solution to this conundrum is to use the open source "database" called [WURLF](http://wurfl.sourceforge.net/). You can query WURL with a user agent string and it will return a set of capabilities. I think of it as _feature detection_ on the server. Though admittedly it's a bit misleading to call it that.

This means your server can ask questions like "Does this client support HTML5? If no, what do they support?" before the first response is even sent.

WURLF has [commercial support](http://scientiamobile.com/) and a [C# API](http://wurfl.sourceforge.net/dotNet/). For ASP.NET developers, [51Degrees](http://51degrees.mobi/) has an open source project called [Foundation](http://51degrees.codeplex.com/) that is built on top of WURL. It uses an HttpModule to automatically query WURL and populate the [Request.Browser](http://msdn.microsoft.com/en-us/library/system.web.httprequest). Setting up WURLF without Foundation takes a little bit more work, but not too much. Both are available on Nuget: [WURL](http://www.nuget.org/List/Packages/WURFL_Official_API) and [51Degrees](http://nuget.org/List/Packages/51Degrees.mobi).

## What should you do?

I don't think that there is a cut and dry answer _at the moment_. What you do depends heavily on your target audience. If you are targeting the [North American market](http://gs.statcounter.com/#mobile_browser-na-monthly-201009-201109) there's a good chance you'll be okay with a single set of markup, going with a responsive [mobile-first](http://www.lukew.com/ff/entry.asp?933) design. In other words, there would be no need for something like WURLF. 

However, you might need a _very broad reach_ or you might be targeting a market heavy in [feature phones](http://en.wikipedia.org/wiki/Feature_phone) or something else that's [very different from North America](http://gs.statcounter.com/#mobile_browser-sa-monthly-201009-201109). In those cases, it is good to understand your options. 

_Christopher Bennage, cross posted from [dev.bennage.com](http://dev.bennage.com/blog/2011/10/19/mobile-developent-and-device-detection/)_.