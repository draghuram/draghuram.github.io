---
layout: post
title:  "On using libraries and frameworks..."
date:   2016-06-30
categories: java threads threadpools libraries frameworks spring-batch
---

Almost every software product uses third party frameworks - open
source or otherwise. Typically, you should concentrate on the core
part of the product and for everything else (especially for
plumbing), you should consider using third party libraries or
frameworks. 

There are many advantages with such an approach:

- You can spend more time on your product's core functionality. 

- A framework is usually more robust and performant because it is
  presumably developed by people who are knowledgeable about its
  domain. 

- Since many people use a given framework, bugs will be found and will
  be fixed over a period of time.

To be fair, there are many cases when rolling one's own solution is
the right approach but I am not going to talk about it. Instead, I
want to focus on a problem I usually see when people use
frameworks. 

Frameworks abstract away of lots of underlying technical details from
the developers. Even though this is one of the reasons you use
frameworks, I would argue that developers should still try to
understand the underlying details. Only if we understand what is
going on behind the scenes, we can feel truly comfortable using it in
our application. This may sound like a contradiction but it really is
not. Note that even though you are depending on the framework for some
functionality, it is still your application and if there are any
problems in the application, your users look to you to provide the
solution. You can't tell them that you are using some library and the
problem is there and not in your code. Your users really don't care. 

To take an example, we use 
[Spring Batch](http://projects.spring.io/spring-batch/)
in our product. which uses threads and thread pools to run jobs. 
This is rather short explanation for a huge framework but for the purposes of this
discussion, this is sufficient. Recently, I looked at logs from a customer
and noticed that our application spawned 5000 threads. I immediately
knew something was wrong because I knew that we couldn't be running so
many tasks in parallel. On closer examination, it turned out that this
has something to do with the way we configured Batch which uses Java's
ThreadPoolExecutor to manage threads. This class has configuration
parameters for "core pool size" and "max pool size". It turned out
that we configured core pool size to be 5000. Which means,
ThreadPoolExecutor will keep creating threads until the size reaches
5000. It doesn't try to re-use the already created threads even if
they are idle. That is idea behind "core pool size" which is meant to
configure a small number of threads that the application requires at
all times. 

There are obviously several problems with having so many threads
(especially, idle threads). Each thread at the very least uses 1 MB stack size (on
64-bit Linux) so you are talking about wasting lots of RAM. Even if
one were to assume that the unused memory is swapped out, you are
still unnecessarily putting stress on system resources. 

So my point is that even though we are well off using Spring Batch for
our job management, we should still understand its thread model and
how and when it creates threads. Only then can we tune it
properly. Just using Spring Batch doesn't obviate the need to learn
the low level details such as threading. 

In fact, I would like to extend this logic and say that to be really
good developer, it is not sufficient to understand languages and
frameworks alone. One should really know some details at OS level such
as processes, IO, and inter-process communication. This may sound like
lots of work but without such understanding, one can't truly be an
expert.
