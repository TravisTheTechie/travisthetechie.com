---
layout: post
title: Obsolete UseSubscriptionService() - MassTransit Problems
categories: [code]
tags: [MassTransit]
description: Have SubscriptionService warnings in MassTransit?
---

This is the start of a series on common problems, and solutions, when working with
<a href="http://masstransit-project.com/">MassTransit ESB</a>. This post is on version 2.7.4.

You see the following warning with a simple MSMQ example program, 
<code>'MassTransit.SubscriptionClientConfiguratorExtensions.UseSubscriptionService(MassTransit.BusConfigurators.ServiceBusConfigurator, string)' is obsolete: 'The extension method on UseMsmq should be used instead'</code>

<script src="https://gist.github.com/TravisTheTechie/6045068.js?file=Program.cs"></script>

To reduce confusion, the MSMQ related items have been moved into a configuration delegate inside 
UseMsmq(). Additionally, the namespace on UseSubscriptionService() was not correct for a time, you might 
need to add an import. This is corrected in later versions.

<script src="https://gist.github.com/TravisTheTechie/6045068.js?file=Program.v2.cs"></script>