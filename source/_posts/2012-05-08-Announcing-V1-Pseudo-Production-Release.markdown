---
layout: post
title: "Announcing V1 Pseudo-Production Release"
date: 2012-05-08 11:45
comments: true
categories: 
- release
---

As part of our CQRS Journey we plan to have [several pseudo-production releases](http://cqrsjourney.github.com/blog/2012/04/12/Road-to-V1/) of the Contoso Conference Management System so that we can explore the real-world issues of data-versioning and software updates in an application that implements the CQRS pattern in several bounded contexts. Over the next few weeks we plan more pseudo-production releases and as we go through them we will be describing our experiences in the guidance documentation. 

Today we are releasing the first of these pseudo-production releases: Contoso Conference Management System (V1). 

{% img left /images/posts/cqrsjourney-conference-v1.png %}


The current release consists of three bounded contexts:

*	_Conference Management_ (implemented using a traditional CRUD-style architecture).
*	_Orders and Registrations_ (implementing the CQRS pattern and using event sourcing).
*	_Payments_ (implementing the CQRS pattern and using a SQL-based storage).

Keep in mind, while based on the real-world requirements, it is still a <u>sample</u> application. It doesn’t include the following:

*	Authorization (on the backlog for V2).
*	Styling for the conference management web site (on the backlog for V2).
*	Integration with a real third-party  payment processor (out of scope for the guidance project; we'll keep the simulated one).
*	Conference details (description, speakers, tracks, sessions, etc.) - you will see static data in the registration hub for now.
*	Perf testing (on the backlog for V3).

If you would like to explore the code in the V1 release, you can **download it from GitHub [here](https://github.com/mspnp/cqrs-journey-code/tree/V1-pseudo-prod)**.
To help you get started with building/deploying/running the V1 release code see the release notes [here](https://github.com/mspnp/cqrs-journey-doc/blob/master/Appendix1_Running.markdown).

The current release uses the Windows Azure Service Bus to provide its messaging infrastructure and can be deployed to Windows Azure. You can access a deployed version of the application as a [Registrant](http://cqrsjourney-conference.cloudapp.net) and as a [Business Customer](http://cqrsjourney-conference.cloudapp.net:8080). Please feel free to use the application and to generate some sample data for us so that we can migrate it for our V2 release.

Note: You can also run a copy of the application locally without using Windows Azure or Windows Azure Service Bus as described in the [release notes](https://github.com/mspnp/cqrs-journey-doc/blob/master/Appendix1_Running.markdown). 

We would appreciate your feedback on both the code and the written guidance. You can submit your reviews either via GitHub (comments, pull requests, issues) or via our [lightweight review system](http://pundit.cloudapp.net).

If you'd like to participate in this sample system evolution and work on any improvements of the existing bounded contexts or new ones, check out [our backlog](https://github.com/mspnp/cqrs-journey-code/issues). We'll be happy to see your pull requests!

