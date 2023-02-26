---
title: "How about you support the standard, m'kay?"
date: 2004-05-01
---
've been working on some vCard/vCalendar export code at work for the
past couple of days, the main purpose being to import the resulting
vCard/vCalendar files into Outlook.  The problem being that Outlook
doesn't have any decent support for the vCalendar spec.

First gripe: The vCalendar spec outlines 2 types of "calendar entities":
vEvent and vTodo.  vEvent support is so-so and Outlook doesn't support
vTodo at all.  :(

Gripe the 2nd: A vCalendar file is pretty much an envelope around
vEvents.  This would allow you to create multiple vEvents and vTodos and
wrap them up in a single file for import.  If Outlook is presented with
a vCalendar file that contains multiple vEvents it grabs the first one
and ignores the rest.

Gripe C: Parameter support. Frankly it kind of stinks. The following
vCalendar parameters are things that:

a.) Are supported, but the results are different from what is outlined
in the spec.

OR

b.) Are not supported, the spec does not require that it be supported
but Outlook has functionality that could support it.

Group A:

PRIORITY: The parameter is defined as 1 being highest priority, 2 being
second highest priority and so on with 0 (zero) being undefined. 
Outlook decided that greater than 0 is High priority, 0 is Normal
priority, and less than 0 is Low priority.  The spec doesn't even
outline negative numbers, since you're not supposed to use them! 
According to the spec, the lower the number the higher the priority. 
According to Outlook, the lower the number the lower the priority. 
Complete opposite.

CLASS: This parameter supports the following properties: PUBLIC,
PRIVATE, CONFIDENTIAL.  The strange thing is when you set it
CONFIDENTIAL, Outlook changes the sensitivity of the event, but doesn't
mark it as private.  Maybe I'm alone on this one, but if something is
confidential it sure as hell is private!

Group B:

DALARM: This parameter lets you specify when you should be alerted about
a calendar event.  Outlook ignores this one entirely, but the spec does
say that adherence is optional.  Since Outlook does have an option to
remind the user about an event, I figured that they would have some
rudimentary support for this.

TRANSP: Supposedly, setting this to 0 means that the event will show
time as "Free".  Outlook ignores this one.  The spec even goes as far to
let the application interpret the number however it wants (unlike the
PRIORITY field, which Outlook freely redefines).

 