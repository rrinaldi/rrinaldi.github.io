---
title: PDC 2008 Reflections
date: 2008-11-03
---
When I left the LA Convention Center on Thursday I was saddened.  I had
so much fun at PDC that I didn't want it to end.  I wanted to stay there
forever and learn all about all the new and interesting things coming
out of MSFT and MS Research.  As soon as I got back to my hotel,
however, I was eager to get home.  The more I thought about it, the more
I realized that my brain was full and it was time to head back to home
and bother my coworkers.  Tell them all about the grand and wonderful
things I learned. (Really, I'll just speak the wonders of Pex and C\#
4.0 and M and Oslo and Azure and there I go again getting all excited!)

 

## C\# 4.0

I'm really looking forward to C\# 4.0.  The concept of having an "object
that is statically typed to be dynamic" is really interesting.  I've
been looking at different dynamic languages that are out there (Ruby,
Python and Boo (Okay, Boo isn't really dynamic but it pretends!)) and
I've been envious of the rapid prototyping you can do since the language
just "gets out of your way".  I've also been enjoying some of the
JavaScript work I've been doing since its also dynamic.

Dynamic typing gives you great power but (cheesy Spiderman quote) "With
great power comes great responsibility".  I will be the first to say
that I will abuse this new feature.  I mean, like really abuse it. Like
apply it to every problem.  Every problems solution will be "Make it
dynamic!".  Unfortunately that is how I learn.  I have to figure out
what something *isn't* good at to figure out what it *is*.

## Oslo

Now here is something that I'm looking at with a keen interest.  Oslo
comes in three parts: M, the modeling language (that is actually
comprised of 3 parts: M itself, MGrammer, and MSchema), Quadrant, the
visual modeling tool and Repository, a model storage database.  Of the 3
parts I'm most in interested in M and using it to create textual DSLs. 
I dont' know about you, but a lot of the problems I run into with
applications that are heavy on the use of meta-data is being able to
effectively create a user interface to model those meta-data rules. 
Many times the problem could be solved a lot easier using a DSL that
effectively read like English. Example:

> Let's say you have a ticketing system that had a customizable rules
> system.  Every time a ticket is updated you need run through a list of
> rules and if the rule matches the current state of the ticket the rule
> event is fired (in this case it's send of an email to the people
> specified in the rule).

I spent some time creating a UI to administer rules for something like
the above.  No matter where I put checkboxes or dropdowns the UI never
came together the way I wanted it. I guess the best way to put it is
that it has been found lacking.  What I really wanted was something like
this:

> *When ticket status is urgent*
>
> *and customer is "Big Corp"*
>
> *then send email to Sales, Account Managers and ryan@ryanscompany.com*

Status and Customer being properties of the ticket, Sales and Account
Managers being keywords that mean the Sales people and Account Manager
on the ticket.

With M, you get the ability to define exactly that.  Using MGrammer you
define a grammar for your language.  The M runtime will then give you a
simple data structure of your language and you can then process it how
you see fit. Super cool stuff.

The other parts of Oslo I'm not so interested in at this moment.  I'm
not entirely sure I like the Repository.  Well, I should rephrase that.
At this point I'm not sure what it's purpose is.  I don't want all of my
models sitting in one database.  I want each one of my applications to
work with the models it cares about and (if required) publish those
models and data into a larger data mart.  I want silo-ed applications! 

 

## Azure

Now Azure is pretty damn cool.  MS took the hard part of scaling and
said "We'll do it for you".  You can take your apps and put them up in
MS's cloud and they will handle the scaling up and scaling out of your
application automagically. (I shouldn't say completely automagically,
you can't take any app and throw it up in the cloud.  You have to write
it with the cloud in mind).  The interesting part to me is how they are
going to set the pricing model.  If it's geared towards the enterprise
(I'm talking the 50,000+ employees enterprise) then I have a feeling
that it will be of no value to me.  If they have SLAs and price points
that make it more approachable for the small to mid-size businesses then
I'm all over it.  I'm really interested to see if we can take some of
our internal applications and put them in the cloud.

(Before I get hate mail: Yes I know Amazon and Google have already done
it.  There is more to Azure and I'll get to it in another post!)
