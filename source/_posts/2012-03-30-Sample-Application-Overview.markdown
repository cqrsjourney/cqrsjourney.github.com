---
layout: post
title: "Sample Application Overview"
date: 2012-03-30 10:15
comments: true
categories: 
- RI 
- Journey
---
## Contoso Conference Management System

This post summarizes the key features and functionality of the proposed Contoso Conference Management System that we are builing in our CQRS Journey projects.
You can read our motivation for choosing this domain [here][pickingdomain] and [here][journeypreface].

## Introduction

Contoso plans to build an online conference management system that will enable Contoso's customers to plan and manage conferences that may be held at a physical location. The system will enable Contoso's customers to:

* Plan the tracks, sessions, and speakers that make up a conference.
* Manage the calls for speakers and paper submission process.
* Manage registration (the sale of seats) for the conference.
* Manage the conference on site, including badge printing and attendee lists.

The following sections describe these functions in more detail.

## Overview

The Conference Management System will be a multi-tennant, cloud-hosted application. Business customers will need to register with the system before they can create and manage their conferences.

## Conference Planning

When a business customer creates a new conference, he must first define some characteristics of the conference such as:

* Will the paper submission process require reviewers.
* What will be the fee structure for paying Contoso.
* Assigning key personnel such as the Program Chair and the Event Planner.

## Building a Program

The business customer must define the conference program. For a simple conference this may be defined directly. For a more complex conference this may involve several steps:

* Identifying Tracks and Track Chairs.
* Identifying Reviewers.
* Making calls for submissions.
* Reviewing the papers and assigning speakers to sessions.
* Finalizing Track programs.

## Selling Seats

The business customer will define how many seats are available for the conference and also for any events that are part of the conference that only limited numbers may attend.

The system must manage the sale of seats to ensure that the conference and sub-events are not over subscribed. This part of the system will also operate wait-lists so that if cancellations are made, then the seats can be re-allocated.

The system will require that the names of the attendees are associated with the purchased seats so that badges can be printed.

## On-site Management

When attendees arrive at the conference they should be registered against an attendee list, given badges, and given the opportunity to purchase additional seats for any extra events they would like to attend. The system that runs on-site at the conference should not assume that it is permanently connected to the main conference management system.

## Additional Features

Contoso plans to roll out additional features as and when resources are available. These include:

* Support for Event Planners to manage equipment, signage, etc.
* Tracking attendees at sessions via a barcode on the badge.
* Score submissions for session feedback.
* Live feed of session scores to track the best sessions.
* Reporting feeback to speakers.
* Archiving conference materials.
* Publishing proceedings.

## Ubiquitous language

[Here](https://github.com/mspnp/cqrs-journey-wiki/wiki/Ubiquitous-language) are the working definitions for the terms in our ubiquitous language for the Conference Managament System sample we are building. We will be adding to and modifying this list as the project proceeds...



## More info

Follow our progress in these 2 repos (you can set the watchers):

* [https://github.com/mspnp/cqrs-journey-doc](https://github.com/mspnp/cqrs-journey-doc)
* [https://github.com/mspnp/cqrs-journey-code](https://github.com/mspnp/cqrs-journey-code)


[pickingdomain]:        http://blogs.msdn.com/b/agile/archive/2012/01/24/picking-a-domain-for-cqrs-journey-ri.aspx
[journeypreface]:       https://github.com/mspnp/cqrs-journey-doc/blob/master/Journey_00_Preface.markdown