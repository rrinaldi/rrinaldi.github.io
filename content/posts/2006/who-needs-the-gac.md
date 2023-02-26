---
title: Who needs the GAC?
date: 2006-08-17
---
I certainly don't.  Most of the time.

Lately I've been [spending
time](http://blogs.geekdojo.net/ryan/archive/2006/08/14/12087.aspx) working
with Team Build to automate the builds of a few of our applications and
I've discovered that way too many apps deploy themselves into the GAC. 
Discovered isn't the right word, I've known for awhile that all of our
3rd party controls go into the GAC, but I didn't realize how big of a
pain it was going to be.

In my not-so-humble opinion, if you aren't creating a framework of some
sort that is going to be versioned fairly slowly (I'm talking 1 1/2 to 2
year dev cycles) don't be putting yourself in the GAC.  Controls that
update themselves monthly are not candidates to be installed in the
GAC.  They are just to volatile.  Also, my build server is going to
be building various web apps, some windows services, and a winforms app
or two.  I don't want to be constantly installing software onto that
machine. 

Another issue of having every Tom, Dick, and Harry install things into
the GAC is it now makes it more difficult for me get another developer
up and running.  Instead of a simple "Get the latest code from this
branch of the Acme Project" it turns into a "Get the latest, install Xyz
Corps MegaControls package, then install Abc Systems SimpleGrid Plus,
then install...".  Let me drop all of the references I need in a
directory that is in source control and the new developer is up and
running and building in a couple minutes.  Otherwise he will be burning
a day or more installing software.
