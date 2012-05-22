---
layout: post
title: "V2 Pseudo-Production Release is out"
date: 2012-05-21 11:30
comments: true
categories: 
- release
- migration
---

This is our [second pseudo-production release][v2plans] of the Contoso Conference Management System. The plan was to explore the **migration process** to understand better how this works in a CQRS/ES implementation and to see if we could perform a no-downtime upgrade with our current infrastructure.

The picture below depicts a portion of our migrated read models (only some of which are actually in SQL Azure).  
<img src="/images/posts/cqrsjourney-conference-v2-migration.png" border="0"/>


The following user stories made it into the release:

1. Providing a better user experience for **zero-cost orders** (at present the registrant is still taken to the payments system even if there’s nothing to pay).

2. Displaying the number of **remaining seats** of each seat type in the UI (since there was no read model for this in V1).

3. Applying **UX designs** to the **Conference Creation/Management BC**.

Unfortunately, it was not possible this time to perform a no-downtime upgrade. This was due to:

* The fact that we weren't storing all the integration events needed in order to regenerate some read models, nor did we have an API for querying the state of the system from an external Bounded Context. So we now have a **message log** for every message that goes through the service bus. 
* Because of this, we have also decided to migrate the event store infrastructure to account for the additional metadata that the message log requires, and we will use as the base for replaying events when regenerating read models (as the message log is much easier to query and is already sorted by time).

Our migration resulted in 1 min 35 secs downtime. 

Now that we have the infrastructure in place, a no-downtime upgrade seems to be an attainable goal for our V3 release.

In addition to the behind-the-scenes changes listed in the previous [post][v2plans], the team made the following changes:

* As mentioned above, there is a now a message log that persists all commands and events. This grew out of the need to persist the integration events. In addition to regenerating read models from events, this is also intended to future-proof the application by capturing everything that might be of interest at some point in the future.
* The Conference solution now includes a migration program to migrate the data to the new event store, re-create the integration events that the V1 release did not persist, and rebuild the read-models with additonal data.
* Several bug fixes (see the [backlog for V2](https://github.com/mspnp/cqrs-journey-code/issues?labels=&milestone=5&page=1&state=closed) or the [commit history](https://github.com/mspnp/cqrs-journey-code/commits/dev))

You can access the updated version of the application as a [Registrant](http://cqrsjourney-conference.cloudapp.net) or as a [Business Customer](http://cqrsjourney-conference.cloudapp.net:8080):

<a href="http://cqrsjourney-conference.cloudapp.net" alt="CQRS Journey : Conference Management System"><img src="/images/posts/cqrsjourney-conference-v2.png" border="0"/></a> &nbsp; <a href="http://cqrsjourney-conference.cloudapp.net:8080" alt="CQRS Journey : Conference Management System - Admin Portal"><img src="/images/posts/cqrsjourney-confmgmt-v2.png" border="0"/></a>

We are now starting work on V3 and you can track our progress against the [V3 milestone][v3milestone].

You can read about the V2 release in more detail [here][journey6] and about the V1 release [here][v1release].


[v2plans]:  http://cqrsjourney.github.com/blog/2012/05/15/Plan-for-V2/
[v3milestone]: https://github.com/mspnp/cqrs-journey-code/issues?milestone=5
[journey6]: https://github.com/mspnp/cqrs-journey-doc/blob/master/Journey_06_V2Release.markdown
[v1release]: http://cqrsjourney.github.com/blog/2012/05/08/Announcing-V1-Pseudo-Production-Release/