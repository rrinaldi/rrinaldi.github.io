---
title: "Programming by coincidence"
date: 2010-03-25
---
As a developer it’s of super duper importance that we understand what
each and every line of code that we write does and how it works.  While
a lot of code that we write leverages libraries to provide wonderful
abstractions over complex implementations we owe it to ourselves, the
businesses that we work for and other developers on our teams to
understand what these libraries are doing and how they are doing it.

But why?  Because when they fail (and they will fail!) you need to know
where to begin troubleshooting and without an understanding of what the
code is doing you are up a creek.  So since you can’t troubleshoot you
need to find an alternate implementation that does work.  But an
alternate implementation of what?!?  You don’t have the foggiest idea
what the code was doing in the first place so how can you write (or,
sigh, find) code that does the same \*thing\* but in a different way?

This leads developers to go down the rabbit hole of CPDD (Copy Paste
Driven Development).  A few copy-pastes later from the [bathroom wall of
code](http://www.codinghorror.com/blog/2009/05/the-bathroom-wall-of-code.html)
and you have a mess of code that nobody really understands but “works”
(for a very small value of “works”).  Now you back where you started.  A
bunch of code that appears to be doing what you want and you are
oblivious to the implementation details.

So the next time you are copying some code from [Stack
Overflow](http://stackoverflow.com) do me a favor, heck do us all a
favor, and just ask yourself “What is this code doing?”.  Once you have
the answer, and you are satisfied that it is working the way you really
intended feel free to paste away.  But until then, don’t infect your
codebase with germy disgusting code that you got off the bathroom wall.