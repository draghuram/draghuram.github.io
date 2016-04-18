---
layout: post
title:  "Automated Testing"
date:   2016-04-17
categories: jekyll testing groovy testng rest
---

**This article was originally posted on [my old
 blog](https://techfortytwo.wordpress.com) on July 29, 2013.**

I am a big fan of automated testing. I have always tried to automate
tasks so writing automated tests came naturally to me. I lost count of
number of python scripts that I wrote to test the product I work
on. The product wasn't exactly architected to suit automated testing
so I had to jump through some hoops to do it. There was no way I
was going to manually test my changes using UI repeatedly. 

As time passed, my understanding of test-suitable architecture got
better and concepts such as 
[dependency injection](http://en.wikipedia.org/wiki/Dependency_injection)
started making sense. By a fortuitous coincidence, I had
started work on a new product that was being built from scratch and it
used Spring framework which encourages dependency injection based
design. So at this point, I started using 
[TestNG](http://testng.org) and liked it quite a bit. 

I also started reading about different development practices and kept
running into
[TDD](http://en.wikipedia.org/wiki/Test-driven_development) but
for some reason, I couldn't completely accept that it is possible to
write a test **before** actual code changes are made. But
my understanding of TDD has changed dramatically after reading the book 
[Growing Object-Oriented Software, Guided by Tests](http://www.amazon.com/Growing-Object-Oriented-Software-Guided-Tests/dp/0321503627).

The book is very well written and talks in detail about
developing software guided by the tests, as the title says. The
biggest take away for me was the fact that "T" in "TDD" doesn't
necessarily refer to a unit test. In fact, the authors suggest that
one should start by writing an integration test (I use the term
"integration test" here to mean tests that exercise the product just
as a UI or an API client does). Once the test is satisfied, we can
think about proper class design and with it comes, unit tests. 

This was something that I could practice successfully in the last
year or so. Writing integration tests is definitely easier than
writing unit tests before hand. For one thing, we may not be sure
about the class design until we get some kind of implementation
done. Until such class design is ready, one can not write unit tests.  

To give a practical example, I have been working on a product that
exposes its functionality via REST API. I have made it a habit
to write an API test before I actually implement it. There are
few exceptions here and there but for the most part, I could stick
with the habit without problem. I came up with a nice little tool that
integrates the following pieces: 

- TestNG as test framework
- [Groovy](http://groovy.codehaus.org) as the language to write tests
  in (Groovy integrates nicely with Java)
- Spring's
  [RestTemplate](http://static.springsource.org/spring/docs/3.2.x/javadoc-api/org/springframework/web/client/RestTemplate.html)
  to handle REST requests and responses. 

This combination has been working great and I am generally happy
about the state of my code as steadily increasing number of tests give
me some confidence that it is in good shape. I can also personally
attest to the advantage frequently cited by TDD advocates: that it is
far easier to refactor the code backed by tests than the code with
very little or no tests. 
