---
title: "Messaging"
date: 2008-11-04
---
Something that has running on a background thread for awhile is "How do
we implement pub/sub messaging?".  One of the cons to having very
silo-ed systems is how do you handle the cross-system reporting?  For
instance: When you want to get a list of all the customers that have
more than 10 licenses and have more than 20 open tickets (totally
contrived but you get the idea).  That query spans 2 different domains:
Billing and Support.  Support knows how many tickets somebody has and
Billing knows how many licenses a customer has but it's not like you can
"join across systems" to get that information.

Enter the datamart! Wouldn't be great if somehow each source system
could populate a central repository of data with the key pieces of data
that it has authority over?  Yeah that would be great! They way we have
been approaching that is having snapshots of our source systems update a
central warehouse every few hours.  While functional, it leaves a lot to
be desired.  Data can be out of date, when the update is happening you
might get funky results, etc.  So in our quest to get realtime reporting
we are looking to implement some sort of messaging sub system in our
applications so we can just "write the updates to the wire" which the
datamart (or any other interested system) could read.

Enter pub/sub messaging!  Pub/Sub seems ideal for our needs, but how do
we go about implementing it?  If you ask MS the answer is "Install
BizTalk!".  Now I don't know about you, but I tried to install BizTalk
once.  The experience taught me that I don't want to do it again.  It
seems WAY overkill for what we are trying to do.  We don't need
orchestraions (or maybe we do? Problem is, to know if your problem
requires it you have to implement BizTalk first and then see if it
works.  That doesn't sound like a very agile solution.). So if BizTalk
isn't the answer, maybe using something like NServiceBus,
SimpleServiceBus or MassTransit is?  The problem here now is that I
don't have enough information to make that decision!  Like a lot of Open
Source applications, all 3 suffer from poor documentation.  Not on the
implementation side (from the "How do I make it go?" point of view, all
3 have pretty good documentation) but on the "Is this going to solve my
problem" front I can't find anything.  The last option is SQL Service
Broker.  From a technology standpoint SQL Service Broker is
interesting.  Managing durable messages and conversations inside of your
database.  From a developer stand point, I don't think I like it.  I'm
back in TSQL hell, but now writing TSQL that isn't standard against a
product that is probably used by only 1% of the SQL Server install
base.  I don't think there will be a lot of Google results when I run
into problems no matter how good my Google-Fu is.

 

So that is where I am at today.  Any advice?  If my thought processes
keep dead-locking trying to come up with a solution, I think I'm just
going to start with NServiceBus and see what happens.