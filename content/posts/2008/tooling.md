---
title: "Tooling"
date: 2008-11-16
---
What tools do you use? If you are reading this I bet you use some flavor
of Visual Studio and some form of source control, but like most
developers your tooling stops there.  Why?  Have you tried the various
Visual Studio add-ins like ReSharper or CodeRush?  How about SQL Schema
diff tools like SQL Compare from Red-Gate? How about a build server like
Team Build or Cruise Control?

Most developers I know would answer no to most of those questions.  And
honestly, I don't get it.  Do you like spending time writing reams of
similar code?  Manually diffing schema? Figuring out why a build doesn't
work in a new environment?

"Ryan, those things are too expensive.  I could never get those things
approved!" I call bull.  Have you tried to use them? Have you seen
productivity gains?  If so, I bet it would be a rather easy sell to your
manager.  Do a simple ROI on it and you'll be amazed at how **cheap**
most of these tools are!

If you are looking for the quick win, create a build server.  Once you
see how easier deployment is when you can xcopy a build to a new
environment you'll be sold.  Then you add in things like unit tests and
longer running build verification tests and you'll be amazed.  You'll
start to **trust** your builds and rollouts to new environments won't be
feared.

Here is another thing I don't get.  Developers, as a whole, put up with
a lot of friction before doing something about it and I'm not sure why. 
We spend all day writing applications that make other people's lives
more productive yet we will put up with friction at almost ever step of
the way.

"But that's the way it is. Writing software is hard and this is the way
it's always been."

Yeah, writing software is hard, but that doesn't mean we can't write
software to make it easier!  There are two tools that I use everyday
that you can't buy anywhere.  OutWit, a Outlook add-in that creates TFS
work items and IntelliPages, a small applications that lets us search
our company directory/quick dialer.  Both of these applications make my
life easier and neither one existed until a developer on the team
decided it to make time to bring it life. (I made OutWit and
[Ray](http://ray.jez.net/) made IntelliPages, which has been so
successful internally it's now part of our standard desktop image across
the organization. :))

Another tool I build/use is a simple command line app that is part of
each solution and is tasked with knowing how to promote builds from one
environment to the next. Get the build from the build server, put in
environment, update Team Build with new environment information, that
sort of thing.

My point is that as developers you need to look outside of Visual Studio
more often and find tools that lower the amount of friction you deal
with daily.  If you are adamant that there is no way you can buy a tool,
then build it.  You have the power. :)