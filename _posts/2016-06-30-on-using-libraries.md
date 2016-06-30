---
layout: post
title:  "On using libraries and frameworks..."
date:   2016-06-30
categories: java threads threadpools libraries frameworks spring-batch
---

Almost every software product uses third party libraries or frameworks
- open source or otherwise. Typically, you should concentrate on the core
part of your product and for everything else (especially for
plumbing part), you should consider using third party libraries.

There are many advantages with such an approach:

- You can spend more time on your product's core functionality. 

- A library is usually more robust and performant because it is
  presumably developed by people who are knowledgeable about its
  domain. 

- Since many people use a given library, bugs will be found and
  fixed over a period of time.

To be fair, there are many cases when rolling one's own solution is
the right approach but I am not going to talk about them. Instead, I
want to focus on a problem I usually see when people use libraries.

Libraries try to shield developers from having to know the low level
details and in turn, provide a high level API that they can
comfortably use. Even though this is one of the reasons for using
libraries, I would like to argue that developers should still try to
understand the underlying implementation details. Only if we
understand what is going on behind the scenes, can we feel truly
be comfortable using it in our application (at least that is how I
feel). This may sound like a contradiction but it really is not. Note
that even though you are depending on the library for some 
functionality, it is still your application and if there are any
problems, your users look to you to provide the solution. You can't
tell them that you are using some third party library and the 
problem is there and not in your code. Your users really don't care. 

To take an example, in our product, we use 
[Spring Batch](http://projects.spring.io/spring-batch/)
that uses Java threads and thread pools to run jobs. 
This is rather short explanation for a huge framework but for the
purposes of this discussion, this is sufficient. Recently, I looked at
logs from one of our customers and noticed that our application
spawned 5000 threads. This immediately set off alarm bells because I
knew that we couldn't be running so many tasks in parallel. On closer
examination, it turned out that this had something to do with the way
we configured 
Batch's threading parameters.  

[Spring Batch](http://projects.spring.io/spring-batch/) uses 
[Java's ThreadPoolExecutor](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html)
to manage threads. This class has properties for "core pool size" and
"max pool size". It turned out that we configured core pool size to be
5000 which means that `ThreadPoolExecutor` will keep creating threads
until the pool size reaches 5000. It doesn't try to re-use the already
created threads even if they are idle. This is because "core pool" is
meant to be configured with a small number of threads that the
application requires at all times. 

There are obviously several problems with having so many threads
(especially, idle threads). Each thread at the very least uses 1 MB
stack size (on 64-bit Linux) so you are talking about wasting lots of
RAM. Even if one were to assume that the unused memory is swapped out,
you are still unnecessarily putting stress on system resources. The
fix in this case is to use a small number for "core pool size".

So my point is that even though we are well off using Spring Batch for
our job management, we should still understand how and when it creates
threads and in general, its threading model. Only then can we
effectively use the library. Just using Spring Batch doesn't obviate
the need to learn the low level details such as its threading model.

In fact, I would like to extend this logic and say that to be really
a good developer, it is not sufficient to understand languages and
frameworks alone. One should really know some details at OS level such
as about processes, I/O, and inter-process communication. This may
sound like lots of work but without such understanding, one can't
truly be an efficient software developer.

