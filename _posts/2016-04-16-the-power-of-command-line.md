---
layout: post
title:  "The power of the command line"
date:   2016-04-16
categories: jekyll unix commandline
---

**This article was originally posted on [my old
 blog](https://techfortytwo.wordpress.com) on Dec 16, 2012.**

If there is one central theme that permeates my
development philosophy, it is the belief that working from command
line offers power and flexibility that can not be matched by GUI
applications. 

Unix commands such as *grep* and *find* are very
powerful and the best thing about such commands is what you can do by
combining them. Even seemingly simplistic commands such as *ls,
tail, and less* can be combined to provide very useful
functionality. For example, here is what I regularly use to view the
latest log file in a directory: 

```
$ ls -1tr log*txt | tail -1 | xargs less
````

Since I use this command frequently, it is always available in history
so it is trivial to find and run it. 

I understand that some people are more comfortable using GUIs and
there is nothing wrong about it. But personally, I like working from
command line. Perhaps this has to do with my love of Unix and with its
philosophy ([Art of Unix Programming](http://www.catb.org/esr/writings/taoup/html)).
I still remember the day when a friend suggested I read the book
[The Design of the UNIX Operating System](http://www.amazon.com/Design-Operating-System-Prentice-Hall-Software/dp/0132017997).
Even though it is a bit old now, I highly recommend the book to any
Operating System aficionados out there. 

I have been very fortunate to be able to use *Linux* as my primary
working environment for most of my career. Even when I had to work
on *Windows*, I could always use [Cygwin](http://www.cygwin.com). 
Folks at *Cygwin* deserve tremendous praise for their work and for
helping people like me survive *Windows* :-). 

Of course, not everything can be done from command line and
rightly so. For example, I can't imagine using Gmail from a text
browser. But even there, I make extensive use of the keyboard
shortcuts without which there is no way I could manage all my email
and mailing list subscriptions. Keyboard shortcuts quite simply
improve productivity. It is really tortuous to have to use mouse to
carry out oft repeated operations. 

Speaking of GUI applications, I have an issue with IDEs such as 
[Eclipse](http://www.eclipse.org) in that they present too much
information which distracts the developer. If I am writing code, I want to
concentrate on the code itself and don't want to be inundated with
tons of information that has no immediate value. I would like to be
able to ask for the information when I want rather than being
presented with it all the time. No doubt, you can customize the IDEs
to suit your needs but that only increases the complexity of the
tool. 

To summarize, I would like to use utilities that are simple but can be
combined to provide a richer functionality. This in short is the Unix
philosophy. 
