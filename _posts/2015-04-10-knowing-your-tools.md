---
layout: post
title: Knowing your tools
categories: [Code]
tags: [Growth]
description: >
             A small reminder story about the importance of learning the tools you use every day.
             They don't go away and fighting them just makes life harder.
---

This past week I've been working on learning some [Spring MVC], using [Maven] to do the builds.
An interesting encounter, because I use Maven every week but have no clue how it works. How does
this fit in with me [suggesting that knowing your tools][skilling-up] is important &mdash;
part of the skill set everyone needs to develop?

With my work, I often have to launch some piece of software using Maven. Much of the software at
Atlassian uses Maven for builds, driving this. I am familiar with Maven, in that I know how to run
`mvn clean install -DskipTests=true`. If you ask me to modify a `pom.xml` or know what other
command line arguments to pass, I haven't a clue.

Juxtapose this with Git. I may not be a Git master, but I can delve into the reflog to find things,
branch/rebase/merge like just about anyone else, octopus merge, and can generally recover from any
flub I've run into so far. This comes from me spending some effort to learn some details about Git
and then pushing myself in trying to do stuff with Git from time to time. Also, just accepting that
Git is an important part of my workflow and embracing it.

In this past year, I have tried to hide from Maven. This week it has not paid off. What, in
retrospect, should have been a 2 minute fix took me an hour to track down and Google the answer for.
The takeaway for me here is that I do need to spend even a little bit of time learning more about
Maven if I'm ever going to stop hiding from and just poking it with a stick when I need something.
In the meantime, you're welcomed to follow along the disaster that is me
[learning to use Spring][springrocket]!

[skilling-up]: /2015/03/skilling-up.html
[Spring MVC]: http://en.wikipedia.org/wiki/Spring_Framework
[Maven]: https://maven.apache.org/
[springrocket]: https://bitbucket.org/travisthetechie/springrocket
