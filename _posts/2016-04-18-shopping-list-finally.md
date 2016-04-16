---
layout: post
title:  "Shopping list, Finally!"
date:   2016-04-18
categories: testing testng angularjs boorstrap groovy ui
---

**This article was originally posted as part of [my old
 blog](https://techfortytwo.wordpress.com) on Feb 21, 2015.**

Like many passionate developers, I have worked on several
side projects ranging from single file scripts to small web
sites. However, there was one on my todo list that I have never been
able to finish; until now, that is. I wanted to build a shopping list
application for almost 5 years. For some reason, however, the effort
never took off in earnest. There were several false starts when I did
little bit and would leave it aside as other things came up. 

I finally managed to complete it in the last couple of months and
in the process, learned few valuable lessons on how to
successfully finish (side) projects that are moderately complex. I
thought I would share these lessons in the hope that someone out there
who is struggling to complete such projects would find them helpful. 

## The Chess Strategy

By very definition, you can't dedicate large chunks of time to
these projects as you need to concentrate on your day job. However,
I found that you need to do precisely that in the beginning stages
of the project in order for it to succeed. It is very important that
you put in lot of effort to get the project off the ground and build
a critical mass. What does "critical mass" constitute? It
obviously depends on the project but I would venture that you need to
build the application to the point that you can start using it even if
not all the functionality is there. In my case, I built the
application to the point that I could use it for my shopping
needs. Admittedly, UI was plain ugly but I could use it and in the
process, generate valuable feedback. 

Once the project reached this stage, you can fix bugs and add features
in small increments. I made a task list and handled one at a time,
mostly in half an hour to 45 minute sessions. Think swim classes and
tennis lessons for kids :-).

As the project neared completion, I again needed to step up the pace
and spend longer chunks of time to wrap it up. In this stage, there
would be lots of small things that you need to take care of such as
writing documentation (or polishing existing docs). Other things you
may want to do at this point include code cleanup or adding tests if
you haven't already done so. More over, if you are going to publish
the project some where, you need to get the project ready (by picking
a license, for example). It is ideal if you do all these things in
quick succession instead of dragging them on. 

To summarize, a successful side project usually needs to go
through three phases. Sort of like opening, middlegame, and endgame in
chess. 

## Testing

I am usually an ardent proponent of automated testing (tests to be
written first if possible). Here I don't mean unit testing but testing
at the API level. However, when I started this project, I convinced
myself that it was not worth writing tests while I was implementing
the REST APIs. The result was that I had to test APIs manually with
each change. Finally midway through the project, I got fed up with the
manual testing and wrote automated tests (using 
[Groovy](http://groovy-lang.org) and
[TestNG](http://testng.org)). Even if writing tests requires
investment of time initially, they definitely return the investment
many times over. You will get a sense of confidence in code that no
amount of manual testing can provide. So my suggestion is that do not
be tempted to skip automated tests. Make the investment and you will
not regret it. 

## Now, to Shopping list...

Coming to the actual application itself, I had great fun doing it as I
had to learn lots of new technologies
([AngularJS](https://angularjs.org),
[Bootstrap](http://getbootstrap.com), and JavaScript to name
a few). I had to solve many problems along the way but solving them
gave me immense satisfaction. 
[Stackoverflow](http://stackoverflow.com) is your friend. 

Even though I had to dabble in multiple technologies for this project,
one technology deserves a big shout out. 
[AngularJS](https://angularjs.org), allowed someone like me to
build a decent UI and that is saying something :-). If you read
previous articles in my blog, you would know that I prefer command
line and stay away from UIs if given a chance (sometimes, even when
not given a chance). Add to it the fact that I am a total newbie to
JavaScript, not to mention to UI development itself. However, Angular
proved to be very intuitive to learn and worked like a charm. 

The source code for the application is available at 
[shoppinglist](https://github.com/draghuram/shoppinglist) so
head over there if you are curious. There is even a demo instance
available at <https://shoppinglist-demo.appspot.com>. 

Feel free to play around and let me know if you have any comments.
