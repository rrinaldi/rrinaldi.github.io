---
title: Never ever catch System.Exception
date: 2007-06-29
---
…except when you should. :)

Patrick Cauldwell wrote a great post on [how to handle
exceptions](http://feeds.feedburner.com/~r/PatrickCauldwellsBlog/~3/129044640/ExceptionHandlingPolicy.aspx) and
I agree with everything he says except for this:

"If you find yourself arguing for catching Exception, you probably have
a design problem."

In most cases he is completely right. In every web app I write I never
catch System.Exception and I have no reason to.  If I'm code reviewing
and I see somebody catch System.Exception I flag it as something that
needs to be changed.  But in the last app I wrote I needed to catch
System.Exception and there is only one good reason why: Microsoft gave
me no choice.

Yep.  I have no other option.  Here's the background: I wrote a nice
little server application that receives multiple kinds of data.  Xml
files, CSV, structured text documents, etc.  Each piece of data is
labeled with what kind data it is and as the data comes in I store it
and it's label to disk.  I have client software that has plugins that
are specifically written for each type of data.  When the clients start
up they read in from a config file what types of data they support and
register themselves with the server and start polling.  The server then
responds with a payload that the client supports and the client loads up
the plugin that handles that data type and pass the payload along to
it.  The data is processed and then the client polls for more and the
process repeats until there is nothing left to process.

So here is where the big problem is that makes me catch
System.Exception: When the plugin crashes, the client needs to keep on
chugging.  It tells the server there is a problem, marks the data as
problematic, notifies the appropriate people and then it keeps on
keeping on.  I know that catching System.Exception is bad.  What if I'm
out of memory or the application domain is being torn down for some
reason?  What if it really is one of those unrecoverable exceptions? But
you never can tell the difference between the unrecoverable and
recoverable exceptions since they all inherit from System.Exception. The
other part of this problem is that I have no control over what
exceptions the plugin can throw and I need to handle all of them.

Microsoft tried to have different base classes
(System.ApplicationException) for different types of exceptions. That
didn't work to well and since System.ApplicationException has only 10
exceptions in the entire framework that inherit from it.

I would love to be able to just catch System.ApplicationException and
know that anything else that should crash my app will crash my app but
since I can't I have to go on catching System.Exception.
