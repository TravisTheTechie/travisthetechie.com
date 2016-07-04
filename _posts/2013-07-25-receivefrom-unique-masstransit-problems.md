---
layout: post
title: ReceiveFrom() Unique - MassTransit Problems
categories: [code]
tags: [MassTransit]
description: Problems getting messages to consumers with MassTransit?
---

Continuing the series of <a href="/2013/07/obsolete-usesubscriptionservice.html">common MassTransit</a> 
problems, I want to talk about what is likely the most common problem. Ever. All the time.

To be fair, there's a good reason why it is. And we are totally open to input on how to avoid this 
being the most common problem with MassTransit. But the number one most important thing you need to do... 
is make sure each instance of <code>IServiceBus</code> has it's own, unique queue to receive from. You can 
see an example of this in our
<a href="https://github.com/MassTransit/MassTransit/blob/updating-starbucks-demo-to-rabbit-with-proper-line-endings/src/Samples/Starbucks/Starbucks.Customer/Program.cs#L48">demo code for customers</a>. 
Each customer needs to uniquely receive messages.

What happens if multiple processes receive from the same queue you ask? Well, on MSMQ you'll see 
exceptions in the logs for non-transactional queues. But if there are no exceptions, then one process 
might read a message it doesn't have consumers registered for and just discard the message. The process
that message was destined for doesn't get it.

If you are using RabbitMQ and you want to scale out, you might have multiple processes reading from the 
same queue. This is known as competing consumers and should be considered an edge case. There are some 
caveats associated with it before you head down that path.

TL;DR - every <code>IServiceBus</code> needs it's own queue. Just how it is.

