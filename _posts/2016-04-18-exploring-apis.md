---
layout: post
title:  "Exploting APIs"
date:   2016-04-18
categories: api groovy repl jython osgi
---

**This article was originally posted as part of [my old
 blog](https://techfortytwo.wordpress.com) on Aug 2, 2013.**

SDKs and APIs are complicated beasts. You can never understand them by
just reading the documentation, however well written it is . So what
is the alternative? Personally, I can not truly claim that I
understand an API without actually using it. That doesn't mean that I
need to write a full-fledged application but I need to be able to call
the API and see it in action. For the purpose of this discussion, I
will be assuming Java APIs but the facts are valid in general. 

One obvious way is to write a small program that invokes the API and
run that program with different values to see the API behavior. This
works ok in some cases but for the most part, the process becomes too
tedious. Particularly in case of Java, there is lots of boilerplate
code and any small change will have to go through the build-run
cycle. 

Wouldn't it be simply better if you can just call these APIs from
command line without going through lot of set up? That is exactly what
you can do with 
[REPL](http://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)
languages. For example, to explore a Python API, you just need to get
to python prompt and start calling the API (the API module needs to
be either installed first or made accessible in some other way, of
course).

Now I wanted the same convenience when it comes to calling Java APIs
and for very long time, 
[Jython](http://www.jython.org) filled that need. You can
seamlessly instantiate Java objects and call their methods, all from
the python command prompt (you do need to place the relevant JAR file
in the CLASSPATH). I have used this mechanism not only to play
with external SDKs but also to understand and use some of our internal
libraries. Of late, I started using 
[Groovy](http://groovy.codehaus.org) for the same purpose. 

Things have been working pretty well until we started using 
[OSGi](http://www.osgi.org). It is similar
to a web container. In OSGi, Java classes that need to be used by
other components are exported as services. But to actually make use of
the service, the calling code has to also run in the container. This
immediately presented a problem for me. How can I quickly test/explore
OSGi services? I could not use my usual "Groovy command prompt" way
because unless Groovy shell itself is running in the container, the
services can not be accessed. 

After spending some time on the problem, I found that someone else
solved similar problem for web applications so it became just a matter
of adapting it for OSGi. The result can be seen at
[groovy-osgi-console](https://github.com/draghuram/groovy-osgi-console)
project.

In conclusion, it is very important to have a simple and quick way of
exploring APIs and for me, using 
[REPL](http://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)
languages is that way. 
