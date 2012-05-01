---
layout: post
title: "Open Call for Enhancements to Event Store Implementation"
date: 2012-05-01 10:36
comments: true
categories: 
- Contributions
- Infrastructure
---

In the process of our conversion of the Registration process BC to use event sourcing, we have realized we needed some robust event sourcing infrastructure (both for storing the events, and publishing them). We wanted this implementation to be Windows Azure-friendly, as this is where we’ll bedeploying our system to.

We have now built our initial implementation of the Azure table-based event store and it’s ready for a broad community review and for enhancements. It seems to be self-contained enough and will benefit from crowd-sourcing. Get it from here:

*	Repo: [https://github.com/mspnp/cqrs-journey-code](https://github.com/mspnp/cqrs-journey-code)
*	Infrastructure solution: [https://github.com/mspnp/cqrs-journey-code/blob/dev/source/Infrastructure.sln](https://github.com/mspnp/cqrs-journey-code/blob/dev/source/Infrastructure.sln)


We really look forward to your participation in getting this event store production ready!

_Notes:_

1.	There’s another implementation based on SQL server. It is meant for running the sample app locally and it’s not ready for production. Nor is it in our scope to make it production-ready. So, when prioritizing where to direct your effort, please choose the Azure table-based implementation.
2.	This is currently not intended to be a general-purpose, pluggable component. We’ve designed and developed it to fit with our sample application.
