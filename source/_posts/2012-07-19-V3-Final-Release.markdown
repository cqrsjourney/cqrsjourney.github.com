---
layout: post
title: "V3 Final Release"
date: 2012-07-19 10:31
comments: true
categories: 
- release
- migration
---

This is our [third (and final for this project) pseudo-production release][v3plans] of the Contoso Conference Management System. The plan was to focus on hardening and optimizing the system, and to see if we could perform the no-downtime upgrade that we didn't manage to achieve in the previous update from [V1 to V2][v2release].

There were no new business features implemented in this release, but we did make significant changes to the code as part of our efforts to harden and optimize the system.

<a href="http://en.wikipedia.org/wiki/File:3_tourist_helping_artist_blacksmith_in_finland.JPG"><img src="/images/posts/hardening.jpg" alt="Original image under the Creative Commons Attribution-Share Alike 3.0 Unported license" border="0" /></a>

## Hardening the system

As part of this release, the team revisited the **RegistrationProcessManager** to ensure its resilience to a wide range of potential failure conditions. These changes fall into two categories:

* Resilience in the face of duplicate events: the system must guarantee idempotent behavior, so that if for any reason it tries to process an individual event more than once, then this does not result in inconsistencies.
* Robustness when sending commands: the team implemented a pseudo-transaction to provide guarantees that the system always sends any outstanding commands from the **RegistrationProcessManager** whenever it saves the process manager's state. A pseudo-transaction is necessary because it is neither advisable nor possible to enlist the Windows Azure Service Bus and a SQL Database table together in a distributed transaction.

## No-downtime migration

The team implemented a no-downtime migration strategy to get from V2 to V3 and successfully performed this migration on the live system deployed to Windows Azure. To help with this process, we created an ad-hoc processor that keeps the V2 read-models up to date during the migration process. This was necessary because we replace the V2 processor with the V3 processor before we switch to the new V3 front-end.

## Optimizing the system

The optimizations added by the team were optimizations to improve both the performance and the scalability of the system. These optimizations took the majority of the team's effort in this release. As is often the case with performance tuning, addressing one bottleneck frequently revealed another elsewhere in the system. The optimizations occurred in two places; first, in the UI flow, and second, in the infrastructure.

### UI optimizations

The optimizations implemented in the UI flow were designed to streamline the behind-the-scenes processes that take place between the time that a registrant selects seats for a conference and the time the registrant pays for those seats. The changes mean that the user is far less likely to have to wait at any point in this process, but still ensuring that the system checks that the requested seats are available before accepting payment. It does this in two ways. First, when there are plenty of seats available for a conference, the system assumes that the reservation will succeed and so performs the reservation asynchronously while the registrant is completing other screens in the UI and before the regenerating gets to the payment stage. Secondly, we reorganized the **Order** entity to perform the totals calculation as one of its first tasks instead of one of its last tasks, making the information available in a read model much sooner that was previously the case.

### Infrastructure optimizations

These were the most effective optimizations, but took the longest time to identify and implement. The optimizations included:

* Handling the majority of I/O operations asynchronously. This is recommended practice, but makes the code much harder to read especially when combined with transient fault handling logic.
* Processing some commands in-process instead of pushing them through the service bus. In some cases it is possible to handle  commands in the same process where they are sent, and this therefore reduces the number of messages we are sending through the service bus and reduces the latency in delivering those command messages.
* Implementing snapshots in the event sourcing sub-system. This is a common optimization to event sourcing, and we implemented this in memory using the Memento pattern.
* Caching read-model data. Again, this is a common optimization, but this raises the question of how frequently the cache is updated.
* Tuning the Windows Azure Service Bus by using features such as filters and by implementing parallel publishing, parallel sessions, partitioned topics, and more. For proven perf optimization practices, see this [guide][SBperf].
* Using sequential GUIDs to optimize insert behavior into Windows Azure SQL Database tables.

For full details of these optimizations and more, take a look at Chapter 7, "[Adding Resilience and Optimizing Performance][journey7]," in the journey guide. This chapter also identifies some of the additional optimizations we would like to perform given time.

You can read about the V3 release in detail [here][journey7], and about all our lessons learned from the project [here][epilogue].
The code base corresponding to this release is [available][tags] under the *V3-pseudo-prod* tag. You can also see the list of [implemented stories][v3milestone].

You can read about the previous [V2 release][v2release] and about the previous [V1 release][v1release].


[v3plans]:  http://cqrsjourney.github.com/blog/2012/05/30/plans-for-v3/
[v3milestone]: https://github.com/mspnp/cqrs-journey-code/issues?milestone=6&state=closed
[v1release]: http://cqrsjourney.github.com/blog/2012/05/08/Announcing-V1-Pseudo-Production-Release/
[v2release]: http://cqrsjourney.github.com/blog/2012/05/21/V2-Pseudo-Production-Release-is-out/
[journey7]:  https://github.com/mspnp/cqrs-journey-doc/blob/master/Journey_07_V3Release.markdown
[epilogue]:  https://github.com/mspnp/cqrs-journey-doc/blob/master/Journey_40_Conclusions.markdown
[SBperf]: http://aka.ms/SBperf
[tags]:  https://github.com/mspnp/cqrs-journey-code/tags